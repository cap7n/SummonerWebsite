# Items & Equipment

Two pillars live here: **item equipping & collecting**, and **item-based abilities**. Nothing is implemented yet — this page records intent and the decisions that need making, so building can start from a real spec instead of a vibe.

## The intent

- **No classes, no skill trees.** What you can do is what you carry. Your build *is* your inventory.
- **You pick starting items at the [Graveyard](graveyard.md)** before deploying — the run's opening draft.
- **Collecting is physical.** Items exist in the world on a [run](runs.md), often as [POI](runs.md#pois) rewards; you (or your bubble?) have to reach them, and getting them home matters. A great item across the map from the [caravan](caravan.md) is a real dilemma — and if the caravan is what carries loot home, losing it loses the haul too.
- **Equipping is scarce.** Limited slots force real choices — the roguelite loop's drafting tension, but with objects you went and grabbed rather than menu picks.
- **Abilities come from items.** Active abilities (castable) and passive modifiers both. An item that changes how the *bubble* behaves (stretch faster, larger area, sever pods…) is the most Summoner-flavoured ability space and probably the first one to explore.

## Sketch of the space

!!! warning "Not decided — everything below is candidate design, not commitment"

    **Item categories that suggest themselves:**

    | Category | Example fantasy | Feeds pillar |
    |---|---|---|
    | Bubble mods | +area (bigger army cap), tighter formation, aura effects | Horde control |
    | Summon items | troops of a type: bruisers, runners, chanters | Horde control / [Graveyard](graveyard.md) |
    | Summoner actives | dash, rally-shout (snap-regroup), ward circle | Item-based abilities |
    | Caravan gear | armour, speed, repair kits, extra guards | [Caravan](caravan.md) / party utility |
    | Trinkets / passives | troop HP, regroup speed, on-kill effects | Roguelite build variety |

    **Open questions (the load-bearing ones):**

    - Who carries an item home — the summoner personally, the bubble engulfing it, or **the [caravan](caravan.md)**? The caravan is the strongest candidate: it makes loot physically at risk and gives the caravan a reason to exist beyond "thing that can die".
    - Do items persist between runs (collection = meta-progression) or reset (roguelike-pure)? This is the single biggest roguelite structure decision — see [Runs](runs.md).
    - **Two currencies?** [Tombstone points](graveyard.md) already carry meta-progression. If items persist too, they must progress a *different* axis (unit power vs. player capability) or one of them is noise.
    - Slot model: paper-doll (head/hand/etc.), generic slots (any 4 items), or size-based bag? 
    - In [co-op](coop.md): per-player loot or shared pool? Trading? (At **4 players** a shared pool means one grabby friend ends the discussion — instanced drops are the safer default.)
    - Are ability items *used up*, on cooldown, or channelled by committing troops (spend X troops from the bubble to cast — very on-theme)?
