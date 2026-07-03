# Admin Editor

**TechTree** includes an in-game admin editor for building and maintaining the tree.

The editor is designed so you can adjust progression without manually editing JSON files for every change.

---

## What You Can Edit

- Node position.
- Node price.
- Node currency.
- Parent nodes.
- Node permission.
- Rewards.
- Image type and image value.
- Public name.
- Public description.
- Vanilla exclusion settings.

---

## Image Types

Nodes can use different image sources.

- `Item` image.
- `Url` image.
- `Local` image.

`Item` images use a Rust `item ID` and `skin ID`.

`Url` images use an external image link.

`Local` images use files placed inside the plugin data folder.

---

## Editor Workflow

- Open **TechTree**.
- Switch to **Edit Mode**.
- Select a node.
- Click `Modify`.
- Change the fields you need.
- Click `Confirm`.
- Save the editor session.

**Important:** changes are not meant to be left unsaved.

Always save after editing a tree.

---

## Recommended Usage

Use the editor for regular changes.

Use JSON files only for backups, recovery, mass editing, or advanced maintenance.
