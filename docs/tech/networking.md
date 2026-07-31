# Networking (co-op)

Summoner's multiplayer is **not being invented from scratch**. It reuses the stack already built, shipped and debugged in **OTR** (`Desktop/OTR`), the 2-player co-op car game. Same author, same engine family, same problems already solved once.

Target: **4 players**, no anti-cheat. See [Co-op](../game/coop.md) for the design side.

## The OTR stack (what gets reused)

| Piece | What it does | Reuse verdict |
|---|---|---|
| **GodotSteam + `SteamMultiplayerPeer`** | Transport. Friends-only Steam lobby, host = peer 1, clients get Steam-derived IDs. Drop-in replacement for ENet — RPCs unchanged. | **As-is.** Bump lobby size 2 → 4. |
| **`NetworkTickManager` (autoload)** | One sync channel for the whole game. Entities register in `_ready()`, implement `get_sync_state()` / `apply_sync_state()`. Fixed tick (60 Hz in OTR), dirty flags, MTU-safe chunking at 1200 bytes. | **As-is, retuned.** Concept is exactly right; tick rate and payload shape change. |
| **`StateBuffer` + Hermite interpolation** | Client renders at `now − 3 × send_interval`, velocity-aware cubic interpolation between snapshots, extrapolates on buffer dry, snaps past a distance threshold. | **As-is.** Bubbles move slower and straighter than cars — it will look better here than it does there. |
| **Distributed sync ownership** | Entities may declare `get_sync_owner_peer_id()`, so a player-controlled entity is simulated on that player's own machine. OTR uses it for the drone. | **Central to Summoner.** Each summoner + bubble is owned by its player: zero input lag on your own army. |
| **Visual error correction** | Snap authority, keep a decaying visual offset. | **As-is.** |

The two hard rules from OTR carry over unchanged:

!!! note "Inherited rules"
    - **No per-script sync RPCs.** All state goes through the one tick manager. Never write `_rpc_sync_transform` on an entity.
    - **No raw exponential lerp** for networked entities. Snapshots into a `StateBuffer`, interpolate from there.

## What Summoner changes

- **Lobby size 4** (OTR: `MAX_LOBBY_MEMBERS = 2`). Solo must still work — a one-peer "lobby" with the same code path, no separate single-player mode.
- **No RPC-sender hardening as a design constraint.** Cheating is explicitly not a threat here; validate where it's free, don't architect for it.
- **Different payload entirely.** OTR syncs ~10 chunky entities (cars, turret, drone, a handful of enemies). Summoner has hundreds of tiny identical ones. That's the whole problem:

## The troop-sync problem — SOLVED <span class="pill done">DONE</span> {#the-troop-sync-problem}

Four players × 100–200 troops plus enemies is over a thousand bodies — far past "one entity, one snapshot, every tick". Three candidate answers were considered; the spike (`Summoner/Spikes/NetCrowdSpike`, 2026-07-30/31) settled it.

**Decided: troops are entities on the wire — per-troop quantized streaming.** A troop costs **6 bytes** (u16 index + u16 x + u16 z quantized over the map), sent as **deltas at 15 Hz** (only troops that moved) with a **1 Hz keyframe** carrying an alive-bitmask, plus reliable kill events. Receivers keep a per-crowd snapshot ring and render ~200 ms in the past (the `StateBuffer` idea, one ring per crowd instead of an object per entity). Packets chunk under MTU.

Measured in the spike, mid-battle, ~810 agents:

| Metric | Result |
|---|---|
| Host upload per client | **~0.2 Mbit/s** (~10× under the ~2 Mbit/s comfort budget) |
| Consistency | **Identical battle end-state on host and client** (same alive counts) |
| Sim cost (660 owned agents, GDScript) | **~2 ms/frame** |
| Real internet (Steam, 2 players, 2026-07-31) | Stable connection, correct battle on both screens |
| Real internet (Steam, **3 players**, 6 min, 2026-07-31) | 144 fps locked, sim ≤ 3 ms, **peak host upload ~1 Mbit/s with 2 clients** (~0.5 Mbit/s each, as predicted) |

