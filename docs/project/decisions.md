# Decision Log

Why things are the way they are. Newest first. When an [open question](open-questions.md) gets answered, it lands here.

| Date | Decision | Why |
|---|---|---|
| 2026-07-30 | **The bubble is simplified to a passive aura** around the summoner — no move orders, no stretching. Both control schemes [parked](../game/bubble.md#parked-prototype-systems); the F1 A/B closes without a winner. | Keep it simple, at least for now. The game's decisions moved up a layer (composition, caravan, map routing), so the bubble doesn't need to carry the tactical load. Parked, not deleted — the code and findings stay. |
| 2026-07-30 | **Runs are hub-and-sortie from a Graveyard**, which doubles as the meta-progression hub: **tombstones** levelled with **points** to strengthen units and unlock unit types; starting items picked there. | Answers the run-structure question and the "what persists" question's backbone in one move, and the hub is thematically the game itself — a graveyard that grows *is* the save file. |
| 2026-07-30 | **A caravan is the run's fail state**: shared, commandable by any player, guarded by its own troops; if it dies the run ends. | Gives a big map a spine and real pressure, ties four split-up players together, and supplies the moment-to-moment tension the simplified bubble gave up. |
| 2026-07-30 | **Maps are big RTS levels with POIs** (objective → reward), Helldivers-shaped. | Makes travel a cost and routing a decision; scales naturally to four players who can split up. |
| 2026-07-30 | **Fog of war with fully shared vision** — anyone reveals for everyone. | Splitting up stays readable, removes "where are you?" friction, and costs one fog state on the wire instead of four. |
| 2026-07-30 | **Camera locks to your character or unlocks to free-roam the map**, RTS-standard. | Already built and proven in the PoC; on big maps free-look is how you read the map and watch the caravan. |
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
