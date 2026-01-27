# Google AI Quick Reference

> One-page cheat sheet. Print it. Pin it. Reference it.

---

## Model Selection Matrix

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           GEMINI MODEL PICKER                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Need deep reasoning?                                                      │
│   ├─► YES → Gemini 3 Pro (+ Deep Think for complex problems)               │
│   └─► NO ↓                                                                  │
│                                                                             │
│   Need speed + quality balance?                                             │
│   ├─► YES → Gemini 3 Flash ⭐ RECOMMENDED DEFAULT                          │
│   └─► NO ↓                                                                  │
│                                                                             │
│   Need maximum throughput?                                                  │
│   ├─► YES → Gemini 2.5 Flash-Lite                                          │
│   └─► NO → Gemini 2.5 Flash                                                │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Model Strings (Copy-Paste Ready)

```python
# Current Production Models (Jan 2026)
GEMINI_3_PRO = "gemini-3-pro"
GEMINI_3_FLASH = "gemini-3-flash"
GEMINI_25_FLASH = "gemini-2.5-flash"
GEMINI_25_FLASH_LITE = "gemini-2.5-flash-lite"

# Media Models
IMAGEN_4 = "imagen-4-generate"
VEO_31 = "veo-3.1-generate-preview"

# Live/Streaming
GEMINI_LIVE = "gemini-2.5-flash-native-audio-preview"
```

---

## Platform Decision

| I want to... | Use this |
|--------------|----------|
| Test a prompt quickly | AI Studio |
| Build a prototype app | Firebase Studio |
| Deploy to production | Vertex AI |
| Add AI to my mobile app | Firebase AI Logic SDK |
| Code with an AI agent | Antigravity / Gemini CLI |
| Build multi-agent systems | ADK |

---

## API Endpoints

```bash
# Gemini Developer API (prototyping, free tier available)
https://generativelanguage.googleapis.com/v1beta/

# Vertex AI API (enterprise, requires GCP)
https://{REGION}-aiplatform.googleapis.com/v1/
```

---

## Quick Code Snippets

### Basic Text Generation (Python)

```python
from google import genai

client = genai.Client(api_key="YOUR_KEY")
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="Explain quantum computing in one paragraph"
)
print(response.text)
```

### With Google Search Grounding

```python
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="What happened in tech news today?",
    config={"tools": [{"google_search": {}}]}
)
```

### Function Calling

```python
tools = [{
    "function_declarations": [{
        "name": "get_weather",
        "description": "Get weather for a location",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {"type": "string"}
            }
        }
    }]
}]

response = client.models.generate_content(
    model="gemini-3-flash",
    contents="What's the weather in Tokyo?",
    config={"tools": tools}
)
```

### Image Generation

```python
response = client.models.generate_images(
    model="imagen-4-generate",
    prompt="A futuristic Tokyo street at night, neon lights, rain"
)
```

### Video Generation

```python
operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="Aerial shot of ocean waves at sunset"
)
# Poll operation.done until complete
```

---

## Pricing Quick Reference (Jan 2026)

| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|----------------------|------------------------|
| Gemini 3 Pro | ~$1.25 | ~$5.00 |
| Gemini 3 Flash | ~$0.075 | ~$0.30 |
| Gemini 2.5 Flash-Lite | ~$0.02 | ~$0.08 |

| Feature | Cost |
|---------|------|
| Google Search Grounding | Per query (varies) |
| Imagen 4 | Per image |
| Veo 3.1 | Per second of video |

*Always check [official pricing](https://ai.google.dev/pricing) for current rates*

---

## Context Windows

| Model | Context Window |
|-------|---------------|
| Gemini 3 Pro | 1M tokens |
| Gemini 3 Flash | 1M tokens |
| Gemini 2.5 Flash | 1M tokens |
| Gemini 2.5 Flash-Lite | 1M tokens |

---

## Capabilities Matrix

| Capability | 3 Pro | 3 Flash | 2.5 Flash | 2.5 Lite |
|------------|-------|---------|-----------|----------|
| Text | ✅ | ✅ | ✅ | ✅ |
| Vision | ✅ | ✅ | ✅ | ✅ |
| Audio | ✅ | ✅ | ✅ | ❌ |
| Code | ✅ | ✅ | ✅ | ✅ |
| Function Calling | ✅ | ✅ | ✅ | ✅ |
| Search Grounding | ✅ | ✅ | ✅ | ✅ |
| Code Execution | ✅ | ✅ | ✅ | ✅ |
| Deep Think | ✅ | ❌ | ❌ | ❌ |

---

## Rate Limits (Free Tier)

| Model | RPM | TPM |
|-------|-----|-----|
| Gemini 3 Flash | 15 | 1M |
| Gemini 2.5 Flash | 15 | 1M |

*Paid tiers have significantly higher limits*

---

## Common Errors & Fixes

| Error | Likely Cause | Fix |
|-------|--------------|-----|
| `RESOURCE_EXHAUSTED` | Rate limit hit | Add backoff, upgrade tier |
| `INVALID_ARGUMENT` | Bad model string | Check model name spelling |
| `PERMISSION_DENIED` | API key issue | Regenerate key, check permissions |
| `SAFETY` block | Content filtered | Adjust safety settings or prompt |

---

## Useful Links

- [AI Studio](https://aistudio.google.com) — Test prompts
- [API Docs](https://ai.google.dev/gemini-api/docs) — Full documentation
- [Pricing](https://ai.google.dev/pricing) — Current rates
- [Model Cards](https://ai.google.dev/gemini-api/docs/models) — Model details
- [Cookbook](https://github.com/google-gemini/cookbook) — Code examples
