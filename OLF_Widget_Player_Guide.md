# 🌐 Inserting a Widget-Player in an OLF File

This guide explains how to embed external web content or public images in Open Learning Format (OLF) files using the `widget-player` element in `content.json`.

---

## 🧩 Element Type: `widget-player`

The `widget-player` element allows you to embed a URL (such as an image, webpage, or video player) directly into a page layout.

---

## ✅ Basic JSON Structure

```json
{
  "widget-player": {
    "id": "UUID",
    "x": 100,
    "y": 100,
    "width": 800,
    "height": 600,
    "source": "https://example.com/image.jpg",
    "category": "Tool_WEB_WIDGET",
    "matrix": "1,0,0,0,1,0,0,0,1"
  }
}
```

---

## 📍 Positioning and Size

| Property | Description                                                  |
|----------|--------------------------------------------------------------|
| `x`, `y` | Top-left corner coordinates on the canvas (absolute)         |
| `width`  | Width of the widget in pixels                                |
| `height` | Height of the widget in pixels                               |

The widget is drawn on a 1920x1080 canvas using absolute positioning.

---

## 🌐 Source URL

- `source` must be a **valid, publicly accessible URL**.
- Can be used to embed:
  - Static images
  - Public videos
  - Online tools and web widgets

Example:

```json
"source": "https://upload.wikimedia.org/wikipedia/commons/a/ae/Mona_Lisa.jpg"
```

---

## 📌 Field Descriptions

| Field        | Description                                |
|--------------|--------------------------------------------|
| `id`         | Unique UUID for the widget                 |
| `source`     | The full URL of the content to embed       |
| `category`   | Must be `"Tool_WEB_WIDGET"`                |
| `matrix`     | Typically an identity matrix               |

---

## ✅ Summary Checklist

- [x] Use a `widget-player` block in the `elements` array.
- [x] Ensure the `source` URL is publicly accessible and hotlink-friendly.
- [x] Set position and size using `x`, `y`, `width`, and `height`.
- [x] Always include the `"category": "Tool_WEB_WIDGET"` field.
