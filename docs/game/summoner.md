# The Summoner

The player character: a single figure who walks the battlefield in person, with the army shaped around them.

## What's decided <span class="pill done">DONE</span>

- **Direct WASD control**, camera-relative (W is always "up the screen"), with sprint (Shift, ~1.7×).
- The summoner is **inside the bubble, always** — the leash guarantees it. Your body position is an army decision: walking to the front line drags the bubble's centre of gravity with you.
- Speed: ~9 u/s walk. The bubble's cap derives from this, so summoner speed is the army's tempo stat.
- Visual: gold/amber against the dark-green world, deliberately the highest-contrast thing on screen so you can always find yourself in a melee.

## Camera {#camera}

RTS camera with two modes, toggled with **F** (Space re-centres and re-follows):

- **Locked** — glued to the summoner. Default.
- **Unlocked / free** — fly around the map like any RTS: pan with arrows / middle-drag / screen-edge; any explicit pan auto-detaches so the mode switch is usually invisible.

Zoom on wheel, orbit on right-drag, Q/E rotate.

On the [big maps](runs.md), unlocked camera isn't a convenience — it's how you read POI layout, watch the [caravan](caravan.md), and see what your three friends have revealed under [shared fog](runs.md#fog-of-war).

## Spells <span class="pill done">DONE (direction)</span> {#spells}

Decided 2026-07-31: **summoners are wizards, and wizards cast.** The game is not only horde — it's horde *plus* spells, and the spells are **hardcore**.

- The feeling being chased is **power**. If you prepared — levelled the right tombstones, brought the right spells — you get to overwhelm the enemy in bodies *and* in magic.
- "Hardcore" means spells that matter: fight-turning, screen-visible, worth building a run around. Not a poke on a cooldown.
- Preparation is the price of that power. Unprepared should feel meaningfully weaker — how much weaker is one of the [open questions](../project/open-questions.md#spells--power).

Everything below the direction is undecided — source of spells (items per [pillar 3](../pillars.md), tombstones, or their own track), costs, count equipped, targeting model, friendly fire, enemy casters. All listed in [Open Questions](../project/open-questions.md#spells--power) for answering.

## Open <span class="pill idea">IDEA</span>

!!! warning "Not decided"
    - Can the summoner fight at all, or is the army the only weapon? (Current prototype: the summoner is untargetable and unarmed; enemies ignore them.)
    - **Summoner death now needs a cost that isn't "run over"** — the [caravan](caravan.md) owns the fail state. Respawn at the caravan? Timer? Lose your fielded troops? This doubles as the co-op downed-state answer.
    - What happens when troops die around the summoner — is losing the whole bubble anything more than being temporarily useless?
    - Do you re-summon mid-run (and from what — [points](graveyard.md)? the caravan?), or is the army you deployed with the army you have?
    - Do [items](items.md) grant the summoner personal abilities (dash, wall, buff aura), army abilities, or both?
    - Per-summoner identity in [co-op](coop.md): are all four summoners identical, or differentiated by their equipped items only? (With 4 on screen, they at least need to be told apart at a glance — colour per player, while gold stays "the player characters" as a class.)
