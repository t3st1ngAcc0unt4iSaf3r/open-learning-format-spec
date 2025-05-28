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


---

# 📑 Understanding `custom-data` vs `text-blocks-container` in OLF `textarea` Elements

This section explains the critical difference between the `custom-data` and `text` parameters within `textarea` elements in `content.json` files of Open Learning Format (OLF) archives.

---

## 🔍 Definitions

### 1. `custom-data`
- **Type**: A raw RTF (Rich Text Format) string.
- **Purpose**: Provides a complete text block with formatting embedded in RTF syntax.
- **Usage**: Prioritized by many ViewSonic viewers for rendering performance and backward compatibility.
- **Limitation**: Not human-readable and harder to manipulate programmatically.

### 2. `text-blocks-container`
- **Type**: A structured JSON array.
- **Purpose**: Describes paragraphs and styled text segments in a clean and editable format.
- **Usage**: Used by internal tooling, editing features, and semantic processors.
- **Limitation**: May be ignored by viewers if `custom-data` is present.

---

## ⚖️ Comparison Table

| Feature                  | `custom-data` (RTF)               | `text-blocks-container` (JSON)   |
|--------------------------|-----------------------------------|----------------------------------|
| Format                   | RTF string                        | JSON structure                   |
| Readability              | ❌ Not human-readable             | ✅ Human-readable                 |
| Granular Styling         | Moderate (RTF tags)               | High (per-word formatting)       |
| Rendering Priority       | ✅ Often rendered first           | ❗ May be ignored                 |
| Ease of Localization     | ❌ Harder                         | ✅ Easier                        |
| Required for OLF         | ✅ Recommended                    | ✅ Required                      |

---

## ✅ Best Practice

**Always update both `custom-data` and `text-blocks-container` fields** to ensure consistent behavior across ViewSonic applications.

- Ensure the `custom-data` RTF reflects the same content as `text-blocks-container`.
- Keep text consistent in translations, updates, and content patching workflows.

---

## ⚠️ Special Note for Translations

> When translating OLF content, it is essential to **update both `custom-data` and `text-blocks-container`**. Failing to do so may cause the viewer to display the original (untranslated) language from `custom-data`.

---

## 🧪 Example

### Sample `textarea` structure:
```json
{
  "textarea": {
    "custom-data": "{\rtf1\ansi\deff0 {\fonttbl {\f0 Segoe UI;}}\f0\fs40 Hola mundo}",
    "custom-data-tag": "RTFxamlStr_UWP",
    "text-blocks-container": [
      {
        "paragraph": {
          "text-align": "center",
          "text-list-container": [
            {
              "text": {
                "text": "Hola mundo",
                "font-family": "Segoe UI",
                "font-size": 53.0,
                "fill": "#FF000000"
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


# 📊 Inserting Polls in an OLF File

This guide explains how to create and integrate interactive poll questions in Open Learning Format (OLF) files using `content-polls.json`.

---

## 🗂️ File Structure Overview

An OLF file with polls typically includes:

```
/content.json
/content-polls.json
```

- `content.json` handles page layout and visual cues.
- `content-polls.json` defines poll logic and question structures.

---

## 🧩 Basic `content-polls.json` Structure

```json
{
  "polls-pool": {
    "id": "UUID",
    "version": "1.0",
    "polls": [ ... poll objects ... ]
  }
}
```

---

## ✅ Poll Types and Example Structures

### 🅰️ Multiple Choice

```json
{
  "multiple-choice": {
    "id": "UUID",
    "is-finished": false,
    "question": "What is the capital of France?",
    "instruction": "Choose one:",
    "time-limit": "00:30",
    "selection-item-container": [
      { "selection-item": { "id": "A", "is-answer": true, "text": "Paris" }},
      { "selection-item": { "id": "B", "is-answer": false, "text": "Berlin" }}
    ]
  }
}
```

### ✅ True or False

```json
{
  "true-or-false": {
    "id": "UUID",
    "is-finished": false,
    "default-answer": 1,
    "question": "The sky is blue.",
    "instruction": "Select True or False.",
    "time-limit": "00:20",
    "first-label": "TRUE",
    "last-label": "FALSE"
  }
}
```

---

## 📌 Poll Metadata Fields

| Field                | Description                                                  |
|----------------------|--------------------------------------------------------------|
| `id`                 | Unique identifier                                            |
| `is-finished`        | Whether responses are locked                                 |
| `question`           | Text of the poll question                                    |
| `instruction`        | Optional instruction for users                               |
| `time-limit`         | Countdown timer in `"MM:SS"` format                          |
| `selection-item-container` | Array of answer choices                                |

---

## 🔗 Linking Polls to Pages

Polls are not directly rendered by layout engines. Use `textarea` elements in `content.json` to:

- Display the question text visually.
- Act as a cue for users to answer the poll (handled in backend/UI).

---

## ✅ Summary Checklist

- [x] Include `content-polls.json` in the OLF archive.
- [x] Use valid UUIDs for each poll and choice.
- [x] Set `is-finished: false` to allow interaction.
- [x] Specify a `time-limit` for timed questions.
- [x] Reference poll context via visual cues in `content.json`.


# 🧩 Inserting Flip Cards in an OLF File

This guide explains how to create and place interactive flashcards (flip cards) in Open Learning Format (OLF) files using the `flashcard` element in `content.json`.

---

## 🧠 What is a Flip Card?

A flip card displays a question or prompt on one side, and flips to show an answer or explanation on the reverse. It is ideal for language learning, terminology, and interactive quizzes.

---

## ✅ Basic Flip Card JSON Structure

```json
{
  "flashcard": {
    "id": "UUID",
    "category": "Tool_FLASH_CARD",
    "question-title": "Front Label",
    "question": "What is the capital of France?",
    "answer": "Paris",
    "explanation": "Paris is the capital and most populous city of France.",
    "question-image": "",
    "question-image-display-mode": "fit",
    "answer-image": "",
    "answer-image-display-mode": "fit",
    "x": 100,
    "y": 100,
    "width": 400,
    "height": 200,
    "matrix": "1,0,0,0,1,0,0,0,1"
  }
}
```

---

## 🔑 Field Descriptions

| Field                    | Description                                                     |
|--------------------------|-----------------------------------------------------------------|
| `id`                     | Unique UUID for this card                                       |
| `category`               | Always set to `"Tool_FLASH_CARD"`                               |
| `question-title`         | Optional label for the front (e.g., `"Question"`)               |
| `question`               | Text shown on the front of the card                             |
| `answer`                 | Title of answer text shown on the back (optional)               |
| `explanation`            | Full text centered on answer body on the back                   |
| `question-image`         | Optional image URL or path for the front                        |
| `answer-image`           | Optional image URL or path for the back                         |
| `x`, `y`                 | Position of the card on canvas (top-left corner)                |
| `width`, `height`        | Size of the card                                                |
| `matrix`                 | Transformation matrix (typically identity)                      |

---

## 📍 Positioning Flip Cards

Flip cards are placed using `x` and `y` fields. Layouts such as a **3x3 grid** can be generated using simple loops.

### Example: Grid Positioning (Python Logic)

```python
rows, cols = 3, 3
card_width, card_height = 400, 200
margin_x, margin_y = 100, 100
spacing_x, spacing_y = 100, 100

