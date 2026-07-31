# Runs, Maps & the Roguelite Loop

Two pillars live here: **roguelite structure** and **instance-based maps**. Not implemented; the structure is now decided, the details are open.

## The loop <span class="pill done">DONE</span>

```
Graveyard hub ──▶ Deploy ──▶ Big RTS map (caravan + POIs) ──▶ Extract ──▶ Graveyard
      ▲                                    │
      └────────── points, items ───────────┘   (caravan dies ⇒ run over)
```

- **Hub-and-sortie.** Runs start and end at the [Graveyard](graveyard.md), where points are spent and starting items picked.
- **Maps are big RTS levels** — an instance, generated or assembled per visit, not a persistent world.
- **The [caravan](caravan.md) crosses the map** and its death ends the run. That's the failure condition; summoner death is a separate open question.
- **POIs are scattered across the map.** Complete a POI's objective, earn rewards. Think Helldivers: a big space, optional side objectives, real travel cost between them.
- **Death is lossy, not erasing.** Tombstone levels persist; exactly what else does is open (below).

## Fog of war <span class="pill done">DONE</span> {#fog-of-war}

- Maps are covered in **fog of war**.
- **Vision is fully shared: anyone reveals for everyone.** No per-player fog, no scouting-for-yourself. One team vision state.

Shared vision is the right call for a 4-player game where players split up — it's what makes splitting *readable* instead of confusing, and it removes a whole class of "where are you?" friction. It's also drastically cheaper to network: one vision state, not four ([Networking](../tech/networking.md)).

## Camera <span class="pill done">DONE</span>

The camera does both jobs, as in any RTS:

- **Locked** to your summoner (follow), or
- **Unlocked** to fly around the map freely.

The prototype already implements this (F toggles, Space re-centres, any explicit pan auto-detaches) — see [The Summoner](summoner.md#camera). On a big map, free-look is not a convenience feature: it's how you read the POI layout and watch the caravan while your body is elsewhere.

## POIs

The reward layer, and the reason maps are big.

!!! warning "Not decided"

    - **Objective types.** What actually happens at a POI — hold a point, kill a nest, escort/retrieve something, survive a wave, solve a small puzzle? Needs at least 3–4 distinct kinds or the map reads as one objective copy-pasted.
    - **Rewards.** [Points](graveyard.md), [items](items.md), caravan repair, reinforcement troops? Different reward types create different routing decisions, which is exactly the interesting part.
    - **Are POIs optional?** Fully optional (greed vs. safety) is the Helldivers shape and the strongest fit with the caravan pressure. A mandatory main objective plus optional POIs is the alternative.
    - **Does the map have a boss / final objective,** or does extraction end it?
    - **Do POIs scale with player count?** Four players clearing four POIs simultaneously is a very different difficulty curve from one player doing them in sequence.

## Map generation <span class="pill done">DONE</span> {#map-generation}

Maps are **procedurally generated** (decided 2026-07-31):

- **Noise heightmap terrain.** The tech stack was chosen with no navmesh baking precisely so terrain can be generated freely and cheaply ([Architecture](../tech/architecture.md)) — there is no bake step to pay per map.
- **Generated road graph.** POI sites scattered with minimum spacing, roads connecting them (spanning tree plus a few loops), the caravan route and extraction placed on the graph. Roads are gameplay: they're what makes routing a visible 4-player argument.
- **Hand-authored POI stamps.** The POIs themselves are small hand-made layouts stamped onto generated sites — authored quality where the gameplay is, generated variety everywhere else.

Why: hand-building maps is this team's declared weak spot, and generation turns that weakness into replayability — every run gets a fresh map for free. What the generator must *guarantee* versus leave to chance is [open](../project/open-questions.md#map-generation).

### How big can a map be? <span class="pill done">MEASURED 2026-07-31</span> {#map-size}

Built and measured (see [Architecture](../tech/architecture.md#terrain-results)): **an 8 km × 8 km map with 7.7 million triangles on screen costs 2.4 ms a frame.** Rendering is nowhere near the limit at any size this game would want, and no floating-origin/recentering machinery is needed either — the map is centred on the origin and float precision stays sub-millimetre out to several kilometres.

What actually costs: **generation time** (~0.5 s per million height samples) and **memory** (4 bytes per sample). So:

- **Map size is a design decision, not a technical one.** Pick it in *minutes of caravan travel* and the tech will follow.
- 2 km is a brisk map, 4 km is a big one, 8 km is possible if a run should feel like an expedition. Terrain detail (metres per height sample) trades against generation time independently of map size.

## Still open

!!! warning "Not decided"

    - **What persists between runs?** Tombstone levels: yes (that's the meta). Points-in-hand, unlocked units, collected items: undecided — see [Graveyard](graveyard.md). This still gates the [item system](items.md).
    - **Map size in real numbers.** "Big" needs a figure once the caravan's speed exists — the map is really measured in *minutes of caravan travel*, not units.
    - **Session length target:** 20 min? 45? Gates map size, POI count, and how much a wipe costs emotionally.
    - **Summoner death.** If the caravan is the fail state, what does dying personally cost — respawn at the caravan, timer, lost troops? At [4 players](coop.md) this doubles as the downed-state answer.
    - **Instance size for four bubbles + a caravan.** Chokes drawn for one army are traffic jams for four.
