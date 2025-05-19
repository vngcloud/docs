# Inference

Tính năng **Inference** giúp bạn triển khai mô hình AI thành một dịch vụ API sẵn sàng sử dụng, phục vụ trực tiếp cho các ứng dụng backend, website, hoặc pipeline phân tích.

**Tổng quan về Inference**

* Deploy mô hình từ **Model Registry** dưới dạng một **REST API endpoint**.
* Hỗ trợ chọn loại máy chủ tính toán (**CPU/GPU**) theo yêu cầu hiệu năng.
* Tự động scale theo lưu lượng request.
* Có thể tích hợp với **AI Gateway** để quản lý bảo mật, rate limit, auth token…

***

## Các bước triển khai Inference

#### **Bước 1: Truy cập giao diện Inference**

1. Đăng nhập vào [VNG Cloud AI Platform](https://aiplatform.console.vngcloud.vn/overview)..
2. Vào **Inference** tại menu bên trái.
3. Nhấn nút **“Create endpoint”**.

#### **Bước 2: Điền thông tin khởi tạo Inference**

| Field             | Mô tả                                                          |
| ----------------- | -------------------------------------------------------------- |
| **Endpoint Name** | Tên endpoint định danh (1–50 ký tự, không chứa ký tự đặc biệt) |
| **Region**        | Khu vực triển khai (hiện tại: `HCM`)                           |
| **Model**         | Chọn model đã được import sẵn trong **Model Registry**         |

#### **Bước 3: Cấu hình tài nguyên và tự động scale**

* **Resource Configuration**

<table><thead><tr><th width="209">Tham số</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Instance Type (CPU / GPU / RAM)</strong></td><td>Chọn loại máy tính chạy model (ví dụ: <code>g1-standard-4x16-1rtx2080ti</code>). Tùy vào model, chọn cấu hình phù hợp với yêu cầu inference</td></tr></tbody></table>

* **Replica Configuration**

<table><thead><tr><th width="294">Tham số</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Min Replica Count</strong></td><td>Số lượng instance tối thiểu luôn sẵn sàng</td></tr><tr><td><strong>Max Replica Count</strong></td><td>Số lượng instance tối đa khi autoscaling</td></tr><tr><td><strong>Auto-scaling Settings (Advanced configuration)</strong></td><td>Hệ thống tự tăng giảm theo các thông số threshold CPU, RAM, GPU Utilization, Response latency.</td></tr></tbody></table>

#### **Bước 4: Tạo và khởi chạy Inference**

* Nhấn **"Create"** để bắt đầu triển khai.
* Quá trình deploy mất vài phút.
* Sau khi hoàn tất, bạn sẽ nhận được thông tin **Endpoint URL để serving.**

***

## Hướng dẫn serving endpoint

Tài liệu này hướng dẫn bạn cách **gọi Inference Endpoint vừa tạo** thông qua việc xác thực bằng Service Account và thực hiện inference chuẩn OpenAI-like API (đặc biệt hữu ích với GenAI models).

### **Bước 1: Tạo Service Account có quyền với AI Platform**

1. Truy cập vào trang quản lý **IAM** trong hệ thống VNG Cloud.
2. Tạo một **Service Account** mới.
3. Gán quyền truy cập **AI Platform** (ví dụ: `aiplatform.viewer`, `aiplatform.user` hoặc cao hơn tùy nhu cầu).
4. Sau khi tạo thành công, bạn sẽ nhận được:
   * `client_id`
   * `client_secret`

> 🔐 Hai thông tin này sẽ được dùng để lấy `access_token` nhằm xác thực khi gọi Inference API.

Tham khảo hướng dẫn tạo Service Account [tại đây](https://docs.vngcloud.vn/vng-cloud-document/vn/identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-service-accounts).

### **Bước 2: Lấy Access Token**

Đầu tiên, mã hóa `client_id` và `client_secret` theo chuẩn Base64 theo định dạng:base64("client\_id:client\_secret")

**Ví dụ**

```sh
echo -n "a5d532c8-38ac-445f-b06c-cd54b2d68f67:1910628f-57b7-42b8-8f9e-e148866fd407" | base64 -w 0

output >> YTVkNTMyYzgtMzhhYy00NDVmLWIwNmMtY2Q1NGIyZDY4ZjY3OjE5MTA2MjhmLTU3YjctNDJiOC04ZjllLWUxNDg4NjZmZDQwNw==
```

**Thực hiện lệnh `curl` để lấy token**

```sh
curl --location 'https://iamapis.vngcloud.vn/accounts-api/v2/auth/token' \
--header 'Authorization: Basic YTVkNTMyYzgtMzhhYy00NDVmLWIwNmMtY2Q1NGIyZDY4ZjY3OjE5MTA2MjhmLTU3YjctNDJiOC04ZjllLWUxNDg4NjZmZDQwNw==' \
--header 'Content-Type: application/json' \
--data '{
"grant_type":"client_credentials",
"scope":"email"
}'
```

**Kết quả trả về**

```sh
{
  "token_type": "Bearer",
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJlckVaZFpkNkRsc21pdjhsMDZIaVB3bHZYWnotLVlGYXlZcVJiczlxc09rIn0",
  "expires_in": 1800,
  "refresh_expires_in": 0
}
```

### Bước 3: Gọi Inference với Access Token

Sau khi đã có `access_token`, bạn có thể gọi API để thực hiện inference theo mẫu sau, inference theo chuẩn của openai.

```sh
curl -X POST "https://inference-aiplatform-hcm.api.vngcloud.vn/v1/<endpoint-id>/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <access_token>" \
  -d '{
    "model": "<model name>",
    "messages": [
      {
        "role": "system",
        "content": "assistant"
      },
      {
        "role": "user",
        "content": "How are you"
      }
    ],
    "temperature": 0.7,
    "max_tokens": 500
}'
```
