# AWS AIF-C01 Quiz Platform

A free, self-hosted quiz platform for the **AWS Certified AI Practitioner (AIF-C01)** exam.  
302 practice questions · 9 exam topics · 3 practice modes · works fully offline after first load.

---

## 🚀 Live Site

👉 `https://YOUR-USERNAME.github.io/aif-c01-quiz/`

---

## 📁 File Structure

```
aif-c01-quiz/
├── index.html        ← The quiz app (never needs editing)
├── questions.json    ← All questions — edit this to add/update questions
└── README.md
```

> **Key principle:** `index.html` loads `questions.json` at runtime via `fetch()`.  
> To update questions, **only edit `questions.json`** — never touch `index.html`.

---

## 📚 Topics (Exam Blueprint Order)

| # | Topic | Questions |
|---|-------|-----------|
| 1 | 🧠 AI / ML Concepts | 83 |
| 2 | ⚡ Bedrock | 78 |
| 3 | ✍️ Prompt Engineering | 27 |
| 4 | 🤖 Amazon Q | 8 |
| 5 | 🛠️ Managed AI Services | 43 |
| 6 | 🔬 SageMaker | 4 |
| 7 | 🛡️ Responsible AI | 26 |
| 8 | ☁️ Cloud Basics | 13 |
| 9 | 🔒 Security | 20 |

**Valid `topic` values** (must match exactly, case-sensitive):
```
AI / ML Concepts
Bedrock
Prompt Engineering
Amazon Q
Managed AI Services
SageMaker
Responsible AI
Cloud Basics
Security
```

---

## 📝 questions.json Format

The file is a **JSON array** of question objects. Every question must follow this exact structure:

### Standard question (4 options)

```json
[
  {
    "id": 1,
    "question": "A company wants to reduce hallucinations in their generative AI application. Which technique should the AI practitioner use?",
    "options": {
      "A": "Increase the model temperature parameter",
      "B": "Implement Retrieval Augmented Generation (RAG)",
      "C": "Use a smaller foundation model",
      "D": "Decrease the max token limit"
    },
    "answer": "B",
    "topic": "Bedrock"
  },
  {
    "id": 2,
    "question": "Which Amazon SageMaker feature automatically builds, trains, and tunes ML models?",
    "options": {
      "A": "SageMaker Canvas",
      "B": "SageMaker Clarify",
      "C": "SageMaker Autopilot",
      "D": "SageMaker Ground Truth"
    },
    "answer": "C",
    "topic": "SageMaker"
  }
]
```

### 5-option question (optional E)

```json
{
  "id": 50,
  "question": "Which AWS services can be used for natural language processing? (Choose two.)",
  "options": {
    "A": "Amazon Rekognition",
    "B": "Amazon Comprehend",
    "C": "Amazon Polly",
    "D": "Amazon Bedrock",
    "E": "Amazon Translate"
  },
  "answer": "B",
  "topic": "Managed AI Services"
}
```

---

## Field Reference

| Field | Type | Required | Rules |
|-------|------|----------|-------|
| `id` | number | ✅ | Unique integer. New questions: use max existing id + 1. |
| `question` | string | ✅ | Full question text. No HTML. |
| `options` | object | ✅ | Keys `"A"` `"B"` `"C"` `"D"` required. `"E"` optional. |
| `answer` | string | ✅ | Single letter matching a key in `options` — e.g. `"B"`. |
| `topic` | string | ✅ | Must exactly match one of the 9 valid topic strings above. |

---

## ➕ Adding New Questions

1. Open `questions.json`
2. Scroll to the last `}` before the closing `]`
3. Add a comma after it, then your new question object
4. Save, commit, push → live site updates automatically

```json
  ... existing last question ...
  },         ← add comma here
  {
    "id": 303,
    "question": "Your new question text here?",
    "options": {
      "A": "Option A",
      "B": "Option B",
      "C": "Option C",
      "D": "Option D"
    },
    "answer": "A",
    "topic": "Bedrock"
  }
]            ← closing bracket, no comma
```

---

## ❌ Common Mistakes

```jsonc
// ❌ Wrong topic spelling
"topic": "ML Concepts"          // missing "AI / "
"topic": "bedrock"              // must be "Bedrock"
"topic": "Responsible AI & Security"  // must be "Responsible AI"

// ❌ Trailing comma on last item
  { "id": 303, ... },   // comma before ] will break JSON
]

// ❌ Answer key not in options
"answer": "E"           // only valid if options has an "E" key
```

Validate your JSON at [jsonlint.com](https://jsonlint.com) before pushing.

---

## 🛠️ GitHub Pages Setup

1. Create a **public** repo at [github.com/new](https://github.com/new) named `aif-c01-quiz`
2. Upload `index.html`, `questions.json`, and `README.md` to the repo root
3. Go to **Settings → Pages → Source: Deploy from branch → main / root → Save**
4. Wait ~60 sec → live at `https://YOUR-USERNAME.github.io/aif-c01-quiz/`

---

## ⚠️ Running Locally

`fetch()` is blocked when opening HTML files directly. Use a local server:

```bash
python3 -m http.server 8080
# open http://localhost:8080
```
