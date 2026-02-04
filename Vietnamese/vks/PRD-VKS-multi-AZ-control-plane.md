# PRD: VKS Multi-AZ Support cho Control Plane

## Document Information

| Field        | Value                              |
| ------------ | ---------------------------------- |
| Product      | VKS - VNG Kubernetes Service       |
| Feature      | Multi-AZ Support cho Control Plane |
| Version      | 1.0                                |
| Created Date | 2025-12-24                         |
| Status       | Draft                              |
| Author       | Ngọc Huyền                       |

---

## 1. Overview

### 1.1 Background

Hiện tại, VKS (VNG Kubernetes Service) chỉ hỗ trợ triển khai Kubernetes Cluster theo mô hình **Single-AZ** (Single Availability Zone), trong đó Control Plane nằm trong một Availability Zone duy nhất. Điều này tạo ra rủi ro về tính sẵn sàng cao (High Availability) khi xảy ra sự cố ở AZ đó.

Để đáp ứng nhu cầu về High Availability cho Control Plane, cần bổ sung tính năng **Multi-AZ Support cho Control Plane** cho phép triển khai Control Plane trên nhiều Availability Zones khác nhau.

**Vấn đề/Pain points:**

- Control Plane Single-AZ có single point of failure tại AZ level
- Không đáp ứng yêu cầu HA cho các ứng dụng production quan trọng
- Khách hàng enterprise yêu cầu khả năng disaster recovery cao hơn cho Control Plane

**Sự khác biệt chính so với giải pháp hiện tại:**

- **Single-AZ Cluster**: Control Plane nằm trong 1 AZ, sử dụng 1 subnet. Nếu AZ gặp sự cố, Control Plane không thể hoạt động
- **Multi-AZ Cluster**: Control Plane được phân bổ trên nhiều AZ (tối thiểu 2 AZ), sử dụng nhiều subnets từ các AZ khác nhau. Nếu 1 AZ gặp sự cố, Control Plane vẫn hoạt động bình thường

> **Lưu ý:** Trong phiên bản này, Node Group vẫn chỉ hỗ trợ triển khai trong 1 subnet (1 AZ). Khi tạo cluster Multi-AZ, người dùng chọn 1 subnet cho Node Group từ danh sách subnets đã cấu hình cho cluster.

### 1.2 Objective

Cung cấp khả năng triển khai Kubernetes Cluster với Control Plane Multi-AZ, cho phép người dùng:

- Đảm bảo High Availability cho Control Plane với khả năng chịu lỗi ở cấp độ AZ
- Tự động failover Control Plane khi một AZ gặp sự cố mà không cần can thiệp thủ công
- Triển khai workload production với độ tin cậy cao hơn
- Tuân thủ các yêu cầu compliance về disaster recovery

### 1.3 Scope

| Function               | Description                                                                                         | Portal                                                                                                             | User Story   |
| ---------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------ |
| Xem danh sách Cluster | Hiển thị danh sách clusters với thông tin Control Plane Availability                           | Bổ sung cột "Control Plane Availability" (Single-AZ/Multi-AZ)                                                    | US-01        |
| Xem chi tiết Cluster  | Hiển thị thông tin chi tiết cluster bao gồm Control Plane Availability và danh sách Subnets  | Bổ sung Control Plane Availability trong General Info, Subnets list với AZ trong Network section, Copy Subnet ID | US-02        |
| Tạo mới Cluster      | Tạo cluster với lựa chọn Control Plane Availability (Single-AZ/Multi-AZ) và cấu hình subnets | Bổ sung Control Plane Availability dropdown, Subnets multi-select cho Multi-AZ, Node Group Subnet selection       | US-03, US-04 |
| Upgrade Cluster        | Upgrade Control Plane version cho Multi-AZ cluster                                                  | Không thay đổi UI                                                                                               | US-05        |
| Delete Cluster         | Xóa Multi-AZ cluster và cleanup resources across all AZs                                          | Không thay đổi UI                                                                                               | US-06        |

**Ngoài phạm vi (Out of Scope):**

- Chuyển đổi cluster từ Single-AZ sang Multi-AZ sau khi đã tạo
- Multi-AZ Node Group (Node Group hiện tại chỉ hỗ trợ 1 subnet duy nhất)
- Custom placement strategy cho pods

---

## 2. User Stories (Gherkin Format)

### Feature: VKS Multi-AZ Cluster Management

---

#### US-01: Phân biệt Control Plane Availability trên trang danh sách

**As a** DevOps engineer managing multiple Kubernetes clusters,
**I want** to see clusters by their control plane availability (Single-AZ or Multi-AZ) on the cluster list page,
**So that** I can quickly identify which clusters have high availability configuration.

**Acceptance Criteria:**

```gherkin
Feature: Hiển thị Control Plane Availability trên trang danh sách Cluster

  Background:
    Given người dùng đang ở trang danh sách Kubernetes Cluster

  Scenario: Hiển thị cột Control Plane Availability
    When trang danh sách cluster được load
    Then hệ thống hiển thị cột "Control Plane Availability" trong bảng danh sách
    And cột "Control Plane Availability" nằm sau cột "Name"
    And mỗi cluster hiển thị giá trị "Single-AZ" hoặc "Multi-AZ"
```

---

#### US-02: Xem chi tiết Cluster Multi-AZ

**As a** DevOps engineer monitoring cluster infrastructure,
**I want** to view detailed information about my Multi-AZ Cluster including subnet distribution across availability zones,
**So that** I can verify the high availability setup and troubleshoot network issues across different AZs.

**Acceptance Criteria:**

```gherkin
Feature: Xem thông tin chi tiết của Multi-AZ Cluster

  Background:
    Given người dùng đang ở trang chi tiết của một Multi-AZ Cluster

  Scenario: Hiển thị Control Plane Availability trong General Information
    When trang chi tiết cluster được load
    Then hệ thống hiển thị field "Control Plane Availability" trong section "General Information"
    And giá trị hiển thị là "Multi-AZ" với badge màu xanh đậm

  Scenario: Hiển thị danh sách Subnets với AZ
    When trang chi tiết cluster được load
    Then hệ thống hiển thị field "Subnets" trong section Network
    And hiển thị danh sách tất cả subnets đang sử dụng:
      | Subnet Name | Subnet ID                    | AZ     | CIDR          |
      | subnet-1    | sub-85ba01f6-02ec-4dfc-...  | HCM-1A | 0.0.0.0/16    |
      | subnet-2    | sub-12345678-abcd-efgh-...  | HCM-1B | 0.0.0.0/16    |

  Scenario: Copy Subnet ID
    Given trang chi tiết cluster đang hiển thị danh sách Subnets
    When người dùng click vào icon copy bên cạnh Subnet ID
    Then Subnet ID được copy vào clipboard
    And hiển thị tooltip/toast "Copied" để xác nhận

  Scenario: Hiển thị Availability Zone trong Node Group
    When người dùng click vào tab "Node group"
    Then bảng Node Group hiển thị cột "Availability Zone"
    And mỗi node group hiển thị AZ tương ứng (VD: HCM-1A, HCM-1B)
```

