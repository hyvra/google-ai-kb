# Google AI Ecosystem Knowledge Base

> A comprehensive reference for Google's AI services, models, tools, and platforms. Built for developers who need quick answers on what to use and when.

[![Last Updated](https://img.shields.io/badge/Updated-January%202026-blue)]()
[![Models](https://img.shields.io/badge/Models-Gemini%203-green)]()
[![License](https://img.shields.io/badge/License-MIT-yellow)]()

---

## 🚀 Quick Start Decision Tree

```
What are you building?
│
├─► Chatbot / Assistant
│   └─► Gemini 3 Flash + Function Calling
│
├─► Complex Analysis / Research
│   └─► Gemini 3 Pro + Deep Think Mode
│
├─► High-Volume API (cost-sensitive)
│   └─► Gemini 2.5 Flash-Lite
│
├─► Real-Time Voice App
│   └─► Gemini Live API
│
├─► Image Generation
│   └─► Imagen 4 (quality) or Nano Banana Pro (speed)
│
├─► Video Generation
│   └─► Veo 3.1
│
├─► Multi-Agent System
│   └─► ADK + Agent Engine
│
├─► Mobile/Web App with AI
│   └─► Firebase AI Logic SDK
│
└─► Autonomous Coding Tasks
    └─► Antigravity or Gemini CLI
```

---

## 📁 Knowledge Base Structure

```
google-ai-kb/
├── README.md                    # You are here
├── QUICKREF.md                  # One-page cheat sheet
│
├── models/
│   ├── README.md                # Models overview & comparison
│   ├── gemini-3-pro.md          # Flagship reasoning model
│   ├── gemini-3-flash.md        # Recommended daily driver
│   ├── gemini-25-flash.md       # Balanced performance
│   ├── gemini-25-flash-lite.md  # Economy/scale model
│   ├── gemini-live.md           # Real-time audio/video
│   ├── imagen.md                # Image generation
│   └── veo.md                   # Video generation
│
├── tools/
│   ├── README.md                # Tools overview
│   ├── function-calling.md      # Connect to external APIs
│   ├── google-search.md         # Search grounding
│   ├── code-execution.md        # Sandboxed Python
│   ├── url-context.md           # Web page analysis
│   └── computer-use.md          # Browser automation
│
├── platforms/
│   ├── README.md                # Platforms comparison
│   ├── ai-studio.md             # Prompt playground
│   ├── vertex-ai.md             # Enterprise platform
│   ├── firebase-ai-logic.md     # Mobile/web SDKs
│   └── antigravity.md           # Agentic IDE
│
├── frameworks/
│   ├── README.md                # Frameworks overview
│   ├── adk.md                   # Agent Development Kit
│   ├── genkit.md                # Server-side AI workflows
│   └── gemini-cli.md            # Terminal coding agent
│
├── guides/
│   ├── choosing-a-model.md      # Decision guide
│   ├── pricing-comparison.md    # Cost breakdown
│   ├── migration-paths.md       # Upgrading between tiers
│   └── architecture-patterns.md # Common app architectures
│
└── assets/
    └── ecosystem-diagram.md     # Visual reference
```

---

## 🧠 Models at a Glance

| Model | Speed | Cost | Best For |
|-------|-------|------|----------|
| [Gemini 3 Pro](models/gemini-3-pro.md) | Medium | $$$ | Complex reasoning, research, agentic workflows |
| [Gemini 3 Flash](models/gemini-3-flash.md) | Fast | $ | Daily tasks, coding, chat interfaces |
| [Gemini 2.5 Flash](models/gemini-25-flash.md) | Very Fast | $ | Balanced workloads, streaming |
| [Gemini 2.5 Flash-Lite](models/gemini-25-flash-lite.md) | Fastest | ¢ | High-volume, simple tasks |
| [Gemini Live](models/gemini-live.md) | Real-time | $$ | Voice apps, video streaming |
| [Imagen 4](models/imagen.md) | - | $$ | High-quality image generation |
| [Veo 3.1](models/veo.md) | - | $$$ | Video generation with audio |

---

## 🏗️ Platforms at a Glance

| Platform | Purpose | When to Use |
|----------|---------|-------------|
| [AI Studio](platforms/ai-studio.md) | Prototype & Test | Exploring prompts, quick experiments |
| [Vertex AI](platforms/vertex-ai.md) | Production & Enterprise | Scale, compliance, governance |
| [Firebase AI Logic](platforms/firebase-ai-logic.md) | Mobile & Web Apps | Client-side AI integration |
| [Antigravity](platforms/antigravity.md) | Agentic IDE | Autonomous dev tasks |

---

## 🔧 Built-in Tools

| Tool | What It Does |
|------|--------------|
| [Function Calling](tools/function-calling.md) | Connect models to external APIs |
| [Google Search](tools/google-search.md) | Ground responses in real-time web data |
| [Code Execution](tools/code-execution.md) | Run Python in a sandbox |
| [URL Context](tools/url-context.md) | Analyze web pages |
| [Computer Use](tools/computer-use.md) | Browser automation |

---

## ⚙️ Frameworks

| Framework | Language | Purpose |
|-----------|----------|---------|
| [ADK](frameworks/adk.md) | Python/TypeScript | Build multi-agent systems |
| [Genkit](frameworks/genkit.md) | JS/Go/Python | Server-side AI workflows |
| [Gemini CLI](frameworks/gemini-cli.md) | Terminal | Agentic coding from command line |

---

## 📚 Guides

- [Choosing a Model](guides/choosing-a-model.md) — Decision flowchart
- [Pricing Comparison](guides/pricing-comparison.md) — Cost breakdown by use case
- [Migration Paths](guides/migration-paths.md) — Moving between tiers
- [Architecture Patterns](guides/architecture-patterns.md) — Common app structures

---

## 🔗 Official Resources

| Resource | URL |
|----------|-----|
| Gemini API Docs | https://ai.google.dev/gemini-api/docs |
| Vertex AI Docs | https://cloud.google.com/vertex-ai/docs |
| Firebase AI Logic | https://firebase.google.com/docs/ai-logic |
| ADK Docs | https://google.github.io/adk-docs |
| AI Studio | https://aistudio.google.com |
| Antigravity | https://antigravity.google |

---

## Contributing

Found something outdated or missing? PRs welcome.

---

## License

MIT — use this however you want.
