# Engine & Prototype Workflow

## Engine

**Godot 4.7** (stable, win64), Forward+ renderer, Jolt physics, D3D12.

## Repository layout

| Path | What |
|---|---|
| `Summoner/Summoner/` | **The one game project.** Systems live in `systems/<name>/` with their own test scenes, launched from `scenes/DevMenu.tscn` |
| `Summoner/Summoner builds/` | **The one shareable build** (`SummonerDev`) — every harness in one exe |
| `Summoner/SummonerWebsite/` | This wiki |

!!! note "One project, one build (2026-07-31, binding)"
    Cap7n's rule after two parallel builds caused a "did we lose the multiplayer?" scare: **never split work into side projects or parallel builds.** New systems go into `systems/` with a test scene and a row in the dev launcher; the netcode spike was folded back in the same day (`systems/net` + `systems/crowd`, `Spikes/` folder retired). If something truly needs isolated testing, cap7n will say so explicitly.
| `Summoner/Summoner Marketing/` | Non-code sibling |
| `Desktop/OTR/` | **Sibling project** — the 2-player co-op car game whose network stack Summoner reuses ([Networking](networking.md)) |

**The PoC gameplay code was trashed on 2026-07-31** (developer's call: "if the old code is useless we can trash it"). What survived the cut, because it wasn't useless:

- `systems/summoner/player.gd` + `rts_camera.gd` — the WASD summoner and the locked/free RTS camera, kept as the starting point of system 6 ([Architecture](architecture.md)).
- `assets/shaders/grid.gdshader` — may serve the terrain later.
- **The whole playable PoC is preserved at git tag `poc-final`** — both control schemes behind the F1 toggle, one `git checkout poc-final` away. That's the drawer to reach into if the simplified bubble feels flat.

All branches were collapsed into **`main`** on 2026-07-31 (tests done, vision clear — one line of history now). F5 boots the graybox Graveyard hub (`scenes/hub/Hub.tscn`).

## Prototype verification workflow

The prototype is verified without a human watching, which keeps iteration honest:

```bash
# parse + boot check (headless, no shaders compiled)
godot --headless --path . --quit-after 90

# render real frames to PNG for visual verification
godot --path . --write-movie out/frame.png --fixed-fps 20 --quit-after 150

# scripted playtests: a temp scene drives Input actions and asserts outcomes
godot --headless --path . res://_tmp_test.tscn
```

Scripted tests have been used to verify: troop scatter stays in-bounds and separated, WASD movement, camera detach/recenter, full 50v50 combat resolution (multiple runs to check for side bias), and leash/speed-cap invariants.

## PoC → rebuild

The current code is a **disposable proof of concept** (one ~600-line `troop_bubble.gd` doing formation, movement, combat, two control schemes, and rendering). The rebuild is now designed and unblocked — the full system list, ground rules and build order live on the **[Architecture](architecture.md)** page. In short: isolated systems with their own test scenes, troops as data (packed arrays + spatial grid + MultiMesh), boids on a heightmap instead of navmesh pathfinding, one simulating owner per crowd, events shaped like network messages from day one.

What the spikes already settled (2026-07-30/31):

- **Scale**: ~810 agents at ~2 ms sim in GDScript — spatial partitioning in, physics bodies out.
- **Wire**: troops are streamed entities (6 B, 15 Hz deltas) — [numbers](networking.md#the-troop-sync-problem).
- **Steam**: OTR's layer runs on 4.7; real-internet session held up.

Still genuinely new to this project: fog of war on a big map, the route/road graph for caravan and enemy packs, a hub scene with persistent save state ([Graveyard](../game/graveyard.md)), and a save format for tombstone levels.

!!! note "Godot pieces this implies"
    Heightmap terrain with a cheap `height_at()` lookup (no colliders needed for troops), a fog implementation (viewport-texture mask over the terrain shader is the usual cheap answer), and level chunking only if maps get genuinely big. Deliberately **not** implied anymore: navigation meshes — the route graph replaced them.

!!! note "Editor-conflict rule"
    Don't edit a `.tscn`/`.tres` from tooling while it's open in the Godot editor — the editor clobbers it on save. Close the scene first or hand over the change as steps.
