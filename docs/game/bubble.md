# The Bubble (Horde Control)

The core verb of Summoner. The bubble is a circular formation of troops (currently 50) that trails the summoner. It is the *only* way the player commands the army.

## Invariants (decided, both control schemes)

These hold no matter which control scheme wins the A/B:

- **The bubble can never move faster than the summoner.** Its travel speed is capped at the summoner's own speed. No out-running your own army boundary.
- **The summoner can never end up outside the bubble.** A hard leash: whatever the bubble is doing, it is dragged along before it may leave the summoner behind (margin ~0.75 units inside the edge).
- **Troops walk, they don't teleport.** Returning to formation happens at walking speed (`regroup` walk, ~5 u/s with per-troop variance) — the squad's own travel is exempt so the formation keeps up with a sprinting summoner.
- Troop scatter inside the disc is random but **relaxed apart** (min separation ~0.85) so it reads as a crowd, not a clump.

## The A/B test <span class="pill wip">WIP</span>

Two control schemes are implemented side by side in the prototype, toggled live with **F1** so they can be compared inside the same battle. **Right-click is "cancel" in both.**

### System A — Click-move

Left-click sends the whole bubble marching to that spot (gold ring marker, constant march speed, still leashed and speed-capped). On arrival it **parks** and holds that ground until right-clicked (recall) or given a new order.

### System B — Stretch (the favoured direction)

Hold left-click and the bubble **stretches a pod toward the cursor** — the outline becomes a teardrop (two circles joined by outer tangents), like a water drop being pulled.

- A floating counter **X / max** appears at the pod tip. X climbs while you hold: slowly at short reach (~2.5 troops/s), faster the further you stretch (~16/s at full reach, 22 units).
- **X troops physically walk into the pod** as it fills; the nearest free troops are recruited first.
- **Area is conserved**: disc + pod always sum to the resting circle's area, so committing troops visibly thins the main disc. (Total area becomes an upgradeable stat later.)
- **Release** retracts the pod — *unless* it is touching an enemy bubble, in which case it **latches** and stays connected.
- **Right-click breaks the connection** and the pod pulls back in.
- When contact is pod-only, **only pod troops fight**; the main disc holds formation. The stretch is a probing weapon: poke with 10, hold 40 in reserve.
- If a pod troop dies, a replacement is auto-recruited from the disc — a latched pod slowly drains your army until you break off.

!!! warning "Not decided — severing"
    What happens if a stretched pod could be **cut loose** as its own group is deliberately open, with three candidate designs. See [Open Questions](../project/open-questions.md#severed-pods).

## Enemy bubbles

Enemy armies are bubbles too (same code, different faction/colour). They currently just hold ground and fight when touched; they do not stretch. Whether enemy AI ever stretches is open.

## Known feel issues <span class="pill risk">RISK</span>

Carried on the [Backlog](../project/backlog.md):

- Melees collapse into a single scrum: nearest-enemy targeting pulls both sides into one ball. Likely fix: cap chase distance from formation slot so front ranks fight and back ranks hold.
- When a pod pokes an enemy bubble, **all** enemy troops respond and chase — drags their whole army out of its circle. Likely fix: defenders-only response rule.
- Right-click double-duty: breaking a pod grip also starts a camera orbit (right-drag). Cosmetic at tap-length, but a candidate for rebinding.
