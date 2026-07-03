# TechTree Overview

**TechTree** replaces or complements the default Rust workbench tech tree with an editable progression system.

It lets server owners customize progression without forcing every change into Rust's vanilla tree.

---

## Main Features

- Editable **workbench tech trees**.
- Support for **vanilla nodes** and **custom nodes**.
- `Item`, `Url`, and `Local` node images.
- Custom prices and currencies.
- Node rewards.
- Branch permissions.
- Player unlock tracking.
- Vanilla synchronization tools.
- Admin editor directly in game.
- API methods and hooks for other plugins.

---

## Workbench Categories

- `Workbench_1`.
- `Workbench_2`.
- `Workbench_3`.
- `Engineering`.

Each category has its own saved tree data.

---

## Vanilla Nodes And Custom Nodes

**Vanilla nodes** come from Rust's original Facepunch tech tree.

They have a `vanilla ID`, which allows **TechTree** to recognize, synchronize, recover, or exclude them.

**Custom nodes** are created inside the **TechTree editor**.

They belong only to TechTree data and are not restored by vanilla synchronization.

---

## Same Editing Options

Both **vanilla** and **custom** nodes can use the same customization features.

- Price.
- Currency.
- Parent nodes.
- Permissions.
- Rewards.
- Image.
- Name.
- Description.

A custom node can even reproduce a vanilla unlock if needed.

Their main purpose is to create server-specific content, custom items, plugin rewards, profession branches, VIP branches, or progression that does not exist in vanilla Rust.
