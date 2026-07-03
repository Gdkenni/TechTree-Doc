# How To Correctly Exclude Vanilla Nodes

This tutorial explains how to remove vanilla nodes without having them come back later.

Use this page when you want a vanilla unlock to stay removed from a custom or seasonal tree.

---

## Important Rule

**Exclude from vanilla sync** must be used together with **Disable Future Vanilla Imports**.

If `Disable Future Vanilla Imports` is not enabled, vanilla synchronization can import removed vanilla nodes again later.

Think of it like this:

- `Exclude from vanilla sync` marks one vanilla node as intentionally removed.
- `Disable Future Vanilla Imports` tells the workbench to stop accepting new vanilla imports later.

You need both when the goal is to keep a vanilla node removed permanently.

---

## Why This Matters

Vanilla nodes are linked to Rust's vanilla tech tree through a `vanilla ID`.

If a vanilla node is removed without proper exclusion, TechTree may treat it as missing vanilla content later.

That can make the node appear again during synchronization.

Custom nodes do not need vanilla exclusion.

If you remove a custom node, it is simply removed from your TechTree data.

---

## Step 1: Disable Future Vanilla Imports

Open **Excluded Nodes** and enable `Disable future vanilla imports`.

![|272x598](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/vanilla-sync-excluded-nodes-modal.png)

This tells TechTree that this workbench tree should stop accepting future vanilla imports.

This step is required before node exclusions can do their job correctly.

---

## Step 2: Exclude The Vanilla Node

Select the vanilla node you want to remove.

Click `Modify`.

Enable `Exclude from vanilla sync`.

![|272x600](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/vanilla-sync-node-exclude-toggle.png)

Confirm the edit.

This adds the vanilla ID to the excluded list.

Do this before removing the node from the tree.

---

## Step 3: Remove The Node

After the node is excluded:

- Select the same node again.
- Click `Remove`.
- Save the editor session.

The node is now removed from the tree and marked as intentionally excluded.

---

## Safe Workflow

Use this workflow when you want to remove one vanilla node permanently from a customized tree.

- Open **TechTree** at the correct workbench.
- Switch to **Edit Mode**.
- Open **Excluded Nodes**.
- Enable `Disable Future Vanilla Imports`.
- Select the vanilla node you want to remove.
- Click `Modify`.
- Enable `Exclude from vanilla sync`.
- Click `Confirm`.
- Select the same node again.
- Click `Remove`.
- Press `Save`.

---

## Fully Custom Tree Workflow

Use this when you want to convert a workbench tree into a fully custom layout.

- Open **Edit Mode**.
- Open **Excluded Nodes**.
- Enable `Disable Future Vanilla Imports`.
- Click `Exclude All`.
- Remove the vanilla nodes you do not want.
- Build your custom tree.
- Save.

This is usually the cleanest approach when you do not want Rust updates to rebuild the vanilla progression on that workbench.

---

## Excluded Nodes Modal

The **Excluded Nodes** modal shows which vanilla nodes are currently excluded.

From this modal you can:

- Enable or disable future vanilla imports.
- Exclude all vanilla nodes.
- Clear all exclusions.
- Restore individual excluded nodes.

---

## When Not To Exclude

Do not exclude a vanilla node if you want to keep receiving future vanilla progression changes naturally.

In that case, keep **Auto Vanilla Synchronization** enabled and avoid permanently removing vanilla nodes.

---

## Quick Check

If a removed vanilla node keeps coming back, check these points:

- `Disable Future Vanilla Imports` is enabled.
- The node was excluded before being removed.
- The editor session was saved.
- You are editing the correct workbench category.
