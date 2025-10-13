# Sử dụng API để khởi tạo Cluster và Node Group

### Giới thiệu

VKS API cho phép người dùng tự động khởi tạo **Cluster** và **Node Group** thay vì thao tác thủ công trên giao diện.\
Tài liệu chi tiết: [https://docs.api.vngcloud.vn/service-docs/vks-api.html](https://docs.api.vngcloud.vn/service-docs/vks-api.html?utm_source=chatgpt.com)

***

### Chuẩn bị

| Thành phần                   | Mô tả                            |
| ---------------------------- | -------------------------------- |
| **Token**                    | Bearer token hợp lệ              |
| **VPC / Subnet**             | Đã được tạo sẵn                  |
| **Image / Flavor**           | Kiểm tra danh sách hợp lệ        |
| **SSH Key / Security Group** | Dùng cho truy cập & bảo mật node |

***

### Tạo Cluster + Node Group qua API

**Endpoint:**

```
POST /v1/clusters
```

**Body ví dụ:**

```json
{
  "name": "cluster-demo-01",
  "version": "v1.29.13-vks.1740045600",
  "description": "Cluster demo tạo qua API",
  "isBuyMorePoc": false,
  "isPoc": false,
  "isEnableAutoRenew": false
  "enablePrivateCluster": false,
  "networkType": "CILIUM_OVERLAY",
  "ipipEncapsulationMode": "ALWAYS",
  "cidr": "192.168.0.0/16",
  "vpcId": "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subnetId": "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "whitelistIp": "0.0.0.0/0",
  "nodeGroups": [
    {
      "name": "nodegroup-demo",
      "numNodes": 3,
      "enableAutoHealing": true,
      "autoScaleConfig": null,
      "upgradeConfig": {
        "maxSurge": 1,
        "maxUnavailable": 0,
        "strategy": "SURGE"
      },
      "enablePrivateNodes": false,
      "imageId": "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "flavorId": "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "diskSize": 100,
      "diskType": "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "securityGroups": ["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"],
      "sshKeyId": "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "labels": {},
      "taints": [],
      "subnetId": "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "enabledEncryptionVolume": false
    }
  ],
  "enabledBlockStoreCsiPlugin": true,
  "enabledLoadBalancerPlugin": true,
  "enabledServiceEndpoint": false,
  "autoUpgradeConfig": null,
  "releaseChannel": "STABLE",
  "fleetConfig": null
}

```

> 💡 **Gợi ý:**
>
> * `secondarySubnets` cho phép triển khai **Multi-AZ** (ví dụ: HCM-1A, HCM-1B, HCM-1C) giúp tăng **High Availability**.
> * Có thể thêm autoScaleConfig, labels, taints… nếu cần tùy chỉnh nâng cao.

***

### Tạo Node Group riêng qua API

**Endpoint:**

```
POST /v1/clusters/{clusterId}/node-groups
```

Body tương tự phần `nodeGroups` ở trên.

***

### Một số API khác

| Mục đích              | API                                |
| --------------------- | ---------------------------------- |
| Lấy danh sách Cluster | `GET /v1/clusters`                 |
| Xóa Cluster           | `DELETE /v1/clusters/{id}`         |
| Lấy kubeconfig        | `GET /v1/clusters/{id}/kubeconfig` |
