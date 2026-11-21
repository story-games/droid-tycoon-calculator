# Documentation

How the Droid Tycoon Calculator works and the logic behind each tab.

| Document | What it covers |
|---|---|
| [architecture.md](architecture.md) | How the single-page app is built: data, shared logic, tabs, rendering. |
| [standard-fusion.md](standard-fusion.md) | The Standard tab: recipe matching, quantity rules, results. |
| [variant-fusion.md](variant-fusion.md) | The Variant & Scourge tab: lowest-variant rule, left-slot tie-breaker, Scourge. |

## Reference images

The images in [`images/`](images/) are snapshots of the source spreadsheet ([Star Wars Droid Tycoon - Fusion Recipes & Scourge Equivalents](https://docs.google.com/spreadsheets/d/1XHNAyen1vCPaDLuKN17lJYUkNHrCM-uXqtiDXD8O3Ls/edit?pli=1&gid=1#gid=1)). They were the starting point for the code; where a newer public source disagrees, the docs say which one the app follows.

| Image | Content |
|---|---|
| [standard-recipes.png](images/standard-recipes.png) | The original 17 standard fusion recipes. |
| [standard-recipes-v3.png](images/standard-recipes-v3.png) | Updated sheet with 28 recipes (11 new, including Common rarity and Protocol type). |
| [scourge-rules.png](images/scourge-rules.png) | Scourge mix patterns and three rules. **Superseded** by the general rule in [variant-fusion.md](variant-fusion.md); kept for history. |
| [scourge-recipes.png](images/scourge-recipes.png) | The original 17 recipes laid out as 1x Scourge anchor + 2x Kyber/Stellar filler. |
