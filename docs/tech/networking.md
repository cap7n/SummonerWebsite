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

## The troop-sync problem {#the-troop-sync-problem}

Four players × 50 troops = **200 friendly bodies**, plus whatever the enemy fields. Sync them the OTR way — one entity, one snapshot, every tick — and the numbers say no:

| Approach | Per tick | At 60 Hz, per receiving peer | Host upstream (3 clients) |
|---|---|---|---|
| Per-troop entity sync (~20 B/troop, 200 troops) | ~4 KB | ~240 KB/s | **~720 KB/s (≈5.8 Mbit/s)** |
| Per-troop at 20 Hz | ~4 KB | ~80 KB/s | ~240 KB/s |
| **Bubble-shape sync** (~40 B/bubble, ~10 bubbles) | ~0.4 KB | ~24 KB/s | ~72 KB/s |

Per-troop sync also blows past MTU every single tick (4 KB → four chunked packets per peer per tick, ~240 packets/s/peer), which is exactly the case the chunker exists to survive, not to live in.

!!! warning "Not decided — the proposed way out"
    **Sync the organism, not the units.**

    Put the *bubble* on the wire, not the troops: centre, stretch vector, fill fraction, alive count, faction, latch state — a few dozen bytes per bubble. Each machine then grows its own crowd inside that shape locally: same seeded scatter, same formation solver, same walk-back logic. Combat sends **counts and events** (`bubble 3 lost 7`), never per-troop transforms.

    - Why it's allowed: the [design pillar](../pillars.md) says a troop is never individually meaningful. If troop #17 stands 30 cm to the left on your screen, nothing in the game reads that. And with no anti-cheat requirement, a client owning its own crowd's visuals is fine.
    - Why it might fail: melee reads badly if the crowd on each screen isn't at least *roughly* agreed — a death animation should play near where that screen thinks the fight is. Kills as counts (not identities) is the mitigation to test.
    - **This is the feasibility spike**, and it must run before the rebuild's architecture locks. It decides whether a troop is an entity or a particle — which is the single biggest structural question in the rebuild.

!!! note "The 2026-07-30 simplification made this much easier"
    Now that the [bubble](../game/bubble.md) is a plain circle locked to the summoner — no move orders, no stretching — a player's bubble state is *almost entirely implied by their summoner transform*. Shape-sync shrinks from "centre + stretch vector + fill + counts" to roughly **transform + alive count per unit type**. The crowd is grown locally from that. If the spike was going to work before, it will work comfortably now.

## Other things that go on the wire

| State | Notes |
|---|---|
| **[Caravan](../game/caravan.md)** | Host-authoritative, one entity, cheap. Any peer can *request* a move order (input RPC); the host applies it and syncs the result. Its death is a run-ending event — send it reliably, never as interpolated state. |
| **[Fog of war](../game/runs.md#fog-of-war)** | Shared vision means **one** fog state for the party, not four. Reveal is a coarse grid; send deltas (newly revealed cells) reliably, not the whole grid per tick. Massively cheaper than per-player fog — a real argument for the shared-vision decision beyond feel. |
| **[POI](../game/runs.md#pois) state** | Low-frequency events (started / progress tick / completed / rewarded). Reliable RPC, not tick state. |
| **Summoners** | Client-owned via `get_sync_owner_peer_id()` — your own movement is local and lag-free, exactly like OTR's drone. |
| **Enemies** | Host-authoritative. Same troop-volume problem as friendly bubbles; the spike's answer applies to both. |

## Order of work

1. Spike shape-sync vs per-troop sync in a throwaway scene (2 peers, 100 troops, measure bytes + how the crowd reads).
2. Rebuild the architecture with the winner baked in ([Engine & Prototype Workflow](engine.md)).
3. Steam layer last — it's the part that already works.
