# Gemini 2.5 Flash

> Balanced performance model. Proven reliability with controllable thinking.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Model String | `gemini-2.5-flash` |
| Context Window | 1,000,000 tokens |
| Speed | Very Fast |
| Cost | $ |
| Status | Stable |

---

## When to Use

✅ **Use Gemini 2.5 Flash for:**
- Production workloads needing proven stability
- Balanced speed/quality requirements
- Streaming applications
- When you need controllable thinking budgets

❌ **Consider alternatives for:**
- Cutting-edge capabilities → Gemini 3 Flash
- Maximum throughput → Gemini 2.5 Flash-Lite
- Complex reasoning → Gemini 3 Pro

---

## Key Features

### Controllable Thinking Budget

```python
from google import genai

client = genai.Client()

# Minimal thinking for simple tasks
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="What is 2+2?",
    config={"thinking_config": {"thinking_budget": 0}}
)

# More thinking for complex tasks
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Explain quantum entanglement",
    config={"thinking_config": {"thinking_budget": 4096}}
)
```

### Native Streaming

```python
for chunk in client.models.generate_content_stream(
    model="gemini-2.5-flash",
    contents="Write a comprehensive guide..."
):
    print(chunk.text, end="", flush=True)
```

---

## Pricing

| Type | Cost (per 1M tokens) |
|------|---------------------|
| Input | ~$0.075 |
| Output | ~$0.30 |

Similar to Gemini 3 Flash pricing.

---

## Related

- [Gemini 3 Flash](gemini-3-flash.md) — Newer, more capable
- [Gemini 2.5 Flash-Lite](gemini-25-flash-lite.md) — Faster, cheaper
