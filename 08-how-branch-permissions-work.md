# How Branch Permissions Work

**Branch permissions** allow you to lock a node or an entire branch behind a custom permission.

They are useful for VIP paths, professions, server ranks, quest progression, or special unlock routes.

---

## Requirement

Branch permissions require:

```json
"Use Permissions ?": true
```

If `Use Permissions ?` is `false`, branch permissions are not enforced.

---

## What A Branch Permission Is

A branch permission is a custom permission typed directly on a node in the editor.

Example:

```text
vip.weapons
```

If a player does not have the permission, the node and its child branch are locked for that player.

---

## Difference From Global Permissions

Branch permissions are not the same thing as:

- `techtree.use`.
- `techtree.unlock.free`.
- `techtree.unlock.instant`.

Global permissions control access and special unlock behavior.

Branch permissions control specific nodes or branches.

Both require `Use Permissions ?` to be enabled.

---

## Recommended Workflow

- Enable `Use Permissions ?` in the config.
- Open the **TechTree editor**.
- Select the first node of the restricted branch.
- Click `Modify`.
- Enter your custom permission in the `Permission` field.
- Click `Confirm`.
- Save the editor session.
- Grant the permission to the correct players or groups.

---

## Permission Placement

**Permission on a root node:**

- Locks the whole branch.

**Permission on a child node:**

- Locks that node and the child branch after it.

**No permission:**

- The node is public unless it inherits a permission from a parent branch.

---

## Good Examples

```text
vip.weapons
profession.electrician
progression.tier2
donator.crafting
```

---

## Common Mistake

Typing a permission in the node editor is not enough.

You must also grant that permission with your permission manager.

If the permission is never granted, the branch stays locked for everyone.
