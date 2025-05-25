# OLF Shape Element Parameters

This document summarizes the **required parameters** for OLF shape elements: `polygon`, `ellipse`, and `quadrant`. Note that **opacity parameters** are required to control transparency in all shapes. Additionally, element IDs must be valid UUID v4 strings in the 8-4-4-4-12 hex-hyphen pattern; the Viewer will ignore any element whose ID deviates from this pattern (e.g., "this-is-a-custom-name").

---

## 1. Polygon

A general-purpose shape defined by a list of vertices.

| Parameter        | Type   | Description                                                       |
| ---------------- | ------ | ----------------------------------------------------------------- |
| `id`             | String | Unique identifier for the polygon element.                        |
| `points`         | String | Space-separated list of `x,y` coordinate pairs defining vertices. |
| `matrix`         | String | 9 comma-separated values for the 3×3 transformation matrix.       |
| `fill`           | String | Fill color in `"#RRGGBB"` format or `"none"` for no fill.         |
| `fill-opacity`   | Number | Required. Opacity of the fill (0.0–1.0).                          |
| `stroke`         | String | Stroke (border) color in `"#RRGGBB"` format.                      |
| `stroke-width`   | Number | Stroke thickness in pixels.                                       |
| `stroke-opacity` | Number | Required. Opacity of the stroke (0.0–1.0).                        |

---

## 2. Ellipse

A specialized element for true circles or ovals, using bounding box or radii.

| Parameter                 | Type    | Description                                                                        |
| ------------------------- | ------- | ---------------------------------------------------------------------------------- |
| `id`                      | String  | Unique identifier for the ellipse element.                                         |
| `x`                       | Number  | X-coordinate of the top-left corner of the bounding box.                           |
| `y`                       | Number  | Y-coordinate of the top-left corner of the bounding box.                           |
| `width`                   | Number  | Width of the bounding box (2× radius\_x).                                          |
| `height`                  | Number  | Height of the bounding box (2× radius\_y).                                         |
| `matrix`                  | String  | 9 comma-separated values for the 3×3 transformation matrix.                        |
| `fill`                    | String  | Fill color in `#RRGGBB` format or `none`.                                          |
| `fill-opacity`            | Number  | Required. Opacity of the fill (0.0–1.0).                                           |
| `stroke`                  | String  | Stroke color in `#RRGGBB` format.                                                  |
| `stroke-width`            | Number  | Stroke thickness in pixels.                                                        |
| `stroke-opacity`          | Number  | Required. Opacity of the stroke (0.0–1.0).                                         |
| `angle-start`             | Number  | Start angle of the arc (in degrees).                                               |
| `angle-end`               | Number  | End angle of the arc (in degrees).                                                 |
| `is-pie`                  | Boolean | Required. `true` to draw a pie slice (connect to center), `false` for an open arc. |
| `show-length-measurement` | Boolean | Optional. Toggle display of length measurement.                                    |
| `show-angle-measurement`  | Boolean | Optional. Toggle display of angle measurement.                                     |

**Notes:**

* Angle parameters define full circles when spanning 0 to 360.
* Use `is-pie` to toggle between pie slices (`true`, connects to center) or open arcs (`false`, only the curved outline).

## 3. Quadrant

A custom polygon-like shape for a quarter-circle or specialized segment.

| Parameter        | Type   | Description                                                   |
| ---------------- | ------ | ------------------------------------------------------------- |
| `id`             | String | Unique identifier for the quadrant element.                   |
| `points`         | String | Space-separated list of `x,y` coordinate pairs for the shape. |
| `matrix`         | String | 9 comma-separated values for the 3×3 transformation matrix.   |
| `fill`           | String | Fill color in `"#RRGGBB"` or `"none"`.                        |
| `fill-opacity`   | Number | Required. Opacity of the fill (0.0–1.0).                      |
| `stroke`         | String | Stroke color in `"#RRGGBB"` format.                           |
| `stroke-width`   | Number | Stroke thickness in pixels.                                   |
| `stroke-opacity` | Number | Required. Opacity of the stroke (0.0–1.0).                    |

---

All element types share common styling keys (`fill`, `fill-opacity`, `stroke`, `stroke-width`, `stroke-opacity`) and transform (`matrix`). Ensure **opacity parameters** are always explicitly set to achieve the desired transparency or visibility.
