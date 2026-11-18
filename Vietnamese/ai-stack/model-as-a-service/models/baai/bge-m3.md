---
description: "BGE-M3 is a multilingual, multi-function, long-context text embedding model that unifies dense, sparse (lexical), and multi-vector (ColBERT-style) retrieval in a single backbone; it supports >100 languages and up to 8192..."
---

# BGE-M3

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `baai/bge-m3` · Loại: Embedding

BGE-M3 is a multilingual, multi-function, long-context text embedding model that unifies dense, sparse (lexical), and multi-vector (ColBERT-style) retrieval in a single backbone; it supports >100 languages and up to 8192...

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 8K tokens |
| Output tối đa | — tokens |
| Đầu vào | text |
| Đầu ra | embeddings |
| Endpoints | `/v1/embeddings` |

## Tham số hỗ trợ

`encoding_format`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/embeddings \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-m3",
    "input": "Hello"
  }'
```
