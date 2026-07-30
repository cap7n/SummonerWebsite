# Combat

How armies fight when bubbles touch. The prototype implements a first full loop; numbers are placeholders, the *shape* of the rules is the part being evaluated.

## Engagement <span class="pill done">DONE</span>

Combat starts on **contact between bubble shapes** — no attack orders exist:

- Disc-on-disc overlap → both armies fully commit.
- Pod-tip-on-disc (stretch scheme) → **only the pod troops fight**; the rest of the disc holds formation. The enemy is fully alerted, however (see feel issues on [The Bubble](bubble.md)).
- Rings flare while a fight is on; the HUD shows both army counts live.

## Troop resolution <span class="pill done">DONE</span>

Each troop is an independent unit with HP and a state (formation / fighting / dead):

| Stat | Prototype value |
|---|---|
| HP | 24 |
| Damage per hit | 6 (4 hits to kill) |
| Attack interval | 0.7 s |
| Attack range | 0.9 (melee) |
| Chase move speed | 6 u/s |

- Targeting: nearest living enemy, kept until it dies, then re-pick.
- Hits flash the victim white; team colour bleeds toward bruised red as HP drops — a health bar with zero UI.
- Death: shrink-and-sink, then the node frees itself.
- A separation pass keeps bodies from stacking (O(n²) per bubble — fine at 50v50, needs a spatial grid somewhere north of a few hundred troops).

Mirror-matched 50v50 fights resolve with realistic variance (winner keeps ~8–16 survivors either side) — Lanchester dynamics, no scripted outcome.

## What combat is *for* (intent)

!!! warning "Not decided"
    The prototype only proves that fights resolve. The design questions are open:

    - **Troop types.** Are all troops identical, or do [items](items.md) summon typed troops (tanky/fast/ranged)? Ranged troops break the "contact = combat" simplicity — worth it?
    - **The summoner in combat.** Targetable? Killable? See [The Summoner](summoner.md).
    - **Retreat.** Currently latching is sticky and breaking off is free. Should disengaging cost something (parting shots, pod troops must survive the walk home)?
    - **Horde scale.** Pillar says "horde" — is 50 the army, or the starting army? The separation pass and per-troop nodes cap out around a few hundred; a real horde (500+) forces a different architecture. Feeds the rebuild.
