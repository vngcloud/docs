# Sử dụng GreenNode CLI để quản lý AgentBase

### Giới thiệu

**GreenNode CLI** (lệnh `grn`) là công cụ dòng lệnh để quản lý tài nguyên GreenNode ngay trên terminal. Với **GreenNode AgentBase**, nhóm lệnh `grn agentbase` cho phép bạn tạo và vận hành trọn vòng đời của agent — Identity, Runtime, Memory, MCP Gateway, Policy và Container Registry — thay vì thao tác qua Portal.

Nhóm lệnh `agentbase` nằm sẵn trong binary `grn` mặc định, không cần build riêng:

```bash
grn agentbase --help
```

Trang reference đầy đủ: [https://greennodehub.github.io/greennode-cli/](https://greennodehub.github.io/greennode-cli/).

CLI là một trong các cách làm việc với AgentBase, bên cạnh [Portal](README.md) và [MCP](su-dung-greennode-mcp-de-quan-ly-agentbase.md). Chọn CLI khi bạn cần thao tác nhanh, lặp lại được, hoặc muốn đưa việc deploy agent vào script tự động hoá và CI/CD.

{% hint style="info" %}
Nhóm lệnh `agentbase` đang được bổ sung dần vào trang reference công khai. Trong lúc chờ, dùng `grn agentbase --help` hoặc `grn agentbase <nhóm> --help` để xem danh sách lệnh và tham số của phiên bản bạn đang cài.
{% endhint %}

---

### 1. Cài đặt

`grn` là một binary duy nhất, không phụ thuộc thư viện ngoài. Tải bản mới nhất cho hệ điều hành của bạn tại [GitHub Releases](https://github.com/GreenNodeHub/greennode-cli/releases).

**macOS**

```bash
# Apple Silicon (M1/M2/M3)
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-darwin-arm64
# Intel
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-darwin-amd64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Linux**

```bash
# x86_64
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-linux-amd64
# ARM64
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-linux-arm64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Windows:** tải `grn-windows-amd64.exe` từ GitHub Releases và thêm vào `PATH`.

**Build từ source** (cần [Go 1.22+](https://go.dev/dl/)):

```bash
git clone https://github.com/GreenNodeHub/greennode-cli.git
cd greennode-cli/go
go build -o grn . && sudo mv grn /usr/local/bin/
```

Kiểm tra: `grn --version`

---

### 2. Cấu hình và xác thực

Nhóm lệnh `agentbase` **dùng chung profile** `~/.greennode` với các nhóm lệnh khác của `grn` (`vks`, `vserver`) — không có file cấu hình riêng. Có 2 chế độ xác thực.

**Machine mode (M2M)** — khuyến nghị cho CI/CD và script:

```bash
grn configure
```

```
GRN Client ID [None]: <your-client-id>
GRN Client Secret [None]: <your-client-secret>
Default region name [HCM-3]:
Default output format [json]:
Project ID (leave blank to auto-detect) [None]:
```

**Client ID** và **Client Secret** lấy tại **GreenNode IAM Portal → Service Accounts** ([hcm-3.console.vngcloud.vn/iam](https://hcm-3.console.vngcloud.vn/iam/)). Để trống **Project ID** thì wizard tự phát hiện.

**User mode (PKCE)** — khuyến nghị khi làm việc trực tiếp trên máy cá nhân:

```bash
grn login      # đăng nhập qua browser
grn logout     # xoá login đã lưu
```

Chế độ đang dùng được quyết định bởi `auth_mode` trong profile (`user` hoặc `machine`). `grn login` chỉ lưu **refresh token** xuống đĩa (`0600`); access token giữ trong bộ nhớ tiến trình và tự refresh trước khi hết hạn.

#### File cấu hình và biến môi trường

Cấu hình lưu tại `~/.greennode/credentials` (quyền `0600`) và `~/.greennode/config`. Bạn có thể ghi đè bằng biến môi trường — biến môi trường luôn ưu tiên hơn file:

| Biến môi trường | Ý nghĩa |
|---|---|
| `GRN_ACCESS_KEY_ID` | Client ID |
| `GRN_SECRET_ACCESS_KEY` | Client Secret |
| `GRN_DEFAULT_REGION` | Region mặc định |
| `GRN_DEFAULT_PROJECT_ID` | Project ID |
| `GRN_PROFILE` | Profile sử dụng (mặc định `default`) |
| `GRN_DEFAULT_OUTPUT` | Định dạng output mặc định |

Với nhiều môi trường, dùng profile: `grn configure --profile staging`, sau đó `grn --profile staging agentbase runtime list`.

#### Chọn môi trường dev / prod

Môi trường được chọn qua `iam_env` trong profile (mặc định `prod`). AgentBase gọi tới `agentbase.api.vngcloud.vn` ở prod và `agentbase.api-dev.vngcloud.tech` ở dev.

```bash
grn configure set iam_env <dev|prod>   # machine mode
grn login --iam-env <dev|prod>         # user mode
grn agentbase context current          # xem environment + endpoint đang active
```

{% hint style="info" %}
Ở **user mode**, `iam_env` gắn với token đã đăng nhập — muốn đổi môi trường phải `grn login --iam-env <env>` lại. Ở **machine mode**, bạn đổi `iam_env` tự do.
{% endhint %}

---

### 3. Các nhóm lệnh AgentBase

Cấu trúc lệnh: `grn agentbase <nhóm> <lệnh> [options]`. Mỗi nhóm ánh xạ tới một service của AgentBase:

| Nhóm lệnh | Quản lý | Trang liên quan |
|---|---|---|
| `context` | Xem environment, endpoint, header và decorator đang active | — |
| `identity` | Workload Identity và Outbound Auth (OAuth2, static API key, delegated), api-key delegate | [Access Control](access-control/README.md) |
| `gateway` | Tạo và quản lý MCP Gateway, access logs, Inbound Auth JWT, private network routes | [MCP Gateway](mcp-governance/mcp-gateway/README.md) |
| `runtime` | Deploy container chạy code agent (image, command, args, env, autoscaling), endpoint, logs, metrics, trace | [Agent Runtime](agent-runtime/README.md) |
| `memory` | Memory container, strategy, session, event và record | [Memory](memory/README.md) |
| `catalog` | Runtime flavor, OpenClaw version và workspace | [OpenClaw](agent-runtime/openclaw/README.md) |
| `policy` | Policy Group, policy, condition operator và decision | [Policy Groups](mcp-governance/policy-groups/README.md) |
| `cr` | Repository, image, artifact và registry credential trên vCR | [Container Registry](container-registry/README.md) |
| `deploy` | Orchestrator gộp `identity` + `memory` + `runtime` (+ `cr`) thành một vòng đời duy nhất | — |

Xem trợ giúp bất cứ lúc nào bằng `grn agentbase <nhóm> --help`.

Mọi lệnh đều nhận `-o` (`--output`) để chọn định dạng kết quả, và `--interactive` để CLI hỏi lần lượt các tham số bắt buộc còn thiếu:

| Giá trị `-o` | Ý nghĩa |
|---|---|
| `table` (mặc định) | Bảng dễ đọc, secret được che |
| `json` | JSON thuần, secret hiển thị đầy đủ (ví dụ để pipe vào `docker login`) |
| `id` | Chỉ in ID — tiện cho script |

{% hint style="warning" %}
`-o json` in secret ra ở dạng rõ (Client Secret, robot account password). Không dùng `-o json` trong log CI công khai hoặc terminal đang share màn hình.
{% endhint %}

---

### 4. Deploy một agent bằng `deploy`

Trong AgentBase, một **agent** là tập tài nguyên dùng chung một **name** làm khoá liên kết: một Identity (luôn có), một Memory container (tuỳ chọn — agent stateless thì bỏ), và một Runtime chạy code agent. Nhóm lệnh `deploy` là orchestrator phía client, gộp các service này lại thành một lifecycle:

| Lệnh | Tác dụng |
|---|---|
| `deploy generate` | In ra manifest mẫu (YAML hoặc JSON) |
| `deploy up` | Áp manifest — tạo tài nguyên nếu chưa có, rồi chờ Runtime về `ACTIVE` |
| `deploy status` | Xem trạng thái của agent trên tất cả service |
| `deploy destroy` | Xoá Runtime và Memory của agent (thêm `--purge` để xoá cả Identity) |

Sinh manifest mẫu rồi điền thông tin:

```bash
grn agentbase deploy generate > agent.yaml
```

```yaml
# name là khoá liên kết dùng chung giữa identity + memory + runtime
# (3-50 ký tự, ^[a-zA-Z0-9_-]+$). identity luôn được tạo.
name: my-agent
description: "A customer-support agent"

identity:
  allowedReturnUrls:
    - https://app.example.com/callback

# memory: TUỲ CHỌN. Bỏ cả block này nếu agent stateless.
# Nếu có, cần ít nhất một strategy (name/type/namespaceTemplate).
memory:
  eventExpiryDuration: 3600
  strategies:
    - name: prefs
      type: USER_PREFERENCE
      namespaceTemplate: "/strategies/USER_PREFERENCE/actors/{actorId}"

runtime:
  image: registry.vngcloud.vn/<your-repo>/my-agent:v1
  imageAuth: auto          # "auto" tự lấy pull credential từ robot account vCR của bạn
  command: [./agent]
  args: [--port, "8080"]
  env: {LOG_LEVEL: info}
  flavorId: agent.small
  autoscaling: {minReplicas: 1, maxReplicas: 3, cpuUtilization: 70, memoryUtilization: 80}
```

Áp manifest, theo dõi, rồi xoá khi không còn dùng:

```bash
grn agentbase deploy up --file agent.yaml
grn agentbase deploy status my-agent
grn agentbase deploy destroy my-agent            # xoá runtime + memory
grn agentbase deploy destroy my-agent --purge    # xoá cả identity
```

`deploy up` là **idempotent** — chạy lại nhiều lần không tạo trùng tài nguyên. `up`, `status` và `destroy` đều tra tài nguyên theo name nên không cần file state.

{% hint style="warning" %}
Khi `deploy up` lỗi giữa đường, CLI **không rollback** các tài nguyên đã tạo. Chạy lại `deploy up` (idempotent) để tiếp tục, hoặc `deploy destroy` để dọn sạch rồi làm lại. `deploy destroy --purge` xoá cả Identity và **không thể hoàn tác**.
{% endhint %}

---

### 5. Xử lý sự cố thường gặp

| Triệu chứng | Cách xử lý |
|---|---|
| `authentication failed: ...` | Chạy `grn configure` (machine) hoặc `grn login` (user). Kiểm tra environment và profile bằng `grn agentbase context current` |
| Lỗi 404 khi tra tài nguyên | `deploy` và `status` tra theo name — sai name hoặc tài nguyên nằm ở môi trường khác đều báo là không tồn tại |
| Runtime treo ở trạng thái `CREATING` | Runtime hội tụ không đồng bộ — dùng `grn agentbase runtime wait <id>` hoặc `deploy status <name>` để chờ |
| Đổi dev ↔ prod không có tác dụng | Machine mode: `grn configure set iam_env <env>`. User mode: phải `grn login --iam-env <env>` lại vì token gắn với môi trường |

---

Nếu gặp vấn đề, liên hệ GreenNode qua email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Trung tâm hỗ trợ: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
