# Droid Tycoon Calculator

Droid fusion calculator for the Fortnite island Droid Tycoon.

**Live:** https://story-games.github.io/droid-tycoon-calculator/

## How to use

Open the live link above, or open `index.html` in your browser. No build or dependencies needed.

## V1 — "Standard" tab ✅

Based on `docs/images/standard-recipes.png` (17 standard fusion recipes).

- 3 boxes to enter components (with autocomplete).
- Each component narrows the search: with `ARG` in Component 1, you get WHL-EX, ARM-CORE and every other recipe that uses ARG.
- **Slot order does not matter** for the droid; **quantity does** (`ARG + ARG` only matches recipes with 2x ARG).
- Combination that doesn't exist → **RANDOM** result.
- 3 components that form a recipe → shows the resulting droid.

## V2 — "Scourge" tab ✅

Based on `docs/images/scourge-rules.png` and `docs/images/scourge-recipes.png`.

The Scourge recipes are **the same 17 as V1**; what changes is each component's **tier**. So this tab reuses the same data (`RECIPES`) and only adds a tier selector per slot.

Tiers: Scourge, Stellar, Kyber, Beskar, Rainbow, Diamond, Gold, Base.

Applied rules (from the source document):

1. **Slot 1 = Scourge (anchor).** Scourge ties with Stellar in rarity weight, and the leftmost slot breaks the tie. For the droid, position still doesn't matter; it only matters for the tier.
2. **Slots 2 and 3: only Kyber, Stellar or Scourge.** Any lower tier (Base, Gold, Diamond, Rainbow, Beskar) triggers the lowest-tier rule and the result is not Scourge.
3. **Ideal: 1 Scourge + 2 Kyber/Stellar.** Saves 2/3 of your Scourge stock. 3 Scourge gives a base-tier Scourge (inefficient).

Possible results in this tab:

| Situation | Result |
|---|---|
| Scourge in Slot 1 + Kyber/Stellar/Scourge in the others | Scourge Equivalent (or base tier with 3 Scourge) |
| Any lower tier | Not Scourge |
| No Scourge | Not Scourge |
| Scourge present, but not in Slot 1 | Scourge not guaranteed (case not covered by the document) |
| Components that don't form a recipe | RANDOM |

> The tier rules follow the document and **have not been validated in-game yet**.

## Structure

- `index.html` — single page (HTML + CSS + vanilla JS), with Standard, Scourge and Credits tabs.
- `docs/` — how it works and the logic behind each tab ([start here](docs/README.md)).
- `docs/images/` — reference images from the source spreadsheet.

## Source

[Star Wars Droid Tycoon - Fusion Recipes & Scourge Equivalents](https://docs.google.com/spreadsheets/d/1XHNAyen1vCPaDLuKN17lJYUkNHrCM-uXqtiDXD8O3Ls/edit?pli=1&gid=1#gid=1)

## Credits

Made by **hckoalla** at **Story Games**.

- [Discord](https://www.storygames.com.br/p/discord.html)
- [Facebook](https://www.facebook.com/storydevgames/)
- [Instagram](https://www.instagram.com/storydevgames/)
- [X](https://x.com/storydevgames)
- [itch.io](https://storydevgames.itch.io/)
- [Website](https://www.storygames.com.br/)

Fan-made tool. Not affiliated with Epic Games, Lucasfilm or Disney. Fortnite and Star Wars are trademarks of their respective owners.