---

#### US-03: Tạo Multi-AZ Cluster

**As a** platform engineer deploying production workloads,
**I want** to create a Kubernetes Cluster with Multi-AZ configuration by selecting subnets from different availability zones,
**So that** I can ensure high availability for my applications and protect against AZ-level failures without manual intervention.

**Acceptance Criteria:**

```gherkin
Feature: Tạo Kubernetes Cluster với Multi-AZ Configuration

  Background:
    Given người dùng đang ở trang tạo mới Kubernetes Cluster

  Scenario: Hiển thị Control Plane Availability selection
    When người dùng đến phần "Network Configuration"
    Then hệ thống hiển thị trường "Control Plane Availability *" với badge [NEW] và 2 options trong dropdown:
      | Option     | Description                                                                                    |
      | Single-AZ  | Triển khai cluster trong một Availability Zone. Phù hợp cho môi trường development và testing. |
      | Multi-AZ   | Triển khai cluster trên nhiều Availability Zones để đảm bảo High Availability.                 |
    And helper text: "Select a control plane availability of this cluster."

  Scenario: Chọn Single-AZ
    When người dùng chọn Control Plane Availability = "Single-AZ"
    Then trường "Subnet *" hiển thị là dropdown single-select
    And dropdown có default là subnet đầu tiên trong danh sách (VD: "sub-1A (10.60.0.0/24)")
    And người dùng có thể chọn lại subnet khác bất cứ lúc nào

  Scenario: VPC dropdown chỉ hiển thị VPC có DNS enable khi chọn Multi-AZ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    When người dùng click vào dropdown VPC
    Then dropdown chỉ hiển thị các VPC đã enable DNS
    And các VPC chưa enable DNS không hiển thị trong dropdown

  Scenario: Chọn Multi-AZ
    When người dùng chọn Control Plane Availability = "Multi-AZ"
    Then trường "Subnets *" hiển thị là multi-select dropdown
    And dropdown có default là 1 subnet mỗi zone (tự động chọn subnet đầu tiên của mỗi AZ có sẵn)
    And helper text: "Select Subnets for this Cluster. Note that each zone must have at least one Subnet."
    And các subnet đã chọn hiển thị dạng chip/tag bên dưới dropdown
    And mỗi chip hiển thị: "{subnet_name} {CIDR} • {AZ}" với nút (x) để xóa
    And ví dụ: nếu VPC có subnet ở HCM-1A và HCM-1B, default sẽ chọn sẵn 2 subnet (1 subnet/zone)

  Scenario: Default subnet selection cho Multi-AZ
    Given người dùng đã chọn VPC với các subnets:
      | Subnet Name | AZ     | CIDR           |
      | sub-1A      | HCM-1A | 10.60.0.0/24   |
      | sub-2A      | HCM-1A | 10.60.3.0/24   |
      | sub-1B      | HCM-1B | 10.60.1.0/24   |
      | sub-1C      | HCM-1C | 10.60.2.0/24   |
    When người dùng chọn Control Plane Availability = "Multi-AZ"
    Then hệ thống tự động chọn sẵn 3 subnet (1 subnet đầu tiên của mỗi AZ):
      | Subnet Name | AZ     |
      | sub-1A      | HCM-1A |
      | sub-1B      | HCM-1B |
      | sub-1C      | HCM-1C |
    And sub-2A không được chọn mặc định (vì đã có sub-1A cùng AZ HCM-1A)
    And người dùng có thể thêm/bớt subnet tùy ý

  Scenario: Xóa subnet đã chọn trong Multi-AZ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    And đã chọn các subnets: sub-1A (10.60.0.0/24) • HCM-1A, sub-1B (10.60.1.0/24) • HCM-1B
    When người dùng click nút (x) trên chip sub-1B
    Then sub-1B bị xóa khỏi danh sách đã chọn
    And sub-1B quay lại dropdown để có thể chọn lại

  Scenario: Validation - VPC không có subnet
    Given người dùng đã chọn VPC
    When VPC không có subnet nào
    Then hệ thống hiển thị warning message màu đỏ dưới field Subnets
    And nút "Create Cluster" bị disable

  Scenario: Validation - Chưa đủ subnet cho Multi-AZ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    When người dùng chỉ chọn 1 subnet
    Then hệ thống hiển thị warning message: "Vui lòng chọn ít nhất 2 subnet"
    And nút "Create Cluster" bị disable

  Scenario: Validation - Subnet cùng AZ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    When người dùng chọn 2 subnet cùng thuộc 1 AZ
    Then hệ thống hiển thị error message: "Các subnet phải thuộc ít nhất 2 Availability Zone khác nhau"
    And nút "Create Cluster" bị disable

  Scenario: Chọn đủ subnet hợp lệ cho Multi-AZ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    When người dùng chọn subnet sub-1A (10.60.0.0/24) ở HCM-1A
    And người dùng chọn subnet sub-1B (10.60.1.0/24) ở HCM-1B
    Then validation passed
    And nút "Create Cluster" được enable

  Scenario Outline: Tổ hợp subnet hợp lệ và không hợp lệ
    Given người dùng đã chọn Control Plane Availability = "Multi-AZ"
    When người dùng chọn các subnet:
      | Subnet                | AZ          |
      | <sub1>                | <az1>       |
      | <sub2>                | <az2>       |
    Then validation result là <result>

    Examples:
      | sub1                  | az1    | sub2                  | az2    | result   |
      | sub-1A (10.60.0.0/24) | HCM-1A | sub-1B (10.60.1.0/24) | HCM-1B | Valid    |
      | sub-1A (10.60.0.0/24) | HCM-1A | sub-1C (10.60.2.0/24) | HCM-1C | Valid    |
      | sub-1A (10.60.0.0/24) | HCM-1A | sub-2A (10.60.3.0/24) | HCM-1A | Invalid  |
      | sub-1B (10.60.1.0/24) | HCM-1B | sub-2B (10.60.4.0/24) | HCM-1B | Invalid  |

  Scenario: Tạo Multi-AZ Cluster thành công
    Given người dùng đã điền đầy đủ thông tin hợp lệ
    And Control Plane Availability = "Multi-AZ"
    And đã chọn ít nhất 2 subnets từ 2 AZ khác nhau
    When người dùng click "Create Cluster"
    Then hệ thống tạo cluster với Multi-AZ configuration
    And Control Plane được triển khai trên các AZ đã chọn
    And người dùng được chuyển đến trang chi tiết Cluster
```

---

