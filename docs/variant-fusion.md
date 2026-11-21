# Variant & Scourge fusion

Source: [Droidex fusion guide](https://droidex.dubtrackr.win/guides/droid-fusion/) (fan resource, reviewed for Droid Tycoon v1.40.0, November 2026).

> These rules come from a fan resource and **have not been validated in-game by us**.

## Two independent questions

A fusion answers two separate questions, and the code keeps them separate:

| Question | Decided by | Does slot order matter? |
|---|---|---|
| **Which droid?** (species) | The components, same as the [Standard tab](standard-fusion.md) | No |
| **Which variant?** (quality) | The variant of each slot | **Only on ties** |

That is why this tab reuses `RECIPES` and only adds a variant selector per slot.

## The rule

> The output takes the **lowest** input variant. On a **tie**, the **leftmost** slot wins.

Variants, low to high, with the weight used in code:

| Variant | Weight |
|---|---|
| Default | 0 |
| Gold | 1 |
| Diamond | 2 |
| Rainbow | 3 |
| Beskar | 4 |
| Galactic | 5 |
| Stellar | 6 |
| **Scourge** | **6** |
| Kyber | 7 |

Scourge has the **same weight as Stellar**, below Kyber. That one fact explains every Scourge behavior:

| Input (slot 1 + 2 + 3) | Output | Why |
|---|---|---|
| Scourge + Kyber + Kyber | Scourge | Scourge is the lowest. |
| Kyber + Scourge + Kyber | Scourge | Still the lowest; position doesn't matter without a tie. |
| Scourge + Stellar + Stellar | Scourge | Tie; Scourge is leftmost. |
| Stellar + Scourge + Kyber | **Stellar** | Tie; Stellar is leftmost. |
| Scourge + Beskar + Kyber | **Beskar** | Beskar is lower than Scourge. |
| Rainbow + Rainbow + Diamond | Diamond | Diamond is the lowest. |

**Cheapest Scourge: 1 Scourge + 2 Kyber**, in any order. With Stellar filler, the Scourge must be to the left of the Stellars.

## Code

```js
// Winning slot: lowest weight, leftmost on ties (indexOf returns the first match).
const resolveVariant = tiers => {
  const weights = tiers.map(t => tierOf(t).weight);
  return weights.indexOf(Math.min(...weights));
};
```

`explainVariant` wraps it to build the result box:

| Situation | Color | Message |
|---|---|---|
| Output is Scourge | green | Scourge + cost note (ideal with 1 Scourge; warns when using 2–3). |
| Scourge was in the input but lost | red | Which variant took over and how to fix it. |
| No Scourge in the input | green | The resulting variant and the slot that set it. |

When a tie decided the result between different variants (Stellar vs Scourge), the note says so.

## Render flow (`renderScourge`)

| Input | Result box |
|---|---|
| Nothing selected | "Select a component" |
| Components no recipe fits | **RANDOM** (red) |
| 1–2 components | "Possible droids: N recipes" |
| 3 components, some variant missing | Droid name + "Choose each slot's variant" |
| 3 components, all variants set | Droid + resulting variant |

The table shows the cheapest Scourge layout for each recipe: the first component as **Scourge**, the other two as **Kyber/Stellar** filler.

## History: why this tab was rewritten

The first version followed [images/scourge-rules.png](images/scourge-rules.png), which described the Scourge case as three special rules (Scourge must be in Slot 1, filler must be Kyber/Stellar, 1 Scourge is optimal). Those rules are **special cases of the general rule above**, and they got two things wrong:

- "Scourge must be in Slot 1" is only true when Stellar is present. With Kyber filler, any position works.
- It only answered "Scourge or not"; it ignored Galactic and couldn't tell which variant you actually get.

## Not covered

- **Kyber colors** (Inactive, Green, Blue, Purple). Treated as plain Kyber.
- **Non-recipe fusions** (3 identical droids raising variant or rarity). The app shows RANDOM for any combination that isn't a named recipe.
