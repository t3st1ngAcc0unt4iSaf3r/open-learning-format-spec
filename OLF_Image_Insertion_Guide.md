# 🖼️ Inserting Images in an OLF File

This guide explains how to embed and position image elements in an Open Learning Format (OLF) file by defining an `image` element within the `content.json` structure.

---

## 🧩 Element Type: `image`

Images are added to a page using the `image` object inside the `elements` array of a `page`. The image file must be placed in an `/images/` subfolder within the OLF ZIP archive.

---

## ✅ Basic JSON Structure

```json
{
  "image": {
    "id": "UUID",
    "x": 100,
    "y": 150,
    "width": 640,
    "height": 480,
    "mime-type": "image/png",
    "source": "images/example.png",
    "matrix": "1,0,0,0,1,0,0,0,1"
  }
}
```

---

## 📍 Positioning, Width, and Height

| Property | Description                                                  |
|----------|--------------------------------------------------------------|
| `x`, `y` | Coordinates for the top-left corner of the image on canvas   |
| `width`  | Width of the image in pixels (displayed width)               |
| `height` | Height of the image in pixels (displayed height)             |

Positioning defines where the image appears on the 1920x1080 canvas. The origin `(0, 0)` is the top-left corner.

---

## 🗂️ Source and File Requirements

- `source` must match the exact path to the image file in the archive (e.g., `"images/photo.jpg"`).
- Supported formats: `image/png`, `image/jpeg`.
- Ensure images are **added to the ZIP file** in an `images/` folder.

---

## 🧾 Metadata Example for a Page with an Image

```json
"page": {
  "id": "UUID",
  "matrix": "1,0,0,0,1,0,0,0,1",
  "viewbox": "0,0,1920,1080",
  "is-hidden": false,
  "elements": [ ... image elements here ... ],
  "backgrounds": [
    {
      "background": {
        "id": "UUID",
        "type": "color",
        "fill": "#FFFFFF",
        "opacity": 1.0
      }
    }
  ]
}
```

---

## ✅ Summary Checklist

- [x] Place image files in the `images/` folder inside the ZIP archive.
- [x] Set `x`, `y`, `width`, and `height` to define layout and size.
- [x] Use supported image formats (`image/png` or `image/jpeg`).
- [x] Match the `source` field exactly to the image file path.
- [x] Set `matrix` to identity unless transformation is needed.
