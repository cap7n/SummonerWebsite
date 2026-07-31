# The Bubble (Horde Control)

Your army travels as a **bubble around your summoner**. That's it — the bubble is not steered, ordered, or shaped. Where you walk, it goes; what it touches, it fights.

!!! note "Scope decision — 2026-07-30"
    The bubble was deliberately **simplified**. Both prototype control schemes (click-to-move and the stretch/pod teardrop) are **parked**, and the F1 A/B test is closed without a winner. Keeping it simple *for now* — the interesting decisions have moved to unit composition ([Graveyard](graveyard.md)), the [caravan](caravan.md), and the [map layer](runs.md). The parked work is preserved below, because the findings survive even though the code doesn't.

## What the bubble is now

- A circular formation of troops that **follows your summoner**, always. No move orders, no click targets, no stretching.
- Troops hold scattered formation slots inside the disc; they walk (never teleport) back into place after a fight.
- **Contact is combat.** Enemies that touch the bubble get fought. Positioning your body *is* your engagement decision.
- The bubble's contents are not fixed: what's inside comes from the unit types you unlocked and summoned at the [Graveyard](graveyard.md).

## Invariants (unchanged, still binding)

- **The bubble never moves faster than the summoner.** It has no independent travel speed at all now.
- **The summoner can never end up outside the bubble.** Hard leash, ~0.75 units inside the edge.
- **Troops walk, they don't teleport** (~5 u/s regroup with per-troop variance; the squad's own travel is exempt so formation keeps up with a sprint).
- Scatter is random but **relaxed apart** (min separation ~0.85) so it reads as a crowd, not a clump.

## What "horde control" means now

With the shape locked, control lives in three other places — this is a real shift and worth naming:

| Layer | Your decision |
|---|---|
| **Body** | Where you stand. The only way to commit or withhold force is to walk in or walk away. |
| **Composition** | Which unit types you brought and levelled ([Graveyard](graveyard.md), [Items](items.md)) |
| **Map** | Which [POI](runs.md) to take, and where the [caravan](caravan.md) goes — the shared, four-player layer |

!!! warning "The honest risk"
    A passive bubble means moment-to-moment play is *walking*. Whether that's enough tactile decision-making, or whether the map/caravan layer has to carry all the tension, is the thing to feel-test first. If it's flat, the parked systems below are the drawer to reach into — that's why they're parked and not deleted.

## Parked prototype systems <span class="pill parked">PARKED</span> {#parked-prototype-systems}

Built, working, playable — preserved at git tag `poc-final` (`git checkout poc-final`), kept for reference:

??? info "System A — Click-move (parked)"
    Left-click sent the whole bubble marching to a spot (gold ring marker, constant march speed, still leashed and speed-capped). On arrival it **parked** and held ground until recalled or re-ordered.

??? info "System B — Stretch / teardrop pod (parked)"
    Hold left-click and the bubble **stretched a pod toward the cursor** — the outline became a teardrop (two circles joined by outer tangents), like a water drop being pulled.

    - A floating **X / max** counter at the pod tip climbed while held: ~2.5 troops/s at short reach, ~16/s at full reach (22 units).
    - **X troops physically walked into the pod**; nearest free troops recruited first.
    - **Area conserved**: disc + pod always summed to the resting circle, so committing visibly thinned the main disc.
    - **Release retracted** the pod unless it touched an enemy bubble — then it **latched** until right-click broke it.
    - Pod-only contact committed **only pod troops**: poke with 10, hold 40 in reserve.
    - A latched pod auto-recruited replacements for its dead — it slowly drained your army until you broke off.

    Severing a pod into its own group was never built; the [three candidate designs](../project/open-questions.md#severed-pods) are still on file.

**Findings that outlive the code** (the reason the experiment was worth running):

- Committing troops *gradually* (a counter that fills while you hold) reads as a genuine commitment gesture — the tension was real.
- Area conservation is legible without any UI: you *see* the disc thin out.
- Nearest-enemy targeting collapses both armies into one scrum; any future melee needs a chase-distance cap.
- A pod poke alerting the enemy's *whole* army dragged them out of formation — response rules have to be defenders-only.

## Enemy bubbles

Enemy armies use the same bubble code with a different faction and colour. They hold ground and fight on contact. Enemy behaviour (patrol / advance / respond) is still unbuilt.

## Friendly bubbles (co-op)

Up to four friendly bubbles share a battlefield. Overlap and merging rules are open, but the invariants are per-bubble and expected to survive: your leash is to *your* summoner, your speed cap is *your* speed. See [Co-op](coop.md).
