# Droid Tycoon Calculator

Droid fusion calculator for the Fortnite island Droid Tycoon.

**Live:** https://story-games.github.io/droid-tycoon-calculator/

## How to use

Open the live link above, or open `index.html` in your browser. No build or dependencies needed.

## V1 — "Standard" tab ✅

Based on `docs/images/standard-recipes.png` (original 17 recipes) and `docs/images/standard-recipes-v3.png` (11 new recipes) — **28 recipes** in total, from Common to Mythic.

Names follow the [Droidex](https://droidex.dubtrackr.win/guides/droid-fusion/) (v1.40.0): `AXI-POD`, `SRV-O`. `LOW-MO` stays Astromech, as in the older public guides. `BDX` is written `BDX EXPLORER` (its full in-game name).

- 3 boxes to enter components (with autocomplete).
- Each component narrows the search: with `ARG` in Component 1, you get WHL-EX, ARM-CORE and every other recipe that uses ARG.
- **Slot order does not matter** for the droid; **quantity does** (`ARG + ARG` only matches recipes with 2x ARG).
- Combination that doesn't exist → **RANDOM** result.
- 3 components that form a recipe → shows the resulting droid.

## V2 — "Variant & Scourge" tab ✅

Calculates the **variant** (quality) of the fusion result. Based on the [Droidex fusion guide](https://droidex.dubtrackr.win/guides/droid-fusion/) (v1.40.0).

The droid is decided by the components (same as V1). The variant follows one rule:

> The output takes the **lowest** input variant. On a **tie**, the **leftmost** slot wins.

Low to high: Default, Gold, Diamond, Rainbow, Beskar, Galactic, **Stellar = Scourge**, Kyber.

Because Scourge ranks with Stellar (below Kyber):

| Input (slot 1 + 2 + 3) | Result |
|---|---|
| Scourge + Kyber + Kyber (any order) | Scourge — the cheapest way |
| Scourge + Stellar + Stellar | Scourge (tie, Scourge is leftmost) |
| Stellar + Scourge + Kyber | Stellar (tie, Stellar is leftmost) |
| Scourge + Beskar + Kyber | Beskar (lowest) |

> These rules come from a fan resource and **have not been validated in-game yet**. The first version of this tab followed `docs/images/scourge-rules.png`, which turned out to describe special cases of this rule — see [docs/variant-fusion.md](docs/variant-fusion.md).

## Structure

- `index.html` — single page (HTML + CSS + vanilla JS), with Standard, Variant & Scourge and Credits tabs.
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
