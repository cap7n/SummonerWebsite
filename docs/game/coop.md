# Co-op

A founding pillar: Summoner is designed to be played together, each player with **their own summoner and their own bubble**. Not implemented yet — this page exists so every other system gets designed with co-op in the room.

## What's decided <span class="pill done">DONE</span>

| Decision | Value |
|---|---|
| **Player count** | **4** (1–4; solo must stay playable) |
| **Anti-cheat** | **None.** Explicitly out of scope — friends-only sessions, trust the client |
| **Network stack** | **Same system as [OTR](../tech/networking.md)** — Steam lobby + `SteamMultiplayerPeer`, one tick manager, `StateBuffer` interpolation |

Each player steers their own army organism. Co-op is **cooperative horde control**: the interesting decisions are *between* the bubbles — who takes the choke, who stretches to flank, who holds the reserve. [Instance-based maps](runs.md) exist partly *for* co-op: join at instance boundaries, no mid-simulation sync horror.

### Why "we don't care about cheating"

It's a co-op game played with friends in a private lobby. There's no ladder, no trading economy, no competitive integrity to protect. That decision buys real budget:

- Client-authoritative movement is allowed — a player's own summoner (and probably their own bubble) can be simulated on their machine with zero input lag and no reconciliation. OTR already does exactly this for the drone via per-entity sync ownership.
- RPC handlers don't need the full validate-the-sender treatment OTR applies. (Keeping the habit costs nothing, so do it where it's free — just don't design *around* it.)
- If a desync produces a slightly different troop scatter on each machine, that's a bug to fix, not an exploit to prevent.

## The 4-player consequence

Going from 2 to 4 changes the load-bearing numbers, not the fantasy:

- **Troop count in the world:** 4 × 50 = **200 friendly troops** plus enemies. The prototype's O(n²) separation and per-troop nodes cap out around a few hundred *total*. 4-player co-op alone puts the rebuild's [combat](combat.md) architecture over that line — spatial partitioning is no longer optional.
- **Screen space:** four bubbles need room. Instance layouts (chokes, corridors) have to be sized for four organisms, or stretching stops being a decision and starts being a traffic jam.
- **Sync budget:** naively syncing 200 troops at 60 Hz is not viable — see [Networking](../tech/networking.md#the-troop-sync-problem) for the numbers and the proposed way out (sync the *shape*, not the units).
- **Every bubble-bubble rule gets harder.** Overlap, merging, and friendly-pod pass-through all have to work with four discs in one choke, not two.

## Still open

!!! warning "Not decided"

    - **Bubble-bubble interaction:** do friendly bubbles overlap freely, merge at the seam, or stay exclusive? Can one player's pod stretch *through* an ally's disc? (At 4 players, "exclusive" may be unplayable in tight maps.)
    - **Loot:** per-player instanced or shared pool? ([Items](items.md))
    - **Downed state:** when one summoner's army is wiped, what keeps them playing — spectate, ghost-walk, or can an ally's bubble shelter/revive them? At 4 players this happens *often*; it needs a real answer, not a placeholder.
    - **Scaling:** enemy bubbles per player, bigger enemy bubbles, or asymmetric objectives? Does a 4-player run have the same map pool as a solo run?
    - **Army size per player at 4:** does everyone keep 50, or does the per-player cap shrink so the total stays sane? (Feel question — 50 each is the fantasy, budget may argue.)
    - **Joining:** drop-in at instance boundaries only, or lobby-locked at run start? Roguelite progress makes mid-run joins awkward.

## Prototype implication (now)

The PoC is single-player, and stays that way. What co-op demands of the **rebuild** is architectural, not featural:

- Keep simulation state (troops, bubbles) cleanly separated from input/control, so a second, third, and fourth controller — local or networked — attach without surgery.
- Give every bubble an owner peer from day one, even in single-player (owner = the only peer).
- Design the bubble's state as something *describable in a few dozen bytes* (centre, stretch vector, fill, counts), because that's what has to go over the wire.

The [sync feasibility spike](../project/backlog.md) should happen **before** the rebuild's architecture locks, because its answer decides whether troops are entities or particles.
