# The Graveyard (Hub & Meta Progression)

Players start every session in the **graveyard**. It's the safe hub *and* the meta-progression screen — one place, walked around in person rather than a menu.

## What's decided <span class="pill done">DONE</span>

- The graveyard is the **starting location and the meta hub**. All four players are here between runs.
- It's a **real shared online space, not a menu** — all four players spawn into it together before a run; the hub *is* the lobby (decided 2026-07-31). A graybox `Hub` scene with the four spawn points exists in the game project (`Summoner/scenes/hub/`).
- It contains **15 graves** (decided 2026-08-01). Buying a grave with points grants its [item](items.md) and **locks that tombstone to the buyer**; spending more points on your grave upgrades its item. A grave is both the upgrade node and (for summoning items) the source of a kind of unit.
- **Points** are the one currency, and a **respendable per-run budget** — re-allocated fully at the start of every run (every run is a draft; no permanent point meta). The pool is **host-owned and shared**: one total in the host's lobby, copied to every player (host's world collected 20 → everyone spends 20, individually). Points found by anyone on a run raise the pool. Permanent progression comes from **world unlocks that stay in the graveyard** instead (e.g. a rescued merchant sets up shop here).
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

    - **Where exactly do points come from on a run?** [POI](runs.md) rewards, caravan survival, kills, extraction — or a mix? Whether they can be spent *mid-run* changes the pacing.
    - **What does a lost run cost?** Points respend anyway — does a wipe shrink the pool, or is the lost time the whole price?
    - **Which world finds become permanent graveyard unlocks** (merchant, extra graves, unit types)? That's the meta axis now.
    - **Unit types themselves.** How many, and what axes do they differ on — tanky / fast / ranged / support? Ranged units break the "contact = combat" simplicity of the [bubble](bubble.md), so this is a load-bearing choice, not flavour.
    - **Are the 15 graves one shared graveyard state** (host's world? party save?) or does each player see their own 15? Locking a grave to a player implies one shared state — where does it live and persist?
    - **Does the graveyard have anything to do besides shopping?** A hub you only pass through is a menu with walking. Something that makes it a *place* (a defensible ground, a training dummy, visible progress) is worth designing.
