# Open Questions

The decisions that are deliberately **not made yet**. When one gets decided, move it to the [Decision Log](decisions.md) with the reasoning, and update the owning page.

## Severed pods {#severed-pods}

*The* signature open question. When a stretched pod is cut loose (a mechanic we want, not yet built — currently right-click just retracts), what does the severed group become? All three candidates were liked; they may even coexist as [item](../game/items.md)-granted variants:

| # | Behaviour | Character | Cost |
|---|---|---|---|
| 1 | **Holds ground** — parks where severed, fights anything that touches it, not steerable | Simple, sets up "deploy a garrison" upgrades | Cheapest |
| 2 | **Commandable** — becomes a selectable mini-bubble you can send marching | Most powerful, most RTS | Needs a selection system |
| 3 | **Seeker** — auto-marches at the nearest enemy bubble, fire-and-forget | Most aggressive, feels like a thrown weapon | Needs pathing + target policy |

## Control & combat

- Chase cap: how far may a fighting troop stray from its slot? (Fix for the melee-scrum issue — [Combat](../game/combat.md).)
- Enemy response rule: defenders-only, or full-army response to a pod poke?
- Rebind break-connection off right-click, or live with the orbit overlap?
- Should enemy AI ever stretch?
- Troop types: identical troops vs typed summons?

## Structure & meta

- What persists between runs? (Gates the whole [item system](../game/items.md).)
- Run structure: linear / node-map / hub-and-sortie?
- Summoner killability & the run's failure condition.
- Bubble area, max troops, fill rate as upgrade axes — which are items, which are meta?

## Co-op

Settled 2026-07-30: **4 players**, **no anti-cheat**, **OTR's network stack** (see [Networking](../tech/networking.md)). What's left:

- Friendly bubble overlap/merge rules — does an ally's disc block your pod, or can you stretch through it? (Four discs in one choke makes "exclusive" possibly unplayable.)
- Loot sharing: per-player instanced or shared pool?
- Downed state when a player's army is wiped — at 4 players this happens constantly, so it needs a real mechanic.
- Scaling: enemies per player, bigger enemy bubbles, or asymmetric objectives?
- Per-player army size at 4 — is it still 50 each, or does the cap shrink to keep 200 bodies sane?
- Joining: drop-in at instance boundaries, or lobby-locked at run start?
- **Are troops entities or particles on the wire?** The [troop-sync spike](../tech/networking.md#the-troop-sync-problem) decides it — **must run before the rebuild locks its architecture.**