for idx in range(rows * cols):
    row = idx // cols
    col = idx % cols
    x = margin_x + col * (card_width + spacing_x)
    y = margin_y + row * (card_height + spacing_y)
```

---

## 📦 File Packaging

Make sure your OLF archive contains:

```
/content.json
```

- Place all flip cards in the `elements` array of one or more pages.
- Include any referenced images in an `/images/` folder if used.

---

## ✅ Summary Checklist

- [x] Use the `flashcard` element with unique UUIDs
- [x] Define `x`, `y`, `width`, and `height` for placement
- [x] Provide `question` and `answer` text
- [x] Use `"Tool_FLASH_CARD"` as the `category`
- [x] Include images optionally, or leave blank


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


---


# Important


# 📘 OLF Required Parameters Summary

This document summarizes the **required** parameters and structure for a valid `content.json` in an Open Learning Format (OLF) file. Note that if any of these are missing, the OLF file will not open.

---

## 🧱 Top-Level Structure

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

---

## 🧾 Metadata (`meta`) Block

Required fields inside `meta`:

- `id`: Unique UUID
- `create-platform`
- `create-by-library`
- `create-time`
- `modify-time`
- `create-library-version`
- `create-version`
- `modify-version`
- `modify-platform`

---

## 📄 Page Structure

Each item in `pageset` must be wrapped in `"page"`:

```json
{
  "page": {
    "id": "uuid",
    "matrix": "1,0,0,0,1,0,0,0,1",
    "viewbox": "0,0,1920,1080",
    "is-hidden": false,
    "elements": [ ... ],
    "backgrounds": [ ... ]
  }
}
```

---

## 🧩 Element Requirements

### Polygon

```json
"polygon": {
  "id": "uuid",
  "points": "x1,y1 x2,y2 x3,y3 x4,y4",
  "fill": "#FFFFFF",
  "stroke": "#000000",
  "stroke-width": 2,
  "matrix": "1,0,0,0,1,0,0,0,1"
}
```

- `points`: Required, defines absolute position on canvas
- `matrix`: Typically identity
- `x`, `y`, `width`, `height`: Optional (informational only)

---

## 🎨 Background Block

At least one background should be defined:

```json
{
  "background": {
    "id": "uuid",
    "type": "color",
    "fill": "#FFFFFF",
    "opacity": 1.0
  }
}
```

---

## ✅ Packaging Notes

- All files must be placed in the root of the ZIP archive.
- Always verify that all JSON files inside the ZIP file are readable as text. 
- File must be renamed from `.zip` to `.olf`.