#### US-04: Cấu hình Node Group Network Setting khi tạo Multi-AZ Cluster

**As a** DevOps engineer creating a Multi-AZ Cluster,
**I want** to select a specific subnet (and its corresponding AZ) for the initial Node Group in the cluster creation flow,
**So that** I can control which Availability Zone my worker nodes are deployed in when the cluster is first created.

**Acceptance Criteria:**

```gherkin
Feature: Node Group Network Setting trong flow tạo Multi-AZ Cluster

  Background:
    Given người dùng đang ở trang tạo mới Kubernetes Cluster
    And người dùng đã chọn Control Plane Availability = "Multi-AZ"
    And đã chọn các subnets cho cluster: sub-1A (10.60.0.0/24) • HCM-1A, sub-1B (10.60.1.0/24) • HCM-1B

  Scenario: Hiển thị Node Group Network Setting cho Multi-AZ Cluster
    When người dùng đến section "Node group network setting"
    Then section hiển thị với các fields:
    And field "VPC *" hiển thị giá trị kế thừa từ Network Configuration (disabled, không cho phép thay đổi)
    And helper text dưới VPC: "Select a VPC for this server. Click here to manage your VPCs."
    And field "Subnet *" hiển thị là dropdown với các subnets đã chọn cho cluster
    And dropdown có default là subnet đầu tiên: "sub-1A (10.60.0.0/24)"
    And helper text dưới Subnet: "Select a Subnet for this Cluster."

  Scenario: VPC kế thừa từ Network Configuration
    When người dùng đến section "Node group network setting"
    Then field "VPC" hiển thị tên VPC đã chọn ở Network Configuration (VD: vinhph2-network (10.76.0.0))
    And field "VPC" có trạng thái disabled (read-only)

  Scenario: Chọn Subnet cho Node Group
    Given field "Subnet" đang hiển thị dropdown với default "sub-1A (10.60.0.0/24)"
    When người dùng click vào dropdown "Subnet"
    Then hệ thống hiển thị danh sách các subnets đã chọn cho cluster:
      | Display Value           | AZ     |
      | sub-1A (10.60.0.0/24)   | HCM-1A |
      | sub-1B (10.60.1.0/24)   | HCM-1B |
    And chỉ hiển thị các subnets đã chọn cho cluster, không hiển thị subnet khác trong VPC
    And có thể chọn lại subnet khác bất cứ lúc nào

  Scenario: Tạo Cluster với Node Group trong Subnet đã chọn
    Given người dùng đã chọn Subnet = "sub-1A (10.60.0.0/24)" cho Node Group
    And đã điền đầy đủ các thông tin khác
    When người dùng click "Create Cluster"
    Then hệ thống tạo cluster với Multi-AZ configuration
    And Node Group được tạo trong sub-1A (AZ: HCM-1A)
    And người dùng được chuyển đến trang chi tiết Cluster
```

---

#### US-05: Upgrade Cluster Control Plane (Multi-AZ)

**As a** user managing a Multi-AZ Cluster,
**I want** to upgrade my cluster to a supported Kubernetes version,
**So that** I can use new features securely while maintaining high availability.

> **Note:** US này không thay đổi UI portal hiện tại, chỉ mô tả behavior cần QC verify cho Multi-AZ cluster.

**Acceptance Criteria:**

```gherkin
Feature: Upgrade Control Plane cho Multi-AZ Cluster

  Background:
    Given người dùng có một Multi-AZ Cluster đang hoạt động
    And cluster đang ở version cũ hơn (VD: v1.29.x)
    And có version mới được hỗ trợ (VD: v1.30.x)

  Scenario: Upgrade Control Plane thành công
    Given người dùng đang ở trang chi tiết cluster
    When người dùng thực hiện upgrade Control Plane lên version mới
    Then hệ thống upgrade Control Plane trên tất cả các AZ
    And cluster vẫn available trong quá trình upgrade (rolling upgrade)
    And sau khi hoàn tất, Control Plane version hiển thị version mới
    And Cluster Type vẫn giữ nguyên là "Multi-AZ"

  Scenario: Cluster vẫn hoạt động trong quá trình upgrade
    Given quá trình upgrade đang diễn ra
    Then Control Plane vẫn có thể xử lý API requests
    And các workload hiện có không bị gián đoạn
    And Node Groups vẫn hoạt động bình thường

  Scenario: Rollback khi upgrade thất bại
    Given quá trình upgrade gặp lỗi
    Then hệ thống tự động rollback về version trước đó
    And cluster trở về trạng thái ổn định
    And thông báo lỗi được hiển thị cho người dùng
```

---

#### US-06: Delete Cluster (Multi-AZ)

**As a** user,
**I want** to delete a Multi-AZ cluster,
**So that** unused resources are cleaned up properly across all availability zones.

> **Note:** US này không thay đổi UI portal hiện tại, chỉ mô tả behavior cần QC verify cho Multi-AZ cluster.

**Acceptance Criteria:**

```gherkin
Feature: Delete Multi-AZ Cluster

  Background:
    Given người dùng có một Multi-AZ Cluster
    And cluster có resources trên nhiều AZ (VD: HAN-01, HAN-02)

  Scenario: Delete Multi-AZ Cluster thành công
    Given người dùng đang ở trang chi tiết cluster hoặc trang danh sách
    When người dùng thực hiện delete cluster
    And xác nhận hành động delete
    Then hệ thống xóa tất cả Control Plane components trên mọi AZ
    And hệ thống xóa tất cả Node Groups và Worker Nodes
    And hệ thống giải phóng tất cả network resources (subnets vẫn còn trong VPC)
    And cluster bị xóa khỏi danh sách
    And người dùng được chuyển về trang danh sách cluster

  Scenario: Cleanup resources across all AZs
    Given quá trình delete đang diễn ra
    Then resources trên AZ HAN-01 được cleanup
    And resources trên AZ HAN-02 được cleanup
    And không còn orphaned resources sau khi delete hoàn tất

  Scenario: Delete cluster có Node Groups ở nhiều AZ
    Given cluster có Node Group 1 ở HAN-01
    And cluster có Node Group 2 ở HAN-02
    When người dùng delete cluster
    Then tất cả Node Groups đều bị xóa
    And Worker Nodes ở cả 2 AZ đều được terminate
```

---

## 3. Functional Requirements

### 3.1 Trang Danh sách Cluster (Cluster List Page)

#### 3.1.1 Current State

- Hiển thị danh sách cluster với các cột: Name, Control plane version, Status, Access, Total nodes, Created at
- Không có thông tin về Control Plane Availability

#### 3.1.2 Proposed Changes

**Bổ sung cột Control Plane Availability:**

