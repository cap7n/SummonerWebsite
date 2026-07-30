# Summoner Design Wiki

**Summoner is a co-op horde-control roguelite.** You play a summoner walking the battlefield in person, surrounded by a **bubble** — a living formation of troops that moves with you. You don't micro units; you shape the bubble: stretch it toward an enemy force to commit troops, latch on, break off. Between and during runs you collect and equip items, and your abilities come from what you carry, not from a class sheet.

Built in **Godot 4.7**.

---

## The pitch in one line

*Herd an army as a single living shape: walk it into the fight, stretch it like a drop of water to strike, and build your power from the items you drag home.*

## The core idea

The twist that makes Summoner its own thing is the **bubble as the unit of control**. RTS games give you a mouse and 50 health bars; Summoner gives you one organism. Every army decision is expressed through one shape — where you walk it, where you stretch it, what you let it touch. The tension is *commitment*: troops flow into a stretched pod a few at a time, so how long you hold the stretch **is** how much force you commit.

Around that core sit six feature pillars: **co-op**, **horde control**, **item equipping & collecting**, **roguelite structure**, **item-based abilities**, and **instance-based maps**. See [Design Pillars](pillars.md) for what each one means and doesn't mean.

## Where the game is right now

Summoner is at the **proof-of-concept** stage: one Godot project, one test arena, two control schemes being A/B tested against each other. The PoC exists to answer *"is the bubble fun to steer?"* — everything else is design intent, recorded here so it doesn't evaporate.

| Area | Status |
|---|---|
| Summoner: WASD + sprint, camera-relative | ✅ Working |
| RTS camera: follow / free, orbit, zoom, edge scroll | ✅ Working |
| Bubble follows summoner, leashed (can never leave you outside) | ✅ Working |
| 50-troop random scatter with relaxation (no overlaps) | ✅ Working |
| Troop combat: contact engagement, per-troop HP, melee resolution | ✅ Working |
| **Stretch system**: teardrop pod, X/max counter, latch, RMB break | ✅ Working (system B) |
| Click-to-move: march, park, recall | ✅ Working (system A) |
| A/B toggle between control schemes (F1) | ✅ Working |
| Enemy bubble AI | ⬜ Static dummy only |
| Co-op | ⬜ Not started |
| Items, equipment, abilities | ⬜ Not started |
| Runs / maps / roguelite loop | ⬜ Not started |
| Robust architecture rebuild | 📋 Planned after the A/B verdict |

!!! warning "The PoC is disposable"
    The current prototype code is a proof of concept and is planned to be **rebuilt on a more robust architecture** once the control-scheme A/B is settled. Don't document prototype internals here as if they're final — record the *decisions and feel findings*, which are the part that survives the rewrite.

## How to use this wiki

Start with the **[Design Pillars](pillars.md)**. Then **[The Bubble](game/bubble.md)** for the core verb and the A/B test that's running, and **[Open Questions](project/open-questions.md)** for the decisions that are deliberately still open. The **[Backlog](project/backlog.md)** tracks tasks; the **[Decision Log](project/decisions.md)** tracks *why*.

!!! note "The one rule of this wiki"
    **This wiki records decisions, it doesn't replace making them.** If a page starts describing something that hasn't actually been decided or built, mark it clearly (a `!!! warning "Not decided"` box) or move it to [Open Questions](project/open-questions.md). Stale certainty is worse than an honest "open question."
