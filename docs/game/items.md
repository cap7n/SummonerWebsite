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

**The 15 graves + 4 altars (decided 2026-08-01):** 6× **Skeletons** (10 melee bones each — buy three graves, walk with 30), 3× **Shield Skeletons** (tanky), 3× **Archer Skeletons** (ranged), 3× **Mage Skeletons** (long-range glass). Four **altars** hold the active spells: **Fireball**, **Bone Harvest** (10 temporary uncontrollable skeletons at a point), **Mend Bones** (heal), **War Cry** (+attack). Casting costs **mana** (pool 100, regen 4/s) on top of cooldowns — the anti-spam budget. **No mod graves in the hub yet** — mods arrive later (drops/rewards). Ranged units are in: the "contact = combat" fork was taken.

**Items are tradable.** Any item (including mods) can be handed to another player. 15 graves shared by 4 players is fewer than 4 × 8 slots — scarcity and specialisation are the point, and trading is how the party negotiates it.

**Hot-swapping is allowed but never free** (2026-08-01): the tray's top row is **standby** — parked actives are inactive, and anything equipped onto the bar **mid-run arrives cold**: spells on full cooldown, summon items at 0 troops with regen re-raising the pool from scratch. In the graveyard, swapping is free (deploy always starts you full and ready). This is the guard against 8 slots being 8 interchangeable machine guns.

**Nothing is irreversible** (2026-08-01): at your tombstone, Q undoes one upgrade level at a time and then releases the grave itself (full refund). In the inventory, a **Sell** zone takes any item you hold — your grave backs it → grave released and points refunded; nothing backs it (found item) → discarded; a *friend's* grave backs it → can't sell, trade it back (only the payer's tombstone releases those points).

**Points** are the one currency ([Graveyard](graveyard.md)), and they are a **respendable budget, not a consumable** (decided 2026-08-01): every run you re-allocate your full total in the graveyard — every run is a draft. The pool is **host-owned and shared**: the host's lobby has one point total, copied to every player (host's world collected 20 → everyone has 20 to spend individually). Points found by anyone on a run raise the pool. So points carry **no permanent per-player meta progression** — permanence comes from elsewhere: things found in the world that then *stay* in the graveyard (e.g. a rescued merchant who sets up shop at the start of your runs).

**Mods and items are not locked to each other** — both trade freely as separate objects; socketing is just an arrangement, not a bond.

## Why this shape works

- **Summoning items make composition tangible.** Your army isn't a stat screen — it's eight physical objects, each a pool of bodies with its own regen. Losing troops mid-run and watching an item tick back up is the passive bubble's economy.
- **Regen-per-item is the pacing knob.** Between-fight recovery speed is itemised, so "sustain build vs burst build" is a real choice.
- **The graveyard stays the stage.** Graves-as-item-sources keeps meta progression physical and visible — a claimed, levelled grave is a trophy in a shared space.
- **Trading + collective points make the meta co-op**, matching the [pillars](../pillars.md): the party grows together, then argues about who gets the good grave.

## Still open

!!! warning "Not decided"

    - **Are all 4 mod slots open from the start,** or do they unlock (per-item upgrade, point cost, item rarity)?
    - **Do the 15 graves offer fixed items** (the catalogue is the graveyard) **or rotate/randomise** per meta-state?
    - **Where do run-found items fit** — do POIs drop items directly, or only points? (If items drop, who carries them home — the [caravan](caravan.md) question stands.)
    - **Permanent unlocks**: which world finds persist in the graveyard (merchant, extra graves, new unit types)? This is now the whole meta-progression axis, since points respend.
    - **Maybe explore: persistent characters.** The host-owned shared pool means your progress lives in your friend's lobby, not with you. Flagged as a deliberate experiment (colleague's call) — revisit after playtests whether per-player persistent characters/profiles feel better.
