# Engine & Prototype Workflow

## Engine

**Godot 4.7** (stable, win64), Forward+ renderer, Jolt physics, D3D12.

## Repository layout

| Path | What |
|---|---|
| `Summoner/Summoner/` | The Godot project (PoC) |
| `Summoner/SummonerWebsite/` | This wiki |
| `Summoner/Summoner Marketing/`, `Summoner builds/` | Non-code siblings |

The PoC repo has two branches:

- **`main`** — click-to-move system only (the original PoC).
- **`experiment/alt-system`** — the stretch/pod system, plus click-to-move restored behind the **F1 A/B toggle**. This is where active work happens.

## Prototype verification workflow

The prototype is verified without a human watching, which keeps iteration honest:

```bash
# parse + boot check (headless, no shaders compiled)
godot --headless --path . --quit-after 90

# render real frames to PNG for visual verification
godot --path . --write-movie out/frame.png --fixed-fps 20 --quit-after 150

# scripted playtests: a temp scene drives Input actions and asserts outcomes
godot --headless --path . res://_tmp_test.tscn
```

Scripted tests have been used to verify: troop scatter stays in-bounds and separated, WASD movement, camera detach/recenter, full 50v50 combat resolution (multiple runs to check for side bias), and leash/speed-cap invariants.

## PoC → rebuild

The current code is a **disposable proof of concept** (one ~600-line `troop_bubble.gd` doing formation, movement, combat, two control schemes, and rendering). After the A/B verdict, the plan is a deliberate rebuild on an architecture the developer understands and co-designs — roughly: unit brain / formation shape / commander / renderer as separate pieces, with simulation state separated from control input for [co-op](../game/coop.md)'s sake.

!!! note "Editor-conflict rule"
    Don't edit a `.tscn`/`.tres` from tooling while it's open in the Godot editor — the editor clobbers it on save. Close the scene first or hand over the change as steps.
