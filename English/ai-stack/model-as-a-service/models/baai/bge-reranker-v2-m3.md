---
description: "BGE-Reranker-v2-m3 is a lightweight multilingual cross-encoder reranker from BAAI, built on the BGE-M3 (XLM-RoBERTa) backbone. Given a query and candidate documents it outputs a relevance score for each pair, used..."
---

# BGE Reranker v2 m3

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `baai/bge-reranker-v2-m3` · Type: Rerank

BGE-Reranker-v2-m3 is a lightweight multilingual cross-encoder reranker from BAAI, built on the BGE-M3 (XLM-RoBERTa) backbone. Given a query and candidate documents it outputs a relevance score for each pair, used...

## Specs

| Spec | Value |
| --- | --- |
| Context length | 8K tokens |
| Max output | — tokens |
| Input | text |
| Output | rerank |
| Endpoints | `/v1/rerank` |

## Supported parameters

`top_n`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-reranker-v2-m3",
    "query": "GreenNode",
    "documents": ["GreenNode MaaS", "Other"]
  }'
```
