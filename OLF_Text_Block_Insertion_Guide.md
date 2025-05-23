# 📝 Inserting a Text Block in an OLF File

## 🔧 Element Type: `textarea`

Text content in an OLF file is inserted using the `textarea` element inside a page's `elements` array within `content.json`. This supports rich text formatting through **RTF strings** and a `text-blocks-container` for precise styling and layout control.

---

## ✅ Basic JSON Structure

```json
{
  "textarea": {
    "id": "UUID",
    "x": 100,
    "y": 150,
    "width": 800,
    "height": 200,
    "custom-data": "{\\rtf1\\ansi\\deff0{\\fonttbl{\\f0\\fnil\\fcharset0 Segoe UI;}}\\viewkind4\\uc1\\pard\\f0\\fs40 Hello World!\\par}",
    "custom-data-tag": "RTFxamlStr_UWP",
    "matrix": "1,0,0,0,1,0,0,0,1",
    "text-blocks-container": [
      {
        "paragraph": {
          "id": "UUID",
          "font-size": 40,
          "text-align": "left",
          "text-list-container": [
            {
              "text": {
                "id": "UUID",
                "text": "Hello World!",
                "font-family": "Segoe UI",
                "font-size": 40,
                "fill": "#000000",
                "background": "#FFFFFF",
                "font-style": "normal",
                "font-stretch": "normal",
                "font-weight": "normal",
                "text-decoration": "none",
                "baseline-align": "baseline",
                "fill-opacity": 1.0,
                "background-opacity": 1.0
              }
            }
          ]
        }
      }
    ]
  }
}
```

---

## 📍 Positioning the Text

| Field     | Purpose                          |
|-----------|----------------------------------|
| `x`, `y`  | Top-left corner of the text box  |
| `width`   | Width of the text area           |
| `height`  | Height of the text area          |
| `matrix`  | Transformation matrix (identity by default) |

Text is rendered within the rectangular area defined by `(x, y, width, height)`.

---

## 🎨 Controlling Font Size, Typeface, and Color

| Property         | Description                                      |
|------------------|--------------------------------------------------|
| `font-family`    | Font name (e.g., `"Segoe UI"`, `"Arial"`)        |
| `font-size`      | Size in points (e.g., `40`)                       |
| `fill`           | Font color (hex format, e.g., `"#FF0000"`)       |
| `background`     | Background color (hex format)                    |
| `fill-opacity`   | Font transparency (`1.0` = opaque)               |
| `background-opacity` | Background transparency                     |
| `font-style`     | `"normal"` or `"italic"`                         |
| `font-weight`    | `"normal"` or `"bold"`                           |
| `text-decoration`| `"none"`, `"underline"`, `"line-through"`        |

---

## 🧾 Using `custom-data`

The `custom-data` field holds the **RTF representation** of the text, matching what is rendered from the `text-blocks-container`.

Example:

```rtf
"{\rtf1\ansi\deff0{\fonttbl{\f0\fnil\fcharset0 Segoe UI;}}\viewkind4\uc1\pard\f0\fs40 Hello World!\par}"
```

---

## ✅ Summary Checklist

- [x] Use a `textarea` block inside `elements`.
- [x] Define `x`, `y`, `width`, `height` to place the text.
- [x] Use `text-blocks-container` to control styling.
- [x] Ensure the `custom-data` field contains matching RTF text.
- [x] Use consistent UUIDs and identity `matrix`.
