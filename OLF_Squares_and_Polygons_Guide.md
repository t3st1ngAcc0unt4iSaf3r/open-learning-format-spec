# 📐 Creating Squares and Polygons in OLF Files

This guide explains how to create and position **square** and **polygon** elements in an `.olf` file—a ZIP archive containing a `content.json` layout definition.

---

## 🔹 General Polygon Structure

Polygons in OLF are defined in the `elements` array of a `page` object in `content.json`. Each polygon is described using **absolute coordinates** in the `points` field.

### ✅ Basic JSON Template

```json
{
  "polygon": {
    "id": "UUID",
    "x": 0.0,
    "y": 0.0,
    "width": 100,
    "height": 100,
    "matrix": "1,0,0,0,1,0,0,0,1",
    "fill": "#FFFFFF",
    "stroke": "#00FF00",
    "stroke-width": 2,
    "fill-opacity": 1.0,
    "stroke-opacity": 1.0,
    "points": "100,100 200,100 200,200 100,200"
  }
}
```

### 🔑 Key Fields

| Field           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `points`        | Absolute coordinates for each vertex of the polygon, in `"x,y"` format.     |
| `fill`          | Fill color in hex (e.g., `#FFFFFF` for white).                              |
| `stroke`        | Border color (e.g., `#00FF00` for green).                                   |
| `stroke-width`  | Border thickness (e.g., `2`).                                                |
| `fill-opacity`  | Transparency of the fill (1.0 is fully opaque).                             |
| `stroke-opacity`| Transparency of the border (1.0 is fully opaque).                           |
| `matrix`        | Typically an identity matrix for untransformed placement.                   |
| `x`, `y`        | Ignored for placement. Use `points` instead.                                |

---

## 🔳 Example: Creating a Square

To make a **square at (100, 100)** with size 100x100:

```json
"points": "100,100 200,100 200,200 100,200"
```

To place multiple squares side-by-side:

```python
# Python logic
start_x = 100
start_y = 400
square_size = 100
spacing = 10

for i in range(10):
    x0 = start_x + i * (square_size + spacing)
    y0 = start_y
    x1 = x0 + square_size
    y1 = y0 + square_size
    points = f"{x0},{y0} {x1},{y0} {x1},{y1} {x0},{y1}"
```

---

## 🖼️ Page and Canvas Settings

Each OLF file requires a valid `content.json` structure with a `page` definition:

```json
{
  "id": "UUID",
  "matrix": "1,0,0,0,1,0,0,0,1",
  "viewbox": "0,0,1920,1080",
  "is-hidden": false,
  "elements": [ ... polygons here ... ],
  "backgrounds": [{
    "background": {
      "id": "UUID",
      "type": "color",
      "fill": "#FFFFFF",
      "opacity": 1.0
    }
  }]
}
```

---

## 🧾 Metadata Block Example

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
  "modify-platform": "Whiteboard for Windows - Sparrow"
}
```

---

## 📦 Packaging as `.olf`

1. Save your `content.json`.
2. Create a ZIP archive including `content.json`.
3. Rename the `.zip` file to `.olf`.

Example:

```bash
zip -r my_shapes.zip content.json
mv my_shapes.zip my_shapes.olf
```

---

## ✅ Summary Checklist

- [x] Use `polygon` with `points` for placement.
- [x] Define `fill`, `stroke`, and `opacity` values explicitly.
- [x] Ignore `x`, `y`; rely solely on `points`.
- [x] Ensure the JSON is minified before packaging.
- [x] Validate all UUIDs are unique.
