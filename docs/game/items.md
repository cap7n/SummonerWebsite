# Items & Equipment

The item system is **decided** (2026-08-01). Your build is your inventory: no classes, no skill trees — what you carry is what you can do, and what you carry is mostly *an army*.

## The model <span class="pill done">DONE</span>

**Three item variants:**

| Variant | What it is | Example |
|---|---|---|
| **Summoning item** | Holds a unit type with stats. The item *is* a troop pool. | `x/10 Skeletons · regen 1 per 10 s · 10 HP · 10 ATK · 2 DEF · melee` |
| **Spell item** | A castable or passive spell: range, AoE, effect. Some are temporary summons. | Fireball, ward circle, raise-dead |
| **Modifier (mod)** | Socketed *under* a summoning or spell item; changes how it works. | +regen, +HP, bigger AoE |

**Slots:** every player has **8 item slots**. Each item slot has **4 mod slots** under it — you only see the top row of 8; dragging a mod over an item grows the panel upward to reveal its mod sockets. Max loadout: 8 items × (1 + 4 mods) = 40 pieces.

**Items come from [graves](graveyard.md):** the graveyard has **15 graves**. Buying a grave with points grants its item and **locks that tombstone to you** — no one else can buy it. Spending more points on your grave upgrades its item.

**Items are tradable.** Any item (including mods) can be handed to another player. 15 graves shared by 4 players is fewer than 4 × 8 slots — scarcity and specialisation are the point, and trading is how the party negotiates it.

**Points** are the one currency ([Graveyard](graveyard.md)): start ~10, spent in the graveyard, **found collectively during runs** — points found by anyone raise *everyone's* total (find 3 in a run → every player has 13 next run, spent individually). This closes the old two-currency worry: there is only points.

## Why this shape works

- **Summoning items make composition tangible.** Your army isn't a stat screen — it's eight physical objects, each a pool of bodies with its own regen. Losing troops mid-run and watching an item tick back up is the passive bubble's economy.
- **Regen-per-item is the pacing knob.** Between-fight recovery speed is itemised, so "sustain build vs burst build" is a real choice.
- **The graveyard stays the stage.** Graves-as-item-sources keeps meta progression physical and visible — a claimed, levelled grave is a trophy in a shared space.
- **Trading + collective points make the meta co-op**, matching the [pillars](../pillars.md): the party grows together, then argues about who gets the good grave.

## Still open

!!! warning "Not decided"

    - **Points: respendable budget or consumable currency?** "All 13 to spend each run" reads like a *budget re-allocated every run* (every run is a draft); grave buys that lock permanently read like *purchases*. Which is it — or hybrid (grave claims permanent, upgrades re-allocated)?
    - **Does a traded item move with its socketed mods,** or must mods be unsocketed first?
    - **Are all 4 mod slots open from the start,** or do they unlock (per-item upgrade, point cost, item rarity)?
    - **Do the 15 graves offer fixed items** (the catalogue is the graveyard) **or rotate/randomise** per meta-state?
    - **Where do run-found items fit** — do POIs drop items directly, or only points? (If items drop, who carries them home — the [caravan](caravan.md) question stands.)
    - **What happens on party mismatch** — playing with a different group: do your items travel with your profile?
