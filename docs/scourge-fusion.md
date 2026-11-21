# Scourge fusion

Sources: [images/scourge-rules.png](images/scourge-rules.png) and [images/scourge-recipes.png](images/scourge-recipes.png).

> These rules come from the source spreadsheet and **have not been validated in-game yet**.

## Two independent questions

A Scourge fusion answers two separate questions, and the code keeps them separate:

| Question | Decided by | Does slot order matter? |
|---|---|---|
| **Which droid?** (species) | The components, same as the [Standard tab](standard-fusion.md) | No |
| **Which quality?** (tier) | The tier of each slot | **Yes** |

The Scourge recipes are the same recipes as the standard ones. That is why the tab reuses `RECIPES` and only adds a tier selector per slot.

The source only shows Scourge layouts for the original 17 recipes. The 11 new recipes (see [standard-fusion.md](standard-fusion.md)) are shown in this tab assuming the same tier rules apply.

## Tiers

From highest to lowest: **Scourge, Stellar, Kyber**, Beskar, Rainbow, Diamond, Gold, Base.

Only the first three are "safe" for a Scourge fusion (`SCOURGE_SAFE_TIERS`).

## The three rules

### Rule 1 — Slot 1 is the Scourge anchor

Scourge ties with Stellar in rarity weight. When there is a tie, the **leftmost slot** decides the output. So the Scourge component must be in Slot 1.

### Rule 2 — Strict filler (Kyber or Stellar only)

Slots 2 and 3 must be Kyber, Stellar or Scourge. Non-activated Kyber works fine. Any lower tier (Base, Gold, Diamond, Rainbow, Beskar) triggers the **lowest-tier-matches** rule and ruins the Scourge outcome.

### Rule 3 — Resource optimization

The ideal mix is **1 Scourge + 2 Kyber/Stellar**. It saves two-thirds of your Scourge stock.

| Mix | Output | Notes |
|---|---|---|
| 1 Scourge + 2 Kyber | Scourge Equivalent | Ideal. |
| 1 Scourge + 2 Stellar | Scourge Equivalent | Ideal. |
| 2 Scourge + 1 Kyber | Scourge Equivalent | Reliable, but uses 2 Scourge. |
| 3 Scourge | Scourge Base Tier | Inefficient. |

## Evaluation order (`evaluateScourgeTier`)

The checks run in this order; the first one that applies wins:

```
1. Any tier outside Scourge/Stellar/Kyber?  → NOT SCOURGE      (Rule 2)
2. No Scourge at all?                        → NOT SCOURGE
3. Slot 1 is not Scourge?                    → SCOURGE NOT GUARANTEED (Rule 1)
4. Count the Scourge components:
     1 → SCOURGE EQUIVALENT  (ideal)
     2 → SCOURGE EQUIVALENT  (uses 2 Scourge)
     3 → SCOURGE (BASE TIER) (inefficient)
```

Rule 2 is checked before Rule 1 on purpose: a lower tier ruins the result no matter where the Scourge is, so that is the more important message.

**SCOURGE NOT GUARANTEED** (yellow) covers a case the source does not describe: a Scourge present but not in Slot 1. The source only guarantees the outcome with the Scourge in Slot 1, so the app doesn't guess.

## Full render flow (`renderScourge`)

| Input | Result box |
|---|---|
| Nothing selected | "Select a component" + tip to put the Scourge in Slot 1 |
| Components no recipe fits | **RANDOM** (red) |
| 1–2 components | "Possible droids: N recipes" |
| 3 components, some tier missing | Droid name + "Choose each slot's tier" |
| 3 components, all tiers set | Droid + tier evaluation (green / red / yellow) |

## Table

The table shows the optimal layout from the source: the first component of each recipe as the **Scourge** anchor, the other two as **Kyber/Stellar** filler (`scourgeCellLabel`). It is a guide for building the fusion, not a reflection of the tiers you picked.
