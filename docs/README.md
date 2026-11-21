# Documentation

How the Droid Tycoon Calculator works and the logic behind each tab.

| Document | What it covers |
|---|---|
| [architecture.md](architecture.md) | How the single-page app is built: data, shared logic, tabs, rendering. |
| [standard-fusion.md](standard-fusion.md) | The Standard tab: recipe matching, quantity rules, results. |
| [scourge-fusion.md](scourge-fusion.md) | The Scourge tab: tier rules, slot anchor, result evaluation. |

## Reference images

The images in [`images/`](images/) are snapshots of the source spreadsheet ([Star Wars Droid Tycoon - Fusion Recipes & Scourge Equivalents](https://docs.google.com/spreadsheets/d/1XHNAyen1vCPaDLuKN17lJYUkNHrCM-uXqtiDXD8O3Ls/edit?pli=1&gid=1#gid=1)). They are the ground truth the code was built from.

| Image | Content |
|---|---|
| [standard-recipes.png](images/standard-recipes.png) | The 17 standard fusion recipes. |
| [scourge-rules.png](images/scourge-rules.png) | Scourge input mix patterns and the three optimal fusion rules. |
| [scourge-recipes.png](images/scourge-recipes.png) | The 17 recipes laid out as 1x Scourge anchor + 2x Kyber/Stellar filler. |
