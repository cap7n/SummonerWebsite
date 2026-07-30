# Runs, Maps & the Roguelite Loop

Two pillars live here: **roguelite structure** and **instance-based maps**. Not implemented; intent and open decisions below.

## The intent

- The game is played in **runs**: enter, fight/collect/push as far as you can, die or extract, repeat stronger or wiser.
- **Maps are instances.** A level is generated or assembled when you enter it and stops existing when you leave. No persistent overworld simulation, no save-scummed world state. Clean boundaries, clean co-op joins, honest scope.
- Death is **lossy but not erasing** — the roguelite deal. Exactly what persists is *the* open question (below).

## Why instances (and not an open world)

- A prototype-friendly unit of content: one arena is already an instance; a run is a sequence of them.
- Co-op drop-in is tractable: a friend joins at the next instance boundary instead of mid-simulation.
- The bubble system loves bounded spaces: chokepoints, arena edges, and narrow connections make *shape* decisions matter (a stretched pod through a corridor is a genuinely different move than in open field).

## Open questions

!!! warning "Not decided"

    - **What persists between runs?** Items collected ([Items](items.md))? Unlocked item pool? Troop count upgrades? Nothing but knowledge? This decision defines the genre position between roguelite and roguelike, and it should be made *before* the item system is built.
    - **Run structure:** linear chain of instances (A→B→C→boss), branching node map (Slay-the-Spire style), or hub-and-sortie (village → pick a gate → instance → home)? Hub-and-sortie fits "carry items home" best.
    - **Generation:** hand-built maps drawn from a pool, procedural assembly of hand-built rooms, or full procgen? (Start with a pool of hand-built maps — cheapest way to learn what layouts make bubble control interesting.)
    - **Failure:** what does dying actually cost? Bubble wiped = run over, or summoner death = run over? (Ties to the summoner-killability question in [The Summoner](summoner.md).)
    - **Session length target:** a run should take how long — 20 min? 45? This gates map count per run and co-op scheduling.
