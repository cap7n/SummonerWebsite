# The Graveyard (Hub & Meta Progression)

Players start every session in the **graveyard**. It's the safe hub *and* the meta-progression screen — one place, walked around in person rather than a menu.

## What's decided <span class="pill done">DONE</span>

- The graveyard is the **starting location and the meta hub**. All four players are here between runs.
- It's a **real shared online space, not a menu** — all four players spawn into it together before a run; the hub *is* the lobby (decided 2026-07-31). A graybox `Hub` scene with the four spawn points exists in the game project (`Summoner/scenes/hub/`).
- It contains **15 graves** (decided 2026-08-01). Buying a grave with points grants its [item](items.md) and **locks that tombstone to the buyer**; spending more points on your grave upgrades its item. A grave is both the upgrade node and (for summoning items) the source of a kind of unit.
- **Points** are the one meta currency. Players start with ~10, spend them here on buying and upgrading graves, and **find more collectively on runs** — points found by anyone raise everyone's total (find 3 → every player has 13 next run, spent individually).
- Players carry their loadout in **8 item slots** (each with 4 mod sockets) — see [Items](items.md).
- Deployment goes from the graveyard into a [run](runs.md) — hub-and-sortie, not a linear chain.

## The shape of it

```
Graveyard (hub, 4 players)
├── 15 graves ── buy with points ──▶ item + grave locked to you
│                 spend more     ──▶ upgrade the grave's item
├── Your loadout: 8 item slots × 4 mod sockets ── tradable with the party
└── Deploy ──▶ Run: big RTS map, POIs, caravan ──▶ (survive) back to the graveyard
```

The fantasy is coherent with the fiction: you're a summoner, your army comes out of graves, and the graveyard growing over time *is* your save file. Levelling a tombstone should be visible on the tombstone — a hub that visibly accumulates is the cheapest progression feedback there is.

## Open questions

!!! warning "Not decided"

    - **Points: respendable budget or consumable currency?** "All 13 to spend each run" reads like a per-run draft budget; permanent grave locks read like purchases. The load-bearing item question — see [Items](items.md).
    - **Where exactly do points come from on a run?** [POI](runs.md) rewards, caravan survival, kills, extraction — or a mix? Whether they can be spent *mid-run* changes the pacing.
    - **What resets on death?** Grave locks/levels are presumably permanent (that's the meta); whether a wipe costs points or items is open.
    - **Unit types themselves.** How many, and what axes do they differ on — tanky / fast / ranged / support? Ranged units break the "contact = combat" simplicity of the [bubble](bubble.md), so this is a load-bearing choice, not flavour.
    - **Are the 15 graves one shared graveyard state** (host's world? party save?) or does each player see their own 15? Locking a grave to a player implies one shared state — where does it live and persist?
    - **Does the graveyard have anything to do besides shopping?** A hub you only pass through is a menu with walking. Something that makes it a *place* (a defensible ground, a training dummy, visible progress) is worth designing.
