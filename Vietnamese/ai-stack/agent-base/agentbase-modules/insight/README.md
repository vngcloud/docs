# Insight

> Giám sát và gỡ lỗi các agent đã triển khai bằng runtime log, endpoint log và các chỉ số tài nguyên (CPU/RAM). Tất cả các thao tác Insight sử dụng Runtime API.

---


## Tổng quan (Overview)

AgentBase Insight cung cấp ba nguồn dữ liệu chỉ đọc:

| Nguồn dữ liệu           | Mô tả                                    | API                                                         |
| ----------------------- | ----------------------------------------- | ----------------------------------------------------------- |
| **Runtime Log**   | stdout/stderr từ container của tất cả replica | `POST /agent-runtimes/{id}/logs`                          |
| **Endpoint Log**  | Log thuộc phạm vi một endpoint cụ thể    | `POST /agent-runtimes/{id}/endpoints/{endpointId}/logs`   |
| **Metrics**       | Mức sử dụng CPU và RAM tại thời điểm hiện tại | `GET /agent-runtimes/{id}/endpoints/{endpointId}/metrics` |

---

## Điều kiện cần (Prerequisites)

Bạn cần runtime ID và (đối với endpoint log/metrics) endpoint ID.

```bash
TOKEN=$(bash .claude/skills/agentbase/scripts/get_token.sh)

# List runtimes to get IDs
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {id, name, status}'

# Get endpoints for a runtime
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints?page=1&size=10" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {id, name, url, status}'
```

---

## Runtime Log

Lấy log từ container của tất cả replica trong một runtime. Sử dụng phân trang dựa trên offset (`from`/`limit`).

### Portal (GUI)

1. Mở https://aiplatform.console.vngcloud.vn/runtime
2. Mở trang chi tiết runtime → tab **"Monitor"** → nhấn vào một endpoint → phần **"Log"**

![1774581394627](../image/07-insight/1774581394627.png)

---

### RESTful API

> **Điều kiện cần (Prerequisites):** Tất cả các ví dụ API dưới đây sử dụng `$TOKEN` — một IAM bearer token. Xem [Cấu hình xác thực](../getting-started.md#configure-authentication) để biết cách lấy token.

```bash
RUNTIME_ID="<your-runtime-id>"

# Fetch first 100 log lines
curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"from": 0, "limit": 100}' | jq .
```

**Phản hồi:**

```json
{
  "totalCount": 342,
  "logs": [
    "2026-03-18T09:01:00Z INFO  Starting agent on port 8080",
    "2026-03-18T09:01:02Z INFO  Health check passed",
    "2026-03-18T09:05:33Z INFO  Received request"
  ]
}
```

**Phân trang với `from`:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"from": 100, "limit": 100}' | jq .
```

**Lấy toàn bộ log:**

```bash
OFFSET=0; LIMIT=500
while true; do
  RESULT=$(curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
    -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
    -d "{\"from\": $OFFSET, \"limit\": $LIMIT}")
  TOTAL=$(echo "$RESULT" | jq '.totalCount')
  echo "$RESULT" | jq -r '.logs[]'
  OFFSET=$((OFFSET + LIMIT))
  [ "$OFFSET" -ge "$TOTAL" ] && break
done
```

**Lọc lỗi trên máy cục bộ:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"from": 0, "limit": 1000}' | jq -r '.logs[]' | grep -i "error\|traceback\|exception\|failed"
```

**Giới hạn:** `from` tối đa = 5000, `limit` tối đa = 1000

---

## Chỉ số tài nguyên (CPU / RAM)

Lấy mức sử dụng CPU và RAM tại thời điểm hiện tại cho một endpoint cụ thể.

### Portal (GUI)

Mở trang chi tiết runtime → tab **"Monitor"** → nhấn vào một endpoint → phần **"Metrics"**

![1774581238335](../image/07-insight/1774581238335.png)

---

### RESTful API

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/metrics" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Các trường phản hồi:** `cpuCores` (double), `memoryBytes` (int64)

```json
{
  "cpuCores": 0.42,
  "memoryBytes": 536870912
}
```

**Chuyển đổi sang dạng dễ đọc:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/metrics" \
  -H "Authorization: Bearer $TOKEN" | jq '{
    cpu_cores: .cpuCores,
    memory_mb: (.memoryBytes / 1048576 | floor),
    memory_gb: (.memoryBytes / 1073741824 | . * 100 | floor / 100)
  }'
