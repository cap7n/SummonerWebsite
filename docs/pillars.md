# Design Pillars

The six features Summoner is being built around, plus the working rules. These are strong defaults, not laws — break them on purpose, not by accident.

## 1. Horde control, one organism

You command an army, but you never micro a unit. The **bubble is the interface**: everything the army does is expressed by moving, stretching, and splitting one living shape. If a feature requires clicking on an individual troop, it's probably fighting this pillar.

## 2. Co-op native

Summoner is designed to be played **with up to three friends — 4 players**, each with their own summoner and their own bubble. Co-op is not a mode bolted on later: any system we design (stretching, items, revives, map instances) should be asked *"what does this do with four bubbles on the field?"* at design time. Solo stays playable; it's just a lobby of one.

Cheating is **explicitly not a concern** (private sessions, no ladder), which buys client-authoritative simplicity. The stack is the one already proven in OTR — see [Networking](tech/networking.md). Drop-in rules and how friendly bubbles interact are still [open questions](project/open-questions.md).

## 3. Items are the power system

There are no classes and no skill trees. **Abilities come from items**: what you collect on a run and choose to equip is what you can do. Equipping is a real decision (slots are scarce), collecting is a real activity (items drop in the world, you have to get them home). See [Items & Equipment](game/items.md).

## 4. Roguelite structure

The game is played in **runs**. Death matters but doesn't erase you: some things persist (collected items? unlocks? — [open](project/open-questions.md)), the rest resets. The run structure is what makes item-collecting tense instead of a chore.

## 5. Instance-based maps

Levels are **instanced**: you enter a map, it's generated/assembled for that visit, you fight through it, you leave (or die). No persistent overworld simulation. This keeps scope honest, makes co-op sessions joinable, and gives the roguelite loop clean boundaries.

## 6. Prototype honestly, rebuild deliberately

The current PoC exists to answer feel questions cheaply, and it will be **rebuilt on an architecture the developer understands and owns**. Prototype code is allowed to be ugly; the rebuild is not allowed to start until the control-scheme A/B has a verdict. Findings outlive code — record them here.

## Working-relationship notes

- **Feel first, numbers second.** The A/B toggle (F1) exists so control schemes are compared in the same battle, not from memory.
- **Verify with rendered frames, not vibes.** The prototype workflow renders real PNG frames headlessly for visual checks — see [Engine & Prototype Workflow](tech/engine.md).
- **Dark green, not blue.** The palette is dark green by explicit preference. (The developer hates blue. It's in the [Decision Log](project/decisions.md). It's binding.)
