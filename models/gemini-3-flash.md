# Gemini 3 Flash

> The recommended default model. Best balance of speed, capability, and cost.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Model String | `gemini-3-flash` |
| Context Window | 1,000,000 tokens |
| Speed | Fast |
| Cost | $ (cost-effective) |
| Release | December 2025 |

---

## Why It's Recommended

Gemini 3 Flash is the **default choice** for most applications because:

1. **Pro-grade reasoning** at Flash-level speed
2. **Best agentic coding** — 78% on SWE-bench (beats Pro)
3. **Native tool use** — optimized for function calling
4. **Cost-effective** — fraction of Pro pricing
5. **Fast** — suitable for interactive applications

---

## When to Use

✅ **Use Gemini 3 Flash for:**
- General-purpose chat and Q&A
- Coding assistance and generation
- Agentic workflows
- Document analysis
- Real-time applications
- Production APIs

❌ **Consider alternatives for:**
- Maximum reasoning depth → Gemini 3 Pro
- Lowest possible cost → Gemini 2.5 Flash-Lite
- Real-time voice → Gemini Live API

---

## Key Capabilities

### Multimodal Input

```python
from google import genai

client = genai.Client()

# Text + Image
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=[
        {"text": "What's in this image?"},
        {"inline_data": {"mime_type": "image/jpeg", "data": base64_image}}
    ]
)

# Text + PDF
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=[
        {"text": "Summarize this document"},
        {"file_data": {"file_uri": "gs://bucket/document.pdf"}}
    ]
)

# Text + Audio
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=[
        {"text": "Transcribe and summarize"},
        {"inline_data": {"mime_type": "audio/mp3", "data": base64_audio}}
    ]
)
```

### Native Tool Use

Gemini 3 Flash excels at tool use:

```python
# Multiple tools in one request
tools = [
    {"google_search": {}},
    {"code_execution": {}},
    {"function_declarations": [
        {
            "name": "get_weather",
            "description": "Get current weather",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {"type": "string"}
                }
            }
        }
    ]}
]

response = client.models.generate_content(
    model="gemini-3-flash",
    contents="What's the weather in Tokyo? Also search for today's news there.",
    config={"tools": tools}
)
```

### Thinking Budget (Optional)

Control reasoning depth:

```python
# More reasoning for complex tasks
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="Explain the proof of Fermat's Last Theorem",
    config={
        "thinking_config": {
            "thinking_budget": 4096
        }
    }
)
```

---

## Code Examples

### Basic Chat

```python
from google import genai

client = genai.Client(api_key="YOUR_KEY")

response = client.models.generate_content(
    model="gemini-3-flash",
    contents="Explain microservices architecture"
)
print(response.text)
```

### Streaming Response

```python
for chunk in client.models.generate_content_stream(
    model="gemini-3-flash",
    contents="Write a detailed guide to Docker"
):
    print(chunk.text, end="", flush=True)
```

### Multi-turn Chat

```python
chat = client.chats.create(model="gemini-3-flash")

response1 = chat.send_message("What is React?")
print(response1.text)

response2 = chat.send_message("How does it compare to Vue?")
print(response2.text)

response3 = chat.send_message("Show me a code example")
print(response3.text)
```

### With System Instructions

```python
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="Review this code for bugs",
    config={
        "system_instruction": """You are a senior code reviewer.
        Focus on: security, performance, maintainability.
        Be specific and provide fixes."""
    }
)
```

### JSON Output

```python
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="List 5 startup ideas for AI tools",
    config={
        "response_mime_type": "application/json",
        "response_schema": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "name": {"type": "string"},
                    "description": {"type": "string"},
                    "target_market": {"type": "string"}
                }
            }
        }
    }
)
```

---

## Pricing

| Type | Cost (per 1M tokens) |
|------|---------------------|
| Input | ~$0.075 |
| Output | ~$0.30 |

*~10-20x cheaper than Gemini 3 Pro*

---

## Benchmarks

| Benchmark | Score |
|-----------|-------|
| SWE-bench Verified | 78% |
| MMLU | 85%+ |
| HumanEval | 85%+ |
| GPQA Diamond | ~85% |

**Notable:** Gemini 3 Flash outperforms Gemini 3 Pro on SWE-bench due to optimization for agentic coding.

---

## Rate Limits

### Free Tier
- 15 requests per minute
- 1,000,000 tokens per minute

### Paid Tier
- Significantly higher (check quota page)

---

## Best Practices

### 1. Start with Flash, Upgrade if Needed

```python
# Try Flash first
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=complex_prompt
)

# If quality insufficient, try Pro
if needs_deeper_reasoning(response):
    response = client.models.generate_content(
        model="gemini-3-pro",
        contents=complex_prompt,
        config={"thinking_config": {"thinking_budget": 10000}}
    )
```

### 2. Use Appropriate Context Length

```python
# Don't stuff context unnecessarily
# Flash handles 1M tokens, but shorter = faster + cheaper

# Good: Include only relevant context
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=f"Based on this excerpt: {relevant_section}\n\nQuestion: {question}"
)
```

### 3. Leverage Tool Use

```python
# Flash is optimized for tools - use them!
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="Calculate compound interest for $10K at 5% for 10 years",
    config={"tools": [{"code_execution": {}}]}
)
```

---

## Common Use Cases

### Chatbot / Assistant

```python
system = """You are a helpful assistant. Be concise but thorough.
If you don't know something, say so."""

chat = client.chats.create(
    model="gemini-3-flash",
    config={"system_instruction": system}
)
```

### Code Generation

```python
response = client.models.generate_content(
    model="gemini-3-flash",
    contents="""Write a Python function that:
    - Takes a list of URLs
    - Fetches them concurrently
    - Returns results with error handling
    - Include type hints and docstrings"""
)
```

### Document Processing

```python
response = client.models.generate_content(
    model="gemini-3-flash",
    contents=[
        {"text": "Extract all action items from this meeting transcript"},
        {"file_data": {"file_uri": "gs://bucket/meeting.txt"}}
    ],
    config={
        "response_mime_type": "application/json",
        "response_schema": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "action": {"type": "string"},
                    "owner": {"type": "string"},
                    "deadline": {"type": "string"}
                }
            }
        }
    }
)
```

---

## Gemini 3 Flash vs Others

| Aspect | 3 Flash | 3 Pro | 2.5 Flash | 2.5 Lite |
|--------|---------|-------|-----------|----------|
| Speed | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Intelligence | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| Cost | ⭐⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Tool Use | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |

---

## Related

- [Gemini 3 Pro](gemini-3-pro.md) — When you need deeper reasoning
- [Gemini 2.5 Flash-Lite](gemini-25-flash-lite.md) — When you need lower cost
- [Function Calling](../tools/function-calling.md) — Connect to external APIs
- [Code Execution](../tools/code-execution.md) — Run Python in sandbox
