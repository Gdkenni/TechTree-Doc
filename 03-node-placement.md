# Node Placement And Lines

This page explains how to place nodes so the connection lines stay clean and readable.

The important idea is simple:

**TechTree progression is meant to flow from top to bottom.**

Parent nodes should usually be placed above their child nodes.

![|300](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/node-lines-logic.png)

---

## How Lines Are Drawn

TechTree does not draw freeform lines.

Lines are generated from the parent and child positions.

For each parent:

- The line starts from the **bottom** of the parent node.
- It goes toward a shared corridor.
- If the parent has several children, a horizontal line connects the branch.
- Each child is connected from that corridor to the **top** of the child node.

This means the layout works best when children are placed **below** their parent.

![|300](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/node-lines-good-bad.png)

---

## Recommended Direction

Use this visual logic:

```text
Parent
  |
  +--- Child
  |
  +--- Child
```

In the editor, this means:

- Parent node higher on the tree.
- Child node lower on the tree.
- Sibling nodes placed on the same row when possible.
- Branches spread left and right from the parent.

---

## Good Placement

A clean branch usually looks like this:

- One parent above.
- Children below.
- Children aligned on the same horizontal row.
- Enough horizontal space between children.
- The next progression step below the previous one.

This creates short vertical lines and a clear horizontal branch line.

---

## Bad Placement

Avoid placing a child:

- Above its parent.
- On the same row as its parent.
- Too far away from its parent.
- Inside another unrelated branch.
- In a position that makes lines cross several branches.

If a child is placed above or beside its parent, the line system still tries to connect them through the parent/child anchors.

The result can look confusing because the tree is no longer following the expected top-to-bottom flow.

---

## Parent And Child Logic

Node position and parent selection are separate.

The `Position` field controls where the node is drawn.

The `Parent` field controls which node must be unlocked before it.

Changing the position does not change the parent.

Changing the parent does not automatically move the node.

You need both:

- A correct parent relationship.
- A good visual position.

---

## Moving A Node For Better Lines

To clean up a branch:

- Select the node.
- Click `Modify`.
- Use the `Position` field.
- Click `Select`.
- Pick a better empty cell below its parent.
- Confirm.
- Save.

![|150x300](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/node-placement-modify-panel.png)

The position selector only allows empty cells when selecting a new position.

---

## Parent With One Child

For a simple chain, place nodes vertically.

```text
Parent
  |
Child
  |
Child
```

This is the cleanest layout for a straight progression path.

---

## Parent With Several Children

For a branch, place children below the parent on the same row.

```text
        Parent
          |
  +-------+-------+
  |       |       |
Child   Child   Child
```

This matches the way TechTree creates the horizontal branch corridor.

If one child is much lower than the others, the branch line can feel stretched.

If one child is above the parent, the branch becomes hard to read.

---

## Separate Branches

When creating separate progression branches:

- Keep each branch in its own visual area.
- Leave empty columns between unrelated branches.
- Avoid connecting across the whole tree unless it is intentional.
- Put special branches slightly aside from the main vanilla path.

The goal is that a player can understand the route by looking at the lines.

---

## Grid Setting

Use `Grid Setting` when you need more room before placing nodes.

![|280x40](https://raw.githubusercontent.com/Gdkenni/TechTree-Doc/master/images/node-placement-grid-setting-button.png)

You can expand the grid:

- Up.
- Down.
- Left.
- Right.

You can also shrink empty space or reset bounds from current nodes.

Expanding the grid before moving a large branch is safer than forcing nodes into a cramped area.

---

## Update Grid

If nodes are moved near the edge of the current grid bounds, TechTree may show an `Update Grid` action.

Use it to refresh the grid bounds from the current node layout.

This keeps the scrollable tree area correctly sized after layout changes.

---

## Practical Rules

- Place parents above children.
- Place children below the parent.
- Keep sibling nodes on the same row when possible.
- Use horizontal spacing for branches.
- Use vertical spacing for progression depth.
- Avoid crossing lines.
- Save after placement changes.

If the line looks strange, the parent relationship may be correct, but the visual position probably needs to be adjusted.
