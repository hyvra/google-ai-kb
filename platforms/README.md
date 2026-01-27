# Google AI Platforms Overview

> Where to build, test, and deploy your AI applications.

---

## The Landscape

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         GOOGLE AI PLATFORMS                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   EXPLORATION          BUILD              PRODUCTION         SPECIALIZED    │
│   ───────────         ─────              ──────────         ───────────    │
│                                                                             │
│   ┌──────────┐      ┌──────────┐       ┌──────────┐       ┌──────────┐    │
│   │   AI     │      │ Firebase │       │  Vertex  │       │Antigravity│    │
│   │  Studio  │  →   │  Studio  │   →   │    AI    │       │          │    │
│   └──────────┘      └──────────┘       └──────────┘       └──────────┘    │
│                                                                             │
│   Test prompts      Build apps         Scale &            Autonomous       │
│   Explore models    Prototype          Govern             coding           │
│   Export code       Deploy                                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Quick Comparison

| Platform | Purpose | User | API Used | Cost |
|----------|---------|------|----------|------|
| [AI Studio](ai-studio.md) | Prompt testing | Developers | Gemini Developer API | Free tier |
| [Firebase Studio](firebase-ai-logic.md) | App building | Builders | Either | Free tier |
| [Vertex AI](vertex-ai.md) | Production | Enterprise | Vertex AI API | Pay-as-you-go |
| [Antigravity](antigravity.md) | Agentic coding | Developers | Multi-model | Free preview |

---

## Decision Flow

```
What do you need?
│
├─► "I want to test a prompt quickly"
│   └─► AI Studio
│
├─► "I want to build an app with AI"
│   └─► Firebase Studio (browser IDE)
│       OR your IDE + Firebase AI Logic SDK
│
├─► "I need production deployment with SLAs"
│   └─► Vertex AI
│
├─► "I want AI to help me code autonomously"
│   └─► Antigravity (desktop)
│       OR Gemini CLI (terminal)
│
└─► "I'm building a mobile/web app"
    └─► Firebase AI Logic SDK
```

---

## API Relationship

```
                    ┌─────────────────────────┐
                    │      Your App           │
                    └───────────┬─────────────┘
                                │
              ┌─────────────────┴─────────────────┐
              │                                   │
              ▼                                   ▼
    ┌─────────────────────┐           ┌─────────────────────┐
    │  Gemini Developer   │           │    Vertex AI        │
    │       API           │           │    Gemini API       │
    ├─────────────────────┤           ├─────────────────────┤
    │ • Free tier         │           │ • Enterprise SLA    │
    │ • Quick start       │           │ • IAM/compliance    │
    │ • Generous quotas   │           │ • Fine-tuning       │
    │ • ai.google.dev     │           │ • cloud.google.com  │
    └─────────────────────┘           └─────────────────────┘
              │                                   │
              │                                   │
              └─────────────┬─────────────────────┘
                            │
                            ▼
                    ┌─────────────────────┐
                    │   Gemini Models     │
                    │   (Same models,     │
                    │    different APIs)  │
                    └─────────────────────┘
```

---

## Feature Matrix

| Feature | AI Studio | Firebase Studio | Vertex AI | Antigravity |
|---------|-----------|-----------------|-----------|-------------|
| Prompt testing | ✅ | ❌ | ✅ | ❌ |
| Code export | ✅ | ✅ | ✅ | ✅ |
| App building | ❌ | ✅ | ❌ | ✅ |
| Deployment | ❌ | ✅ | ✅ | ❌ |
| IAM/Auth | ❌ | ✅ | ✅ | ❌ |
| Fine-tuning | ❌ | ❌ | ✅ | ❌ |
| Monitoring | Basic | ✅ | ✅ | ❌ |
| Multi-model | ❌ | ❌ | ✅ | ✅ |
| Browser-based | ✅ | ✅ | ✅ | ❌ |

---

## Detailed Docs

- [AI Studio](ai-studio.md) — Prompt playground & experimentation
- [Vertex AI](vertex-ai.md) — Enterprise platform
- [Firebase AI Logic](firebase-ai-logic.md) — Mobile/web SDKs
- [Antigravity](antigravity.md) — Agentic development IDE

---

## Common Patterns

### Pattern 1: Prototype → Production

```
1. AI Studio: Test prompts, find right model
2. Firebase Studio: Build working prototype
3. Vertex AI: Deploy with monitoring, compliance
```

### Pattern 2: Mobile App with AI

```
1. Firebase AI Logic SDK: Integrate into app
2. Choose API: Developer (free tier) or Vertex (enterprise)
3. Add App Check: Protect against abuse
```

### Pattern 3: Agentic Development

```
1. Antigravity: Complex coding tasks
2. Gemini CLI: Terminal-based automation
3. ADK: Build your own agents
```

---

## Pricing Summary

| Platform | Cost Model |
|----------|------------|
| AI Studio | Free (quota limits) |
| Vertex AI | Pay-per-token + features |
| Firebase AI Logic | API costs pass-through |
| Antigravity | Free preview |

---

## Related

- [Choosing a Model](../guides/choosing-a-model.md)
- [Pricing Comparison](../guides/pricing-comparison.md)
- [Frameworks](../frameworks/README.md)