| Cột                       | Vị trí        | Giá trị            | Badge Style                                       |
| -------------------------- | --------------- | -------------------- | ------------------------------------------------- |
| Control Plane Availability | Sau cột "Name" | Single-AZ / Multi-AZ | Single-AZ: Badge xám, Multi-AZ: Badge xanh đậm |

**Behavior:**

- Cột Control Plane Availability hiển thị badge để phân biệt trực quan giữa Single-AZ và Multi-AZ cluster
- Các cluster hiện tại (trước khi có Multi-AZ) sẽ hiển thị là "Single-AZ"

---

### 3.2 Trang Chi tiết Cluster (Cluster Detail Page)

#### 3.2.1 Current State

- Section "General Information" hiển thị: ID, Version, Description, Created at, Whitelist, BlockStore CSI Driver, vLB Integration, Fleet
- Section Network hiển thị: VPC, Subnet (single), Network Type, Access

#### 3.2.2 Proposed Changes

**A. General Information - Bổ sung:**

| Field                      | Vị trí            | Giá trị                                                |
| -------------------------- | ------------------- | -------------------------------------------------------- |
| Control Plane Availability | Sau field "Version" | Single-AZ (badge xám) hoặc Multi-AZ (badge xanh đậm) |

**B. Network Section - Thay đổi cho Multi-AZ:**

| Field   | Single-AZ                                    | Multi-AZ                                       |
| ------- | -------------------------------------------- | ---------------------------------------------- |
| Subnet  | Hiển thị 1 subnet: "sub-1A (10.60.0.0/24)" | Không hiển thị                              |
| Subnets | Không hiển thị                            | Hiển thị danh sách subnets với AZ và CIDR |

**Format hiển thị Subnets cho Multi-AZ:**

```
Subnets (2)
├── sub-85ba01f6-02ec-4dfc-8884-ee0036c68a5b
│   Name: sub-1A (10.60.0.0/24) | AZ: HCM-1A
└── sub-12345678-abcd-efgh-ijkl-mnopqrstuvwx
    Name: sub-1B (10.60.1.0/24) | AZ: HCM-1B
```

**C. Node Group Tab - Bổ sung cột:**

| Cột              | Vị trí                   | Mô tả                                            |
| ----------------- | -------------------------- | -------------------------------------------------- |
| Availability Zone | Sau cột "Node Group Name" | Hiển thị AZ của node group (VD: HCM-1A, HCM-1B) |

---

### 3.3 Trang Tạo mới Cluster (Create Cluster Page)

#### 3.3.1 Current State

- Phần Network Configuration có field "Subnet" là dropdown single-select
- Không có lựa chọn Control Plane Availability

#### 3.3.2 Proposed Changes

**A. Control Plane Availability Selection (Mới)**

| Field                        | Type     | Options             | Default   | Required |
| ---------------------------- | -------- | ------------------- | --------- | -------- |
| Control Plane Availability * | Dropdown | Single-AZ, Multi-AZ | Single-AZ | Yes      |

- Badge [NEW] hiển thị bên cạnh label "Control Plane Availability"
- Helper text: "Select a control plane availability of this cluster."

**B. Subnet/Subnets Selection**

| Control Plane Availability | Field Label | Type                   | Default                                                               | Validation                                          |
| -------------------------- | ----------- | ---------------------- | --------------------------------------------------------------------- | --------------------------------------------------- |
| Single-AZ                  | Subnet *    | Dropdown single-select | Subnet đầu tiên trong danh sách                                   | Required, chọn 1 subnet, có thể chọn lại       |
| Multi-AZ                   | Subnets *   | Multi-select dropdown  | 1 subnet mỗi zone (tự động chọn subnet đầu tiên của mỗi AZ) | Required, tối thiểu 2 subnets từ 2 AZ khác nhau |

**Default Value:**

- **Single-AZ:** Dropdown có default là subnet đầu tiên trong danh sách (VD: "sub-1A (10.60.0.0/24)")
- **Multi-AZ:** Tự động chọn sẵn 1 subnet mỗi zone có trong VPC
  - Ví dụ: Nếu VPC có subnets ở HCM-1A, HCM-1B, HCM-1C → Default chọn sẵn 3 subnets (1 subnet đầu tiên của mỗi AZ)
  - Ví dụ: Nếu VPC chỉ có subnets ở HCM-1A và HCM-1B → Default chọn sẵn 2 subnets (1 subnet/zone)

**Helper text cho Subnets (Multi-AZ):**

- "Select Subnets for this Cluster. Note that each zone must have at least one Subnet."

**Subnet Chip Display cho Multi-AZ:**

Các subnet đã chọn hiển thị dạng chip/tag bên dưới dropdown:

| Element     | Description                                            |
| ----------- | ------------------------------------------------------ |
| Chip format | "{subnet_name} {CIDR} • {AZ}" với nút (x) để xóa |
| Ví dụ     | "sub-1A 10.60.0.0/24 • HCM-1A" [x]                    |

**Behavior:**

- **Single-AZ:** Dropdown có default là subnet đầu tiên trong danh sách
- **Multi-AZ:** Hệ thống tự động chọn sẵn 1 subnet đầu tiên của mỗi AZ có trong VPC
- Click (x) trên chip để xóa subnet khỏi danh sách đã chọn
- Subnet bị xóa sẽ quay lại dropdown để có thể chọn lại
- Có thể chọn lại subnet bất cứ lúc nào (cả Single-AZ và Multi-AZ)
- User có thể thêm/bớt subnet nhưng phải đảm bảo tối thiểu 2 subnet từ 2 AZ khác nhau (Multi-AZ)

**C. Advanced Cilium Network Setting (khi Network type = Cilium VPC Native Routing)**

> **Note:** Section này chỉ hiển thị khi Network type = "Cilium VPC Native Routing"

| Field                 | Type     | Description                                                                 | Required |
| --------------------- | -------- | --------------------------------------------------------------------------- | -------- |
| Node CIDR mask size * | Dropdown | Specifies the size of the IP address range allocated for pods on each node. | Yes      |

- Helper text: "Specifies the size of the IP address range allocated for pods on each node. Click here to learn more."
- Field "Default Pod IP range" được move xuống section "Node group network setting"

#### 3.3.3 Business Rules

| Rule                       | Description                                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Default Subnets (Multi-AZ) | Khi chọn Multi-AZ, hệ thống tự động chọn sẵn 1 subnet đầu tiên của mỗi AZ có trong VPC                                          |
| Minimum Subnets            | Multi-AZ Cluster yêu cầu tối thiểu 2 subnets                                                                                              |
| AZ Distribution            | Các subnets phải thuộc ít nhất 2 AZ khác nhau                                                                                           |
| Same VPC                   | Tất cả subnets phải thuộc cùng một VPC                                                                                                  |
| Node Group AZ              | Node Group sẽ được tạo trong AZ của subnet được chọn                                                                                |
| VPC No Subnet              | Nếu VPC không có subnet, hiển thị warning message màu đỏ                                                                              |
| DNS in VPC                 | Multi-AZ Control Plane chỉ support VPC có DNS enable. Nếu VPC chưa enable DNS, hệ thống sẽ không hiển thị VPC đó khi tạo cluster |

