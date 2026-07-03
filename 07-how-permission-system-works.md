# How Permission System Works

TechTree has permission checks controlled by this config option:

```json
"Use Permissions ?": true
```

When this option is `false`, TechTree permission checks are not enforced.

When this option is `true`, TechTree checks **global permissions** and **branch permissions**.

---

## When Use Permissions Is False

- Players can open TechTree without `techtree.use`.
- `techtree.unlock.free` does not apply.
- `techtree.unlock.instant` does not apply.
- Branch permissions are not enforced.

This is the simplest setup for public progression.

---

## When Use Permissions Is True

- Players need `techtree.use` to open TechTree.
- Players with `techtree.unlock.free` unlock nodes for free.
- Players with `techtree.unlock.instant` skip the unlock timer.
- Branch permissions are enforced when a node has a custom permission set.

Use this setup if you want restricted access, VIP unlock benefits, or branch restrictions.

---

## Global Permissions

### `techtree.use`

Allows the player to open and use TechTree when permissions are enabled.

### `techtree.unlock.free`

Makes node unlock costs free for players with this permission.

### `techtree.unlock.instant`

Removes the unlock timer for players with this permission.

---

## Common Mistakes

### Players Cannot Open TechTree

**Cause:**

- `Use Permissions ?` is `true`.
- Players do not have `techtree.use`.

**Fix:**

- Grant `techtree.use` to the default group or to the groups allowed to use TechTree.

### VIP Free Unlock Does Not Work

**Cause:**

- `Use Permissions ?` is `false`.

**Fix:**

- Enable `Use Permissions ?`.
- Grant `techtree.use`.
- Grant `techtree.unlock.free` to the correct group.
