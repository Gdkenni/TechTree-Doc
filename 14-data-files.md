# Data Files

**TechTree** stores editable tree data and player unlock data separately.

This helps with backups, wipes, maintenance, and manual recovery.

---

## Folder Layout

All files are in the TechTree data folder, `carbon/data/TechTree/` or `oxide/data/TechTree/`.

```text
TechTree/
  Data/Data_Workbench_1.json
  Data/Data_Workbench_2.json
  Data/Data_Workbench_3.json
  Data/Data_Engineering.json
  Data/Subcategory/<Workbench>/<id>.json
  Players/<steamid>.json
  Themes.json
  Images/
```

---

## Main Trees

Each workbench category has one main tree file in `Data/`.

Categories:

- `Workbench_1`.
- `Workbench_2`.
- `Workbench_3`.
- `Engineering`.

If a main tree file is missing, TechTree builds it from Rust's vanilla tree.

---

## Subcategories

Each subcategory has its own file in `Data/Subcategory/<Workbench>/`.

The file name comes from the subcategory title: lowercase letters and digits, other characters become `_`.

Example: `New subcategory 2` is saved as `new_subcategory_2.json`.

Renaming the subcategory renames the file when you click `SAVE`.

---

## Tree File

A tree file contains:

- `TechTree`: the list of nodes.
- `Grid Bounds`: the grid size.
- `Disable Future Vanilla Imports`.
- `Enable Auto Vanilla Sync`.
- `Excluded Vanilla IDs`: vanilla IDs excluded from synchronization.
- `Extra`: rewards given when a player unlocks every node of the tree.

Subcategory files also contain:

- `Subcategory Title`.
- `Subcategory Order`.
- `Subcategory Access`: `Locked`, `Hidden` or `Public`.
- `Subcategory Conditions`: permissions and completed categories.

Tree completion rewards example:

```json
"Extra": {
  "Reward On All Node Unlocked": [
    { "Type": "ConsoleCommand", "Value": "inventory.giveto playerID scrap 500" }
  ]
}
```

---

## Node Format

```json
{
  "ID": 123,
  "Vanilla ID": 456,
  "Parent": [111],
  "Permission": "vip.weapons",
  "Image URL or Item": { "Type": "Item", "Value": { "Item ID": -932201673, "Skin ID": 0 } },
  "Grid Position": { "x": 0.5, "y": 2.0 },
  "Player Info": { "Ingame Name": { "Lang": { "en": "My node" } }, "Description": { "Lang": {} } },
  "Price": { "Rarity": 2, "Value": 40 },
  "Curency": { "Item ID": -932201673, "Skin ID": 0 },
  "Rewards": [ { "Type": "ConsoleCommand", "Value": "say playerID unlocked a node" } ]
}
```

- `Vanilla ID` and `Permission` are omitted when empty.
- `Image URL or Item` types: `Item`, `Url` (a link) or `Local` (a local image value).
- `Price` without `Rarity` is a custom price.
- When `Rarity` is set, `Value` is replaced by the rarity price table at load.
- `Curency` is the real key name, with one `r`.
- Reward types: `ChatCommand`, `ConsoleCommand`, `Economics`.

Old files with a plain number as price are still accepted:

```json
"Price": 60
```

---

## Player Data

Player data stores unlocked nodes for each player, per workbench.

```json
{ "UnlockedByWorkbench": { "Workbench_1": [123, 456], "Workbench_2": [] } }
```

All trees of a workbench share one list, subcategories included.

This data is separate from the tree layout.

You can wipe player progression without deleting the tree design.

Unknown node IDs are removed when the player data loads.

---

## Themes

All themes are stored in `Themes.json`.

The selected theme is chosen through the config. See **Themes And Node Styles**.

---

## Local Images

Local images are stored in `Images/`, with subfolders.

See **Local Images**.

---

## Backups

Before making large changes, back up:

- TechTree config.
- The `Data/` folder, subcategories included.
- Player data files.
- `Themes.json`.
- Local images.

This is especially important before changing node IDs, rebuilding trees, or changing live server progression.
