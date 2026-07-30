# The Graveyard (Hub & Meta Progression)

Players start every session in the **graveyard**. It's the safe hub *and* the meta-progression screen — one place, walked around in person rather than a menu.

## What's decided <span class="pill done">DONE</span>

- The graveyard is the **starting location and the meta hub**. All four players are here between runs.
- It contains **tombstones**. A tombstone is both the upgrade node and the summoning source for a kind of unit.
- **Points** are the meta currency. You spend points at tombstones to:
    - **Level up** a unit type (make that unit stronger), and
    - **Unlock / summon different kinds of units** (broaden what your bubble can contain).
- Players also **pick their starting items** here before deploying ([Items](items.md)).
- Deployment goes from the graveyard into a [run](runs.md) — hub-and-sortie, not a linear chain.

## The shape of it

```
Graveyard (hub, 4 players)
├── Tombstones ── spend points ── level units / unlock unit types
├── Starting-item pick
└── Deploy ──▶ Run: big RTS map, POIs, caravan ──▶ (survive) back to the graveyard
```

The fantasy is coherent with the fiction: you're a summoner, your army comes out of graves, and the graveyard growing over time *is* your save file. Levelling a tombstone should be visible on the tombstone — a hub that visibly accumulates is the cheapest progression feedback there is.

## Open questions

!!! warning "Not decided"

    - **Where do points come from?** [POI](runs.md) rewards, caravan survival, kills, run completion — or a mix? Whether points also drop *during* a run (spend mid-run?) or only settle at extraction changes the whole pacing.
    - **What resets on death?** Tombstone levels are presumably permanent (that's the meta), but points-in-hand, unlocked-but-unsummoned units, and collected items may not be. This is the roguelite line — see [Runs](runs.md).
    - **Per-player or shared graveyard?** In [4-player co-op](coop.md): does each player own their own tombstones and army, or is the graveyard a shared base everyone upgrades? Shared is warmer and cheaper to build; per-player protects solo progress and lets players specialise.
    - **Unit types themselves.** How many, and what axes do they differ on — tanky / fast / ranged / support? Ranged units break the "contact = combat" simplicity of the [bubble](bubble.md), so this is a load-bearing choice, not flavour.
    - **Is there a point cost to *fielding* an army?** Levelling is one thing; whether summoning a unit into a run also costs points (an army-composition budget per run) is the difference between "power grows forever" and "every run is a draft".
    - **Are the starting-item picks limited by slots, points, or unlocks?** Ties into [Items](items.md).
    - **Does the graveyard have anything to do besides shopping?** A hub you only pass through is a menu with walking. Something that makes it a *place* (a defensible ground, a training dummy, visible progress) is worth designing.
