# Sử dụng GreenNode CLI để quản lý VKS

### Giới thiệu

**GreenNode CLI** (lệnh `grn`) là công cụ dòng lệnh để quản lý tài nguyên GreenNode trực tiếp từ terminal. Với VKS, bạn có thể tạo và quản lý toàn bộ vòng đời **Cluster** và **Node Group** thay vì thao tác thủ công trên giao diện.

Tài liệu tham khảo lệnh đầy đủ: [https://vngcloud.github.io/greennode-cli/](https://vngcloud.github.io/greennode-cli/).

CLI là một trong các cách làm việc với VKS, bên cạnh [Console](README.md), [API](su-dung-api-de-khoi-tao-cluster-va-node-group.md) và [Terraform](su-dung-terraform-de-khoi-tao-cluster-va-node-group.md). Chọn CLI khi cần thao tác nhanh, lặp lại hoặc viết script tự động hoá nhẹ.

---

### 1. Cài đặt

Tài liệu gốc: [Installation](https://vngcloud.github.io/greennode-cli/installation/).

Tải binary mới nhất cho hệ điều hành của bạn từ [GitHub Releases](https://github.com/vngcloud/greennode-cli/releases).

**macOS**

```bash
# Apple Silicon (M1/M2/M3)
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-darwin-arm64
# Intel
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-darwin-amd64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Linux**

```bash
# x86_64
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-linux-amd64
# ARM64
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-linux-arm64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Windows:** tải `grn-windows-amd64.exe` từ GitHub Releases và thêm vào `PATH`.

**Build từ source** (cần [Go 1.22+](https://go.dev/dl/)): `git clone`, `cd greennode-cli/go`, `go build -o grn .`

Kiểm tra: `grn --version`

---

### 2. Cấu hình

Tài liệu gốc: [Configuration](https://vngcloud.github.io/greennode-cli/configuration/).

Chạy wizard và nhập thông tin:

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

Credential (Client ID / Secret) lấy tại **GreenNode IAM Portal → Service Accounts** ([hcm-3.console.vngcloud.vn/iam](https://hcm-3.console.vngcloud.vn/iam/)). Để trống **Project ID** thì wizard tự phát hiện.

**Region khả dụng:**

| Region    | VKS Endpoint                          |
| --------- | ------------------------------------- |
| `HCM-3` | `https://vks.api.vngcloud.vn`       |
| `HAN`   | `https://vks-han-1.api.vngcloud.vn` |

Cấu hình lưu tại `~/.greenode/credentials` (quyền `0600`) và `~/.greenode/config`. Có thể ghi đè bằng biến môi trường (`GRN_ACCESS_KEY_ID`, `GRN_SECRET_ACCESS_KEY`, `GRN_DEFAULT_REGION`, `GRN_DEFAULT_PROJECT_ID`, `GRN_PROFILE`, `GRN_DEFAULT_OUTPUT`) — biến môi trường ưu tiên hơn file.

Nhiều môi trường thì dùng profile: `grn configure --profile staging`, rồi `grn --profile staging vks ...`.

---

### 3. Các lệnh VKS

Tài liệu gốc: [VKS Commands Overview](https://vngcloud.github.io/greennode-cli/commands/vks/).

Cấu trúc: `grn [global-options] vks <command> [command-options]`. Xem trợ giúp bất kỳ lúc nào với `grn vks` hoặc `grn vks <command> --help`.

| Nhóm                  | Lệnh                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Cluster**      | [list-clusters](https://vngcloud.github.io/greennode-cli/commands/vks/list-clusters/), [get-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/get-cluster/), [create-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/create-cluster/), [update-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/update-cluster/), [delete-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/delete-cluster/)                                                                                                                                                                                                                                                                                                                                 |
| **Node Group**   | [list-nodegroups](https://vngcloud.github.io/greennode-cli/commands/vks/list-nodegroups/), [get-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/get-nodegroup/), [create-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/create-nodegroup/), [update-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/update-nodegroup/), [update-nodegroup-metadata](https://vngcloud.github.io/greennode-cli/commands/vks/update-nodegroup-metadata/), [upgrade-nodegroup-version](https://vngcloud.github.io/greennode-cli/commands/vks/upgrade-nodegroup-version/), [list-nodes](https://vngcloud.github.io/greennode-cli/commands/vks/list-nodes/), [delete-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/delete-nodegroup/) |
| **Versions**     | [list-cluster-versions](https://vngcloud.github.io/greennode-cli/commands/vks/list-cluster-versions/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Auto-Upgrade** | [config-auto-upgrade](https://vngcloud.github.io/greennode-cli/commands/vks/config-auto-upgrade/), [delete-auto-upgrade-config](https://vngcloud.github.io/greennode-cli/commands/vks/delete-auto-upgrade-config/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Auto-Healing** | [config-auto-healing](https://vngcloud.github.io/greennode-cli/commands/vks/config-auto-healing/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Events**       | [get-cluster-events](https://vngcloud.github.io/greennode-cli/commands/vks/get-cluster-events/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **Kubeconfig**   | [generate-kubeconfig](https://vngcloud.github.io/greennode-cli/commands/vks/generate-kubeconfig/), [update-kubeconfig](https://vngcloud.github.io/greennode-cli/commands/vks/update-kubeconfig/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **Quota**        | [get-quota](https://vngcloud.github.io/greennode-cli/commands/vks/get-quota/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **Waiter**       | [wait](https://vngcloud.github.io/greennode-cli/commands/vks/wait/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

Tuỳ chọn toàn cục (`--profile`, `--region`, `--output`, `--query`, `--endpoint-url`, `--debug`) và các chủ đề khác (Output, Pagination, Dry-run, Shell Completion) xem trong [tài liệu CLI](https://vngcloud.github.io/greennode-cli/).

---

### Ví dụ nhanh: tạo cluster đến khi kubectl chạy được

{% hint style="warning" %}
`create-cluster` chỉ dựng **control plane**. Cluster chưa có node worker cho tới khi tạo **Node Group**.
{% endhint %}

```bash
# 1. Tạo control plane
grn vks create-cluster --name my-cluster \
  --k8s-version v1.30.10-vks.1746550800 \
  --network-type CILIUM_OVERLAY --cidr 192.168.0.0/16 \
  --vpc-id <net-...> --subnet-id <sub-...>
grn vks wait cluster-active --cluster-id <cls-...>

# 2. Thêm node group
grn vks create-nodegroup --cluster-id <cls-...> --name default \
  --flavor-id <flv-...> --disk-type SSD --ssh-key-id <ssh-...> --num-nodes 2
grn vks wait nodegroup-active --cluster-id <cls-...> --nodegroup-id <ng-...>

# 3. Lấy kubeconfig rồi kiểm chứng
grn vks generate-kubeconfig --cluster-id <cls-...>
grn vks update-kubeconfig --cluster-id <cls-...>   # sau khi kubeconfig ACTIVE
kubectl get nodes
```

Xem `grn vks list-cluster-versions` để lấy `--k8s-version`; các ID còn lại (VPC, subnet, flavor, SSH key) lấy trên Console.

---

Nếu gặp vấn đề, liên hệ GreenNode qua email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Trung tâm hỗ trợ: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
