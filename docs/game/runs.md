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

## Still open

!!! warning "Not decided"

    - **What persists between runs?** Tombstone levels: yes (that's the meta). Points-in-hand, unlocked units, collected items: undecided — see [Graveyard](graveyard.md). This still gates the [item system](items.md).
    - **Generation:** hand-built maps from a pool, procedural assembly of hand-built chunks, or full procgen? Start with a pool of hand-built maps — cheapest way to learn what layouts make caravan routing and POI greed interesting.
    - **Map size in real numbers.** "Big" needs a figure once the caravan's speed exists — the map is really measured in *minutes of caravan travel*, not units.
    - **Session length target:** 20 min? 45? Gates map size, POI count, and how much a wipe costs emotionally.
    - **Summoner death.** If the caravan is the fail state, what does dying personally cost — respawn at the caravan, timer, lost troops? At [4 players](coop.md) this doubles as the downed-state answer.
    - **Instance size for four bubbles + a caravan.** Chokes drawn for one army are traffic jams for four.
