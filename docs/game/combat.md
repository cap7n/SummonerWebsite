# Combat

How armies fight when bubbles touch. The prototype implements a first full loop; numbers are placeholders, the *shape* of the rules is the part being evaluated.

## Engagement <span class="pill done">DONE</span>

Combat starts on **contact between bubbles** — no attack orders exist, and with the [bubble simplified](bubble.md) there is no way to commit troops except to walk your summoner into range:

- Disc-on-disc overlap → both armies commit.
- Rings flare while a fight is on; the HUD shows both army counts live.
- Pod-tip contact (partial commitment) was a feature of the parked stretch scheme and no longer applies.

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

    - **Troop types.** Decided in principle — [tombstones](graveyard.md) summon different *kinds* of unit and level them. What the kinds actually are is open. Ranged units break the "contact = combat" simplicity, so that one is a design fork, not a stat.
    - **The summoner in combat.** Targetable? Killable? With the [caravan](caravan.md) as the fail state, summoner death needs its own cost — see [The Summoner](summoner.md).
    - **Retreat.** With no move orders, disengaging is just walking away. Should it cost something (parting shots, pursuit), or is free disengagement the point?
    - **Caravan combat.** Its guard troops fight on contact like any bubble, but whether enemies *prefer* the caravan (making it a real defence target) or just fight what's nearest changes the entire threat model.
    - **Horde scale.** Pillar says "horde" — is 50 the army, or the starting army? The separation pass and per-troop nodes cap out around a few hundred; a real horde (500+) forces a different architecture. **4-player [co-op](coop.md) already puts 200 friendlies on the field before a single enemy spawns**, so the rebuild has to clear this bar regardless of how the horde question lands. Feeds the rebuild.
    - **Whose machine resolves a fight?** In co-op, two players' bubbles can touch the same enemy. Host-authoritative resolution is the simple answer; it argues against fully client-owned bubbles. See [Networking](../tech/networking.md).