> **⚠️ Prerequisite (VPC):** Để tạo Multi-AZ Cluster, VPC phải được bật **DNS**. Đây là yêu cầu bắt buộc được cấu hình bên VPC, không hiển thị trên UI của VKS. Nếu VPC chưa bật DNS, hệ thống sẽ không hiển thị VPC đó khi tạo cluster.

---

### 3.4 Node Group Network Setting (trong Create Cluster Flow)

#### 3.4.1 Current State

- Khi tạo Cluster (Single-AZ), section "Node group network setting" không có field chọn Subnet vì Node Group tự động sử dụng subnet đã chọn cho Cluster
- VPC được kế thừa từ Network Configuration

#### 3.4.2 Proposed Changes cho Multi-AZ Cluster

**Section: Node group network setting** (trong flow tạo mới Cluster)

| Field                     | Type                            | Behavior                                                     | Required |
| ------------------------- | ------------------------------- | ------------------------------------------------------------ | -------- |
| Public/Private Node group | Radio Button Group (card style) | Giữ nguyên như hiện tại                                 | Yes      |
| VPC *                     | Dropdown (disabled)             | Kế thừa từ Network Configuration, hiển thị read-only    | -        |
| Subnet *                  | Dropdown (single-select)        | Chọn 1 subnet từ danh sách subnets đã chọn cho cluster | Yes      |
| Whitelist IP              | Text input                      | Giữ nguyên như hiện tại                                 | No       |

**Chi tiết các field:**

**A. VPC (Read-only)**

- Hiển thị tên VPC và CIDR đã chọn ở Network Configuration (VD: "vinhph2-network (10.76.0.0)")
- Trạng thái: Disabled (không cho phép thay đổi)
- Helper text: "Select a VPC for this server. Click here to manage your VPCs."

**B. Subnet Selection**

- Label: "Subnet *"
- Type: Dropdown single-select
- Default: IP đầu tiên trong danh sách subnet (VD: "sub-1A (10.60.0.0/24)")
- Options: Chỉ hiển thị các subnets đã chọn cho Multi-AZ Cluster ở bước Network Configuration
- Format hiển thị: "{subnet_name} ({CIDR})" - VD: "sub-1A (10.60.0.0/24)"
- Helper text: "Select a Subnet for this Cluster."
- AZ được xác định tự động dựa trên subnet đã chọn
- Có thể chọn lại subnet khác bất cứ lúc nào

**Dropdown Options Example:**

| Display Value         | Subnet ID        | AZ     |
| --------------------- | ---------------- | ------ |
| sub-1A (10.60.0.0/24) | sub-85ba01f6-... | HCM-1A |
| sub-1B (10.60.1.0/24) | sub-12345678-... | HCM-1B |

**C. Advanced Cilium Network Setting (khi Network type = Cilium VPC Native Routing)**

> **Note:** Section này chỉ hiển thị khi Network type = "Cilium VPC Native Routing"

| Field                | Type     | Description                                                                                                                 | Required |
| -------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------- | -------- |
| Default Pod IP range | Dropdown | Default Pod IP range will be applied to Node groups by default. Another range can be selected for Node groups if necessary. | Yes      |

- Helper text: "Specifies the IP address range allocated for pods."
- Field này được move từ Cluster level (Network Configuration) xuống Node Group level
- Mỗi Node Group có thể chọn Pod IP range khác với default nếu cần

#### 3.4.3 Business Rules cho Node Group Network Setting

| Rule             | Description                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| VPC Inheritance  | VPC của Node Group bắt buộc kế thừa từ Network Configuration, không cho phép thay đổi |
| Subnet Scope     | Chỉ hiển thị các subnets đã chọn cho cluster ở Network Configuration                    |
| Single Subnet    | Mỗi Node Group chỉ được chọn 1 subnet (và 1 AZ tương ứng)                             |
| AZ Determination | AZ của Node Group được xác định tự động dựa trên subnet đã chọn                  |
| Reselectable     | Có thể chọn lại subnet khác bất cứ lúc nào trước khi tạo cluster                    |
| Immutable Subnet | Không thể thay đổi subnet của Node Group sau khi đã tạo cluster                         |

---

## 4. UI/UX Specifications

### 4.1 Trang Danh sách Cluster (Cluster List)

| Component                         | Type         | Mô tả                                             |
| --------------------------------- | ------------ | --------------------------------------------------- |
| Control Plane Availability Column | Badge (text) | Hiển thị "Single-AZ" hoặc "Multi-AZ" dạng badge |

### 4.2 Trang Chi tiết Cluster (Cluster Detail)

| Component                  | Type                     | Mô tả                                                                   |
| -------------------------- | ------------------------ | ------------------------------------------------------------------------- |
| Control Plane Availability | Badge (text)             | Hiển thị trong section General Information                              |
| Subnets List               | List với tree structure | Hiển thị danh sách subnets với thông tin: Name, ID, AZ (badge), CIDR |
| AZ Column (Node Group)     | Badge (text)             | Cột mới trong bảng Node Group                                          |

### 4.3 Trang Tạo Cluster (Create Cluster)

| Component                  | Type                     | Mô tả                                                                             |
| -------------------------- | ------------------------ | ----------------------------------------------------------------------------------- |
| Control Plane Availability | Dropdown                 | 2 options: Single-AZ, Multi-AZ                                                      |
| NEW Badge                  | Badge (text)             | Hiển thị bên cạnh label "Control Plane Availability"                            |
| Subnet (Single-AZ)         | Dropdown (single-select) | Chọn 1 subnet, có thể chọn lại                                                 |
| Subnets (Multi-AZ)         | Multi-select dropdown    | Cho phép chọn nhiều subnet, hiển thị chips bên dưới với nút (x) để xóa |
| Subnet Chip                | Chip/Tag                 | Format: "{subnet_name} {CIDR} • {AZ}" với nút (x)                                |
| Validation Message         | Alert (warning/error)    | Hiển thị khi chưa đủ điều kiện subnet hoặc VPC không có subnet           |

### 4.4 Node Group Network Setting (trong Create Cluster Flow)

| Component                 | Type                            | Mô tả                                                         |
| ------------------------- | ------------------------------- | --------------------------------------------------------------- |
| Public/Private Node group | Radio Button Group (card style) | Giữ nguyên như hiện tại                                    |
| VPC *                     | Dropdown (disabled)             | Hiển thị VPC kế thừa từ Network Configuration, read-only   |
| VPC Helper text           | Text                            | "Select a VPC for this server. Click here to manage your VPCs." |
| Subnet *                  | Dropdown (single-select)        | Chọn 1 subnet từ danh sách subnets đã chọn cho cluster    |
| Subnet Helper text        | Text                            | "Select a Subnet for this Cluster."                             |
| Whitelist IP              | Text input                      | Giữ nguyên như hiện tại                                    |

