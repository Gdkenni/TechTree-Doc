# Good To Know

This page contains useful notes that do not fit into a single tutorial.

---

## Editor Session

Edits are kept in a draft until you click `SAVE`.

Switching to `PLAYER MODE` or clicking `CLOSE` discards unsaved changes, without confirmation.

`Reset to Vanilla`, theme actions, the economy model and `APPLY TO ALL NODES` are saved immediately.

---

## Use Permissions

`Use Permissions ?` controls TechTree permission checks.

When enabled, it affects **global permissions**, **branch permissions** and subcategory permission conditions.

If branch permissions do not seem to work, check this option first.

---

## Branch Permissions

Typing a permission in the node editor does not automatically grant it.

You must grant the permission with your permission manager.

TechTree does not register branch permissions.

---

## Subcategories

Subcategories are never affected by vanilla synchronization.

All trees of a workbench share the same node IDs and the same player progression.

---

## Prices

Nodes linked to a rarity follow the rarity price table.

In the **Blueprints** economy model, they are paid with blueprint fragments, pages or books.

Custom prices and custom currencies are never changed by the economy model.

---

## Local Images

Local images are supported on **Oxide** and **Carbon**.

On Oxide, they require the **ImageLibrary** plugin.

The `Images/` folder supports subfolders.

Local image values use the **relative path from the Images folder**, without the extension.

Example:

```text
Images/Weapons/rifle_icon.png
```

Stored value:

```text
Weapons/rifle_icon
```

Use the reload button in the local image picker after adding, replacing, moving, or deleting files in the Images folder.

---

## Vanilla Nodes

Vanilla nodes can be edited like normal nodes.

They can have custom prices, rewards, permissions, images, names, and descriptions.

Their difference is the `vanilla ID`.

That ID lets TechTree synchronize, recover, or exclude them.

Vanilla nodes also follow the player's learned blueprints: a known blueprint unlocks the node.

---

## Custom Nodes

Custom nodes do not need vanilla exclusion.

They are not restored by vanilla synchronization.

They are mostly useful for custom items, rewards, server progression, professions and VIP branches.

Use them for content that does not exist in vanilla Rust.

---

## Rewards

Use `ConsoleCommand` for server-side commands.

Use `ChatCommand` for commands the player runs. See **How To Use Rewards** for chat commands.

Use the `playerID` placeholder when the command needs the player's Steam ID.

---

## Editor Safety

Save after editing.

Back up data before large changes.

Test complex progression changes before applying them to a live server.
