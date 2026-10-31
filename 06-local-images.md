# Local Images

**TechTree** supports local node images on **Oxide** and **Carbon**.

This allows admins to use image files stored directly on the server instead of hosting every custom icon on an external website.

---

## Folder

Place local images in the `Images` folder of the TechTree data folder:

```text
carbon/data/TechTree/Images/
oxide/data/TechTree/Images/
```

Use the path that matches your framework.

You can organize images directly in this folder or inside subfolders.

**TechTree supports folder navigation** inside the local image picker.

---

## Supported Formats

- `png`.
- `jpg`.
- `jpeg`.

TechTree stores the **relative path from the Images folder**, without the file extension.

Example:

```text
Images/Weapons/rifle_icon.png
```

The stored local image value is:

```text
Weapons/rifle_icon
```

If the file is directly inside `Images/`, the value is only the file name without extension.

**Important:** do not use two files with the same relative path and different extensions.

Example:

```text
Weapons/rifle_icon.png
Weapons/rifle_icon.jpg
```

Only the first one found is used, and a warning is printed in the server console.

---

## How To Use

- Put the image file in `Images/` or one of its subfolders.
- Open the **TechTree editor**.
- Select a node and click `Modify`.
- In the `General` tab, set `Image` to `Local`.
- Click the search button to open the local image picker.
- Navigate into folders if needed.
- Select the image.
- Click `Confirm`, then `SAVE`.

You can also type the stored value directly in the field.

---

## Local Image Picker

- `Search`: filters images by name.
- The path line shows the current folder, for example `Images/Weapons/`.
- `<- Up` goes back to the parent folder.
- Folder tiles open the folder.
- Image tiles select the image.
- The red `X` closes the picker.

---

## Reload Button

The local image picker has a green **reload** button.

Reload updates the image database from the files currently present in `Images/` and its subfolders.

It shows how many images were added, updated and removed.

This lets you add or replace local images without reloading the whole plugin.

---

## Important Notes

- On **Carbon**, local images use Carbon's image database.
- On **Oxide**, local images require the **ImageLibrary** plugin.
- This is not an in-game upload system.
- Files must be added to the server folder manually.
- If a selected image is deleted, moved, or renamed, the node no longer displays it until you select the new path.
- Local images can be used on vanilla nodes and custom nodes.
