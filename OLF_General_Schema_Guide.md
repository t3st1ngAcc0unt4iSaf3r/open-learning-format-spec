# 📦 General Schema of an OLF File

This guide outlines the core structure and required parameters for creating valid Open Learning Format (OLF) files, including handling multiple pages and custom backgrounds.

---

## 🧾 OLF File Overview

An OLF file is a **ZIP archive** with the `.olf` extension. It contains at minimum:

```
/content.json               # Required — defines the visual and interactive structure
/images/                    # Optional — for embedded images
/content-polls.json         # Optional — for interactive polls
/widgets/                   # Optional — for external content
```

---

## ✅ Required Top-Level JSON Structure

```json
{
  "olf": {
    "width": 1920,
    "height": 1080,
    "viewbox": "0,0,1920,1080",
    "meta": { ... },
    "pageset": [
      { "page": { ... } }
    ],
    "additional": [],
    "links": [],
    "groups": []
  }
}
```

### 🔑 Required Fields

| Field        | Description                              |
|--------------|------------------------------------------|
| `width`      | Canvas width (e.g., `1920`)              |
| `height`     | Canvas height (e.g., `1080`)             |
| `viewbox`    | Coordinate space for rendering           |
| `meta`       | Metadata block with UUID and timestamps  |
| `pageset`    | List of pages to render                  |
| `additional` | Optional extensions (default empty)      |
| `links`      | Optional links (default empty)           |
| `groups`     | Optional grouping (default empty)        |

---

## 🗂️ Metadata Block Example

```json
"meta": {
  "id": "UUID",
  "create-platform": "Whiteboard for Windows - Sparrow",
  "create-by-library": "Viewsonic Open Learning Format library",
  "create-time": "5/23/2025 10:00:00 AM",
  "modify-time": "5/23/2025 10:00:00 AM",
  "create-library-version": "0.0.1.50",
  "create-version": "3.0.0.100 [64 bits]",
  "modify-version": "3.0.0.100 [64 bits]",
  "modify-platform": "Whiteboard for Windows - Sparrow",
  "description": "Lesson file"
}
```

---

## 📄 Declaring Multiple Pages

Each page in the `pageset` is wrapped in an object with a `page` key:

```json
"pageset": [
  { "page": { ... } },
  { "page": { ... } },
  { "page": { ... } }
]
```

Each page must have:

- Unique `id`
- Standard identity `matrix`
- Matching `viewbox`
- `is-hidden`: usually `false`
- Arrays for `elements` and `backgrounds`

---

## 🎨 Applying Custom Backgrounds

A `backgrounds` array defines the background for each page.

### 🎨 Solid Color Background Example

```json
"backgrounds": [
  {
    "background": {
      "id": "UUID",
      "type": "color",
      "fill": "#E0F7FA",
      "opacity": 1.0
    }
  }
]
```

### 🖼️ Background Image (less common)

```json
"backgrounds": [
  {
    "background": {
      "id": "UUID",
      "type": "image",
      "source": "images/bg.jpg",
      "mime-type": "image/jpeg",
      "x": 0,
      "y": 0,
      "width": 1920,
      "height": 1080,
      "matrix": "1,0,0,0,1,0,0,0,1"
    }
  }
]
```

---

## ✅ Summary Checklist

- [x] Use required top-level fields (`width`, `height`, `meta`, `pageset`)
- [x] Ensure all `UUID`s are unique
- [x] Each `page` must define `elements` and `backgrounds`
- [x] Use `viewbox: "0,0,1920,1080"` for consistent layout
- [x] Zip contents and rename `.zip` to `.olf`
