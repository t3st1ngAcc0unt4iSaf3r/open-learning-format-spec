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
