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

## Spells & power <span class="pill idea">NEW 2026-07-31</span> {#spells--power}

The direction is decided — [summoners are wizards with hardcore spells](../game/summoner.md#spells), power fantasy in bodies *and* magic. Everything else is open:

- **Where do spells come from** — items ([pillar 3](../pillars.md) would stay intact), tombstones/points like units, or their own progression track?
- **Cost model**: cooldowns, a mana pool, or a horde-coupled resource (souls from kills — thematic, and it links army performance to casting)? How many spells equipped at once?
- **Targeting**: cast around your body (range-limited, keeps you in the fight) or click-anywhere with the [free camera](../game/summoner.md#camera)? The second turns the unlocked camera into a combat tool — big decision.
- **Can spells target your own troops** — buffs, heals, raise-dead-mid-fight? And is there friendly fire against allies' crowds?
- **Do enemies cast too?** Enemy wizards as elite threats or POI bosses would sell the fantasy from the receiving end.
- **Combat texture — how fast should an even fight resolve?** Total War-style stalemates are probably out (leaning, see [Combat](../game/combat.md)). What replaces attrition: morale/rout, fast time-to-kill, spell breakpoints?
- **What does *unprepared* look like?** If preparation = power, is failing preparation a slow grind or a collapse? And in co-op: what keeps three less-prepared players relevant next to one powerhouse?

## Map generation <span class="pill idea">NEW 2026-07-31</span> {#map-generation}

[Procgen is decided](../game/runs.md#map-generation); the generator's contract is not:

- **How big is a map, in minutes of caravan travel?** The tech no longer constrains this ([measured](../tech/architecture.md#terrain-results)) — it's purely a pacing choice, and it gates POI count and session length.
- **What is guaranteed vs random** — POI count, road connectivity, min/max extraction distance, fairness for 4 spawns?
- **Seeds**: shareable ("play yesterday's map again with friends")? A daily seed for the community?
- How much authored variety do POI stamps need before repetition shows — 3 per objective type? 10?

## The hub

- What do the other three players do while one shops at tombstones — ready-up vote to deploy? Can you test your army in the hub (training dummy, arena pit)?
- Is the hub host-owned (you visit *someone's* graveyard) or does everyone see their own tombstones in a shared space? (Ties into the shared-vs-per-player graveyard question below.)

## Control & combat

- Chase cap: how far may a fighting troop stray from its slot? (Fix for the melee-scrum issue — [Combat](../game/combat.md).)
- Enemy response rule: defenders-only, or does the whole enemy force react?
- **Unit types**: how many, and what axes — tanky / fast / ranged / support? Ranged breaks "contact = combat", so it's a fork, not a stat.
- Do enemies preferentially attack the [caravan](../game/caravan.md), or just fight what's nearest?
- Should enemy bubbles move/patrol at all, or hold ground as static threats on the map?

## Graveyard & meta

Settled 2026-08-01: **15 graves, buy-to-lock, points as the single currency, 8 item slots × 4 mod sockets, items tradable.** Points are a **respendable per-run budget** (every run is a draft, no permanent point meta) drawn from a **host-owned shared pool** copied to every player; mods and items trade freely, not bound to each other ([Items](../game/items.md), [Graveyard](../game/graveyard.md)). What's left:

- Where do points come from on a run — POIs, kills, extraction, caravan survival? Spendable mid-run?
- What resets on a lost run?
- Are all 4 mod sockets open from the start, or unlocked?
- Do the 15 graves offer a fixed catalogue or rotating/random items?
- **Permanent unlocks**: which world finds persist in the graveyard (merchant, extra graves, unit types)? This is the meta-progression axis now that points respend.
- **Maybe explore: persistent characters** — the host-pool model means progress lives in the host's lobby; deliberate experiment, revisit after playtests.

## Run structure

- POI objective types, reward types, and whether POIs are optional (probably yes — that's the Helldivers shape).
- Does the [caravan](../game/caravan.md) auto-advance or move only when told? Different games.
- Caravan command conflicts at 4 players; caravan speed; what it carries; repair.
- Summoner death cost, now that the caravan owns the fail state.
- Session length target, and therefore map size in minutes-of-caravan-travel.

## Co-op

Settled 2026-07-30: **4 players**, **no anti-cheat**, **OTR's network stack** (see [Networking](../tech/networking.md)). What's left:

- Friendly bubble overlap/merge rules — does an ally's disc block your pod, or can you stretch through it? (Four discs in one choke makes "exclusive" possibly unplayable.)
- Loot sharing: per-player instanced or shared pool?
- Downed state when a player's army is wiped — at 4 players this happens constantly, so it needs a real mechanic.
- Scaling: enemies per player, bigger enemy bubbles, or asymmetric objectives?
- Per-player army size at 4 — the spike proved 150+ each is affordable (sim *and* wire), so this is now a design question, not a technical cap.
- Joining: drop-in at instance boundaries, or lobby-locked at run start? (The spike's lobby already pulls late joiners into a running match, so drop-in is technically open.)

Settled 2026-07-31: troops are **entities** on the wire — the [troop-sync spike](../tech/networking.md#the-troop-sync-problem) ran, streaming won, and a real-internet Steam session confirmed it.