### 4.5 Component Types Summary

| Component Type            | Sử dụng cho                                                        |
| ------------------------- | -------------------------------------------------------------------- |
| Badge (text)              | Control Plane Availability, AZ label, NEW badge                      |
| Dropdown (single-select)  | Control Plane Availability, Subnet selection (Single-AZ, Node Group) |
| Multi-select dropdown     | Subnets selection (Multi-AZ)                                         |
| Chip/Tag                  | Hiển thị subnets đã chọn trong Multi-AZ                         |
| Radio Button Group (card) | Public/Private Node group                                            |
| Alert (warning/error)     | Validation messages                                                  |
| List (tree structure)     | Subnets display trong Detail page                                    |
| Text (disabled)           | VPC display (read-only)                                              |

---

## 5. Validation Rules

### 5.1 Create Cluster Validation

| Field                      | Rule                                        | Error Message                                                                       |
| -------------------------- | ------------------------------------------- | ----------------------------------------------------------------------------------- |
| Cluster Name               | Required, 3-63 chars, alphanumeric + hyphen | "Tên cluster phải từ 3-63 ký tự, chỉ bao gồm chữ, số và dấu gạch ngang" |
| Control Plane Availability | Required                                    | "Vui lòng chọn control plane availability"                                        |
| VPC                        | Required                                    | "Vui lòng chọn VPC"                                                               |
| VPC No Subnet              | VPC phải có ít nhất 1 subnet            | Warning message màu đỏ dưới field Subnets                                      |
| Subnet (Single-AZ)         | Required, 1 subnet                          | "Vui lòng chọn subnet"                                                            |
| Subnets (Multi-AZ)         | Required, min 2 subnets                     | "Vui lòng chọn ít nhất 2 subnet"                                                |
| Subnets AZ (Multi-AZ)      | Min 2 different AZs                         | "Các subnet phải thuộc ít nhất 2 Availability Zone khác nhau"                 |
| Subnets VPC (Multi-AZ)     | Same VPC                                    | "Tất cả subnet phải thuộc cùng một VPC"                                       |

### 5.2 Node Group Network Setting Validation (trong Create Cluster Flow)

| Field  | Rule                                        | Error Message                                                  |
| ------ | ------------------------------------------- | -------------------------------------------------------------- |
| Subnet | Must be from cluster's selected subnet list | "Subnet phải thuộc danh sách subnet đã chọn cho cluster" |

### 5.3 Business Rules

| Rule                                 | Description                                                                                                        |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| Immutable Control Plane Availability | Không thể thay đổi Control Plane Availability sau khi tạo cluster                                             |
| Immutable Subnets (Cluster)          | Không thể thêm/bớt subnet sau khi tạo Multi-AZ cluster                                                        |
| Immutable Subnet (Node Group)        | Không thể thay đổi subnet của Node Group sau khi đã tạo cluster                                            |
| Node Group Subnet Scope              | Khi tạo Multi-AZ cluster, Node Group chỉ có thể chọn 1 trong các subnets đã chọn ở Network Configuration |
| VPC Inheritance                      | VPC của Node Group bắt buộc kế thừa từ Network Configuration, không cho phép thay đổi                    |
| Reselectable Subnet                  | Có thể chọn lại subnet (cả Single-AZ và Multi-AZ) trước khi tạo cluster                                   |
| Removable Subnet (Multi-AZ)          | Có thể xóa subnet đã chọn bằng nút (x) trên chip trong Multi-AZ                                           |

---

## 6. Technical Notes

### 6.1 Multi-AZ Architecture

**Control Plane Distribution (Multi-AZ):**

- Control Plane components (API Server, Controller Manager, Scheduler) được triển khai trên nhiều AZ
- etcd cluster được replicate across AZs để đảm bảo data consistency
- Load Balancer phân phối traffic đến Control Plane nodes trên các AZ
- Nếu 1 AZ gặp sự cố, Control Plane vẫn hoạt động bình thường từ AZ còn lại

**Node Group (Single-AZ per Node Group):**

- Mỗi Node Group chỉ triển khai trong 1 subnet (1 AZ)
- Người dùng có thể tạo nhiều Node Group ở các AZ khác nhau để phân bổ workload
- Khi tạo cluster, Node Group đầu tiên chọn 1 trong các subnets đã cấu hình cho cluster

**Network Flow:**

```
                    ┌─────────────────────────────────────────┐
                    │              VPC (10.60.0.0/16)          │
                    │                                         │
┌───────────────────┼─────────────────────────────────────────┼───────────────────┐
│                   │                                         │                   │
│   ┌───────────────┴───────────────┐   ┌───────────────────┴───────────────┐   │
│   │         AZ: HAN-01            │   │         AZ: HAN-02                │   │
│   │    Subnet: 10.60.0.0/24       │   │    Subnet: 10.60.1.0/24           │   │
│   │                               │   │                                   │   │
│   │   ┌─────────────────────┐     │   │   ┌─────────────────────┐         │   │
│   │   │   Control Plane     │     │   │   │   Control Plane     │         │   │
│   │   │   (API Server)      │     │   │   │   (API Server)      │         │   │
│   │   └─────────────────────┘     │   │   └─────────────────────┘         │   │
│   │                               │   │                                   │   │
│   │   ┌─────────────────────┐     │   │                                   │   │
│   │   │   Worker Nodes      │     │   │   (Node Group có thể tạo         │   │
│   │   │   (Node Group 1)    │     │   │    thêm ở AZ này sau)            │   │
│   │   └─────────────────────┘     │   │                                   │   │
│   │                               │   │                                   │   │
│   └───────────────────────────────┘   └───────────────────────────────────┘   │
│                                                                               │
│                        ┌─────────────────────┐                                │
│                        │   vLB Multi-AZ      │                                │
│                        │   (Load Balancer)   │                                │
│                        └─────────────────────┘                                │
│                                                                               │
└───────────────────────────────────────────────────────────────────────────────┘
```

> **Note:** Diagram trên minh họa trường hợp Node Group 1 được tạo trong AZ HAN-01. Người dùng có thể tạo thêm Node Group khác trong AZ HAN-02 sau khi cluster đã được tạo.

### 6.2 Dependencies

| Component                 | Role                                         | Status      |
| ------------------------- | -------------------------------------------- | ----------- |
| vLB Multi-AZ              | Load Balancer phân phối traffic across AZs | Done        |
| Private Endpoint Multi-AZ | Internal endpoint cho cross-AZ communication | QC          |
| vDNS Multi-AZ             | DNS resolution cho internal services         | In Progress |
| VKS Core                  | Control Plane và Node Group management      | QC          |

