# Gemini 2.5 Flash-Lite

> Maximum throughput at minimum cost. Built for scale.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Model String | `gemini-2.5-flash-lite` |
| Context Window | 1,000,000 tokens |
| Speed | Fastest |
| Cost | ¢ (cheapest) |
| Status | Stable |

---

## When to Use

✅ **Use Gemini 2.5 Flash-Lite for:**
- High-volume API calls (>1000 req/min)
- Cost-sensitive applications
- Simple classification/extraction tasks
- Preprocessing pipelines
- When speed > quality

❌ **Don't use for:**
- Complex reasoning
- Nuanced analysis
- Tasks requiring audio understanding
- High-stakes decisions

---

## Key Characteristics

| Aspect | Value |
|--------|-------|
| Latency | Lowest |
| Throughput | Highest |
| Cost | ~$0.02 input / ~$0.08 output per 1M tokens |
| Capabilities | Text, Vision, Code (no Audio) |

---

## Code Example

```python
from google import genai
import asyncio

client = genai.Client()

# High-volume processing
async def process_batch(items):
    tasks = [
        client.models.generate_content_async(
            model="gemini-2.5-flash-lite",
            contents=f"Classify this text: {item}"
        )
        for item in items
    ]
    return await asyncio.gather(*tasks)

# Ideal for simple extraction
response = client.models.generate_content(
    model="gemini-2.5-flash-lite",
    contents="Extract the email from: Contact us at hello@example.com",
    config={
        "response_mime_type": "application/json",
        "response_schema": {
            "type": "object",
            "properties": {"email": {"type": "string"}}
        }
    }
)
```

---

## Limitations

- ❌ No audio input support
- ❌ Less nuanced reasoning
- ❌ May miss subtle context
- ❌ Not ideal for creative tasks

---

## Best Use Cases

1. **Text classification** at scale
2. **Entity extraction** from documents
3. **Simple Q&A** systems
4. **Data preprocessing** pipelines
5. **Content moderation** (first pass)

---

## Related

- [Gemini 3 Flash](gemini-3-flash.md) — When you need better quality
- [Pricing Guide](../guides/pricing-comparison.md) — Cost analysis
