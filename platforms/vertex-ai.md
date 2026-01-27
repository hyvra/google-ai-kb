# Vertex AI

> Google Cloud's enterprise AI platform. Production-grade deployment with governance, compliance, and scale.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| URL | [cloud.google.com/vertex-ai](https://cloud.google.com/vertex-ai) |
| Console | [console.cloud.google.com/vertex-ai](https://console.cloud.google.com/vertex-ai) |
| API | Vertex AI Gemini API |
| Purpose | Enterprise production |
| Billing | GCP pay-as-you-go |

---

## What It Is

Vertex AI is Google Cloud's **unified AI platform** for:
- Deploying Gemini models at scale
- Fine-tuning models on your data
- Building ML pipelines
- Enterprise governance and compliance
- Multi-model orchestration

---

## When to Use

✅ **Use Vertex AI for:**
- Production deployments requiring SLAs
- Enterprise compliance (SOC2, HIPAA, etc.)
- Fine-tuning models
- Data residency requirements
- IAM-based access control
- Monitoring and logging
- Multi-region deployment

❌ **Don't use for:**
- Quick prototyping (use AI Studio)
- Simple apps (use Firebase AI Logic)
- Learning/experimenting (overkill)

---

## Key Features

### 1. Model Garden

Access to multiple models:
- Gemini 3 Pro, Flash, etc.
- Third-party models (Anthropic, Meta, Mistral)
- Open models (Gemma, Llama)
- Specialized models (MedLM, etc.)

### 2. Fine-Tuning

Customize models on your data:
```python
from vertexai.tuning import sft

tuning_job = sft.train(
    source_model="gemini-3-flash",
    train_dataset="gs://bucket/training_data.jsonl",
    epochs=3,
    learning_rate_multiplier=1.0
)
```

### 3. Agent Engine (Agent Builder)

Deploy AI agents at scale:
- Managed runtime
- Session management
- Memory/state persistence
- Tool integration
- Evaluation and monitoring

### 4. Grounding Options

- **Google Search** — Real-time web grounding
- **Vertex AI Search** — Your enterprise data
- **RAG Engine** — Custom knowledge bases

### 5. Enterprise Controls

- **IAM** — Fine-grained access control
- **VPC-SC** — Network security perimeter
- **CMEK** — Customer-managed encryption keys
- **Audit logs** — Compliance logging
- **Data residency** — Regional deployment

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Your Application                          │
└─────────────────────────────────┬───────────────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                     Vertex AI Platform                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐    │
│   │   Model     │  │   Agent     │  │   Vertex AI         │    │
│   │   Garden    │  │   Engine    │  │   Search            │    │
│   └─────────────┘  └─────────────┘  └─────────────────────┘    │
│                                                                 │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐    │
│   │   Fine-     │  │   RAG       │  │   Evaluation        │    │
│   │   Tuning    │  │   Engine    │  │   Service           │    │
│   └─────────────┘  └─────────────┘  └─────────────────────┘    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│   IAM │ VPC-SC │ Audit Logs │ Monitoring │ Data Residency      │
└─────────────────────────────────────────────────────────────────┘
```

---

## Code Examples

### Basic Generation

```python
import vertexai
from vertexai.generative_models import GenerativeModel

vertexai.init(project="your-project", location="us-central1")

model = GenerativeModel("gemini-3-flash")
response = model.generate_content("Explain quantum computing")
print(response.text)
```

### With Grounding

```python
from vertexai.generative_models import GenerativeModel, Tool
from vertexai.preview.generative_models import grounding

model = GenerativeModel("gemini-3-flash")

# Ground with Google Search
tool = Tool.from_google_search_retrieval(
    grounding.GoogleSearchRetrieval()
)

response = model.generate_content(
    "What's the latest news about AI?",
    tools=[tool]
)
```

### Enterprise RAG with Vertex AI Search

```python
from vertexai.preview import rag

# Create RAG corpus
corpus = rag.create_corpus(display_name="company-docs")

# Import documents
rag.import_files(
    corpus.name,
    paths=["gs://bucket/docs/"],
    chunk_size=512
)

# Query with RAG
rag_resource = rag.RagResource(
    rag_corpus=corpus.name,
)

model = GenerativeModel("gemini-3-flash")
response = model.generate_content(
    "What is our company policy on remote work?",
    tools=[Tool.from_retrieval(retrieval=rag.Retrieval(source=rag_resource))]
)
```

---

## Pricing

### Model Usage

| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|----------------------|------------------------|
| Gemini 3 Pro (<128K) | ~$1.25 | ~$5.00 |
| Gemini 3 Pro (>128K) | ~$2.50 | ~$10.00 |
| Gemini 3 Flash | ~$0.075 | ~$0.30 |

### Additional Services

| Service | Cost |
|---------|------|
| Grounding (Google Search) | Per query |
| Vertex AI Search | Per query + storage |
| Fine-tuning | Per training hour |
| Agent Engine | Per session + compute |

*Check [official pricing](https://cloud.google.com/vertex-ai/pricing)*

---

## Vertex AI vs Gemini Developer API

| Aspect | Vertex AI | Developer API |
|--------|-----------|---------------|
| **Target** | Enterprise | Developers |
| **Auth** | GCP IAM | API keys |
| **SLA** | 99.5% uptime | Best effort |
| **Compliance** | SOC2, HIPAA, etc. | Basic |
| **Fine-tuning** | ✅ | ❌ |
| **Data residency** | ✅ | ❌ |
| **Cost** | Pay-as-you-go | Free tier + pay |
| **Setup** | GCP project | API key only |

---

## Getting Started

### 1. Set Up GCP Project

```bash
# Install gcloud CLI
gcloud auth login
gcloud config set project YOUR_PROJECT_ID

# Enable APIs
gcloud services enable aiplatform.googleapis.com
```

### 2. Install SDK

```bash
pip install google-cloud-aiplatform
```

### 3. Initialize

```python
import vertexai
vertexai.init(project="your-project", location="us-central1")
```

### 4. Make Request

```python
from vertexai.generative_models import GenerativeModel

model = GenerativeModel("gemini-3-flash")
response = model.generate_content("Hello!")
```

---

## Best Practices

### 1. Use Service Accounts

```python
# Don't use user credentials in production
# Create a service account with minimal permissions

from google.oauth2 import service_account

credentials = service_account.Credentials.from_service_account_file(
    "service-account.json"
)
vertexai.init(project="project", credentials=credentials)
```

### 2. Implement Retry Logic

```python
from google.api_core import retry

@retry.Retry(predicate=retry.if_exception_type(Exception))
def generate_with_retry(prompt):
    return model.generate_content(prompt)
```

### 3. Monitor Usage

```python
# Enable Cloud Monitoring
# Set up alerts for quota usage
# Track costs with budgets
```

### 4. Use Caching for Repeated Context

```python
# For repeated context (e.g., system prompts), use caching
# Reduces costs and latency
cached_content = caching.CachedContent.create(
    model_name="gemini-3-flash",
    contents=[large_system_prompt],
    ttl=datetime.timedelta(hours=1)
)
```

---

## Regions

Vertex AI is available in multiple regions:

| Region | Location |
|--------|----------|
| us-central1 | Iowa |
| us-east4 | Virginia |
| europe-west4 | Netherlands |
| asia-northeast1 | Tokyo |

*Check [docs](https://cloud.google.com/vertex-ai/docs/general/locations) for full list*

---

## Related

- [AI Studio](ai-studio.md) — Prototyping playground
- [Firebase AI Logic](firebase-ai-logic.md) — Mobile/web SDKs
- [ADK](../frameworks/adk.md) — Agent Development Kit
