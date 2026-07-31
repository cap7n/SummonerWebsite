# Rebuild Architecture (Systems)

The rebuild is **not** "the PoC but tidier". It's a set of **systems that work in isolation and are connected together** — each one lives in its own folder, has its own test scene, and talks to the rest only through explicit interfaces and events. If a system can't demo alone in its harness scene, its boundary is wrong.

Decided 2026-07-31, after both feasibility spikes passed (see [Spike results](#spike-results)).

## Ground rules <span class="pill done">DONE</span>

- **Troops are data, not nodes.** Positions/velocities/HP live in packed arrays, neighbour queries go through a spatial grid, rendering is one MultiMesh per crowd. No physics bodies, no per-troop scene nodes. Measured: ~2 ms/frame for 660 simulated agents in plain GDScript.
- **Boids + heightmap + local avoidance instead of pathfinding.** Troops never navigate alone — they follow a summoner or a caravan, which is a *local* steering problem. No navmesh baking anywhere. The few long-range movers (caravan, enemy packs) follow a small authored **route/road graph** (A* over dozens of nodes, not thousands of polygons).
- **The ownership law.** Every crowd, the caravan, and each summoner has exactly **one simulating owner peer**; everyone else renders its stream. Your machine simulates *your* bubble (zero input lag), the host simulates the world. This is what makes the battle look identical on every screen — and it's the "use all the computers" idea done the sane way (partition by ownership, never split one simulation).
- **Events that could cross a wire.** Systems communicate through signals/events shaped like network messages from day one, so the multiplayer port is plumbing, not surgery. Inherited OTR rules apply ([Networking](networking.md)).

## The systems

| # | System | One-line job | Depends on |
|---|---|---|---|
| 1 | **Crowd Sim** | Boids as data: arrays + spatial grid + MultiMesh. Input: an anchor + slot layout. Output: positions. | Terrain |
| 2 | **Formation** | Pure function: count + radius → scattered slot offsets (golden-angle spiral + jitter). The "bubble" is just this. | — |
| 3 | **Terrain** | Heightmap: `height_at()`, `slope_at()`, avoidance field from obstacles. | — |
| 4 | **Combat** | Contact detection, targeting (chase cap, defenders-only), HP, kill events. | Crowd Sim |
| 5 | **Unit Defs** | `.tres` Resources: stats, visuals, tombstone-level scaling. Data only. | — |
| 6 | **Summoner + Camera** | Exists in the PoC, mostly survives as-is. | Terrain |
| 7 | **Route Graph** | Tiny A* over authored road nodes, for the few long-range movers. | — |
| 8 | **Caravan** | Follows routes, takes orders, has HP, emits "I died" (= run over). | Route Graph |
| 9 | **Fog of War** | Vision sources → shared coverage texture → terrain shader. One state for all players. | Terrain |
| 10 | **POI / Objectives** | Trigger areas + objective state machine + reward events. | — |
| 11 | **Run Director** | The state machine: hub → deploy → play → extract/fail. Pure glue, listens to events. | everything above |
| 12 | **Meta / Save** | Tombstones, points, save file, graveyard hub scene. | Unit Defs |
| 13 | **Net Sync** | Transport + tick + snapshot streaming ([Networking](networking.md)). Already proven in the spike. | 1, 8, 9, 10 |
| 14 | **Map Generator** | Noise heightmap + POI-site scatter + road-graph generation; applies hand-authored POI stamps. [Decided 2026-07-31](../game/runs.md#map-generation). | Terrain, Route Graph |

The rebuild lives **inside the main game project** (`Summoner/Summoner/`, alongside the PoC code it gradually replaces) — one folder per system under `systems/`, plus `scenes/hub/Hub.tscn` (the graybox Graveyard hub with the four player spawns). Map Generator slots into build-order steps 3–5: it's first needed when the caravan wants roads to follow.

## Spike results <span class="pill done">DONE</span> {#spike-results}

Both rebuild-blocking questions were answered in a spike project, since **folded into the main project** as `systems/net` + `systems/crowd` (one-project rule) — the netcrowd harness now runs the streamed armies **on generated terrain**:

- **Crowd scale** — ~810 boid agents across four crowds: **~2 ms sim** on the host, 60 fps headroom to spare. GDScript is enough; no C#/GDExtension needed yet.
- **Streaming consistency** — two instances, quantized 6-byte-per-troop deltas at 15 Hz: **both machines ended the same battle with the identical troop count**, at **~0.2 Mbit/s host upload per client** (~10× under budget).
- **Steam transport** — OTR's GodotSteam layer (Spacewar App ID 480, friends-only lobby, `SteamMultiplayerPeer`) runs on Godot 4.7 unchanged. First real-internet 2-player session (2026-07-31): stable; one stutter bug found and fixed (sender-tick jitter buffer — see [Networking](networking.md#what-the-spike-changed)).

## Terrain results <span class="pill done">DONE 2026-07-31</span> {#terrain-results}

System 3 is **built** (`systems/terrain/`, with its own isolation harness). Design: one height field is the single source of truth — gameplay samples it via `height_at()`, and the GPU displaces chunk meshes from the same data as a texture, so what the sim thinks and what you see cannot drift apart. Every chunk shares one flat mesh and one material.

Measured on the dev machine, worst case = RTS camera pulled out to 1100 m:

| Map | Cell | Peak tris in frame | Worst frame | Heightmap | Generation |
|---|---|---|---|---|---|
| 2 km | 2 m | 2.0 M | 1.4 ms | 4 MB | 0.5 s |
| 4 km | 2 m | 5.6 M | 2.3 ms | 16 MB | 2.0 s |
| 8 km | 2 m | 7.7 M | 2.4 ms | 64 MB | 7.9 s |
| 16 km | 4 m | — | 1.4 ms | 64 MB | 8.4 s |

**Terrain rendering is effectively free** — 2.4 ms is under 15% of a 60 fps budget, on a machine that also has to run 800+ troops. The scaling costs are generation time and memory, both one-off. [Map size is therefore a design question](../game/runs.md#map-size).

!!! note "Two systems were built, measured, and deleted"
    **Distance LOD** turned out *slower* than no LOD (1695 vs 2056 fps at 4 km) — the GDScript pass over thousands of chunks cost more than the triangles it saved. **Chunk skirts** only existed to hide cracks between LOD levels, so they went with it. What was kept because it is load-bearing: a per-chunk `custom_aabb`, since the engine can't know about displacement done in a vertex shader and will otherwise cull terrain you're looking straight at.

## Build order

Each step lands as a playable increment:

1. **Terrain + Crowd Sim + Formation** — the new bubble walks on hills. Replaces the PoC's core.
2. **Combat** — two crowds fight, with the chase cap and defenders-only rules the prototype taught us.
3. **Caravan + Route Graph** — the run has a spine and a fail state. *This is the moment to feel-test the passive bubble for real.*
4. **Fog of War** — the map becomes readable/unknown.
5. **POI / Objectives** — one type, end-to-end, reward included.
6. **Run Director** — win/lose/extract stops being an HUD label.
7. **Meta / Save + Graveyard scene** — the loop closes.
8. **Net Sync port** — last and lowest-risk: the spike already proved the payload, the transport, and the interpolation; every system above will have carried an owner-peer field from day one.

!!! note "Why networking goes last even though it's proven"
    The spike de-risked the *hard* part (scale, consistency, bandwidth, Steam). What remains is wiring — and wiring wants stable systems to wire. Building each system with the ownership law and event-shaped boundaries keeps the port cheap; building the port first would freeze system interfaces before they've earned their shape.
