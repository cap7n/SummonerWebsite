# Summoner Design Wiki

**Summoner is a 4-player co-op horde-control roguelite.** You play a summoner walking the battlefield in person, surrounded by a **bubble** of troops that follows you and fights what it touches. Runs start in a **graveyard** — your hub and your save file — where tombstones are levelled with points to strengthen and unlock the kinds of units you can summon. Then the party deploys onto a big fog-covered RTS map, escorting a **caravan** whose death ends the run, taking POIs for rewards along the way.

Built in **Godot 4.7**.

---

## The pitch in one line

*Raise an army from your graveyard, wear it like a coat, and walk a caravan across hostile ground with three friends.*

## The core idea

You never micro a unit and you never order the army around. Your troops are **on you** — a bubble that moves where your body moves and fights what your body touches. That leaves the real decisions somewhere more interesting than unit selection:

- **Composition** — which unit types you levelled and summoned at the [Graveyard](game/graveyard.md).
- **Position** — where you personally stand, because that *is* your commitment.
- **Spells** — summoners are wizards, and the magic is [hardcore](game/summoner.md#spells): fight-turning if you prepared, and the other half of the power fantasy next to the horde.
- **The map** — where the shared [caravan](game/caravan.md) goes and which [POIs](game/runs.md) are worth the detour, with four players free to split across a big map under shared vision.

Around that sit six feature pillars: **4-player co-op**, **horde control**, **item equipping & collecting**, **roguelite structure**, **item-based abilities**, and **instance-based maps**. See [Design Pillars](pillars.md) for what each one means and doesn't mean.

## Where the game is right now

Summoner is at the **proof-of-concept** stage: one Godot project, one test arena. The PoC answered its feel questions, the design then got *simpler* — the bubble is now a passive aura and both experimental control schemes are parked. Everything above the troop layer (graveyard, caravan, maps, POIs) is design intent, recorded here so it doesn't evaporate.

| Area | Status |
|---|---|
| Summoner: WASD + sprint, camera-relative | ✅ Working (kept from PoC, `systems/summoner/`) |
| RTS camera: locked to character / free-roam, orbit, zoom, edge scroll | ✅ Working (kept from PoC) |
| Bubble follows summoner; troop combat; crowd at 800+ agents | ✅ Proven (PoC + spike) — PoC code trashed, spike crowd core awaits port |
| Click-move & stretch/teardrop control schemes | 🅿️ [Parked](game/bubble.md#parked-prototype-systems) — resurrect via `git checkout poc-final` |
| Graveyard hub scene (graybox, 4 spawns) | 🔨 Started — F5 boots it |
| Spells (hardcore, power fantasy) | ⬜ Direction decided — [questions open](project/open-questions.md#spells--power) |
| Procedural maps (heightmap + roads + POI stamps) | ⬜ [Decided](game/runs.md#map-generation), not started |
| Enemy bubble AI | ⬜ Not started |
| Graveyard hub, tombstones, point economy | ⬜ Not started — [structure decided](game/graveyard.md) |
| Caravan (shared command, escort, fail state) | ⬜ Not started — [structure decided](game/caravan.md) |
| Big RTS maps, fog of war (shared vision), POIs | ⬜ Not started — [structure decided](game/runs.md) |
| Co-op (4 players, OTR network stack) | ✅ **Proven in spike** — [streaming + Steam layer tested over real internet](tech/networking.md#the-troop-sync-problem) |
| Items, equipment, abilities | ⬜ Not started |
| Robust architecture rebuild | 🔨 [Designed, spikes passed](tech/architecture.md) — building systems |

!!! warning "The PoC is disposable"
    The current prototype code is a proof of concept and is planned to be **rebuilt on a more robust architecture** once the control-scheme A/B is settled. Don't document prototype internals here as if they're final — record the *decisions and feel findings*, which are the part that survives the rewrite.

## How to use this wiki

Start with the **[Design Pillars](pillars.md)**. Then **[The Bubble](game/bubble.md)** for what the army is, **[The Graveyard](game/graveyard.md)** and **[The Caravan](game/caravan.md)** for where the decisions actually live, and **[Open Questions](project/open-questions.md)** for what's deliberately still open. The **[Backlog](project/backlog.md)** tracks tasks; the **[Decision Log](project/decisions.md)** tracks *why*.

!!! note "The one rule of this wiki"
    **This wiki records decisions, it doesn't replace making them.** If a page starts describing something that hasn't actually been decided or built, mark it clearly (a `!!! warning "Not decided"` box) or move it to [Open Questions](project/open-questions.md). Stale certainty is worse than an honest "open question."
