# Backlog

The working task list. Legend: <span class="pill done">DONE</span> <span class="pill wip">WIP</span> <span class="pill todo">TODO</span> <span class="pill idea">IDEA</span> <span class="pill risk">RISK</span> <span class="pill parked">PARKED</span>

## Now — prove the new shape

The A/B is closed (both schemes [parked](../game/bubble.md#parked-prototype-systems)). The open risk is whether a passive bubble is enough, so the next things built should be the systems that are *supposed* to carry the tension.

- <span class="pill risk">RISK</span> Strip the bubble to follow-only and play it — is walking your body around enough? Note the verdict in the [Decision Log](decisions.md)
- <span class="pill todo">TODO</span> Caravan v0: a moving object with HP that any player can order, run ends if it dies ([Caravan](../game/caravan.md))
- <span class="pill todo">TODO</span> One POI type end-to-end: enter → objective → reward ([Runs](../game/runs.md#pois))
- <span class="pill todo">TODO</span> Chase-distance cap so melees form a front line instead of a scrum
- <span class="pill todo">TODO</span> Enemy responds with defenders only, not the whole force

## Next — make it a run

- <span class="pill todo">TODO</span> Fog of war on a big map, shared reveal for all players
- <span class="pill todo">TODO</span> Graveyard hub scene: tombstones, point spend, unit levels, starting-item pick ([Graveyard](../game/graveyard.md))
- <span class="pill todo">TODO</span> Save format for tombstone levels / meta state
- <span class="pill todo">TODO</span> Two or three unit types that actually differ (the composition decision needs something to decide *between*)
- <span class="pill todo">TODO</span> Enemy behaviour on a map: static threats vs. patrols
- <span class="pill todo">TODO</span> Win/lose/extract flow (it's an HUD label now)

## The rebuild <span class="pill wip">UNBLOCKED — A/B closed 2026-07-30</span>

- <span class="pill risk">RISK</span> **Troop-sync spike: shape-sync vs per-troop sync** (2 peers, 100 troops, measure bytes *and* how the crowd reads) — **before** the architecture locks; it decides whether a troop is an entity or a particle. [Numbers](../tech/networking.md#the-troop-sync-problem)
- Architecture co-design session: unit brain / formation shape / commander / renderer; simulation separated from control, every bubble owned by a peer from day one
- Spatial partitioning for separation & targeting — **now mandatory**: 4 players × 50 troops = 200 friendlies, past the O(n²) ceiling before enemies are even counted

## Feature pillars, not started

- <span class="pill todo">TODO</span> Items: decide persistence + two-currency question first ([Items](../game/items.md)), then slot model, then first 5 items
- <span class="pill todo">TODO</span> Runs: hand-built map pool, map-scale navigation, extraction
- <span class="pill todo">TODO</span> Co-op: remaining design answers on [Co-op](../game/coop.md) — bubble-bubble rules, downed state, loot, 4-player scaling
- <span class="pill todo">TODO</span> Co-op tech: port OTR's Steam layer (lobby size 2 → 4), tick manager and `StateBuffer` — *after* the sync spike picks the payload

## Done

- <span class="pill done">DONE</span> PoC: summoner WASD + RTS camera (follow/free) — 2026-07-29
- <span class="pill done">DONE</span> Bubble of 50, random relaxed scatter, follow + leash + speed cap — 2026-07-29
- <span class="pill done">DONE</span> Combat loop: engagement, targeting, HP, deaths, HUD counts — 2026-07-29
- <span class="pill done">DONE</span> Dark green palette pass — 2026-07-29
- <span class="pill done">DONE</span> Stretch/pod system (teardrop, X/max counter, latch, RMB break) — 2026-07-29
- <span class="pill done">DONE</span> Walk-back regroup (no snap) — 2026-07-29
- <span class="pill done">DONE</span> A/B toggle F1, help overlay toggle F2 — 2026-07-30
- <span class="pill done">DONE</span> A/B closed by simplifying: bubble is passive, both schemes parked — 2026-07-30
