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

## The rebuild <span class="pill wip">SPIKES PASSED — building systems 2026-07-31</span>

Both blocking spikes are done (`Spikes/NetCrowdSpike`) and the [Architecture](../tech/architecture.md) page holds the system list and build order. Next up, in order, each landing playable:

- <span class="pill done">DONE</span> **Terrain** ([results](../tech/architecture.md#terrain-results)) — and the **crowd + netplay harness now runs on it** (spike folded into `systems/net` + `systems/crowd`, armies draped on generated hills, consistency re-verified) — 2026-07-31
- <span class="pill todo">TODO</span> **Crowd polish on terrain**: slope movement cost (uphill slows), real `RTSCamera` + `Summoner` controller in the netcrowd harness instead of the harness stand-ins
- <span class="pill todo">TODO</span> **Crowd churn polish**: marching slot-trades work but read mechanical ("you actually made them trade places") — curved/staggered weaving instead of straight walks. Good enough for now, per cap7n
- <span class="pill todo">TODO</span> **Combat system** — two crowds fight; chase cap + defenders-only carried over from the prototype findings
- <span class="pill todo">TODO</span> **Caravan + Route Graph** — the run's spine and fail state; *the passive-bubble feel test happens here*
- <span class="pill todo">TODO</span> **Map Generator v0** — noise heightmap + road graph + POI sites ([decided](../game/runs.md#map-generation)); lands alongside caravan/fog
- Then: Fog → POI → Run Director → Graveyard/Save → Net Sync port (order + reasoning on the [Architecture](../tech/architecture.md) page)

## Feature pillars, not started

- <span class="pill todo">TODO</span> Spells: answer the [Spells & power questions](open-questions.md#spells--power), then build the first 3 spells
- <span class="pill wip">WIP</span> Items: system built + **wired into the character** 2026-08-01 — your crowds now spawn from your equipped summoning items (one crowd per item, per-crowd hp/atk/def from `ItemDefs.resolve`, regen raises troops at the summoner's feet via a reliable revive event). Next: balance pass on the 15 defs + enemy scaling; the hub's real 3-D tombstones replace the harness list later (same `Items` API)
- <span class="pill todo">TODO</span> Runs: hand-built map pool, map-scale navigation, extraction
- <span class="pill todo">TODO</span> Co-op: remaining design answers on [Co-op](../game/coop.md) — bubble-bubble rules, downed state, loot, 4-player scaling

## Done

- <span class="pill done">DONE</span> **Item system v0** (`systems/items`): 15-grave catalogue (6 summons / 4 spells / 5 mods), respendable point budget from the host pool, 8 slots × 4 grow-upward mod sockets, trading (fake-player stand-in solo, host-arbitrated in sessions), autotested data rules — 2026-08-01
- <span class="pill done">DONE</span> **First 3-player Steam playtest** + fixes it forced: host-owned roster/forwarding (clients couldn't see each other via transport relay), name tags, idle heartbeat (60% phantom extrapolation → 0%), render-rate summoner + interpolated troops (judder), arrival slack (idle jitter), marching churn, playtest CSV logger — 2026-07-31
- <span class="pill done">DONE</span> **Rebuild skeleton in the game project**: `systems/` folders + graybox Hub scene, 4 spawns, player-height reference block — 2026-07-31
- <span class="pill done">DONE</span> **Troop-sync + crowd-scale spike** (`Spikes/NetCrowdSpike`): 810 agents at ~2 ms sim, per-troop streaming at ~0.2 Mbit/s, identical battle on both peers — 2026-07-30
- <span class="pill done">DONE</span> **Steam layer on 4.7** (OTR's GodotSteam + Spacewar, 4-member lobby, lobby screen w/ ID + start button) + shareable build in `Summoner builds/` — 2026-07-30
- <span class="pill done">DONE</span> **First real-internet 2-player test**: stable; host-stutter-on-client fixed (sender-tick jitter buffer) — 2026-07-31
- <span class="pill done">DONE</span> PoC: summoner WASD + RTS camera (follow/free) — 2026-07-29
- <span class="pill done">DONE</span> Bubble of 50, random relaxed scatter, follow + leash + speed cap — 2026-07-29
- <span class="pill done">DONE</span> Combat loop: engagement, targeting, HP, deaths, HUD counts — 2026-07-29
- <span class="pill done">DONE</span> Dark green palette pass — 2026-07-29
- <span class="pill done">DONE</span> Stretch/pod system (teardrop, X/max counter, latch, RMB break) — 2026-07-29
- <span class="pill done">DONE</span> Walk-back regroup (no snap) — 2026-07-29
- <span class="pill done">DONE</span> A/B toggle F1, help overlay toggle F2 — 2026-07-30
- <span class="pill done">DONE</span> A/B closed by simplifying: bubble is passive, both schemes parked — 2026-07-30
