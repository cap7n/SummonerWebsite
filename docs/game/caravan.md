# The Caravan

The run's beating heart and its fail state. A caravan moves through the map, **any player can command it**, it has its own guard troops, and **if it dies, the run is over**.

## What's decided <span class="pill done">DONE</span>

- One caravan per run, shared by all [four players](coop.md).
- **Anyone can command it to move.** It's not owned by a player; it's the party's shared object.
- It's **protected by its own troops** — a garrison separate from any player's [bubble](bubble.md).
- **Caravan death = run over.** This is the run's failure condition, not summoner death.

## Why it works

It solves three problems at once, which is why it earns its place:

- **It gives the map a spine.** A big [POI-studded map](runs.md) with no pressure is a checklist; a caravan crawling through it turns every POI detour into a real cost — *how far can we stray, and for how long?*
- **It makes co-op cooperative without forcing co-location.** Four players can split across POIs, but the caravan is the string tying them together. Someone always has to be thinking about it.
- **It fixes the [passive-bubble](bubble.md) tension problem.** With the bubble simplified, the caravan is where the moment-to-moment decisions live: escort it, run ahead, split up, come back.

## Open questions

!!! warning "Not decided"

    - **Commanding it:** click-to-move, waypoints, or follow-the-nearest-player? Can two players give conflicting orders (last-one-wins, or a vote)? Simple answer: last order wins, with a visible marker so everyone sees where it's headed.
    - **Does it move on its own?** Auto-advance along a route (constant pressure, Helldivers-ish urgency) vs. it only moves when told (party controls the pace). These are different games — the first is a defence game, the second is an escort puzzle.
    - **Its guard troops:** fixed garrison, or do players assign their own troops to it? Player-assigned is a genuine cost-decision and very on-theme; fixed is far cheaper to build.
    - **HP, repair, healing.** Can damage be undone? Repair at POIs is an obvious reward type; permanent chip damage makes long runs tense.
    - **What is it *for*, in fiction and in mechanics?** Carrying the [items you collect](items.md) home is the strongest candidate — it makes loot physically at risk, ties the caravan to the meta loop, and explains why you can't just abandon it.
    - **Does it need to reach an exit,** or just survive? Extraction-at-the-end vs. survive-the-timer.
    - **Speed vs. the summoner's:** slower than the players (so escorting is a real leash) is almost certainly right, but it sets the whole run's tempo.
    - **What happens on death mechanically** — instant run over, or a "downed" caravan the party can revive under pressure? Instant-loss at 4 players can end everyone's evening on one mistake.