### 6.3 QC Test Criteria (Backend/Infrastructure)

> **Note:** Các tiêu chí kiểm thử dưới đây là guideline cho QC verify backend/infrastructure behavior của Multi-AZ Cluster. QC sẽ tự define chi tiết test cases và bổ sung dựa trên các criteria này.

---

#### Category 2: Kubernetes Core Functionality

| User Story | Description                                                                                         | Expected Behavior                                                   |
| ---------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| US-2.1     | **Kubernetes API Access** - Cluster user truy cập cluster qua kubectl                        | API server accessible, kubectl commands hoạt động bình thường |
| US-2.2     | **Workload Deployment** - Deploy các loại workload (Deployment, StatefulSet, DaemonSet)     | Pods được schedule và chạy đúng cách                        |
| US-2.3     | **Service Networking** - Kubernetes Services hoạt động (ClusterIP, NodePort, LoadBalancer) | Services reachable, cross-AZ communication hoạt động             |
| US-2.5     | **Scaling Workloads** - Scale up/down workloads, HPA auto-scaling                             | Pods scale đúng, distributed across nodes/AZs                     |
| US-2.6     | **AZ Outage Behavior** - Cluster vẫn hoạt động khi 1 AZ down                              | Cluster operational, workloads tiếp tục chạy trên healthy AZs   |

---

#### Category 3: High Availability & Resilience Control Plane

| User Story | Description                                                                                     | Expected Behavior                                                |
| ---------- | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| US-3.1     | **Control Plane Multi-AZ Distribution** - Control plane components chạy trên nhiều AZs | Pods distributed ≥ 2 AZs, etcd quorum maintained, maxSkew ≤ 1  |
| US-3.2     | **AZ Recovery** - Cluster tự động recover khi AZ khôi phục                           | Cluster detect recovered zone, pods rebalance (với Descheduler) |

**Infrastructure Test Scenarios:**

| Scenario                | Zones | Computes  | Compute Diff | Expected: Scale Up      | Expected: Scale Down |
| ----------------------- | ----- | --------- | ------------ | ----------------------- | -------------------- |
| Best practice (3-zone)  | 3     | ≥ 7      | ≤ 1         | PASS                    | PASS                 |
| Best practice (2-zone)  | 2     | ≥ 7      | ≤ 1         | PASS                    | PASS                 |
| Low computes            | 2-3   | 3 < x < 7 | ≤ 1         | FAIL (PodsPending)      | PASS                 |
| Unbalanced distribution | 2-3   | ≥ 7      | > 1          | WARNING (ZoneImbalance) | PASS                 |

**Failure & Recovery Scenarios:**

| Scenario                     | Expected Behavior                                                        |
| ---------------------------- | ------------------------------------------------------------------------ |
| 1 AZ down (3-zone → 2-zone) | Service maintained, pods reschedule to healthy AZs                       |
| 1-2 computes down in 1 zone  | Auto reschedule, service maintained                                      |
| Zone recovery                | Pods rebalance với Descheduler hoặc manual `kubectl rollout restart` |

---

#### Category 4: Operations & Stability

| User Story | Description                                                          | Expected Behavior                                       |
| ---------- | -------------------------------------------------------------------- | ------------------------------------------------------- |
| US-4.1     | **Scale Control Plane** - Scale up/down control plane replicas | No service disruption, PDB respected, quorum maintained |
| US-4.2     | **Backup & Restore** - Backup và restore cluster state        | etcd backup/restore thành công, workloads intact      |

**HPA Scaling Thresholds (Reference):**

| Metric | Scale Up | Scale Down |
| ------ | -------- | ---------- |
| CPU    | > 85%    | < 50%      |
| Memory | > 70%    | < 40%      |

---

#### Key Findings Summary

| Status | Finding                            | Impact                                    |
| ------ | ---------------------------------- | ----------------------------------------- |
| ✅     | 3-zone với ≥7 computes, balanced | All operations PASS                       |
| ✅     | 2-zone với ≥7 computes           | Scale operations PASS                     |
| ❌     | Low compute (3 < x < 7)            | Scale-up FAIL (PodsPending)               |
| ⚠️   | Unbalanced distribution            | ZoneImbalance warning                     |
| ⚠️   | Without Descheduler                | Manual intervention required for recovery |

### 6.4 Backend Requirements (Reference từ QC)

> **Note:** Các yêu cầu dưới đây là backend/infrastructure requirements, không thuộc scope UI của PRD này. Tham khảo chi tiết tại: `k8s-multiAZ-deployment-test-tracking.pdf`

**MUST HAVE:**

| Requirement             | Description                                  | Risk if Not Met                          |
| ----------------------- | -------------------------------------------- | ---------------------------------------- |
| ≥ 2 Availability Zones | Deploy Control Plane across at least 2 zones | Single point of failure, no HA guarantee |

**SHOULD HAVE:**

| Requirement                | Description                                        | Risk if Not Met                                           |
| -------------------------- | -------------------------------------------------- | --------------------------------------------------------- |
| Balanced Node Distribution | Ensure node count across compute hosts is similar  | Inefficient resource utilization, podAntiAffinity issues  |
| Automated Zone Recovery    | Implement automatic rebalancing when zone recovers | Manual intervention required, delayed service restoration |
| Monitoring & Alerting      | Monitor zone health and pod distribution           | Delayed detection of zone imbalance or failures           |
| Pod Disruption Budgets     | Set PDBs for control plane components              | Service disruption during zone failures or maintenance    |

---

## 7. Success Metrics

| Metric                                 | Target                    | Measurement                                                |
| -------------------------------------- | ------------------------- | ---------------------------------------------------------- |
| Multi-AZ Cluster Creation Success Rate | > 95%                     | Số cluster Multi-AZ tạo thành công / Tổng số request |
| Time to Create Multi-AZ Cluster        | < 20 mins                 | Thời gian từ submit đến cluster ACTIVE                 |
| Multi-AZ Adoption Rate                 | > 30% production clusters | Số Multi-AZ clusters / Tổng production clusters          |
| AZ Failover Recovery Time              | < 5 mins                  | Thời gian cluster phục hồi khi 1 AZ down                |
| User Error Rate (Subnet Selection)     | < 5%                      | Số lần validation fail / Tổng số attempts              |

---

## 8. Risks & Mitigations

### 8.1 UI/UX Risks

