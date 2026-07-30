# Decision Log

Why things are the way they are. Newest first. When an [open question](open-questions.md) gets answered, it lands here.

| Date | Decision | Why |
|---|---|---|
| 2026-07-30 | **Co-op is 4 players** (1–4; solo is a lobby of one). | The pillar was always "play it with friends"; 4 is the party size the fantasy wants. Cost is architectural (200+ troops), and it's cheaper to pay for it now than to retrofit. |
| 2026-07-30 | **Anti-cheat is out of scope.** | Private co-op sessions, no ladder or economy — nothing to protect. Buys client-authoritative ownership of your own summoner/bubble (zero input lag, no reconciliation). |
| 2026-07-30 | **Reuse OTR's network stack** — GodotSteam `SteamMultiplayerPeer`, one `NetworkTickManager`, `StateBuffer` + Hermite interpolation, per-entity sync ownership. | Already built, shipped and debugged by the same developer in the same engine. Zero novel transport risk; the only genuinely new problem is troop volume. See [Networking](../tech/networking.md). |
| 2026-07-30 | **Wiki created** (this site), mirroring the TowerDrop wiki stack (MkDocs Material, same conventions). | One place for design truth before the feature set grows. |
| 2026-07-30 | **Both control schemes wired into one build behind F1**, instead of two builds. | A/B testing feel needs instant switching in the same battle; export-per-tweak kills iteration. |
| 2026-07-30 | **PoC is disposable; rebuild planned** on an architecture the developer understands and helps shape. | The prototype answers feel questions; it shouldn't calcify into the codebase. |
| 2026-07-29 | **Stretch release rule:** releasing retracts the pod *unless* it touches an enemy bubble — then it latches until right-click breaks it. | Makes the stretch a commitment gesture with a natural "grip" metaphor; severing deferred to [open questions](open-questions.md#severed-pods). |
| 2026-07-29 | **Pod-only contact commits only pod troops**; disc contact commits everyone. | Turns the stretch into a probing weapon with a reserve, instead of an all-in trigger. |
| 2026-07-29 | **Bubble invariants:** never faster than the summoner; summoner never outside the bubble (hard leash). | The army is an extension of the summoner, not an independent RTS unit. |
| 2026-07-29 | **Troops walk back into formation** (speed-capped regroup) instead of lerp-snapping. | Snap-back after fights broke the "living crowd" illusion. |
| 2026-07-29 | **Stretch system chosen as the direction to explore** over plain click-to-move (kept as A/B baseline). | The teardrop stretch is the game's identity mechanic; click-move is genre-standard. |
| 2026-07-29 | **Palette is dark green.** Not blue. Ever. | Developer preference, strongly held ("i hate bleu xD"). Troops green, summoner gold for contrast, enemy red. |
| 2026-07-29 | **Godot 4.7** for the PoC (over Unity 6, which is also installed). | Existing Godot familiarity and project folder already prepared. |
