# Themes And Node Styles

**Themes** control the colors of TechTree.

**Node styles** control the shape of the nodes.

---

## Open The Theme Modal

- Switch to `EDIT MODE`.
- Click `Theme` in the right panel.

The modal has four columns: `Theme`, `Palette`, `Styles` and `Preview`.

Clicking outside the modal closes it and discards unapplied changes.

---

## Theme Column

- The top line shows how many themes exist and which one is applied.
- Type a name and click `+` to create a new theme from the selected one.
- Click a theme to edit it.
- `Duplicate` copies a theme.
- The red `X` deletes a theme, after confirmation.

The applied theme is marked with a green bar and a check mark.

Creating, duplicating and deleting themes is saved immediately.

If you delete the applied theme, TechTree falls back to `Default`, or to the first remaining theme.

---

## Palette

Each palette color has a swatch, a name and a hex value.

Type a new hex value to change a color, for example `#728b44`.

Default palette:

- `Red`, `Green`, `Blue`, `White`, `Black`, `Grey`.
- `Orange`, `Charcoal`, `DarkGrey`.
- `DarkPanel`, `DarkPanelAlt`, `DarkGreen`.

Colors cannot be added or removed from the modal.

---

## Node Styles

Choose a style for unlocked nodes and one for locked nodes:

- `UNLOCKED STYLE`.
- `LOCKED STYLE`.

Available styles:

- `Default`: square nodes.
- `Circle`: round nodes.

The `Preview` column shows an unlocked node, an available node and a locked node.

---

## Apply And Save

Click `APPLY & SAVE` to save the theme and apply it to every player immediately.

This button is separate from the editor `SAVE` button.

The applied theme is stored in the config as `Selected Theme`.

All themes are stored in `Themes.json`. See **Data Files**.