```

---

### Pseudo-Tailing (Mẫu polling)

Log streaming không được hỗ trợ — sử dụng polling để mô phỏng tailing:

```bash
OFFSET=0
while true; do
  RESULT=$(curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
    -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
    -d "{\"from\": $OFFSET, \"limit\": 50}")
  COUNT=$(echo "$RESULT" | jq '.totalCount')
  echo "$RESULT" | jq -r '.logs[]'
  OFFSET=$COUNT
  sleep 5
done
```

> **Lưu ý:** Polling thường xuyên tạo ra nhiều lời gọi API. Tránh polling trong thời gian dài.

---

## Hướng dẫn phân tích Log (Log Analysis Guide)

### Các mẫu lỗi phổ biến (Common Error Signatures)

| Mẫu                                             | Ý nghĩa                      | Bước tiếp theo                                |
| ------------------------------------------------ | ----------------------------- | --------------------------------------------- |
| `Traceback (most recent call last)`            | Ngoại lệ Python              | Đọc dòng cuối cùng để biết lỗi thực tế       |
| `ModuleNotFoundError: No module named '...'`   | Thiếu dependency              | Thêm vào `requirements.txt` và build lại image |
| `ImportError: cannot import name '...'`        | Sai phiên bản package         | Kiểm tra tính tương thích phiên bản package   |
| `ConnectionRefusedError` / `ConnectionError` | Không thể kết nối dịch vụ bên ngoài | Kiểm tra URL dịch vụ và credential xác thực   |
| `401 Unauthorized` / `403 Forbidden`         | Lỗi xác thực                 | Kiểm tra IAM token và cấu hình xác thực đầu ra |
| `OSError: [Errno 98] Address already in use`   | Xung đột cổng 8080           | Đảm bảo chỉ một tiến trình bind cổng 8080    |
| `MemoryError` / `Killed`                     | Hết bộ nhớ                    | Nâng cấp flavor hoặc tối ưu hóa sử dụng bộ nhớ |
| `TimeoutError` / `ReadTimeout`               | API bên ngoài hết thời gian chờ | Tăng timeout, kiểm tra tình trạng LLM endpoint |
| `Health check failed`                          | `/health` không trả về 200  | Sửa health endpoint                          |

---

### Liên hệ Log với Metrics (Correlating Logs with Metrics)

| CPU       | RAM      | Chẩn đoán                                                                   |
| --------- | -------- | ---------------------------------------------------------------------------- |
| Cao       | Bình thường | Tải nặng CPU — scale up hoặc tối ưu hóa                                    |
| Bình thường | Cao    | Rò rỉ bộ nhớ hoặc cấu trúc dữ liệu lớn — scale up hoặc sửa rò rỉ        |
| Cả hai cao | —      | Cạn kiệt tài nguyên — scale up flavor                                      |
| Cả hai thấp | —     | Nghẽn cổ chai bên ngoài (độ trễ LLM API, mạng) — thêm đo thời gian request trong log |

---

## Tính năng được hỗ trợ (What's Supported)

- **Lọc log theo khoảng thời gian** — Lọc log theo một khoảng thời gian cụ thể (timestamp bắt đầu/kết thúc), giúp bạn thu hẹp chính xác thời điểm sự cố xảy ra mà không cần lấy toàn bộ lịch sử log.
- **Tìm kiếm từ khóa trong log** — Tìm kiếm log theo từ khóa hoặc cụm từ trực tiếp trong truy vấn, chỉ trả về các mục khớp mà không cần grep cục bộ sau khi lấy dữ liệu.
- **Metrics lịch sử** — Truy vấn mức sử dụng CPU và RAM trong một khoảng thời gian, không chỉ ảnh chụp tại thời điểm hiện tại. Hữu ích để phát hiện xu hướng tài nguyên, đột biến và các mẫu dẫn đến sự cố.

---

## Xử lý sự cố (Troubleshooting)

| Lỗi                   | Nguyên nhân                  | Cách khắc phục                                    |
| -------------------- | ---------------------------- | ------------------------------------------------- |
| 401 Unauthorized     | IAM token hết hạn            | Lấy lại token                                     |
| 404 Not Found        | Sai runtime hoặc endpoint ID | Kiểm tra ID bằng các thao tác liệt kê            |
| Log trống            | Container chưa bao giờ khởi động | Kiểm tra trạng thái runtime; xác nhận image pull thành công |
| Log bị cắt tại 5000  | Đạt giới hạn offset tối đa  | Log cũ hơn 5000 mục không thể truy cập           |

---

