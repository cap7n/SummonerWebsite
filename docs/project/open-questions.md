# Open Questions

The decisions that are deliberately **not made yet**. When one gets decided, move it to the [Decision Log](decisions.md) with the reasoning, and update the owning page.

## Severed pods <span class="pill parked">PARKED</span> {#severed-pods}

Parked 2026-07-30 along with the whole stretch system — the [bubble is a passive aura](../game/bubble.md) now, so there is no pod to sever. Kept on file because the idea outlived its mechanism: if the simplified bubble ever needs a way to commit part of the army, this is the drawer. All three candidates were liked; they may yet return as [item](../game/items.md)-granted variants:

| # | Behaviour | Character | Cost |
|---|---|---|---|
| 1 | **Holds ground** — parks where severed, fights anything that touches it, not steerable | Simple, sets up "deploy a garrison" upgrades | Cheapest |
| 2 | **Commandable** — becomes a selectable mini-bubble you can send marching | Most powerful, most RTS | Needs a selection system |
| 3 | **Seeker** — auto-marches at the nearest enemy bubble, fire-and-forget | Most aggressive, feels like a thrown weapon | Needs pathing + target policy |

## The big one right now

**Is a passive bubble enough?** With no move orders and no stretching, moment-to-moment play is walking your body around. The bet is that [composition](../game/graveyard.md), the [caravan](../game/caravan.md) and [POI routing](../game/runs.md) carry the tension instead. This is a feel question and it has to be answered in-engine, not in this wiki.

## Control & combat

- Chase cap: how far may a fighting troop stray from its slot? (Fix for the melee-scrum issue — [Combat](../game/combat.md).)
- Enemy response rule: defenders-only, or does the whole enemy force react?
- **Unit types**: how many, and what axes — tanky / fast / ranged / support? Ranged breaks "contact = combat", so it's a fork, not a stat.
- Do enemies preferentially attack the [caravan](../game/caravan.md), or just fight what's nearest?
- Should enemy bubbles move/patrol at all, or hold ground as static threats on the map?

## Graveyard & meta

- Where do [points](../game/graveyard.md) come from — POIs, kills, extraction, caravan survival?
- What resets on a lost run: points-in-hand, unlocked units, collected items? (Tombstone levels persist — that's settled.)
- **Shared or per-player graveyard** in [co-op](../game/coop.md)?
- Does fielding an army cost points too (per-run draft), or is levelling the only spend?
- Two currencies problem: if [items](../game/items.md) persist as well as points, they must progress different axes.

## Run structure

- POI objective types, reward types, and whether POIs are optional (probably yes — that's the Helldivers shape).
- Does the [caravan](../game/caravan.md) auto-advance or move only when told? Different games.
- Caravan command conflicts at 4 players; caravan speed; what it carries; repair.
- Summoner death cost, now that the caravan owns the fail state.
- Map generation: hand-built pool → procedural assembly → full procgen? (Start hand-built.)
- Session length target, and therefore map size in minutes-of-caravan-travel.

## Co-op

Settled 2026-07-30: **4 players**, **no anti-cheat**, **OTR's network stack** (see [Networking](../tech/networking.md)). What's left:

- Friendly bubble overlap/merge rules — does an ally's disc block your pod, or can you stretch through it? (Four discs in one choke makes "exclusive" possibly unplayable.)
- Loot sharing: per-player instanced or shared pool?
- Downed state when a player's army is wiped — at 4 players this happens constantly, so it needs a real mechanic.
- Scaling: enemies per player, bigger enemy bubbles, or asymmetric objectives?
- Per-player army size at 4 — is it still 50 each, or does the cap shrink to keep 200 bodies sane?
- Joining: drop-in at instance boundaries, or lobby-locked at run start?
- **Are troops entities or particles on the wire?** The [troop-sync spike](../tech/networking.md#the-troop-sync-problem) decides it — **must run before the rebuild locks its architecture.**
