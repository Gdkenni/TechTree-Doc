# Configuration

This page summarizes the main **TechTree** config options.

---

## Wipe Player Data At Wipe

Default:

```json
true
```

Deletes TechTree player unlock data on a new save.

Use this for seasonal progression resets.

---

## Time For Unlock Node

Default:

```json
1.0
```

Unlock progress duration in seconds.

Players with `techtree.unlock.instant` skip this timer when permissions are enabled.

---

## Selected Theme

Default:

```json
"Default"
```

Name of the active theme loaded from `Themes.json`.

---

## Use Permissions

Default:

```json
false
```

Enables TechTree permission checks.

This includes **global permissions** and **branch permissions**.

---

## Use Economics

Default:

```json
false
```

Present in config.

`Economics` is used by the Economics reward type when available.

Node prices still use item currency in the current source.

---

## Replace Tree Vanilla

Default:

```json
true
```

When `true`, TechTree replaces the vanilla tech tree opening behavior.

When `false`, players use the `R` interaction mode near a workbench.
