# Google AI Studio

> The fastest way to experiment with Gemini models. Test prompts, explore capabilities, export code.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| URL | [aistudio.google.com](https://aistudio.google.com) |
| Cost | Free tier available |
| API | Gemini Developer API |
| Purpose | Prototyping & experimentation |

---

## What It Is

AI Studio is Google's **web-based playground** for Gemini models. Think of it as a sandbox where you can:

- Test prompts interactively
- Compare model outputs
- Experiment with parameters
- Export working code
- Access grounding with Google Search

---

## When to Use

✅ **Use AI Studio for:**
- Testing new prompts
- Exploring model capabilities
- Learning the API
- Quick prototypes
- Comparing models side-by-side
- Demoing to stakeholders

❌ **Don't use for:**
- Production deployment
- Building apps (use Firebase Studio)
- Enterprise requirements (use Vertex AI)
- Autonomous coding (use Antigravity)

---

## Key Features

### 1. Prompt Gallery

Pre-built prompts to learn from:
- Text generation
- Chat applications
- Code generation
- Multimodal examples

### 2. Model Comparison

Test the same prompt across different models:
- Gemini 3 Pro vs Flash
- Different parameter settings
- Side-by-side output comparison

### 3. Parameter Tuning

Experiment with:
- **Temperature**: Creativity (0-2)
- **Top-P**: Nucleus sampling
- **Top-K**: Token selection
- **Max tokens**: Response length
- **Stop sequences**: Output termination

### 4. System Instructions

Define model behavior:
```
You are a helpful coding assistant.
Always explain your code.
Use Python unless asked otherwise.
```

### 5. Grounding with Google Search

Enable real-time web information:
- Toggle in settings
- Responses include citations
- Reduces hallucinations

### 6. Code Export

One-click export to:
- Python
- JavaScript/Node.js
- cURL
- Kotlin
- Swift

---

## Interface Overview

```
┌─────────────────────────────────────────────────────────────────┐
│  Google AI Studio                                    [Settings] │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────────────────────────┐  │
│  │   Model         │  │                                     │  │
│  │   ─────────     │  │         PROMPT AREA                 │  │
│  │   gemini-3-flash│  │                                     │  │
│  │                 │  │   Type your prompt here...          │  │
│  │   Parameters    │  │                                     │  │
│  │   ──────────    │  │                                     │  │
│  │   Temp: 0.7     │  ├─────────────────────────────────────┤  │
│  │   Top-P: 0.95   │  │                                     │  │
│  │   Max: 8192     │  │         RESPONSE AREA               │  │
│  │                 │  │                                     │  │
│  │   Tools         │  │   Model output appears here...      │  │
│  │   ─────         │  │                                     │  │
│  │   ☑ Search      │  │                                     │  │
│  │   ☐ Code Exec   │  │                                     │  │
│  │                 │  │                                     │  │
│  └─────────────────┘  └─────────────────────────────────────┘  │
│                                                                 │
│                              [Run] [Get Code] [Save]            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Workflow

### Basic Testing

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Select a model (e.g., `gemini-3-flash`)
3. Enter your prompt
4. Click **Run**
5. Iterate on prompt and parameters

### Export to Code

1. Get your prompt working in AI Studio
2. Click **Get Code**
3. Select language (Python, JS, etc.)
4. Copy generated code
5. Add your API key
6. Run in your environment

### Example Exported Code (Python)

```python
import google.generativeai as genai

genai.configure(api_key="YOUR_API_KEY")

model = genai.GenerativeModel(
    model_name="gemini-3-flash",
    generation_config={
        "temperature": 0.7,
        "top_p": 0.95,
        "max_output_tokens": 8192,
    },
    system_instruction="You are a helpful assistant."
)

response = model.generate_content("Your prompt here")
print(response.text)
```

---

## Rate Limits (Free Tier)

| Model | Requests/min | Tokens/min |
|-------|-------------|------------|
| Gemini 3 Flash | 15 | 1,000,000 |
| Gemini 2.5 Flash | 15 | 1,000,000 |
| Gemini 3 Pro | 2 | 32,000 |

*Paid API keys have higher limits*

---

## Tips & Tricks

### 1. Use Chat Mode for Context

For multi-turn conversations, use the Chat interface rather than single prompts.

### 2. Save Prompts

Save working prompts to your library for later use.

### 3. Compare Models

Open multiple tabs to compare outputs side-by-side.

### 4. Enable Grounding for Facts

When accuracy matters, enable Google Search grounding.

### 5. Start Simple

Begin with default parameters, then tune as needed.

---

## Limitations

- **No deployment** — Export code, deploy elsewhere
- **No persistence** — Sessions don't save automatically
- **Rate limited** — Free tier has quotas
- **No fine-tuning** — Use Vertex AI for that
- **Single user** — No team collaboration features

---

## From AI Studio to Production

```
AI Studio (prototype)
        │
        ▼
┌───────────────────┐
│ Does it work?     │
│                   │
│ YES → Export code │
│ NO  → Iterate     │
└───────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ What's next?                          │
│                                       │
│ • Simple app → Firebase AI Logic SDK  │
│ • Full app   → Firebase Studio        │
│ • Enterprise → Vertex AI              │
└───────────────────────────────────────┘
```

---

## Related

- [Vertex AI](vertex-ai.md) — Enterprise platform
- [Firebase AI Logic](firebase-ai-logic.md) — Mobile/web SDKs
- [Gemini 3 Flash](../models/gemini-3-flash.md) — Recommended model
