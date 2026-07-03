# Local Images

**TechTree** supports local node images on **Oxide** and **Carbon**.

This allows admins to use image files stored directly on the server instead of hosting every custom icon on an external website.

---

## Folder

Place local images here:

```text
oxide/data/TechTree/Images/
```

Use the equivalent plugin data folder path if your server stores plugin data somewhere else.

You can organize images directly in this folder or inside subfolders.

**TechTree supports folder navigation** inside the local image picker.

The picker starts at `Images/` and lets you open folders, go back up, and select images from nested folders.

---

## Supported Formats

- `png`.
- `jpg`.
- `jpeg`.

Use clear and unique image paths.

TechTree stores the **relative path from the Images folder**, without the file extension.

Example:

```text
oxide/data/TechTree/Images/Weapons/rifle_icon.png
```

The stored local image value is:

```text
Weapons/rifle_icon
```

If the file is directly inside `Images/`, the value is only the file name without extension.

Example:

```text
oxide/data/TechTree/Images/my_custom_icon.png
```

Stored value:

```text
my_custom_icon
```

**Important:** do not use two files with the same relative path and different extensions.

Example:

```text
Weapons/rifle_icon.png
Weapons/rifle_icon.jpg
```

Only one of those paths can be used cleanly.

---

## How To Use

- Put the image file in `Images/` or one of its subfolders.
- Open the **TechTree editor**.
- Select a node.
- Click `Modify`.
- Set Image type to `Local`.
- Open the local image picker.
- Navigate into folders if needed.
- Select the image.
- Click `Confirm` and save.

---

## Reload Button

The local image picker has a **reload** button.

Reload updates the image database from the files currently present in `Images/` and its subfolders.

This lets you add or replace local images without reloading the whole plugin.

---

## Important Notes

- Local images are supported on **Oxide** and **Carbon**.
- This is not an in-game upload system.
- Files must be added to the server folder manually.
- If a selected image is deleted, moved, or renamed, the node will no longer display it until you select the new path.
- Local images can be used on vanilla nodes and custom nodes.