!!! note "What the 3-player test forced (2026-07-31)"
    Godot's built-in server relay didn't deliver client↔client traffic over Steam — clients couldn't see each other. Relay is now **off on every transport**; the **host owns an explicit roster**, forwards client snapshots/kills, and distributes Steam names (which bought name tags for free). Idle armies also send 11-byte heartbeats so receivers' interpolation buffers never starve (the logs showed 60% phantom extrapolation from parked armies; now 0%). Localhost tests now rehearse the exact Steam code path.

**Rejected: shape-sync** (stream the bubble, grow the crowd locally from seeded scatter). Killed by a hard requirement that arrived after it was proposed: **the battle must look exactly the same on every screen** — same troops dying in the same places, even when two players' bubbles fight the same enemy pack. Locally-grown crowds can't guarantee that; one authoritative simulation per crowd can, by construction.

**Rejected: deterministic lockstep** (the BAR / Beyond All Reason / classic RTS model — only commands on the wire, every machine simulates everything bit-identically). It's how thousands of units fit in kilobytes, but it demands a fully deterministic sim (fixed-point math, no engine physics, desync tooling forever) that Godot does not provide, and it adds input latency that RTS clicks hide but **direct WASD summoner control would feel immediately**. Kept in the back pocket only for a hypothetical 10× unit-count future.

!!! note "Who simulates what — the ownership law"
    Every crowd has exactly one simulating owner: **your machine owns your bubble** (zero input lag on your own army), **the host owns enemies, caravan, fog and POIs**. Owners resolve their own agents' damage and deaths; everyone else renders the stream. Consistency across screens falls out of this for free — there is only ever one version of any fight. See [Architecture](architecture.md).

## What the spike changed in the inherited stack {#what-the-spike-changed}

- **Tick rate is 15 Hz, not OTR's 60** — crowds interpolate beautifully at 15 Hz and it quarters the bandwidth.
- **`StateBuffer` became a per-crowd ring** of packed-array snapshots (one object per entity would be 1000 tiny allocations per second). Linear interpolation is enough so far; OTR's Hermite is the upgrade path if crowds ever look rubbery.
- **Snapshots are timestamped by sender tick, not receive time** (min-tracked clock offset). Found the hard way in the first real-internet test: receive-time stamping made the host's army stutter on the client, because internet packets arrive in jittery bursts even on a stable connection. Sender-tick stamping restores perfectly even 66.7 ms spacing. This is a rule now, same standing as the two inherited ones above.
- **No rotation on the wire at all.** Troop facing is derived from motion on the receiving side, and capsule crowds don't visually need it anyway. OTR's nastiest stutter class — rotational jitter — structurally cannot recur for troops; if summoner facing ever syncs, it's one heading byte, not a quaternion.
- **Steam layer verified on Godot 4.7**: OTR's GodotSteam GDExtension (4.18.1) + Spacewar App ID 480 + friends-only lobby, `SteamMultiplayerPeer` as a drop-in for `ENetMultiplayerPeer` with zero changes to the RPC/snapshot layer. Lobby screen shows the lobby ID + members; host starts the match, late joiners get pulled in.

## Other things that go on the wire

| State | Notes |
|---|---|
| **[Caravan](../game/caravan.md)** | Host-authoritative, one entity, cheap. Any peer can *request* a move order (input RPC); the host applies it and syncs the result. Its death is a run-ending event — send it reliably, never as interpolated state. |
| **[Fog of war](../game/runs.md#fog-of-war)** | Shared vision means **one** fog state for the party, not four. Reveal is a coarse grid; send deltas (newly revealed cells) reliably, not the whole grid per tick. Massively cheaper than per-player fog — a real argument for the shared-vision decision beyond feel. |
| **[POI](../game/runs.md#pois) state** | Low-frequency events (started / progress tick / completed / rewarded). Reliable RPC, not tick state. |
| **Summoners** | Client-owned via `get_sync_owner_peer_id()` — your own movement is local and lag-free, exactly like OTR's drone. |
| **Enemies** | Host-authoritative. Same troop-volume problem as friendly bubbles; the spike's answer applies to both. |

## Order of work

1. ~~Spike per-troop streaming (2 peers, measure bytes + how the crowd reads).~~ **Done 2026-07-30** — see above.
2. ~~Steam transport on 4.7 + real-internet test.~~ **Done 2026-07-31** — stable; stutter found and fixed.
3. Rebuild the game as isolated systems with the winner baked in — [Architecture](architecture.md) has the build order. Networking ports over **last**, because it's now the lowest-risk piece.
