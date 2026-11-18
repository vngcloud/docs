---
description: "BGE-M3 is a multilingual, multi-function, long-context text embedding model that unifies dense, sparse (lexical), and multi-vector (ColBERT-style) retrieval in a single backbone; it supports >100 languages and up to 8192..."
---

# BGE-M3

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `baai/bge-m3` · Type: Embedding

BGE-M3 is a multilingual, multi-function, long-context text embedding model that unifies dense, sparse (lexical), and multi-vector (ColBERT-style) retrieval in a single backbone; it supports >100 languages and up to 8192...

## Specs

| Spec | Value |
| --- | --- |
| Context length | 8K tokens |
| Max output | — tokens |
| Input | text |
| Output | embeddings |
| Endpoints | `/v1/embeddings` |

## Supported parameters

`encoding_format`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/embeddings \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-m3",
    "input": "Hello"
  }'
```
