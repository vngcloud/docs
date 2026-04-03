# PRD: 1-Click Deploy OpenClaw trên GreenNode AgentBase

## Document Information

| Field        | Value                                        |
| ------------ | -------------------------------------------- |
| Product      | GreenNode AgentBase                          |
| Feature      | 1-Click Deploy OpenClaw — Community Edition |
| Version      | 1.3                                          |
| Created Date | 2026-03-25                                   |
| Updated Date | 2026-03-30                                   |
| Author       | Product Team — AgentBase                    |
| Status       | In Review                                    |

---

## 1. Overview

### 1.1 Background

[OpenClaw](https://open.claw.cloud/) là một open-source AI agent chạy trên máy tính cá nhân, có thể tự động hoàn thành các tác vụ: duyệt web, quản lý file, chạy lệnh, viết code, tích hợp messaging.

**Vấn đề/Pain points:**

* Developer muốn thử OpenClaw phải tự cài đặt, cấu hình API key, chọn model thủ công — mất 30–60 phút setup
* End-user (non-developer) hoàn toàn không thể tiếp cận OpenClaw vì quá nhiều bước kỹ thuật
* GreenNode MaaS chưa có "entry point" thân thiện để giới thiệu đến cộng đồng rộng hơn

**Sự khác biệt chính:**

* **Giải pháp hiện tại** : Tự cài OpenClaw trên máy local, tự nhập API key, tự cấu hình — 30–60 phút, cần kiến thức DevOps
* **Giải pháp mới** : 1-Click Deploy từ Agent Marketplace trên AgentBase — best case 40–60 giây, không cần kiến thức kỹ thuật, tự động kết nối GreenNode MaaS

### 1.2 Objective

Cung cấp khả năng spin up một instance OpenClaw cá nhân từ Agent Marketplace trong 40–60 giây (best case), cho phép người dùng:

* Bất kỳ ai vào web AgentBase đều có thể dùng OpenClaw không cần kiến thức kỹ thuật
* User có tài khoản VNG được tự động kết nối GreenNode MaaS — không cần copy/paste API key
* User không có tài khoản VNG vẫn có thể dùng bằng cách mang API key của bên thứ 3 (BYOK)
* Sau khi deploy, user truy cập thẳng vào portal OpenClaw Gateway để dùng ngay
* User có thể cấu hình Channel (Telegram bot) ngay từ bước thiết lập

### 1.3 Scope

PRD này bao gồm các thay đổi UI/UX cho:

1. Agent Marketplace — OpenClaw featured card và hero banner
2. Màn hình cấu hình Deploy (Screen 3) — AI source, tên instance, flavor, channel
3. Màn hình Provisioning (Screen 5) — "Setting Up Your Workspace"
4. Màn hình Deploy Success (Screen 6) — thông tin instance và gateway password
5. OpenClaw Gateway Dashboard (Screen 7) — portal chat
6. My Agents Dashboard (Screen 8) — quản lý instance

**Ngoài phạm vi (Out of Scope):**

* Billing / usage metering cho từng instance
* Multi-instance per user (giai đoạn 1: 1 instance/user)
* Custom domain cho instance OpenClaw
* Persistent storage / backup dữ liệu OpenClaw
* Team/shared instance

### 1.4 Workflow Overview

| Component          | Integration                | Description                                                 |
| ------------------ | -------------------------- | ----------------------------------------------------------- |
| AgentBase Frontend | GreenNode Portal Auth      | Dùng session login sẵn có, không cần auth popup riêng |
| AgentBase Backend  | GreenNode MaaS (AIP)       | Internal API bridge tự động provision MaaS key           |
| AgentBase Backend  | AgentBase Identity Service | Tạo Identity cho mỗi OpenClaw instance                    |
| AgentBase Backend  | AgentBase Runtime Service  | Deploy container OpenClaw với env vars được inject      |
| AgentBase Frontend | Telegram Bot API           | Cấu hình Channel bot token (optional)                     |

### 1.5 Key Features Summary

| Feature                | Description                                                   | Phase   |
| ---------------------- | ------------------------------------------------------------- | ------- |
| Agent Marketplace      | OpenClaw featured card + hero CTA "Deploy 1-Click"            | MVP     |
| 1-Click Deploy — MaaS | Tự động kết nối GreenNode MaaS, không cần nhập key    | MVP     |
| 1-Click Deploy — BYOK | Mang API key từ provider bên ngoài (OpenAI, Anthropic...)  | MVP     |
| Channel Configuration  | Cấu hình Telegram bot token khi deploy                      | MVP     |
| Flavor Selection       | Chọn cấu hình tài nguyên CPU × RAM                      | MVP     |
| Persistent Disk        | Local disk `5Gi`mount tại `/home/user`                   | MVP     |
| Setting Up Workspace   | Màn hình provisioning với task list và polling            | MVP     |
| Gateway Password       | One-time token để auth vào OpenClaw Gateway lần đầu     | MVP     |
| My Agents Dashboard    | Quản lý instance: Running/Stopped, Open/Stop/Restart/Delete | MVP     |
| Auto-shutdown          | Tự dừng instance sau 24h idle                               | MVP     |
| Multi-instance         | Nhiều instance per user (paid plan)                          | Phase 2 |
| Deploy Node            | Thêm node từ Gateway Dashboard                              | Phase 2 |

---

## 2. User Stories (Gherkin Format)

### Feature: 1-Click Deploy OpenClaw trên AgentBase

---

#### US-01: Deploy OpenClaw với GreenNode MaaS (Happy path)

**As a** GreenNode user muốn dùng AI Agent ngay,
**I want** click "Deploy 1-Click" trên Marketplace và có instance OpenClaw sẵn sàng trong 40–60 giây,
**So that** tôi có thể bắt đầu chat với AI Agent mà không cần setup gì.

**Acceptance Criteria:**

```gherkin
Feature: Deploy OpenClaw 1-Click với GreenNode MaaS

  Background:
    Given người dùng đã đăng nhập GreenNode Portal
    And người dùng chưa có OpenClaw instance nào

  Scenario: Deploy thành công với MaaS mặc định
    When người dùng click "Deploy 1-Click" trên OpenClaw card tại Marketplace
    And người dùng giữ nguyên lựa chọn "GreenNode MaaS" (mặc định)
    And người dùng điền Tên OpenClaw và chọn Flavor
    And người dùng click "Bắt đầu thiết lập"
    Then màn hình "Setting Up Your Workspace" xuất hiện với 4 tasks
    And 4 tasks lần lượt chuyển từ ◌ sang ✓: OpenClaw Token → AI Service Account → AI Service Token → Cloud Computer
    And sau khi tất cả tasks hoàn thành, hệ thống tự redirect đến màn hình Deploy Success
    And màn hình Deploy Success hiển thị instance name, trạng thái ONLINE, URL và gateway password

  Scenario: User chưa đăng nhập click Deploy
    Given người dùng chưa đăng nhập GreenNode Portal
    When người dùng click "Deploy 1-Click" trên Marketplace
    Then hệ thống redirect đến trang GreenNode Login
    And sau khi đăng nhập xong, hệ thống redirect về màn hình cấu hình (Screen 3)

  Scenario: User đã có instance đang chạy click Deploy lần 2
    Given người dùng đã có 1 OpenClaw instance với trạng thái Running
    When người dùng click "Deploy 1-Click" trên Marketplace
    Then hệ thống redirect thẳng về My Agents Dashboard
    And hiển thị banner "Bạn đã có instance đang chạy"
```

---

#### US-02: Deploy OpenClaw với BYOK (Bring Your Own Key)

**As a** user muốn dùng model AI từ provider bên ngoài,
**I want** nhập API key của riêng mình khi cấu hình OpenClaw,
**So that** tôi có thể dùng model yêu thích (gpt-4o, Claude, v.v.) mà không bị giới hạn vào GreenNode MaaS.

**Acceptance Criteria:**

```gherkin
Feature: Deploy OpenClaw với BYOK API key

  Background:
    Given người dùng đã đăng nhập GreenNode Portal
    And người dùng đang ở màn hình cấu hình (Screen 3)

  Scenario: BYOK deploy thành công
    When người dùng chọn radio "Nhập API Key của bạn"
    And người dùng chọn Provider là "OpenAI"
    And người dùng nhập API Key hợp lệ
    And người dùng chọn Model "gpt-4o"
    And người dùng click "Bắt đầu thiết lập"
    Then hệ thống gọi /api/v1/openclaw/validate-key để kiểm tra key
    And sau khi validate thành công, hệ thống tiến hành provisioning
    And instance được deploy với model đã chọn

  Scenario: BYOK key không hợp lệ
    When người dùng chọn BYOK và nhập API key sai định dạng hoặc đã hết hạn
    And người dùng click "Bắt đầu thiết lập"
    Then hệ thống hiển thị lỗi inline bên dưới trường API Key: "API key không hợp lệ"
    And nút "Bắt đầu thiết lập" bị block, không chuyển sang Screen 5

  Scenario Outline: Validation form BYOK
    Given người dùng đã chọn BYOK
    When người dùng bỏ trống trường <field>
    And người dùng click "Bắt đầu thiết lập"
    Then hệ thống hiển thị lỗi "<error_message>"

    Examples:
      | field      | error_message                        |
      | API Key    | "Vui lòng nhập API Key"              |
      | Model      | "Vui lòng chọn model"                |
      | Tên OpenClaw | "Vui lòng nhập tên instance"       |
```

---

#### US-03: Cấu hình Channel Telegram khi deploy

**As a** user muốn tích hợp OpenClaw với Telegram,
**I want** cấu hình Telegram bot token ngay trong bước thiết lập,
**So that** sau khi deploy tôi có thể chat với OpenClaw qua Telegram ngay lập tức.

**Acceptance Criteria:**

```gherkin
Feature: Cấu hình Telegram Channel khi deploy OpenClaw

  Background:
    Given người dùng đang ở màn hình cấu hình (Screen 3)

  Scenario: Deploy với Telegram bot được cấu hình
    When người dùng chọn Channel Provider là "Telegram"
    And người dùng chọn Mode "Pairing"
    And người dùng nhập Bot Token hợp lệ
    And người dùng click "Bắt đầu thiết lập"
    Then instance được deploy với Telegram bot đã kết nối
    And người dùng có thể chat với OpenClaw qua Telegram ngay sau khi deploy

  Scenario: Bỏ qua cấu hình Channel
    When người dùng không nhập Bot Token
    And người dùng click "Bắt đầu thiết lập"
    Then instance vẫn deploy thành công
    And Channel có thể được cấu hình sau tại portal Settings → Config
```

---

#### US-04: Xem màn hình Provisioning

**As a** user vừa submit form cấu hình,
**I want** thấy tiến độ provisioning theo từng task,
**So that** tôi biết hệ thống đang làm gì và ước lượng được thời gian chờ.

**Acceptance Criteria:**

```gherkin
Feature: Màn hình Setting Up Your Workspace

  Background:
    Given người dùng vừa click "Bắt đầu thiết lập" từ Screen 3

  Scenario: Hiển thị và hoàn thành provisioning
    When màn hình "Setting Up Your Workspace" xuất hiện
    Then hệ thống hiển thị 4 tasks theo thứ tự: OpenClaw Token, AI Service Account, AI Service Token, Cloud Computer
    And mỗi task hiển thị spinner ◌ khi đang xử lý và ✓ khi hoàn thành
    And hệ thống poll /api/v1/openclaw/instances/{id}/status mỗi 3 giây
    And khi status = "ready", hệ thống tự redirect đến Screen 6

  Scenario: Provisioning thất bại
    When một trong 4 tasks bị lỗi hoặc timeout
    Then hệ thống hiển thị trạng thái lỗi với link "Troubleshoot"
    And hiển thị nút "Retry"
    And instance không tính vào quota của user
```

---

#### US-05: Lấy gateway password sau khi deploy thành công

**As a** user vừa deploy xong OpenClaw,
**I want** thấy gateway password và URL của instance,
**So that** tôi có thể đăng nhập vào OpenClaw Gateway Dashboard ngay lập tức.

**Acceptance Criteria:**

```gherkin
Feature: Màn hình Deploy Success

  Background:
    Given provisioning đã hoàn thành thành công

  Scenario: Hiển thị đầy đủ thông tin instance
    When màn hình Deploy Success xuất hiện
    Then hệ thống hiển thị: instance name, trạng thái ONLINE, AI model, URL, gateway password, thời gian tạo
    And gateway password chỉ hiển thị 1 lần duy nhất tại màn hình này
    And có nút "Mở OpenClaw" để vào Gateway Dashboard
    And có nút "Sao chép URL" và "Quản lý instance"

  Scenario: Mở OpenClaw từ màn hình Deploy Success
    When người dùng click "Mở OpenClaw"
    Then hệ thống redirect đến https://{instance-id}.openclaw.agentbase.vn
    And người dùng dùng gateway password để auth lần đầu
```

---

#### US-06: Quản lý instance từ My Agents Dashboard

**As a** user có OpenClaw instance đang chạy,
**I want** xem và quản lý instance của mình từ My Agents Dashboard,
**So that** tôi có thể stop, restart, xóa instance hoặc mở lại portal bất kỳ lúc nào.

**Acceptance Criteria:**

```gherkin
Feature: Quản lý OpenClaw Instance từ My Agents Dashboard

  Background:
    Given người dùng đã đăng nhập GreenNode Portal
    And người dùng đang ở trang My Agents

  Scenario: Xem danh sách instance theo trạng thái
    When trang My Agents được load
    Then hệ thống hiển thị 2 section: "Running 🟢" và "Stopped ⚪"
    And mỗi instance card hiển thị: tên, trạng thái, AI model, version, tags
    And section Stopped hiển thị empty state khi chưa có instance nào bị dừng

  Scenario: Mở lại OpenClaw đang Running
    When người dùng click "Open" trên instance card có trạng thái Running
    Then hệ thống redirect thẳng vào OpenClaw Gateway Dashboard
    And không đi qua wizard/provisioning lại

  Scenario: Stop instance
    When người dùng click "Stop" trên instance card
    And xác nhận trong confirm dialog
    Then instance chuyển sang trạng thái Stopped
    And URL của instance không còn accessible
    And card chuyển xuống section Stopped

  Scenario: Restart instance đã Stop
    When người dùng click "Restart" trên instance đang Stopped
    Then instance chuyển qua trạng thái Starting → Running
    And URL hoạt động lại
    And card chuyển lên section Running

  Scenario: Xóa instance
    When người dùng click "Delete" trên instance card
    And xác nhận trong confirm dialog
    Then instance bị xóa vĩnh viễn
    And quota được trả về
    And vị trí card đổi thành slot "Deploy a new Agent"

  Scenario: Auto-shutdown sau 24h idle
    Given instance không có request trong 24 giờ
    When system cron job chạy
    Then instance tự chuyển sang Stopped
    And user nhận email thông báo
    And user có thể Restart từ My Agents Dashboard
```

---

## 3. Functional Requirements

### 3.1 Agent Marketplace — OpenClaw Card

#### 3.1.1 Current State

* Chưa có Agent Marketplace trong AgentBase. User muốn deploy OpenClaw phải tự tìm hiểu và thực hiện 13 bước thủ công.

#### 3.1.2 Proposed Changes

**Hero Banner:**

| Field/Element   | Description                                | Logic/Rule                          | Note           |
| --------------- | ------------------------------------------ | ----------------------------------- | -------------- |
| Headline        | "Agent Marketplace"                        | Static                              | —             |
| CTA button      | "✅ Deploy OpenClaw With 1 Click!"         | Click → kiểm tra auth → Screen 3 | Primary action |
| Hero background | Gradient dark card với 3D floating shapes | Visual only                         | —             |

**OpenClaw Featured Card:**

| Field/Element | Description                                            | Logic/Rule              | Note                     |
| ------------- | ------------------------------------------------------ | ----------------------- | ------------------------ |
| Badge         | FEATURED + FREE                                        | Static                  | Hiển thị nổi bật     |
| Title         | "OpenClaw by GreenNode"                                | Static                  | —                       |
| Description   | "Personal AI agent architected for sovereign cloud..." | Static                  | Tối đa 2 dòng         |
| Stats         | Rating 4.9⭐ · 1,200+ Deploys · < 2 min Setup        | Static (giai đoạn 1)  | Cập nhật real-time sau |
| CTA           | "🚀 Deploy 1-Click / No config needed"                 | Click → kiểm tra auth | Full-width, màu green   |

**Behavior:**

* Click "Deploy 1-Click" hoặc hero CTA → kiểm tra auth
  * Đã login → Screen 3
  * Chưa login → redirect GreenNode Login → sau login quay lại Screen 3
* Đã có instance Running → redirect My Agents + banner thông báo

---

### 3.2 Màn hình Cấu hình Deploy (Screen 3)

#### 3.2.1 Current State

* Không có. User phải tự tạo IAM Service Account, attach policy, tạo vCR repository, build Docker image, tạo Runtime thủ công.

#### 3.2.2 Proposed Changes

**Form Section 1 — AI Source:**

| Field/Element | Type                  | Options                           | Description                                    |
| ------------- | --------------------- | --------------------------------- | ---------------------------------------------- |
| AI Source     | Radio button          | GreenNode MaaS / BYOK             | Mặc định: GreenNode MaaS                    |
| BYOK Provider | Dropdown              | OpenAI, Anthropic, Gemini, Custom | Chỉ hiển thị khi chọn BYOK                 |
| BYOK API Key  | Text input (password) | —                                | Bắt buộc khi BYOK. Icon 👁 toggle visibility |
| BYOK Model    | Dropdown              | Động theo provider              | Bắt buộc khi BYOK                            |

**Form Section 2 — Instance Config:**

| Field/Element | Type       | Options              | Description                                    |
| ------------- | ---------- | -------------------- | ---------------------------------------------- |
| Tên OpenClaw | Text input | —                   | Auto-fill:`openclaw/{username}`. Bắt buộc  |
| Flavor        | Dropdown   | 2×4, 4×8, 8×16... | Bắt buộc. Mặc định:`2×4`               |
| Disk          | Read-only  | `5Gi`              | Fixed giai đoạn 1. Mount path:`/home/user` |

**Form Section 3 — Channel Configuration:**

| Field/Element    | Type         | Options              | Description                               |
| ---------------- | ------------ | -------------------- | ----------------------------------------- |
| Channel Provider | Dropdown     | Telegram             | Mặc định: Telegram                     |
| Mode             | Radio button | Pairing / Allow List | Mặc định: Pairing                      |
| Bot Token        | Text input   | —                   | Không bắt buộc. Cấu hình sau được |

**Business Rules:**

| Rule  | Description                                                                                             |
| ----- | ------------------------------------------------------------------------------------------------------- |
| BR-01 | Khi chọn GreenNode MaaS, không hiển thị trường BYOK                                               |
| BR-02 | Khi chọn BYOK, bắt buộc Provider + API Key + Model. Gọi validate-key trước khi submit             |
| BR-03 | Tên OpenClaw auto-fill từ username, cho phép sửa. Không được trùng với instance đang Running |
| BR-04 | Disk `5Gi`cố định, không cho chỉnh trong MVP                                                     |
| BR-05 | Bot Token không bắt buộc — bỏ trống thì deploy không có Channel, cấu hình sau                |
| BR-06 | 1 user chỉ có tối đa 1 instance Running (free tier)                                                 |

---

### 3.3 Màn hình Provisioning — Setting Up Your Workspace (Screen 5)

#### 3.3.1 Current State

* Không có màn hình provisioning — deploy xong không biết trạng thái gì.

#### 3.3.2 Proposed Changes

**Task List:**

| Task               | Mô tả                                         | Trạng thái |
| ------------------ | ----------------------------------------------- | ------------ |
| OpenClaw Token     | Tạo Identity và token xác thực cho instance | ◌ / ✓ / ✗ |
| AI Service Account | Tạo IAM Service Account kết nối MaaS         | ◌ / ✓ / ✗ |
| AI Service Token   | Lấy access token cho model AI                  | ◌ / ✓ / ✗ |
| Cloud Computer     | Khởi động container OpenClaw                 | ◌ / ✓ / ✗ |

**Behavior:**

* Frontend poll `/api/v1/openclaw/instances/{id}/status` mỗi 3 giây
* Auto-redirect khi status = `ready`
* Nếu timeout (> 3 phút) hoặc task bị lỗi: hiển thị failed state + link Troubleshoot + nút Retry

---

### 3.4 Màn hình Deploy Success (Screen 6)

#### 3.4.1 Current State

* Không có.

#### 3.4.2 Proposed Changes

**Instance Info Card:**

| Field/Element              | Description                            | Logic/Rule                                  | Note                             |
| -------------------------- | -------------------------------------- | ------------------------------------------- | -------------------------------- |
| Instance name              | Ví dụ:`openclaw-nguyenvana-001`    | Auto-generated                              | Read-only                        |
| Trạng thái               | 🟢 ONLINE                              | Từ API                                     | —                               |
| AI Model                   | Ví dụ:`gpt-5.4 · GreenNode MaaS`  | Từ config                                  | —                               |
| URL                        | `https://{id}.openclaw.agentbase.vn` | Auto-generated                              | Có nút copy                    |
| **Gateway password** | Token xác thực một lần             | Chỉ hiển thị 1 lần tại màn hình này | Cảnh báo rõ ràng bên dưới |
| Thời gian tạo            | Timestamp                              | Auto                                        | —                               |

**Business Rules:**

| Rule  | Description                                                                                                   |
| ----- | ------------------------------------------------------------------------------------------------------------- |
| BR-07 | Gateway password hiển thị đúng 1 lần tại Screen 6. Sau khi user rời trang, không thể truy xuất lại |
| BR-08 | Nếu user cần reset gateway password, thực hiện từ My Agents Dashboard (flow Phase 2)                     |

---

### 3.5 My Agents Dashboard (Screen 8)

#### 3.5.1 Current State

* AgentBase có màn hình Runtime list nhưng không có view theo-product "My Agents" dành riêng cho OpenClaw.

#### 3.5.2 Proposed Changes

**Danh sách Instance — Sections:**

| Section     | Điều kiện                     | Mô tả                          |
| ----------- | -------------------------------- | -------------------------------- |
| Running 🟢  | Có ít nhất 1 instance Running | Card grid với nút "Open"       |
| Stopped ⚪  | Có ít nhất 1 instance Stopped | Card grid với nút "Restart"    |
| Empty state | Chưa có instance nào          | Icon + "Deploy a new Agent" slot |

**Actions trên card:**

| Action  | Icon | Description                                               |
| ------- | ---- | --------------------------------------------------------- |
| Open    | ↗   | Redirect vào OpenClaw Gateway Dashboard                  |
| Stop    | ■   | Dừng instance. Hiện confirm dialog                      |
| Restart | ↺   | Khởi động lại instance Stopped                        |
| Delete  | 🗑   | Xóa vĩnh viễn. Hiện confirm dialog với tên instance |

---

## 4. UI/UX Specifications

### 4.1 Color Palette

| Role           | GreenNode Portal                    | OpenClaw Gateway   |
| -------------- | ----------------------------------- | ------------------ |
| Background     | `#F9FAFB`(page),`#FFFFFF`(card) | `#FFFFFF`        |
| Top nav        | `#111111`(dark)                   | `#FFFFFF`        |
| Sidebar        | `#FFFFFF`(white)                  | `#0A0C0A`(dark)  |
| Accent / CTA   | `#16A34A`(green)                  | `#16A34A`(green) |
| Text primary   | `#111111`                         | `#111111`        |
| Text secondary | `#6B7280`                         | `#555555`        |
| Border         | `#E5E7EB`                         | `#E0EAE0`        |
| Error          | `#EF4444`                         | `#EF4444`        |
| Success        | `#16A34A`                         | `#16A34A`        |

### 4.2 Screen 3 — Config Form Card

| Element       | Specification                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------ |
| Card width    | 480px (center)                                                                                         |
| Card style    | White bg,`border-radius: 12px`,`box-shadow: 0 4px 24px rgba(0,0,0,0.08)`                           |
| Radio buttons | Dạng card — full-width, 56px height,`border: 1.5px solid`, selected:`border-color: #16A34A`      |
| BYOK section  | Expandable dưới radio,`border-radius: 8px`, bg `#F9FAFB`                                         |
| CTA button    | Full-width, 48px height,`bg: #16A34A`,`color: #FFFFFF`,`border-radius: 8px`                      |
| Input fields  | `height: 40px`,`border: 1px solid #D1D5DB`,`border-radius: 6px`, focus:`border-color: #16A34A` |

### 4.3 Screen 5 — Provisioning Card

| Element                | Specification                                           |
| ---------------------- | ------------------------------------------------------- |
| Card width             | 480px (center)                                          |
| Spinner                | Arc spinner `#16A34A`, 48px, center                   |
| Task icon — pending   | ◌`#9CA3AF`                                           |
| Task icon — done      | ✓`#16A34A`                                           |
| Task icon — error     | ✗`#EF4444`                                           |
| Button "Connecting..." | Full-width, disabled state, bg `#16A34A`, opacity 60% |

### 4.4 Screen 6 — Deploy Success Card

| Element            | Specification                                                                |
| ------------------ | ---------------------------------------------------------------------------- |
| Success icon       | ✅ check circle, 56px,`color: #16A34A`, glow ring `rgba(22,163,74,0.2)`  |
| Instance info card | White bg,`border: 1px solid #E5E7EB`,`border-radius: 12px`               |
| Gateway password   | Monospace font,`bg: #F0FDF4`,`border: 1px solid #86EFAC`, hiển thị rõ |
| Warning text       | `color: #D97706`, icon ⚠️, text "Password chỉ hiển thị 1 lần..."     |
| Primary CTA        | "Mở OpenClaw" — full-width,`bg: #16A34A`                                 |

### 4.5 Screen 8 — My Agents Dashboard

| Element             | Specification                                                                    |
| ------------------- | -------------------------------------------------------------------------------- |
| Section header      | "Running (n) 🟢" / "Stopped (n) ⚪" —`font-weight: 600`,`font-size: 16px`   |
| Card grid           | 3 columns,`gap: 16px`                                                          |
| Instance card       | White bg,`border: 1px solid #E5E7EB`,`border-radius: 12px`,`padding: 20px` |
| Status pill Running | `bg: #DCFCE7`,`color: #16A34A`,`border-radius: 9999px`                     |
| Status pill Stopped | `bg: #F3F4F6`,`color: #6B7280`,`border-radius: 9999px`                     |
| "Open" button       | Full-width,`bg: #16A34A`,`color: #FFFFFF`                                    |
| Actions menu        | ⋮ icon → dropdown: Stop / Restart / Delete                                     |

---

## 5. Validation Rules

### 5.1 Form Cấu hình Deploy (Screen 3)

| Field         | Rule                                                                                   | Error Message                                                                 |
| ------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Tên OpenClaw | Bắt buộc. Pattern:`openclaw/[a-z0-9-]{3,32}`. Không trùng instance đang Running | "Tên không hợp lệ (chỉ chứa a-z, 0-9, dấu gạch ngang, 3–32 ký tự)" |
| Flavor        | Bắt buộc, phải chọn từ danh sách                                                 | "Vui lòng chọn Flavor"                                                      |
| BYOK Provider | Bắt buộc khi chọn BYOK                                                              | "Vui lòng chọn Provider"                                                    |
| BYOK API Key  | Bắt buộc khi BYOK. Gọi validate-key trước submit                                  | "API key không hợp lệ hoặc đã hết hạn"                                |
| BYOK Model    | Bắt buộc khi BYOK                                                                    | "Vui lòng chọn Model"                                                       |

### 5.2 Business Rules Validation

| Rule             | Description                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| Quota 1 instance | Nếu đã có 1 instance Running → block deploy, redirect My Agents                                          |
| BYOK key test    | Validate key trước khi submit form — gọi `/api/v1/openclaw/validate-key`. Timeout 10 giây              |
| Tên trùng lặp | Tên instance phải unique trong cùng Organization                                                           |
| Gateway password | Không bao giờ trả về qua API sau lần đầu. Không có endpoint "lấy lại password" trong giai đoạn 1 |

---

## 6. Technical Notes

### 6.1 Architecture

```
┌───────────────────────────────────────────────────────┐
│               User Browser (Next.js Frontend)         │
│  Marketplace · Config wizard · My Agents · Success    │
└────────────────────────┬──────────────────────────────┘
                         │ HTTPS REST API
┌────────────────────────▼──────────────────────────────┐
│        AgentBase Backend — OpenClaw Orchestrator       │
│  ┌──────────────┐  ┌─────────────────┐  ┌──────────┐  │
│  │ OpenClaw     │  │ Key Provisioner │  │ Instance │  │
│  │ Manager API  │  │ (MaaS bridge)   │  │ Lifecycle│  │
│  └──────┬───────┘  └────────┬────────┘  └────┬─────┘  │
└─────────┼───────────────────┼────────────────┼─────────┘
          │                   │                │
   ┌──────▼──────┐   ┌────────▼────────┐  ┌───▼──────────┐
   │  AgentBase  │   │ GreenNode MaaS  │  │  AgentBase   │
   │  Identity   │   │ AIP API         │  │  Runtime     │
   │  Service    │   │ (Internal)      │  │  Service     │
   └─────────────┘   └─────────────────┘  └──────┬───────┘
                                                  │
                                         ┌────────▼───────┐
                                         │ Container:      │
                                         │ OpenClaw        │
                                         │ (port 8080)     │
                                         │ Disk: 5Gi       │
                                         │ mount /home/user│
                                         └─────────────────┘
```

### 6.2 Dependencies

| Service/Component          | Type     | Purpose                                       | Version       |
| -------------------------- | -------- | --------------------------------------------- | ------------- |
| GreenNode Portal Auth      | Internal | SSO login, session management                 | —            |
| AgentBase Identity Service | Internal | Tạo Identity cho mỗi instance               | v1            |
| AgentBase Runtime Service  | Internal | Deploy và quản lý container                | v1            |
| GreenNode MaaS (AIP)       | Internal | LLM API endpoint, model `gpt-5.4`           | v1            |
| Container Registry (vCR)   | Internal | Lưu OpenClaw container image                 | —            |
| AgentBase Reverse Proxy    | Internal | Subdomain routing `*.openclaw.agentbase.vn` | Nginx/Traefik |
| Telegram Bot API           | External | Channel integration                           | —            |

### 6.3 Core Functionality

| Functionality       | Description                                        | Technical Implementation                                                       |
| ------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------ |
| MaaS Auto-Provision | Tự động tạo MaaS API key cho instance          | POST `/internal/api-keys/provision`→ lưu vào Identity Service             |
| BYOK Secure Storage | Lưu trữ API key bên thứ 3 an toàn             | Mã hóa AES-256 at rest, chỉ decrypt khi inject vào container               |
| Env Var Injection   | Inject toàn bộ config vào container lúc deploy | AgentBase Runtime contract: inject `OPENAI_*`,`OPENCLAW_*`,`GREENNODE_*` |
| Gateway Password    | One-time auth token cho OpenClaw Gateway           | Generate ngẫu nhiên, lưu hash, chỉ trả về plain text 1 lần              |
| Persistent Disk     | Local volume `5Gi`cho workspace                  | Mount tại `/home/user`, survive restart, lost on delete                     |
| Subdomain Routing   | `{id}.openclaw.agentbase.vn`→ container         | Reverse proxy lookup Runtime endpoint theo instance ID                         |
| Auto-shutdown       | Tự dừng sau 24h không có request               | Cron job kiểm tra `last_request_at`trên mỗi instance                      |

**Deploy Flow — Data Flow:**

1. User submit form Screen 3 → POST `/api/v1/openclaw/deploy`
2. Backend: validate input → provision MaaS key (hoặc encrypt BYOK key) → tạo Identity → tạo Runtime với env vars + disk config
3. Frontend poll `/api/v1/openclaw/instances/{id}/status` mỗi 3s
4. Runtime status = `ready` → trả về `portal_url` + `gateway_password` → redirect Screen 6

**Key Environment Variables:**

| Variable                       | Mô tả                                            | Source                         |
| ------------------------------ | -------------------------------------------------- | ------------------------------ |
| `OPENAI_API_KEY`             | API key để OpenClaw gọi LLM                     | Injected by AgentBase Runtime  |
| `OPENAI_BASE_URL`            | Endpoint URL của LLM provider                     | Injected by AgentBase Runtime  |
| `OPENAI_MODEL`               | Model name, default:`gpt-5.4`                    | Injected by AgentBase Runtime  |
| `OPENCLAW_INSTANCE_ID`       | Định danh instance                               | Injected by AgentBase Runtime  |
| `OPENCLAW_GATEWAY_PASSWORD`  | Gateway token auth lần đầu                      | Injected by AgentBase Runtime  |
| `OPENCLAW_WORKSPACE`         | Mount path persistent disk, default:`/home/user` | Injected by AgentBase Runtime  |
| `OPENCLAW_DISK_SIZE`         | Dung lượng persistent disk, default:`5Gi`      | Injected by AgentBase Runtime  |
| `OPENCLAW_CHANNEL_PROVIDER`  | Channel provider (telegram)                        | Injected by AgentBase Runtime  |
| `OPENCLAW_CHANNEL_BOT_TOKEN` | Bot token cho channel                              | Injected by AgentBase Runtime  |
| `OPENCLAW_CHANNEL_MODE`      | Mode: pairing / allow_list                         | Injected by AgentBase Runtime  |
| `GREENNODE_AGENT_IDENTITY`   | Identity của agent trên AgentBase                | Auto-inject (Runtime contract) |
| `GREENNODE_CLIENT_ID`        | IAM credentials                                    | Auto-inject (Runtime contract) |
| `GREENNODE_CLIENT_SECRET`    | IAM credentials                                    | Auto-inject (Runtime contract) |

> **Lưu ý bảo mật** : OpenClaw dùng biến `OPENAI_API_KEY` và `OPENAI_BASE_URL` (OpenAI-compatible). AgentBase inject đúng tên biến này → không cần patch OpenClaw source code.

### 6.4 High Availability & Resilience

| Aspect                       | Strategy                 | Details                                           |
| ---------------------------- | ------------------------ | ------------------------------------------------- |
| **Redundancy**         | Per-instance isolated    | Mỗi user 1 container riêng, không share        |
| **Failover**           | Manual (giai đoạn 1)   | User tự Restart từ My Agents khi instance lỗi  |
| **Provisioning retry** | Auto-retry 3 lần        | Backend retry mỗi 30s khi provisioning task fail |
| **Auto-shutdown**      | Idle timeout 24h         | Bảo toàn tài nguyên, user nhận email notify  |
| **Disk persistence**   | PersistentVolume `5Gi` | Survive restart, bị xóa khi delete instance     |

**SLA Targets:**

| Metric                      | Target       | Measurement                                        |
| --------------------------- | ------------ | -------------------------------------------------- |
| Availability per instance   | 99.5%        | Uptime sau deploy thành công                     |
| Provisioning time best case | 40–60 giây | Từ submit form → status ready (confirmed by dev) |
| Provisioning time P95       | < 120 giây  | Từ submit form → status ready                    |
| Portal load time            | < 1 giây    | Time to interactive trên Marketplace              |

### 6.5 Operations & Stability

#### Monitoring & Alerting

| Metric                    | Threshold                                | Alert Level | Action                |
| ------------------------- | ---------------------------------------- | ----------- | --------------------- |
| Provisioning failure rate | > 5%                                     | Critical    | Page on-call          |
| Instance deploy time P95  | > 120 giây (expected best case 40–60s) | Warning     | Investigate infra     |
| BYOK validate-key latency | > 5 giây                                | Warning     | Log + notify user     |
| Auto-shutdown cron lag    | > 1 giờ                                 | Warning     | Check cron job health |

#### API Endpoints

| Method     | Endpoint                                    | Mô tả                          |
| ---------- | ------------------------------------------- | -------------------------------- |
| `POST`   | `/api/v1/openclaw/deploy`                 | Tạo mới OpenClaw instance      |
| `GET`    | `/api/v1/openclaw/instances`              | Liệt kê instances của user    |
| `GET`    | `/api/v1/openclaw/instances/{id}`         | Chi tiết 1 instance             |
| `GET`    | `/api/v1/openclaw/instances/{id}/status`  | Poll deployment status           |
| `POST`   | `/api/v1/openclaw/instances/{id}/stop`    | Stop instance                    |
| `POST`   | `/api/v1/openclaw/instances/{id}/restart` | Restart instance                 |
| `DELETE` | `/api/v1/openclaw/instances/{id}`         | Xóa instance                    |
| `POST`   | `/api/v1/openclaw/validate-key`           | Test BYOK API key                |
| `GET`    | `/api/v1/maas/models`                     | Danh sách model MaaS khả dụng |
| `GET`    | `/api/v1/openclaw/flavors`                | Danh sách flavor khả dụng     |

---

## 7. Success Metrics

| Metric                                                    | Baseline | Target (3 tháng) | Measurement                                |
| --------------------------------------------------------- | -------- | ----------------- | ------------------------------------------ |
| Số instance OpenClaw được tạo                        | 0        | 500+              | AgentBase analytics                        |
| Tỉ lệ hoàn thành wizard (không bỏ giữa chừng)     | —       | > 70%             | Funnel tracking Screen 3 → 6              |
| Thời gian trung bình từ "Deploy" → "Chat đầu tiên" | —       | < 3 phút         | Từ submit form đến API call đầu tiên |
| DAU trên portal OpenClaw                                 | —       | 200+              | Gateway request logs                       |
| Tỉ lệ chuyển đổi BYOK → MaaS                        | —       | > 20%             | Provider field analytics                   |
| NPS score sau lần dùng đầu                            | —       | > 40              | In-app survey                              |
| Tỉ lệ user quay lại trong 7 ngày                      | —       | > 40%             | Session analytics                          |
| Tỉ lệ cấu hình Channel (Telegram) khi deploy          | —       | > 30%             | Bot Token field fill rate                  |

---

## 8. Risks & Mitigations

| Risk                                                                           | Impact                           | Mitigation                                                                              |
| ------------------------------------------------------------------------------ | -------------------------------- | --------------------------------------------------------------------------------------- |
| OpenClaw không chạy được headless với env var inject (cần patch source) | Cao — block toàn bộ MVP       | PoC ngay tuần 1: test inject `OPENAI_API_KEY`vào container OpenClaw trước khi dev |
| MaaS chưa có API internal để provision key tự động                      | Cao — block MaaS path           | Confirm với MaaS team trước kick-off. Nếu chưa có: BYOK-only cho MVP              |
| OpenClaw license không cho phép deploy dạng SaaS                            | Trung bình — rủi ro pháp lý | Check license (MIT/Apache). Nếu cần: add credit footer + thông báo                  |
| Free tier quota 100K tokens/ngày không đủ để trải nghiệm tốt          | Trung bình — UX kém, churn    | A/B test quota level sau MVP; hiển thị token counter trên Gateway                    |
| Subdomain wildcard SSL `*.openclaw.agentbase.vn`chưa sẵn sàng             | Thấp — delay routing           | Confirm wildcard cert với infra team trước Sprint 1                                  |
| User quên gateway password — không có flow reset giai đoạn 1             | Trung bình — support burden    | Document rõ trong UI. Thiết kế flow "Reset gateway password" cho Phase 2             |
| Provisioning timeout do infra tải cao                                         | Trung bình — UX xấu           | Retry 3 lần với backoff. Hiển thị Troubleshoot link rõ ràng                       |
| Scope creep từ Channel integration (Allow List cần thêm UI nhập user list) | Trung bình — chậm deadline    | Confirm UX "Allow List" với Design: nếu cần UI phức tạp → defer sang Phase 2      |

---

## 9. Appendix

### A. Glossary

| Term              | Definition                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| MaaS              | Model as a Service — GreenNode hosted LLM API tại `maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| BYOK              | Bring Your Own Key — user tự cung cấp API key từ provider bên ngoài                       |
| Gateway Password  | One-time token để auth lần đầu vào OpenClaw Gateway Dashboard                             |
| Flavor            | Cấu hình tài nguyên container: vCPU × RAM GB (ví dụ:`2×4`= 2 vCPU, 4GB RAM)           |
| Identity          | Định danh agent trong AgentBase Identity Service                                              |
| AgentBase Runtime | Service quản lý vòng đời container agent trên AgentBase                                   |
| Pairing Mode      | Telegram channel mode: 1 OpenClaw ↔ 1 Telegram user                                            |
| Allow List Mode   | Telegram channel mode: 1 OpenClaw ↔ danh sách Telegram user được phép                     |

### B. So sánh với OpenClawCloud

| Tiêu chí          | OpenClawCloud          | AgentBase 1-Click                   |
| ------------------- | ---------------------- | ----------------------------------- |
| Hạ tầng           | Claw.Cloud VPS         | GreenNode (VNG Cloud)               |
| Free tier           | 7 ngày compute        | TBD (quota-based)                   |
| AI Models           | GLM-4.7, GLM-5, Claude | GreenNode MaaS (`gpt-5.4`) + BYOK |
| Auto key inject     | Có (proprietary)      | Có (AgentBase Identity)            |
| Sovereign           | Không                 | Có (data ở VN)                    |
| SSO nội bộ VNG    | Không                 | Có                                 |
| Channel integration | Không                 | Telegram (MVP)                      |
| Flavor selection    | Không                 | Có                                 |
| Persistent disk     | Có                    | `5Gi`mount `/home/user`         |
| Giá                | $0–$39.99/tháng      | TBD (align Sales)                   |

### C. Figma Design Reference

| Screen                           | Figma Node    | Mô tả                                                   |
| -------------------------------- | ------------- | --------------------------------------------------------- |
| Screen 1 — Agent Marketplace    | `668:24274` | GreenNode Portal, Marketplace với OpenClaw featured card |
| Screen 3 — Config AI + Instance | `649:24062` | Form cấu hình: AI source, tên, flavor, channel         |
| Screen 5 — Setting Up Workspace | `671:25754` | Provisioning task list                                    |
| Screen 6 — Deploy Success       | `649:24157` | Light mode, gateway password                              |
| Screen 7 — Gateway Dashboard    | `649:24231` | Chat UI, Dashboard/Logs/Terminal tabs                     |
| Screen 8 — My Agents            | `671:25091` | Running/Stopped sections                                  |

 **Figma file** : `-UI- AgentBase` (fileKey: `IH7ERLh3KfvztmTe6qD9pW`)

### D. References

* [AgentBase Product Overview](../AI-Agent-Normal/Product-Overview-Agentbase.md)
* [AgentBase Runtime Contract](../../greennode-agentbase-skills-main/.claude/skills/agentbase/references/runtime-contract.md)
* [OpenClawCloud](https://open.claw.cloud/)
* [GreenNode MaaS Endpoint](https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1)

### E. Changelog

| Version        | Ngày      | Tác giả    | Nội dung                                                                                                                                                                                                                                                                         |
| -------------- | ---------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **v1.3** | 2026-03-30 | Product Team | Đổi MaaS default model →`gpt-5.4`; thêm persistent disk `5Gi`mount `/home/user`; restructure toàn bộ theo chuẩn PRD 8-section; update provisioning time best case 40–60s (confirmed by dev); chuyển Changelog sang Appendix E                                      |
| **v1.2** | 2026-03-27 | Product Team | Sync screen flow với Figma design mới: Agent Marketplace thay dark landing page; bỏ Auth Popup riêng; Screen 3 thêm Flavor + Channel config; Screen 6 light mode + gateway password; Gateway Dashboard redesign (tabs + sidebar mới); My Agents → Running/Stopped sections |
| **v1.1** | 2026-03-25 | Product Team | Refactor flow UX: thay wizard 4 bước bằng 2-path auth; bỏ Review & Deploy screen; thay Deploying Progress bằng "Setting Up Your Workspace"; cập nhật Screen 7 và 8 sang light mode                                                                                        |
| **v1.0** | 2026-03-25 | Product Team | Khởi tạo PRD                                                                                                                                                                                                                                                                    |

---

*Xem chi tiết lịch sử thay đổi tại Appendix E. Mọi thay đổi cần được review bởi Product Owner trước khi cập nhật.*
