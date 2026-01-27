# Gemini 3 Pro

> Google's flagship reasoning model. Maximum intelligence for complex tasks.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Model String | `gemini-3-pro` |
| Context Window | 1,000,000 tokens |
| Speed | Medium |
| Cost | $$$ (highest tier) |
| Release | November 2025 |

---

## When to Use

✅ **Use Gemini 3 Pro for:**
- Complex multi-step reasoning
- Research and analysis
- Agentic workflows requiring planning
- Mathematical proofs and complex logic
- Code architecture decisions
- Tasks where accuracy > speed

❌ **Don't use for:**
- Simple Q&A (overkill)
- High-volume requests (expensive)
- Real-time chat (latency)
- Cost-sensitive applications

---

## Key Capabilities

### Deep Think Mode

Gemini 3 Pro's signature feature. Extended reasoning that shows its work.

```python
from google import genai

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3-pro",
    contents="What's the optimal strategy for a complex negotiation scenario where...",
    config={
        "thinking_config": {
            "thinking_budget": 10000  # tokens for reasoning
        }
    }
)

# Access the thinking process
print(response.thinking)  # Shows reasoning steps
print(response.text)      # Final answer
```

### Multimodal Understanding

```python
# Analyze complex documents
response = client.models.generate_content(
    model="gemini-3-pro",
    contents=[
        {"text": "Analyze this research paper and identify methodology flaws"},
        {"file_data": {"file_uri": "gs://bucket/paper.pdf"}}
    ]
)
```

### Agentic Capabilities

Best model for multi-step tool use:

```python
tools = [
    {"google_search": {}},
    {"code_execution": {}},
    {"function_declarations": [...]}
]

response = client.models.generate_content(
    model="gemini-3-pro",
    contents="Research the latest developments in quantum computing, write code to visualize the timeline, and summarize findings",
    config={"tools": tools}
)
```

---

## Benchmarks

| Benchmark | Score | Notes |
|-----------|-------|-------|
| GPQA Diamond | 90.4% | PhD-level science questions |
| Humanity's Last Exam | 41% | Outperformed GPT-5 Pro (31.64%) |
| MMLU | 90%+ | Broad knowledge |
| SWE-bench | 75%+ | Code understanding |

---

## Pricing

| Type | Cost (per 1M tokens) |
|------|---------------------|
| Input (≤128K context) | ~$1.25 |
| Input (>128K context) | ~$2.50 |
| Output (≤128K context) | ~$5.00 |
| Output (>128K context) | ~$10.00 |

*Check [official pricing](https://ai.google.dev/pricing) for current rates*

---

## Best Practices

### 1. Use Thinking Budget Wisely

```python
# Simple task - minimal thinking
config = {"thinking_config": {"thinking_budget": 1024}}

# Complex task - more thinking
config = {"thinking_config": {"thinking_budget": 10000}}

# Maximum reasoning
config = {"thinking_config": {"thinking_budget": 32000}}
```

### 2. Structured Output for Reliability

```python
response = client.models.generate_content(
    model="gemini-3-pro",
    contents="Analyze this data...",
    config={
        "response_mime_type": "application/json",
        "response_schema": {
            "type": "object",
            "properties": {
                "analysis": {"type": "string"},
                "confidence": {"type": "number"},
                "recommendations": {"type": "array"}
            }
        }
    }
)
```

### 3. System Instructions for Consistency

```python
response = client.models.generate_content(
    model="gemini-3-pro",
    contents="...",
    config={
        "system_instruction": """You are an expert analyst. 
        Always cite sources. 
        Use structured reasoning.
        Acknowledge uncertainty."""
    }
)
```

---

## Comparison with Gemini 3 Flash

| Aspect | 3 Pro | 3 Flash |
|--------|-------|---------|
| Reasoning depth | Deeper | Good |
| Speed | Slower | Faster |
| Cost | 10-20x more | Baseline |
| Deep Think | ✅ | ❌ |
| Agentic coding | Good | Better* |

*Gemini 3 Flash is actually optimized for agentic coding and scores higher on SWE-bench (78% vs 75%)

---

## Common Use Cases

### Research Assistant

```python
system = """You are a research assistant. For each query:
1. Search for relevant papers and sources
2. Analyze findings critically
3. Synthesize into actionable insights
4. Cite all sources"""

response = client.models.generate_content(
    model="gemini-3-pro",
    contents="What are the latest breakthroughs in solid-state batteries?",
    config={
        "system_instruction": system,
        "tools": [{"google_search": {}}]
    }
)
```

### Code Architecture Review

```python
response = client.models.generate_content(
    model="gemini-3-pro",
    contents=[
        {"text": "Review this codebase architecture. Identify design patterns, potential issues, and suggest improvements."},
        {"file_data": {"file_uri": "gs://bucket/codebase.zip"}}
    ],
    config={"thinking_config": {"thinking_budget": 10000}}
)
```

### Complex Decision Making

```python
response = client.models.generate_content(
    model="gemini-3-pro",
    contents="""
    Given these constraints:
    - Budget: $500K
    - Timeline: 6 months
    - Team: 5 engineers
    - Requirements: [detailed list]
    
    Evaluate build vs buy for this AI infrastructure.
    Consider long-term maintenance, scaling, and opportunity cost.
    """,
    config={"thinking_config": {"thinking_budget": 15000}}
)
```

---

## Limitations

- **Latency**: Not suitable for real-time applications
- **Cost**: Expensive for high-volume use
- **Overkill**: Simple tasks don't benefit from extra capability
- **Rate limits**: Lower than Flash models

---

## Related

- [Gemini 3 Flash](gemini-3-flash.md) — Faster, cheaper alternative
- [Deep Think Guide](../guides/deep-think.md) — Extended reasoning
- [Tools Overview](../tools/README.md) — Available tools
