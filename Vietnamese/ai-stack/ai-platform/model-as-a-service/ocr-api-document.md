---
description: Tài liệu này hướng dẫn cách sử dụng OCR API
---

# OCR API Document

## OCR API Document

Tài liệu này hướng dẫn cách sử dụng OCR API

### Submit OCR (upload file để tạo request)

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`
* **Body**: `multipart/form-data`
  * `flow` (required)
    * `single`: OCR 1 tài liệu
    * hoặc `<FLOW_ID>`: OCR theo bộ tài liệu (nếu bạn được cấp flow)
  * `doc_type` (required nếu `flow=single`): `<DOC_TYPE>`
  * `file_type` (required): `PDF` hoặc `IMAGE`
  * `file` (required): file cần OCR

#### Ví dụ

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```

Response sẽ chứa:

* `request_id`: dùng để lấy kết quả
* (tuỳ trường hợp) `file_ids`: dùng để tải ảnh kết quả

***

### Get OCR Result (dùng `request_id` để lấy text/data)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`

#### Ví dụ

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Nếu gọi ra chưa thấy data?

Điều này bình thường vì OCR đang xử lý.

* Đợi 2–5 giây và gọi lại API này (polling).
* Nếu quá thời gian timeout mà vẫn không có dữ liệu, gửi `request_id` cho team support để kiểm tra.

***

### Các API lấy thêm dữ liệu khác của OCR (tuỳ nhu cầu)

### Lấy bảng (TABLE)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Lấy kết quả chữ ký

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

note: document\_id nằm trong response của Get OCR Result

### Lấy kết quả con dấu

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Tải ảnh kết quả

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

***

### API bổ trợ

### So sánh 2 ảnh chữ ký

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/compare/signature`
* **Body**: `multipart/form-data`
  * `doc_type`: "COMPARE\_SIGNATURE"
  * `file_type`: `IMAGE` hoặc `PDF`
  * `compare_file_type`: `IMAGE` hoặc `PDF`
  * `file`: file chữ ký 1
  * `compare_file`: file chữ ký 2

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/compare/signature' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'doc_type="<COMPARE_SIGNATURE>"' \
  --form 'file_type="IMAGE"' \
  --form 'compare_file_type="IMAGE"' \
  --form 'file=@"<SIGNATURE_1_PATH>"' \
  --form 'compare_file=@"<SIGNATURE_2_PATH>"'
```

### Chuyển ảnh sang file Word (.docx)

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/image2docs`
* **Response**: trả về file `.docx`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/image2docs' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'doc_type="<IMAGE_TO_DOC>"' \
  --form 'file_type="IMAGE"' \
  --form 'file=@"<IMAGE_PATH>"' \
  --output output.docx
```

### Kiểm tra gian lận tài liệu

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/document-frauds`
* **Body**: `multipart/form-data`
  * `doc_type`: `<DOCUMENT_FRAUD>`
  * `file_type`: `IMAGE`
  * `file`: file ảnh

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/document-frauds' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'doc_type="<DOCUMENT_FRAUD>"' \
  --form 'file_type="IMAGE"' \
  --form 'file=@"<IMAGE_PATH>"'
```

***

### Troubleshooting nhanh

* `403 Forbidden`:
  * Thiếu/sai `Authorization` hoặc không có quyền.
* `400 Bad Request` / `4XX`:
  * Thiếu field bắt buộc (`flow`, `file_type`, `file`, ...)
  * `doc_type` không đúng theo cấu hình.
* Polling mãi chưa ra kết quả:
  * Gửi `request_id` + thời điểm gọi + file mẫu (nếu được) cho team support.
