# OCR API Usage Guide

This document provides instructions on how to use the OCR API.

### Submit OCR (upload file to create a request)

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`
* **Body**: `multipart/form-data`
  * `flow` (required)
    * `single`: OCR for a single document
    * or`<FLOW_ID>`: OCR for a document workflow (if provided)
  * `doc_type` (required if `flow=single`): `<DOC_TYPE>`
  * `file_type` (required): `PDF` or `IMAGE`
  * `file` (required): file to be processed by OCR

#### Example

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```

Response will include:

* `request_id`: used to retrieve results
* (optional) `file_ids`: used to download result images

***

### Get OCR Result (use `request_id` to retrieve text/data)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`

#### Example

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### What if no data is returned yet?

This is normal because OCR processing is still in progress.

* Wait 2–5 seconds and call the API again (polling).
* If the timeout is exceeded and no data is returned, send the request\_id to the support team for investigation.

***

### Additional OCR Data APIs (optional, depending on needs)

### Get Table Data(TABLE)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Get Signature Results

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

Note: document\_id is included in the response of Get OCR Result.

### Get Stamp Results

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Download Result Images

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

***

### Quick Troubleshooting

* `403 Forbidden`:
  * Missing/invalid `Authorization` or permission denied.
* `400 Bad Request` / `4XX`:
  * Missing required fields (`flow`, `file_type`, `file`, ...)
  * Invalid `doc_type` configuration..
* Polling does not return results:
  * Provide `request_id` + timestamp + sample file (if possible) to the support team for further investigation.
