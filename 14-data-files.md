# Data Files

**TechTree** stores editable tree data and player unlock data separately.

This helps with backups, wipes, maintenance, and manual recovery.

---

## Main Data

Workbench tree data is stored per category.

Each category contains its own nodes, prices, parents, rewards, images, and vanilla sync settings.

Categories include:

- `Workbench_1`.
- `Workbench_2`.
- `Workbench_3`.
- `Engineering`.

---

## Player Data

Player data stores unlocked nodes for each player.

This data is separate from the tree layout.

You can wipe player progression without deleting the tree design.

---

## Themes

Themes are stored separately from tree data.

The selected theme is chosen through the config and loaded from `Themes.json`.

---

## Local Images

Local images are stored in:

```text
oxide/data/TechTree/Images/
```

The `Images/` folder supports subfolders.

The local image picker lets admins navigate inside those folders.

TechTree stores local images by **relative path from the Images folder**, without the extension.

Example:

```text
Images/Weapons/rifle_icon.png
```

Stored local image value:

```text
Weapons/rifle_icon
```

Reload updates the image database from the current folder structure without reloading the whole plugin.

Supported formats:

- `png`.
- `jpg`.
- `jpeg`.

Local images are supported on **Oxide** and **Carbon**.

---

## Backups

Before making large changes, back up:

- TechTree config.
- TechTree data files.
- Player data files.
- Themes.
- Local images.

This is especially important before changing node IDs, rebuilding trees, or changing live server progression.
