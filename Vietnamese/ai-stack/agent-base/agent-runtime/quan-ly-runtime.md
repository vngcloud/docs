# Quản lý Runtime

> Hướng dẫn dừng, khởi động, cập nhật, quản lý Endpoint, rollback và xóa Agent Runtime.

---

## Điều kiện cần

- Ít nhất 1 Runtime đã tạo
- Vai trò Root hoặc Admin

---

## Dừng Runtime

Dừng Runtime để tiết kiệm chi phí tính toán. Cấu hình, Endpoint và logs được giữ nguyên.

**Bước 1:** Mở **Agent Runtime** → tìm Runtime cần dừng

**Bước 2:** Nhấp **Stop** → xác nhận

{% hint style="warning" %}
Trong khi Runtime ở trạng thái `STOPPED`, mọi request đến Endpoint sẽ trả về lỗi cho đến khi Runtime được khởi động lại.
{% endhint %}

---

## Khởi động Runtime

**Bước 1:** Mở **Agent Runtime** → tìm Runtime ở trạng thái `STOPPED`

**Bước 2:** Nhấp **Start** → Runtime chuyển qua `STARTING` → `ACTIVE`

---

## Cập nhật Runtime / Triển khai phiên bản mới

Mỗi lần cập nhật tạo ra một **Version** bất biến mới. Endpoint DEFAULT tự động trỏ đến phiên bản mới nhất — phiên bản cũ tiếp tục phục vụ traffic cho đến khi deployment hoàn tất.

**Cấu trúc Runtime sau khi có nhiều phiên bản:**

```
Runtime: my-order-agent
│
├── Versions
│   ├── Version 1  (image: my-agent:v1.0.0)
│   └── Version 2  (image: my-agent:v2.0.0)  ← latest
│
├── Endpoints
│   ├── DEFAULT  → https://<default-url>   (tự động trỏ đến phiên bản mới nhất)
│   └── canary   → https://<canary-url>    (ghim vào Version 1)
│
└── Autoscaling: min=1, max=3, CPU threshold=50%
```

### Qua Portal

**Bước 1:** Mở Runtime Detail → nhấp **Edit**

**Bước 2:** Thay đổi Image URL, Flavor, autoscaling hoặc biến môi trường → **Save**

### Qua API

> Lưu ý: Tất cả các trường (trừ `imageAuth`) là bắt buộc trong body PATCH.

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "Production order agent v2",
    "imageUrl": "vcr.vngcloud.vn/<repo-backendName>/my-agent:v2.0.0",
    "imageAuth": {
      "enabled": true,
      "username": "<robot-backendName>",
      "password": "<robot-secret>"
    },
    "command": [],
    "args": [],
    "environmentVariables": {"LOG_LEVEL": "info"},
    "flavorId": "1x1-general",
    "autoscaling": {
      "minReplicas": 1,
      "maxReplicas": 3,
      "cpuUtilization": 50,
      "memoryUtilization": 50
    }
  }' | jq .
```

---

## Quản lý Endpoint

Mỗi Runtime có một Endpoint **DEFAULT** được tạo tự động. Bạn có thể tạo thêm Endpoint ghim vào phiên bản cụ thể (canary, staging...).

### Qua Portal

**Xem danh sách Endpoint:** Mở Runtime Detail → tab **Endpoints**

![Runtime detail — Endpoints tab](../../../.gitbook/assets/1774594267224.png)

**Tạo Endpoint mới:**

1. Tab **Endpoints** → nhấp **Create Endpoint**
2. Điền **Name** và chọn **Version** → **Create**

**Đổi Version của Endpoint:**

1. Tab **Endpoints** → nhấp vào endpoint → **Edit**
2. Chọn **Version** mới → **Save**

### Qua API

**Xem danh sách Endpoint:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

Các trường trả về: `id`, `agentRuntimeId`, `name`, `version`, `url`, `status`, `createdAt`, `updatedAt`

**Tạo Endpoint mới:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "canary", "version": 2}' | jq .
```

**Cập nhật Version của Endpoint:**

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID?version=3" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xóa Endpoint:**

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

## Xem phiên bản và Rollback

Mỗi lần cập nhật tạo một Version bất biến mới. Để rollback, trỏ Endpoint DEFAULT về một phiên bản cũ hơn.

### Qua Portal

Mở Runtime Detail → tab **Versions**

![Runtime detail — Versions tab](../../../.gitbook/assets/1774594455831.png)

### Qua API

**Xem danh sách phiên bản:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/versions?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

Các trường trả về: `agentRuntimeId`, `version` (số nguyên), `imageUrl`, `flavorId`, `autoscaling`, `createdAt`

**Rollback về phiên bản cũ:**

```bash
ENDPOINT_ID=$(curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints?page=1&size=10" \
  -H "Authorization: Bearer $TOKEN" | jq -r '.listData[] | select(.name=="DEFAULT") | .id')

curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID?version=1" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

---

## Xóa Runtime

{% hint style="warning" %}
Xóa Runtime là **không thể hoàn tác**. Tất cả phiên bản, Endpoint và logs sẽ bị xóa vĩnh viễn.
{% endhint %}

### Qua Portal

**Bước 1:** Mở **Agent Runtime** → tìm Runtime cần xóa

**Bước 2:** Nhấp **Delete** → xem lại cảnh báo → xác nhận

### Qua API

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

## Đặt lại Service Account

Nếu IAM service account credentials bị thay đổi hoặc thu hồi, dùng lệnh này để khôi phục Runtime:

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/reset-service-account" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

{% hint style="warning" %}
Lệnh này tạo lại `GREENNODE_CLIENT_ID` và `GREENNODE_CLIENT_SECRET`. Runtime sẽ khởi động lại với credential mới.
{% endhint %}

---

## Kết quả

| Tôi muốn... | Đến |
|---|---|
| Xem logs và metrics | [Insight](logs-va-metrics.md) |
| Cấu hình MCP Gateway | [MCP Governance](../mcp-governance/README.md) |