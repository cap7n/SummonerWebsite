# Items & Equipment

Two pillars live here: **item equipping & collecting**, and **item-based abilities**. Nothing is implemented yet — this page records intent and the decisions that need making, so building can start from a real spec instead of a vibe.

## The intent

- **No classes, no skill trees.** What you can do is what you carry. Your build *is* your inventory.
- **Collecting is physical.** Items exist in the world on a [run](runs.md); you (or your bubble?) have to reach them, and getting them home matters. A great item you can't safely reach is a real dilemma.
- **Equipping is scarce.** Limited slots force real choices — the roguelite loop's drafting tension, but with objects you went and grabbed rather than menu picks.
- **Abilities come from items.** Active abilities (castable) and passive modifiers both. An item that changes how the *bubble* behaves (stretch faster, larger area, sever pods…) is the most Summoner-flavoured ability space and probably the first one to explore.

## Sketch of the space

!!! warning "Not decided — everything below is candidate design, not commitment"

    **Item categories that suggest themselves:**

    | Category | Example fantasy | Feeds pillar |
    |---|---|---|
    | Bubble mods | +area (bigger army cap), faster stretch, pod severing, second pod | Horde control |
    | Summon items | troops of a type: bruisers, runners, chanters | Horde control / abilities |
    | Summoner actives | dash, rally-shout (snap-regroup), ward circle | Item-based abilities |
    | Trinkets / passives | troop HP, regroup speed, on-kill effects | Roguelite build variety |

    **Open questions (the load-bearing ones):**

    - Who carries an item home — the summoner personally, or does the bubble engulf it? (Bubble-engulfing is charming and on-theme.)
    - Do items persist between runs (collection = meta-progression) or reset (roguelike-pure)? This is the single biggest roguelite structure decision — see [Runs](runs.md).
    - Slot model: paper-doll (head/hand/etc.), generic slots (any 4 items), or size-based bag? 
    - In [co-op](coop.md): per-player loot or shared pool? Trading? (At **4 players** a shared pool means one grabby friend ends the discussion — instanced drops are the safer default.)
    - Are ability items *used up*, on cooldown, or channelled by committing troops (spend X troops from the bubble to cast — very on-theme)?
