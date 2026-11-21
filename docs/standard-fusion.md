# Standard fusion

Sources: [Star Wars Droid Tycoon - Fusion Recipes & Scourge Equivalents](https://docs.google.com/spreadsheets/d/1XHNAyen1vCPaDLuKN17lJYUkNHrCM-uXqtiDXD8O3Ls/edit?pli=1&gid=1#gid=1) (original 17) and the [Droidex fusion guide](https://droidex.dubtrackr.win/guides/droid-fusion/) (v1.40.0, 11 new).

A fusion takes **3 components** and produces **1 droid**. There are 28 known recipes. Any other combination produces a random droid.

## Recipe data

| Rarity | Recipes |
|---|---|
| Common | ION PROBE, QUAD SENTRY, LFT-3R |
| Rare | WHL-EX, ZRO-TEC, BTL-R |
| Epic | N-UL, SCRP-R, ARM-CORE, OPT-AR, STRD-3, BI-BIT |
| Legendary | RO-TOR, FUS-3, ORB-XL, QIK-BIT, TOR-Q, HV-EE |
| Mythic | RIV-3T, LUG-G, X-ONK, SRV-O, AXI-POD, LOW-MO, AX-L, MO-TRO, SKM-MR, KL-NK |

### Conflict resolution

The sheets and guides disagree on a few fields. The app follows the most recent public source, the [Droidex](https://droidex.dubtrackr.win/guides/droid-fusion/) (v1.40.0, the update that added the 11 new recipes):

| Field | Original sheet + older guides | v3 sheet | Droidex v1.40.0 | Used |
|---|---|---|---|---|
| Name | AXL-POD | AXI-POD | AXI-POD | **AXI-POD** |
| Name | SRV-0 (zero) | SRV-O (letter) | SRV-O | **SRV-O** |
| LOW-MO type | Astromech | Worker | _(not stated)_ | **Astromech** |
| Component | BDX | BDX EXPLORER | BDX EXPLORER | **BDX EXPLORER** |

The Droidex lists the same 28 recipes as the v3 sheet, with the same components.

### Not covered

Fusions that aren't a named recipe (e.g. 3 identical droids raising variant or rarity) follow other rules in the game. The app shows RANDOM for them.

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
