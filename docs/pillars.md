# Design Pillars

The six features Summoner is being built around, plus the working rules. These are strong defaults, not laws — break them on purpose, not by accident.

## 1. Horde control, one organism

You command an army, but you never micro a unit. Your troops are a **bubble around your summoner** — it follows you, it fights what it touches, and you never order it anywhere. If a feature requires clicking on an individual troop, it's fighting this pillar.

Control is expressed in four places instead: **where you walk**, **what you brought** ([tombstone-summoned unit types](game/graveyard.md)), **what you cast** ([spells](game/summoner.md#spells)), and **the shared map layer** ([caravan](game/caravan.md) + [POI](game/runs.md) routing).

## 2. Co-op native

Summoner is designed to be played **with up to three friends — 4 players**, each with their own summoner and their own bubble. Co-op is not a mode bolted on later: any system we design (stretching, items, revives, map instances) should be asked *"what does this do with four bubbles on the field?"* at design time. Solo stays playable; it's just a lobby of one.

Cheating is **explicitly not a concern** (private sessions, no ladder), which buys client-authoritative simplicity. The stack is the one already proven in OTR — see [Networking](tech/networking.md). Drop-in rules and how friendly bubbles interact are still [open questions](project/open-questions.md).

## 3. Items are the power system

There are no classes and no skill trees. **Abilities come from items**: what you collect on a run and choose to equip is what you can do. Equipping is a real decision (slots are scarce), collecting is a real activity (items drop in the world, you have to get them home). See [Items & Equipment](game/items.md).

Since 2026-07-31 summoners are also **wizards with hardcore [spells](game/summoner.md#spells)** — the power fantasy is overwhelming the enemy in bodies *and* magic, if you prepared. Whether spells arrive *as* items (keeping this pillar intact) or as their own track is an [open question](project/open-questions.md#spells--power).

## 4. Roguelite structure

The game is played in **runs**, out of and back to the [Graveyard](game/graveyard.md) — a hub you walk around, where **tombstones** are levelled with points to strengthen and unlock unit types. Death matters but doesn't erase you: tombstone levels persist, the rest is [open](project/open-questions.md). The [caravan](game/caravan.md) dying is what ends a run.

## 5. Instance-based maps

Levels are **big instanced RTS maps**: you deploy into one, it exists for that visit, you push through it, you leave (or lose the caravan). Fog of war covers them and **vision is shared by the whole party**. POIs are scattered across the map with objectives and rewards — the Helldivers shape: lots of space, real travel cost, optional greed. No persistent overworld simulation. See [Runs, Maps & the Roguelite Loop](game/runs.md).

## 6. Prototype honestly, rebuild deliberately

The current PoC exists to answer feel questions cheaply, and it will be **rebuilt on an architecture the developer understands and owns**. Prototype code is allowed to be ugly, and it's allowed to be **thrown away**: the click-move and stretch control schemes were both built, played, and then [parked](game/bubble.md#parked-prototype-systems) when the design got simpler. Findings outlive code — record them here.

## Working-relationship notes

- **Feel first, numbers second.** Systems get built, played, and cut on how they feel — the control-scheme A/B was run in-engine and settled by simplifying, not by argument.
- **Simple until proven boring.** When a system can be cut without losing the game, cut it and see. Parked, not deleted.
- **Verify with rendered frames, not vibes.** The prototype workflow renders real PNG frames headlessly for visual checks — see [Engine & Prototype Workflow](tech/engine.md).
- **Dark green, not blue.** The palette is dark green by explicit preference. (The developer hates blue. It's in the [Decision Log](project/decisions.md). It's binding.)
