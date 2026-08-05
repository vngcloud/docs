# Sử dụng GreenNode MCP để quản lý AgentBase

### Giới thiệu

**AgentBase MCP** giúp AI assistant (Claude Desktop, Claude Code, Cursor, Windsurf, hoặc bất kỳ MCP client nào) thao tác trực tiếp với **GreenNode AgentBase** bằng ngôn ngữ tự nhiên — liệt kê Runtime, tạo MCP Gateway, tra Policy, xem Memory — mà không cần nhớ cú pháp lệnh hay click qua Portal.

AgentBase MCP là máy chủ triển khai theo chuẩn [Model Context Protocol](https://modelcontextprotocol.io/). Repo: [https://github.com/vngcloud/greennode-agentbase-mcp](https://github.com/vngcloud/greennode-agentbase-mcp)

Điểm khác biệt so với một MCP server thông thường: thay vì expose hàng trăm tool tương ứng từng API, AgentBase MCP chỉ expose **3 meta-tool** — `list_servers`, `search_tools`, `execute`. AI assistant tự tìm operation cần dùng rồi gọi, nên context của client luôn gọn dù AgentBase có bao nhiêu API.

MCP là một trong các cách làm việc với AgentBase, bên cạnh [Portal](README.md) và [CLI](su-dung-greennode-cli-de-quan-ly-agentbase.md). Chọn MCP khi muốn để AI assistant tự tra cứu tài nguyên, gợi ý cấu hình và thực hiện thao tác thay bạn.

{% hint style="info" %}
AgentBase MCP hiện chỉ hỗ trợ môi trường **prod** — các service đứng sau `agentbase.api.vngcloud.vn`.
{% endhint %}

---

### 1. Chuẩn bị

Bạn cần 2 thứ trước khi cấu hình bất kỳ client nào:

| Yêu cầu | Chi tiết |
|---|---|
| **Bearer token** | Token IAM Service Account, đặt vào biến môi trường `GREENNODE_MCP_TOKEN`. Bắt buộc cho cả 2 cách kết nối |
| **Node.js ≥ 20** | Chỉ cần cho cách chạy local (stdio). Cách kết nối HTTP không cần cài gì trên máy |

Token được mint từ **Client ID** và **Client Secret** của Service Account (lấy tại **GreenNode IAM Portal → Service Accounts**):

```bash
export GREENNODE_MCP_TOKEN=$(curl -s -X POST \
  https://iam.api.vngcloud.vn/accounts-api/v2/auth/token \
  -u "$GREENNODE_CLIENT_ID:$GREENNODE_CLIENT_SECRET" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=client_credentials" | jq -r .access_token)
```

{% hint style="warning" %}
`GREENNODE_MCP_TOKEN` là JWT ngắn hạn (khoảng **30 phút**) và có quyền thao tác thật trên tài nguyên AgentBase — coi như password. Không commit vào git, không paste vào file cấu hình dùng chung. Các mẫu cấu hình bên dưới tham chiếu token qua biến môi trường để giá trị không nằm trong file. Khi token hết hạn, mọi lệnh trả về `401` — xem mục [5. Xoay token](#id-5-xoay-token).
{% endhint %}

---

### 2. Hai cách kết nối

| Cách | Cơ chế | Client phù hợp |
|---|---|---|
| **Local stdio** | Client tự spawn server dưới dạng tiến trình con trên máy bạn | Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Roo Code |
| **Remote HTTP** | Client gọi thẳng tới MCP Gateway của AgentBase qua HTTPS, không cài gì trên máy | Claude.ai (web) và mọi client hỗ trợ Streamable HTTP |

Chọn **local stdio** khi bạn kiểm soát được máy chạy và muốn thử nghiệm nhanh. Chọn **remote HTTP** khi không thể hoặc không muốn chạy server cục bộ — Gateway đã bật Inbound Auth theo IAM và ghi access log tập trung.

---

### 3. Cài đặt server cho cách local stdio

```bash
git clone https://github.com/vngcloud/greennode-agentbase-mcp.git
cd greennode-agentbase-mcp
npm install

export GREENNODE_MCP_TOKEN="<your-token>"
```

Kiểm tra server chạy được — lệnh sẽ in banner rồi chờ input, nhấn `Ctrl-C` để thoát:

```bash
npx tsx src/index.ts
```

Server đọc các biến môi trường sau (đều có giá trị mặc định, thường không cần đổi):

| Biến môi trường | Mặc định | Ý nghĩa |
|---|---|---|
| `GREENNODE_MCP_TOKEN` | — | Bearer token dùng để gọi các service AgentBase |
| `TOKEN_ENV` | `GREENNODE_MCP_TOKEN` | Đổi tên biến chứa token, nếu bạn muốn dùng tên khác |
| `TRANSPORT` | `stdio` | `stdio` hoặc `http` |
| `PORT` | `8080` | Port lắng nghe khi `TRANSPORT=http` |
| `MAX_RESPONSE_BYTES` | `25000` | Ngưỡng cắt response để không làm tràn context của client |
| `SEARCH_LIMIT_DEFAULT` | `5` | Số kết quả mặc định của `search_tools` |

{% hint style="info" %}
Cách stdio cần clone repo vì server nạp registry operation dựng sẵn (`registry.generated.json`) lúc khởi động, và file này đi kèm source. Endpoint HTTP đã có registry trong image nên không cần clone.
{% endhint %}

---

### 4. Kết nối MCP client

#### Claude Desktop

Mở (hoặc tạo) file cấu hình MCP:

* macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
* Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "agentbase": {
      "command": "npx",
      "args": ["tsx", "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      }
    }
  }
}
```

Thoát hẳn Claude Desktop (không chỉ đóng cửa sổ) rồi mở lại. Trong chat mới, `agentbase` sẽ xuất hiện trong danh sách MCP server đã kết nối.

{% hint style="warning" %}
Claude Desktop khởi chạy từ working directory khác terminal của bạn, nên `args` và `cwd` phải là **đường dẫn tuyệt đối**. Dùng đường dẫn tương đối, server sẽ không khởi động được.
{% endhint %}

#### Claude Code

Cách nhanh nhất — chạy trong thư mục repo:

```bash
claude mcp add agentbase \
  -e GREENNODE_MCP_TOKEN="<your-token>" \
  -- npx tsx src/index.ts
```

Hoặc thêm trực tiếp vào `~/.claude.json`:

```json
{
  "mcpServers": {
    "agentbase": {
      "type": "stdio",
      "command": "npx",
      "args": ["tsx", "src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      }
    }
  }
}
```

Khởi động lại Claude Code, rồi chạy `/mcp` trong session để xác nhận `agentbase` đã kết nối với 3 tool.

#### Cursor và Windsurf

Cả hai dùng cùng cấu hình như Claude Desktop, chỉ khác vị trí file:

* Cursor: **Settings → Cursor Settings → MCP → Add new MCP server**, hoặc sửa `~/.cursor/mcp.json`
* Windsurf: **Settings → MCP Servers**, hoặc sửa `~/.codeium/windsurf/mcp_config.json`

#### Cline và Roo Code

* Cline: mở panel Cline → icon **MCP** → **Edit MCP Settings** (`~/.cline/mcp_settings.json`)
* Roo Code: **Settings → MCP Servers → Edit** (`~/.roo/mcp_settings.json`)

Cấu hình giống trên, thêm 2 field riêng của extension:

```json
{
  "mcpServers": {
    "agentbase": {
      "command": "npx",
      "args": ["tsx", "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      },
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

Mảng `alwaysAllow` cho phép duyệt trước một số tool để extension không hỏi lại mỗi lần gọi. Thêm `"list_servers"` và `"search_tools"` cho các luồng chỉ đọc, nhưng nên để `"execute"` vẫn hỏi vì tool này thay đổi tài nguyên thật.

#### Claude.ai và các client HTTP

Không cần clone repo. Thêm một MCP server dạng HTTP trỏ tới endpoint Gateway, kèm header `Authorization`:

```json
{
  "mcpServers": {
    "agentbase": {
      "type": "http",
      "url": "https://<agentbase-mcp-gateway-endpoint>/agentbase_mcp/mcp",
      "headers": {
        "Authorization": "Bearer ${GREENNODE_MCP_TOKEN}"
      }
    }
  }
}
```

Với Claude.ai bản web, vào **Settings → Connectors → Add custom connector** và điền URL cùng header Bearer. Connector chạy phía server nên token được lưu tại Anthropic — dùng token cấp riêng cho mục đích này nếu bạn quan tâm điểm đó.

{% hint style="info" %}
Endpoint Gateway được cấp khi tính năng được bật cho project của bạn. Liên hệ [support@greennode.ai](mailto:support@greennode.ai) để nhận endpoint chính xác.
{% endhint %}

---

### 5. Xoay token

Client stdio đọc token **tại thời điểm spawn** và giữ nguyên giá trị đó, nên một server chạy lâu sẽ sống lâu hơn token. Repo có sẵn `scripts/mcp-launch.sh` — script này mint token mới rồi `exec` server, nên mỗi lần client spawn lại là token tự động được làm mới. Trỏ client vào script thay vì `npx tsx`:

```json
"command": "bash",
"args": ["/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/scripts/mcp-launch.sh"]
```

Script cần `GREENNODE_CLIENT_ID` và `GREENNODE_CLIENT_SECRET` có trong môi trường. Mỗi client có một cách buộc spawn lại khác nhau:

| Client | Cách spawn lại server |
|---|---|
| Claude Desktop | Thoát hẳn ứng dụng rồi mở lại |
| Claude Code | Chạy `/mcp` rồi reconnect server `agentbase` |
| Cursor / Windsurf | Nhấn **Restart** cạnh server `agentbase` trong panel MCP |
| Cline / Roo Code | Restart server `agentbase` trong panel MCP của extension |
| Claude.ai (HTTP) | Không tự xoay được — mint token mới và cập nhật lại connector |

Nếu chỉ có token tĩnh mà không có Client Secret trên máy, bỏ qua script và `export GREENNODE_MCP_TOKEN` lại trước khi spawn lại client.

---

### 6. Ba meta-tool

Mọi tương tác đều theo một luồng 3 bước: `list_servers` (định hướng) → `search_tools` (tìm operation) → `execute` (chạy).

| Tool | Tham số | Tác dụng |
|---|---|---|
| `list_servers` | — | Liệt kê các service AgentBase khả dụng kèm số lượng operation và tag. Gọi đầu tiên để định hướng |
| `search_tools` | `query`, `server` (tuỳ chọn), `limit` (tối đa 25) | Tìm operation theo ý định bằng ngôn ngữ tự nhiên. Trả về kết quả kèm luôn input schema đầy đủ, dùng được ngay cho `execute` |
| `execute` | `id`, `args`, `fields` (tuỳ chọn) | Chạy operation theo `id` lấy từ `search_tools`. `fields` là biểu thức JMESPath để chiếu bớt response cho gọn |

`list_servers` trả về 6 service:

| Service | Phạm vi |
|---|---|
| `runtime` | Runtime chạy code agent, endpoint, logs, metrics, trace |
| `gateway` | MCP Gateway, Inbound Auth, access logs, private network |
| `identity` | Workload Identity và Outbound Auth |
| `memory` | Memory container, strategy, session, event, record |
| `policy` | Policy Group, policy và decision |
| `cr` | Repository, image và artifact trên vCR |

{% hint style="warning" %}
Luôn lấy `id` từ kết quả `search_tools`, đừng tự đoán. Operation id phản chiếu `operationId` trong OpenAPI spec gốc nên không phải lúc nào cũng đẹp (`runtime.list_1`, `runtime.get`, `runtime.listEndpoints`…) và có thể thay đổi giữa các phiên bản spec.
{% endhint %}

---

### Ví dụ nhanh: nhờ AI assistant deploy một agent

Sau khi kết nối xong, chỉ cần hỏi AI assistant bằng ngôn ngữ tự nhiên:

```
Liệt kê các Agent Runtime đang chạy trong project của tôi,
rồi cho tôi biết runtime nào đang dùng nhiều CPU nhất trong 1 giờ qua.
```

AI assistant sẽ gọi `list_servers` để nhận ra service `runtime`, gọi `search_tools` với query "list agent runtimes" để lấy operation id và input schema, rồi gọi `execute` để chạy — hỏi lại bạn nếu thiếu thông tin bắt buộc.

Nếu bạn viết agent bằng code thay vì dùng chat client, kết nối qua MCP SDK chính thức theo đúng luồng 3 bước:

```typescript
const { tools } = await client.listTools();
console.log(tools.map(t => t.name));   // ["list_servers","search_tools","execute"]

const search = await client.callTool({
  name: "search_tools",
  arguments: { query: "list agent runtimes", limit: 5 },
});

const result = await client.callTool({
  name: "execute",
  arguments: { id: "runtime.list_1", args: {} },
});
```

---

Nếu gặp vấn đề, liên hệ GreenNode qua email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Trung tâm hỗ trợ: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
