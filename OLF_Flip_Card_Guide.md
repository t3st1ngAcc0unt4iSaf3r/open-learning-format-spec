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
| `answer`                 | Optional title for answer shown on the back                     |
| `explanation`            | Main answer text shown on the back                              |
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
