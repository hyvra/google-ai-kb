# Gemini Models Overview

> Complete guide to Google's Gemini model family and when to use each one.

---

## Model Hierarchy

```
                    ┌─────────────────────┐
                    │   GEMINI 3 PRO      │  ← Maximum Intelligence
                    │   Deep reasoning    │
                    └─────────┬───────────┘
                              │
                    ┌─────────▼───────────┐
                    │  GEMINI 3 FLASH     │  ← Best Balance ⭐
                    │  Fast + Capable     │
                    └─────────┬───────────┘
                              │
                    ┌─────────▼───────────┐
                    │  GEMINI 2.5 FLASH   │  ← Proven Reliability
                    │  Stable workhorse   │
                    └─────────┬───────────┘
                              │
                    ┌─────────▼───────────┐
                    │ GEMINI 2.5 FLASH-LITE│  ← Maximum Speed/Scale
                    │  High throughput    │
                    └─────────────────────┘
```

---

## Comparison Table

| Attribute | Gemini 3 Pro | Gemini 3 Flash | Gemini 2.5 Flash | Gemini 2.5 Flash-Lite |
|-----------|--------------|----------------|------------------|----------------------|
| **Speed** | Medium | Fast | Very Fast | Fastest |
| **Intelligence** | Highest | High | Good | Basic |
| **Cost** | $$$ | $ | $ | ¢ |
| **Context** | 1M tokens | 1M tokens | 1M tokens | 1M tokens |
| **Best For** | Complex reasoning | General purpose | Balanced loads | High volume |

---

## Model Strings

```python
# Use these exact strings in API calls
"gemini-3-pro"           # Flagship
"gemini-3-flash"         # Recommended
"gemini-2.5-flash"       # Balanced
"gemini-2.5-flash-lite"  # Economy
```

---

## Decision Flowchart

```
START
  │
  ▼
┌─────────────────────────────────────┐
│ Is this a complex reasoning task?   │
│ (math, research, multi-step logic)  │
└─────────────────┬───────────────────┘
                  │
        ┌────YES─┴─NO────┐
        ▼                ▼
   Gemini 3 Pro    ┌─────────────────────────────────┐
   + Deep Think    │ Do you need real-time response? │
                   └─────────────────┬───────────────┘
                                     │
                           ┌────YES──┴──NO────┐
                           ▼                  ▼
                    ┌──────────────┐   ┌──────────────────────┐
                    │ Is latency   │   │ Is this high-volume  │
                    │ critical?    │   │ (>1000 req/min)?     │
                    └──────┬───────┘   └──────────┬───────────┘
                           │                      │
                  ┌───YES──┴──NO───┐      ┌──YES──┴──NO───┐
                  ▼                ▼      ▼               ▼
           Gemini 2.5        Gemini 3   Gemini 2.5    Gemini 3
           Flash-Lite        Flash      Flash-Lite    Flash
```

---

## Detailed Model Docs

- [Gemini 3 Pro](gemini-3-pro.md) — Flagship reasoning model
- [Gemini 3 Flash](gemini-3-flash.md) — Recommended daily driver
- [Gemini 2.5 Flash](gemini-25-flash.md) — Balanced performance
- [Gemini 2.5 Flash-Lite](gemini-25-flash-lite.md) — Economy scale
- [Gemini Live](gemini-live.md) — Real-time audio/video
- [Imagen](imagen.md) — Image generation
- [Veo](veo.md) — Video generation

---

## Multimodal Capabilities

All Gemini models support multimodal input:

| Input Type | 3 Pro | 3 Flash | 2.5 Flash | 2.5 Lite |
|------------|-------|---------|-----------|----------|
| Text | ✅ | ✅ | ✅ | ✅ |
| Images | ✅ | ✅ | ✅ | ✅ |
| Video | ✅ | ✅ | ✅ | ✅ |
| Audio | ✅ | ✅ | ✅ | ❌ |
| PDF | ✅ | ✅ | ✅ | ✅ |
| Code | ✅ | ✅ | ✅ | ✅ |

---

## Special Modes

### Deep Think (Gemini 3 Pro only)

Extended reasoning mode for complex problems. The model explicitly shows its reasoning process.

```python
response = client.models.generate_content(
    model="gemini-3-pro",
    contents="Prove that there are infinitely many primes",
    config={"thinking_config": {"thinking_budget": 10000}}
)
```

**When to use:**
- Mathematical proofs
- Strategic planning
- Complex code architecture
- Research analysis

### Thinking Budget (Gemini 3 Flash)

Control reasoning depth with thinking budgets:

```python
config = {
    "thinking_config": {
        "thinking_budget": 1024  # tokens allocated to reasoning
    }
}
```

---

## Model Lifecycle

Google follows a predictable deprecation pattern:

1. **Preview** → New model, may change
2. **Stable** → Production ready
3. **Deprecated** → 6-month warning
4. **Sunset** → Removed

**Current Status (Jan 2026):**
- Gemini 3.x — Stable
- Gemini 2.5.x — Stable
- Gemini 2.0.x — Deprecated (sunset March 2026)

---

## Benchmarks (as of release)

| Benchmark | Gemini 3 Pro | Gemini 3 Flash |
|-----------|--------------|----------------|
| MMLU | 90%+ | 85%+ |
| HumanEval | 90%+ | 85%+ |
| GPQA Diamond | 90.4% | ~85% |
| SWE-bench | 75%+ | 78% |

*Note: Gemini 3 Flash actually outperforms Pro on some agentic coding benchmarks due to optimization for tool use*

---

## Rate Limits

### Free Tier
| Model | Requests/min | Tokens/min |
|-------|-------------|------------|
| Gemini 3 Flash | 15 | 1,000,000 |
| Gemini 2.5 Flash | 15 | 1,000,000 |

### Paid Tier
Significantly higher — check [quota page](https://ai.google.dev/gemini-api/docs/quota)

---

## Next Steps

- [Choosing a Model Guide](../guides/choosing-a-model.md)
- [Pricing Comparison](../guides/pricing-comparison.md)
- [Tools Overview](../tools/README.md)
