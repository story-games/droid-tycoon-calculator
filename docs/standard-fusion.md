# Standard fusion

Sources: [images/standard-recipes.png](images/standard-recipes.png) (original 17) and [images/standard-recipes-v3.png](images/standard-recipes-v3.png) (11 new).

A fusion takes **3 components** and produces **1 droid**. There are 28 known recipes. Any other combination produces a random droid.

## Recipe data

| Rarity | Recipes |
|---|---|
| Common | ION PROBE, QUAD SENTRY, LFT-3R |
| Rare | WHL-EX, ZRO-TEC, BTL-R |
| Epic | N-UL, SCRP-R, ARM-CORE, OPT-AR, STRD-3, BI-BIT |
| Legendary | RO-TOR, FUS-3, ORB-XL, QIK-BIT, TOR-Q, HV-EE |
| Mythic | RIV-3T, LUG-G, X-ONK, SRV-0, AXL-POD, LOW-MO, AX-L, MO-TRO, SKM-MR, KL-NK |

### Conflict resolution

The v3 sheet disagrees with the original sheet on a few fields. The app follows the **public guides** (all list the same original 17):

| Field | Original sheet + public guides | v3 sheet | Used |
|---|---|---|---|
| Name | AXL-POD | AXI-POD | AXL-POD |
| Name | SRV-0 (zero) | SRV-O (letter) | SRV-0 |
| LOW-MO type | Astromech | Worker | Astromech |
| Component | BDX | BDX EXPLORER | BDX EXPLORER (public guides use the full name) |

The 11 new recipes come only from the v3 sheet; no public guide listed them at the time (November 2026).

### Not covered

Public guides mention a separate mechanic: fusing **3 identical droids** to raise their rarity. The app does not model it.

## Rules

### 1. Slot order does not matter

`ARG + MOUSE + MOUSE` and `MOUSE + ARG + MOUSE` are the same fusion (WHL-EX). Internally, the selection is treated as a multiset, not a sequence.

### 2. Quantity matters

Components are counted, not just checked for presence:

| Selected | Matches | Why |
|---|---|---|
| `ARG` | WHL-EX, ARM-CORE | Both contain at least 1 ARG. |
| `ARG + ARG` | ARM-CORE | Only ARM-CORE has 2x ARG. |
| `ARG + ARG + ARG` | _(none)_ | No recipe has 3x ARG → RANDOM. |

This is `recipeAccepts`: for every selected component, the recipe must contain at least that many copies.

```js
const need = countOf(selected);          // { ARG: 2 }
const have = countOf(recipe.components); // { ARG: 2, "B2 HEAVY": 1 }
return Object.entries(need).every(([c, n]) => (have[c] || 0) >= n);
```

### 3. The search narrows as you type

Each filled slot is a filter. Partial input shows every recipe that can still be completed, so you can explore which droids a component leads to.

## Result states

| Input | Result box |
|---|---|
| Nothing selected | "Select a component" (table shows all 28 recipes) |
| 1–2 components, some recipe fits | "Possible droids: N recipes" |
| 3 components forming a recipe | **Fusion result**: droid, rarity and type (green) |
| Any combination no recipe fits | **RANDOM** (red) |

Unknown component names get a red border and are ignored by the filter.

## Table highlight

Cells that match a selected component are highlighted. Each selected component highlights **one** cell, so selecting one `ARG` in ARM-CORE (`ARG, ARG, B2 HEAVY`) highlights only the first `ARG`.
