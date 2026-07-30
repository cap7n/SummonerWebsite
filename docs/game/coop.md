# Co-op

A founding pillar: Summoner is designed to be played with a friend, each with **their own summoner and their own bubble**. Not implemented; this page exists so every other system gets designed with co-op in the room.

## The intent

- **Two summoners, two bubbles**, one battlefield. Each player steers their own army organism.
- Co-op is **cooperative horde control**: the interesting decisions are between the bubbles — who takes the choke, who stretches to flank, who holds the reserve.
- [Instance-based maps](runs.md) exist partly *for* co-op: join at instance boundaries, no mid-simulation sync horror.

## The design questions every system must answer

!!! warning "Not decided"

    - **Bubble-bubble interaction:** do friendly bubbles overlap freely, merge at the seam, or stay exclusive? Can one player's pod stretch *through* an ally's disc?
    - **Player count:** locked to 2, or 2–4? (Every answer above gets harder at 4.)
    - **Loot:** per-player instanced or shared pool? ([Items](items.md))
    - **Downed state:** when one summoner's army is wiped, what keeps them playing — spectate, ghost-walk, or can the ally's bubble shelter/revive them?
    - **Scaling:** enemy bubbles per player, bigger enemy bubbles, or asymmetric objectives?
    - **Tech:** Godot high-level multiplayer, peer-to-peer vs listen server, rollback needs are near zero (no twitch aiming) — but troop-swarm state sync at 50+ units/player needs an early feasibility spike. **This is the one co-op item that should be prototyped before the architecture rebuild locks in**, because it constrains the rebuild.

## Prototype implication (now)

The PoC is single-player, but the rebuild's architecture must not make co-op retrofit-hard: keep simulation state (troops, bubbles) cleanly separated from input/control so a second controller — local or networked — can be attached without surgery.
