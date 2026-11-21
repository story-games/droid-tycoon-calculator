# Architecture

The whole app is one file: `index.html` (HTML + CSS + vanilla JS). No build, no dependencies, no framework. It runs by opening the file or through GitHub Pages.

## Layout

```
index.html
├── <style>        theme variables, tabs, inputs, result box, tables, credits
├── <main>
│   ├── tabs       Standard | Scourge | Credits
│   ├── #panel-standard
│   ├── #panel-scourge
│   └── #panel-credits
└── <script>
    ├── RECIPES            shared data (single source of truth)
    ├── shared logic       normalize, countOf, recipeAccepts, highlightMask, readSlots, setResult, renderRows
    ├── tabs               show/hide panels
    ├── Standard tab       renderStandard
    └── Variant tab        TIERS, resolveVariant, explainVariant, renderScourge
```

## Single source of truth: `RECIPES`

```js
{ name: "WHL-EX", rarity: "Rare", type: "Worker", components: ["ARG", "MOUSE", "MOUSE"] }
```

Both tabs use the same recipes; the Variant tab only adds the variant of each slot. So there is no second recipe list. The Variant tab reuses `RECIPES` and adds a variant layer on top.

`ALL_COMPONENTS` is derived from `RECIPES` (unique, sorted). It feeds the autocomplete `<datalist>` and input validation, so adding a recipe automatically adds its components.

## Shared logic

| Function | Responsibility |
|---|---|
| `normalize(v)` | Trim, uppercase, collapse spaces. `" b1  heavy"` → `"B1 HEAVY"`. |
| `countOf(list)` | Turn a list into a count map. `["ARG","ARG"]` → `{ ARG: 2 }`. |
| `recipeAccepts(recipe, selected)` | True if the recipe contains **at least** the selected components, counting duplicates. |
| `highlightMask(recipe, selected)` | Which recipe cells to highlight. Each selected component consumes one matching cell, so `ARG` highlights only one of two `ARG` cells. |
| `readSlots(inputs)` | Read and normalize inputs; mark unknown components as `invalid` (red border). |
| `setResult(el, …)` | Fill the result box (label, value, note) and set its color class. |
| `renderRows(tbody, recipes, selected, cellLabel?)` | Render the recipe table. `cellLabel` is an optional formatter the Variant tab uses to show the cheapest Scourge layout. |

## Rendering flow

Both tabs follow the same cycle on every `input`/`change` event:

1. Read the slots (`readSlots`).
2. Filter `RECIPES` with `recipeAccepts`.
3. Decide the result state and call `setResult`.
4. Re-render the table with the matches (or all recipes when nothing is selected).

There is no state object; the DOM inputs are the state. Each render recomputes everything from scratch, which is trivial for 28 recipes.

## Result states (CSS classes)

| Class | Color | Meaning |
|---|---|---|
| _(none)_ | neutral | Waiting for input / partial match. |
| `match` | green | A valid fusion result. |
| `random` | red | Combination not in any recipe → random result in-game. |
| `fail` | red | Variant tab: a Scourge was in the input but another variant won. |

## Adding a recipe

Add one object to `RECIPES`. Both tabs, the autocomplete and validation pick it up automatically.
