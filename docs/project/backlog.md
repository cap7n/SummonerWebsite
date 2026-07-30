# Backlog

The working task list. Legend: <span class="pill done">DONE</span> <span class="pill wip">WIP</span> <span class="pill todo">TODO</span> <span class="pill idea">IDEA</span> <span class="pill risk">RISK</span> <span class="pill parked">PARKED</span>

## Now — settle the A/B

- <span class="pill wip">WIP</span> Play both control schemes (F1) against the dummy enemy; pick a direction, note *why* in the [Decision Log](decisions.md)
- <span class="pill todo">TODO</span> Chase-distance cap so melees form a front line instead of a scrum
- <span class="pill todo">TODO</span> Enemy responds with defenders only (not the whole army) to a pod poke
- <span class="pill idea">IDEA</span> Rebind break-connection off right-click (orbit overlap)

## Next — make the fight a game

- <span class="pill todo">TODO</span> Enemy bubble behaviour: patrol / advance / respond (it's a static dummy now)
- <span class="pill todo">TODO</span> Win/lose state and restart flow (it's an HUD label now)
- <span class="pill idea">IDEA</span> First severed-pod experiment — pick one of the [three candidates](open-questions.md#severed-pods)
- <span class="pill idea">IDEA</span> Second enemy bubble / multi-front pressure (the reason stretching exists)

## The rebuild <span class="pill parked">PARKED until A/B verdict</span>

- <span class="pill risk">RISK</span> **Troop-sync spike: shape-sync vs per-troop sync** (2 peers, 100 troops, measure bytes *and* how the crowd reads) — **before** the architecture locks; it decides whether a troop is an entity or a particle. [Numbers](../tech/networking.md#the-troop-sync-problem)
- Architecture co-design session: unit brain / formation shape / commander / renderer; simulation separated from control, every bubble owned by a peer from day one
- Spatial partitioning for separation & targeting — **now mandatory**: 4 players × 50 troops = 200 friendlies, past the O(n²) ceiling before enemies are even counted

## Feature pillars, not started

- <span class="pill todo">TODO</span> Items: decide persistence question first ([Runs](../game/runs.md)), then slot model, then first 5 items
- <span class="pill todo">TODO</span> Runs: hand-built map pool, run chain, failure condition
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