| Risk                            | Impact                     | Mitigation                                           |
| ------------------------------- | -------------------------- | ---------------------------------------------------- |
| User confusion về Cluster Type | Chọn sai loại cluster    | Clear UI descriptions, info boxes, tooltips          |
| Subnet selection complexity     | User chọn subnet cùng AZ | Real-time validation, visual AZ indicators           |
| Longer cluster creation time    | Poor UX                    | Progress indicator, estimated time display           |
| Higher cost for Multi-AZ        | Customer complaint         | Cost preview trước khi tạo, pricing documentation |
| Cross-AZ latency                | Performance impact         | Network optimization, proper placement               |
| vDNS dependency delay           | Blocking release           | Fallback plan với alternative DNS solution          |

### 8.2 Infrastructure Risks (Reference từ QC)

> **Note:** Các risks dưới đây liên quan đến backend/infrastructure, được QC identify trong quá trình test. Tham khảo chi tiết tại: `k8s-multiAZ-deployment-test-tracking.pdf`

| Risk                      | Impact                                    | Mitigation                                                     |
| ------------------------- | ----------------------------------------- | -------------------------------------------------------------- |
| Zone Imbalance            | Cascading failure khi dominant zone fails | Monitoring alerts (ZoneImbalance), Descheduler for rebalancing |
| Single Zone Failure       | Control Plane unavailable                 | ≥ 2 AZ deployment, automatic failover                         |
| Delayed Zone Recovery     | Manual intervention required              | Automated Pod Rebalancing with Descheduler                     |
| No Pod Disruption Budgets | Service disruption during maintenance     | Configure PDBs for control plane components                    |

---

## 9. Appendix

### A. Glossary

| Term                   | Definition                                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Availability Zone (AZ) | Một data center hoặc cluster data centers độc lập trong một region, có power, cooling và networking riêng biệt |
| Single-AZ Cluster      | Kubernetes cluster có Control Plane nằm trong 1 AZ                                                                     |
| Multi-AZ Cluster       | Kubernetes cluster có Control Plane được phân bổ trên nhiều AZ để đảm bảo High Availability                 |
| Control Plane          | Các thành phần quản lý cluster: API Server, Controller Manager, Scheduler, etcd                                     |
| Node Group             | Một nhóm Worker Nodes có cùng cấu hình (instance type, OS, etc.), triển khai trong 1 subnet (1 AZ)                |
| Private DNS            | Internal DNS service để resolve domain names trong VPC                                                                 |
| Failover               | Quá trình tự động chuyển đổi sang backup resource khi primary resource gặp sự cố                              |

### B. Comparison: Single-AZ vs Multi-AZ Cluster

| Feature                       | Single-AZ               | Multi-AZ                                     |
| ----------------------------- | ----------------------- | -------------------------------------------- |
| Control Plane Availability    | 99.9%                   | 99.99%                                       |
| Control Plane Fault Tolerance | Single point of failure | Tolerant to AZ failure                       |
| Cost                          | Lower                   | Higher (multi-AZ Control Plane)              |
| Latency                       | Lower (same AZ)         | Slightly higher (cross-AZ for Control Plane) |
| Network Complexity            | Simple                  | More complex                                 |
| Private DNS (VPC)             | Optional                | Required (prerequisite)                      |
| Use Case                      | Development, Testing    | Production, Mission-critical                 |
| Subnet Requirement            | 1 subnet                | Min 2 subnets (2 AZs) cho Control Plane      |
| Node Group Placement          | Single AZ (1 subnet)    | Single AZ per Node Group (chọn 1 subnet)    |

### C. UI Mockup Summary

**1. Cluster List Page:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ Kubernetes cluster                                                          │
├─────────────────────────────────────────────────────────────────────────────┤
│ [Search...]                                                                 │
├──────┬───────────────┬────────────────────┬────────┬────────┬───────────────┤
│ □    │ Name          │ Cluster Type       │ Status │ Access │ Created at    │
├──────┼───────────────┼────────────────────┼────────┼────────┼───────────────┤
│ □    │ tytv4         │ [Single-AZ]        │ ACTIVE │ Public │ 24/12/2025    │
│ □    │ prod-cluster  │ [Multi-AZ]         │ ACTIVE │ Public │ 24/12/2025    │
│ □    │ dev-cluster   │ [Single-AZ]        │ ACTIVE │ Public │ 23/12/2025    │
└──────┴───────────────┴────────────────────┴────────┴────────┴───────────────┘
```

**2. Create Cluster - Cluster Type Selection:**

```
┌─────────────────────────────────────────────────────────────────┐
│ Cluster Type *                                                  │
├─────────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ○ Single-AZ Cluster                                         │ │
│ │   Triển khai cluster trong một Availability Zone.           │ │
│ │   Phù hợp cho môi trường development và testing.            │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ● Multi-AZ Cluster                              [NEW]       │ │
│ │   Triển khai cluster trên nhiều Availability Zones          │ │
│ │   để đảm bảo High Availability.                             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ℹ️ Multi-AZ Cluster phân bổ Control Plane trên nhiều AZ,   │ │
│ │    đảm bảo cluster tiếp tục hoạt động khi 1 AZ gặp sự cố.  │ │
│ └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

**3. Create Cluster - Multi-AZ Subnet Selection:**

```
┌─────────────────────────────────────────────────────────────────┐
│ Subnets * (Default: 1 subnet mỗi zone)                          │
├─────────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ☑ sub-1A    │ sub-85ba01f6... │ [HAN-01] │ 10.60.0.0/24   │ │  ← Default selected
│ │ ☑ sub-1B    │ sub-12345678... │ [HAN-02] │ 10.60.1.0/24   │ │  ← Default selected
│ │ ☑ sub-1C    │ sub-abcdefgh... │ [HAN-03] │ 10.60.2.0/24   │ │  ← Default selected
│ │ ☐ sub-2A    │ sub-99999999... │ [HAN-01] │ 10.60.3.0/24   │ │  (cùng AZ với sub-1A)
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ ✅ Đã chọn 3 subnet từ 3 AZ khác nhau (default: 1 subnet/zone) │
│                                                                 │
│ Helper text: "Select Subnets for this Cluster. Note that each   │
│ zone must have at least one Subnet."                            │
└─────────────────────────────────────────────────────────────────┘
```

> **Note:** Khi chọn Multi-AZ, hệ thống tự động chọn sẵn 1 subnet đầu tiên của mỗi AZ có trong VPC. User có thể bỏ chọn hoặc chọn thêm subnet khác, miễn đảm bảo tối thiểu 2 subnet từ 2 AZ khác nhau.

### D. References

- [VKS Multi-AZ Implementation MOM](./MOM2412-VKS-Multi-AZ-Implementation.md)
- [AWS EKS Multi-AZ Best Practices](https://aws.amazon.com/blogs/containers/amazon-eks-cluster-multi-zone-auto-scaling-groups/)
- [GKE Regional Clusters](https://cloud.google.com/kubernetes-engine/docs/concepts/regional-clusters)
- [Azure AKS Availability Zones](https://docs.microsoft.com/en-us/azure/aks/availability-zones)
