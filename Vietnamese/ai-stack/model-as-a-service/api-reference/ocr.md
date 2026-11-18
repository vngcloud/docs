---
description: "OCR xử lý tài liệu — upload file và xử lý bất đồng bộ — nên có bộ endpoint riêng thay vì các endpoint tương thích OpenAI."
---

# OCR API

## Header

| Header | Bắt buộc | Giá trị |
| --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` |
| `portal-user-id` | **Bắt buộc** | Portal user ID của bạn, cùng giá trị dùng trong đường dẫn URL. |

## Gửi tài liệu

**POST** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`

Body là `multipart/form-data`:

| Trường | Bắt buộc | Giá trị nhận | Mô tả |
| --- | --- | --- | --- |
| `flow` | **Bắt buộc** | `single` · `<FLOW_ID>` | `single` chạy OCR cho một tài liệu; flow ID chạy một luồng tài liệu. |
| `doc_type` | Bắt buộc khi `flow=single` | `<DOC_TYPE>` | Loại tài liệu cần trích xuất. |
| `file_type` | **Bắt buộc** | `PDF` · `IMAGE` | Loại file upload. |
| `file` | **Bắt buộc** | nhị phân | File cần xử lý. |

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```
{% endcode %}

Response gồm `request_id` (dùng để lấy kết quả) và có thể có `file_ids` (dùng để tải ảnh kết quả).

## Lấy kết quả

**GET** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

{% hint style="info" %}
**Chưa có dữ liệu?**

Tài liệu đang được xử lý. Chờ 2–5 giây rồi gọi lại (polling). Nếu mãi không có kết quả, gửi `request_id` cho bộ phận hỗ trợ.
{% endhint %}

## Các endpoint kết quả khác

`document_id` lấy từ response của bước Lấy kết quả.

| Dữ liệu | Method và đường dẫn (sau `…/ocr/ingest`) |
| --- | --- |
| Bảng | `GET /table/<request_id>/<document_id>` |
| Chữ ký | `GET /signature/<request_id>/<document_id>` |
| Con dấu | `GET /stamp/<request_id>/<document_id>` |
| Ảnh kết quả | `GET /file/<request_id>/<file_id>` |

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

## Xử lý lỗi

| Hiện tượng | Nguyên nhân |
| --- | --- |
| `401 Unauthorized` | Thiếu `Authorization` (`missing api key`) hoặc API key sai (`unknown api key`). |
| `403 Forbidden` | User ID trong đường dẫn khác chủ sở hữu API key (`tenant mismatch`). |
| `400 Bad Request` / 4xx | Thiếu trường bắt buộc (`flow`, `file_type`, `file`, …) hoặc `doc_type` không hợp lệ. |
| Polling không có kết quả | Gửi `request_id`, thời điểm gọi và file mẫu cho bộ phận hỗ trợ. |
