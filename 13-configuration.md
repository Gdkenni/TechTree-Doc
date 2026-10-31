# Configuration

This page summarizes the **TechTree** config options.

All options are inside the `Settings` object.

---

## Wipe Player Data At Wipe

```json
"Wipe Player Data at Wipe": true
```

Deletes TechTree player unlock data on a new save.

Use this for seasonal progression resets.

---

## Time For Unlock Node

```json
"Time For Unlock Node": 1.0
```

Unlock progress duration in seconds.

It is one duration per unlock, even when several nodes are bought at once.

Players with `techtree.unlock.instant` skip this timer when permissions are enabled.

Prototype unlocks are always immediate.

---

## Selected Theme

```json
"Selected Theme": "Default"
```

Name of the active theme loaded from `Themes.json`.

The theme modal updates this value when you click `APPLY & SAVE`.

If the theme does not exist, TechTree uses `Default`, or the first theme, and prints a warning.

---

## Use Permissions

```json
"Use Permissions ?": false
```

Enables TechTree permission checks.

This includes **global permissions**, **branch permissions** and subcategory permission conditions.

---

## Use Economics

```json
"Use Economics ?": false
```

Present in the config, but not used.

`Economics` rewards work whatever this value is.

Node prices always use item currency.

---

## Replace Tree Vanilla

```json
"Replace tree vanilla ? Open with [R] if false": true
```

When `true`, opening a workbench opens TechTree instead of the vanilla tech tree.

When `false`, players look at a workbench and press `R` when `[R] OPEN` is shown.

---

## Economy Model

```json
"Economy model (Legacy / Blueprints)": "Blueprints"
```

`Blueprints` or `Legacy`. See **Pricing And Economy**.

It can also be changed in game, in the rarity prices panel.

---

## Price By Rarity

```json
"Price by rarity": {
  "None": 120,
  "Common": 20,
  "Uncommon": 40,
  "Rare": 100,
  "VeryRare": 300
}
```

Price of the nodes linked to a rarity.

It can also be changed in game, in the rarity prices panel.

---

## Good To Know

- If the config file is invalid, TechTree uses the default config and prints an error.
- The config is saved again at every load, so new options are added automatically.
