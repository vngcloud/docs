---
description: >-
  A functional overview of AI models on MaaS — purpose of use, basic principle
  of operation, and the main input data type for each model category.
---

# Understanding AI Models

GreenNode MaaS lets you use leading AI models right away — for chat, coding, image understanding, and document processing — without training or operating your own GPU infrastructure. This page explains what AI models are for, how they work at a basic level, and what kind of input data each model category expects, so you can pick the right model before browsing [Available Models](available-models.md).

***

## Purpose of Use

AI models on MaaS are pre-trained deep learning models that automate tasks previously requiring direct human effort: answering questions, summarizing or drafting content, generating and fixing code, reading images, generating images from a description, extracting data from documents, or searching by meaning. Instead of writing hard-coded rules for every case, you describe what you need in natural language (a prompt), and the model reasons out a suitable result.

## Principle of Operation

At a basic functional level, an AI model processes a request in three steps:

```
Input (text / image / audio / PDF)
        │
        ▼
   Tokenize the input data
        │
        ▼
Model predicts/generates output based on
 patterns learned from training data
        │
        ▼
   Output (text / image / vector / JSON...)
```

* **Tokenization:** Input data (words, image pixels...) is broken down into small units called **tokens**.
* **Context-based prediction:** A model doesn't "understand" the way a human does — it predicts the most likely next token based on the full context (the prompt, conversation history, system prompt) and patterns learned from a massive amount of training data.
* **Thinking vs. non-thinking modes:** Some models — especially "Reasoning" models such as Qwen, GLM, and DeepSeek — support a **thinking** mode (step-by-step, chain-of-thought reasoning) that improves accuracy on multi-step problems at the cost of a slower response; **non-thinking** mode answers faster for simpler tasks.

{% hint style="info" %}
The more tokens in context (prompt + conversation history), the longer a model takes to process and the higher the cost — see how token-based billing works in [Pricing](pricing.md).
{% endhint %}

## Model Categories by Function

| Category                    | Purpose of Use                                                             | Main Input Data                       | Typical Use-cases                                                          |
| ----------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------- | -------------------------------------------------------------------------- |
| Chat / Drafting              | Q\&A, summarization, writing & editing content                                | Text, system prompt                     | Virtual assistants, report drafting, internal Q\&A                        |
| Code                          | Generate/fix code, code review, write unit tests                             | Text/code, multi-file context           | Script automation, multi-file edits, code-run-fix loops                   |
| Reasoning                     | Solve multi-step logic/business problems, plan, check constraints             | Text describing the problem/constraints | Multi-step calculations, constraint checking, planning                    |
| Vision (multimodal)           | Read, describe, and classify image content                                    | Image + text                            | Reading charts/screenshots, UI checks, extracting content from images     |
| Image Generation             | Generate new images from a text description                                   | Text (prompt)                           | Banners, illustrations, mockups for social/marketing                       |
| OCR / Document AI (IDP)       | Extract text and structured fields from documents                             | Scanned images or PDF files             | Invoice extraction, ID/passport/driver's license reading, image-to-text    |
| Embedding (RAG · Step 1)     | Generate a semantic vector representation of text                            | Text                                    | Semantic search, building RAG pipelines, internal document search          |
| Rerank (RAG · Step 2)        | Re-rank retrieved results by relevance                                        | (Query, retrieved passage) pairs        | Improving accuracy/relevance for RAG and search systems                    |

## Getting Started

| I want to...                                | Go to                                    |
| ---------------------------------------------- | ------------------------------------------ |
| See models grouped by function                | [Available Models](available-models.md)   |
| See unit prices by model                       | [Model Pricing List](model-pricing-list.md) |
| Quickly try a model before integrating         | [Playground](playground.md)               |
| Call a model via API                           | [MaaS API](maas-api.md)                    |
