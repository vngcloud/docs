---
description: Thông tin về các Regions và Availability Zones của VNG Cloud
---
# VNG Regions and Availability Zones

## Tổng quan

### Region là gì?

Region là một vùng địa lý độc lập nơi VNG Cloud triển khai cơ sở hạ tầng. Mỗi region được thiết kế để hoạt động độc lập, đảm bảo dữ liệu của bạn được lưu trữ trong khu vực bạn chọn.

### Availability Zone (AZ) là gì?

Availability Zone là một hoặc nhiều data center riêng biệt trong một region, được trang bị nguồn điện, mạng và kết nối độc lập. Việc triển khai ứng dụng trên nhiều AZ giúp tăng tính sẵn sàng và khả năng chịu lỗi.

### Quy tắc đặt tên

- **Region**: Được đặt theo vị trí địa lý (VD: HCM - Ho Chi Minh, HAN - Ha Noi, BKK - Bangkok)
- **AZ**: Kết hợp tên region + số thứ tự + chữ cái (VD: HCM-1A, HCM-1B, HAN-1A, BKK-1A)

---

## Danh sách VNG Regions

| Region Code | Region Name | Availability Zones              | Console URL                                                                                                                                                                                    |
| ----------- | ----------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HCM         | Ho Chi Minh | HCM-1A, HCM-1B, HCM-1C, BKK-1A | https://hcm-3.console.vngcloud.vn                                                                                                                                                              |
| HAN         | Ha Noi      | HAN-1A                          | [https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server](https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server "https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server") |

---

## Service Availability by Region

{% hint style="info" %}
**Chú thích:**

- x : Service có sẵn tại zone này
- \- : Service chưa có sẵn tại zone này
- Coming Soon: Service sắp được hỗ trợ
{% endhint %}

{% hint style="warning" %}
URL của các service trong cùng 1 region sẽ giống nhau.
{% endhint %}

---

{% tabs %}
{% tab title="vServer" %}

### vServer

| Service                              | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                                                                                                            |
| ------------------------------------ | :----: | :----: | :----: | :----: | :----: | :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Server**                     |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) \| [HAN](https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server)                                                             |
| **Volume**                     |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/volumes)                                                                 |
| **Image**                      |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/images) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/images)                                                                   |
| **Snapshot**                   |        |   x   |   x   |   x   |   -   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/snapshot/overview) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/snapshot/overview)                                             |
| **Network Interface**          |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/external-interface/external-interface-group) \| [HAN](https://han-1.console.vngcloud.vn/vserver/network/external-interface/external-interface-group) |
| **VPC, DHCP, VIP, Peering**    |        |   x   |   x   |   x   |   x   |   -   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/vpc)                                                                                                                                              |
| **Bandwidth**                  |        |   x   |   x   |   x   |   -   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/bandwidth/list) \| [HAN](https://han-1.console.vngcloud.vn/vserver/network/bandwidth/list)                                                           |
| **vLB (Load Balancer)**        |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb) \| [HAN](https://han-1.console.vngcloud.vn/vserver/load-balancer/vlb)                                                                     |
| **GLB (Global Load Balancer)** |   x   |   -   |   x   |   -   |   -   |   -   | [Portal](https://glb.console.vngcloud.vn/overview)                                                                                                                                                        |

{% endtab %}

{% tab title="vNetwork" %}

### vNetwork

| Service                                     | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                |
| ------------------------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ---------------------------------------------------------------------------------------------------------- |
| **Endpoint, NAT, VPN, Cross Connect** |        |   x   |   x   |   x   |   -   |   x   | [HCM](https://hcm-3-vnetwork.console.vngcloud.vn/overview) \| [HAN](https://han-1-vnetwork.console.vngcloud.vn/) |
| **vDNS**                              |   x   |   -   |   x   |   x   |   -   |   -   | [Portal](https://vdns.console.vngcloud.vn/hosted-zones)                                                       |
| **Global View**                       |   x   |   -   |   x   |   x   |   x   |   -   | [Portal](https://regionview.console.vngcloud.vn/resource-region)                                              |

{% endtab %}

{% tab title="vStorage" %}

### vStorage

| Service                | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                    |
| ---------------------- | :----: | :----: | :----: | :----: | :----: | :----: | -------------------------------------------------------------------------------------------------------------- |
| **Storage**      |        |   x   |   -   |   -   |   -   |   x   | [HCM](https://vstorage.console.vngcloud.vn/storage/list) \| [HAN](https://vstorage.console.vngcloud.vn/storage/list) |
| **File Storage** |        |   x   |   x   |   x   |   -   |   -   | [HCM](https://efs.console.vngcloud.vn/overview)                                                                   |
| **Data Sync**    |   x   |   -   |   -   |   -   |   -   |   -   | [Portal](https://datasync.console.vngcloud.vn/overview)                                                           |

{% endtab %}

{% tab title="vDB" %}

### vDB (Database Service)

| Service                       | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                 |
| ----------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ----------------------------------------------------------- |
| **Relational Database** |        |   x   |   x   |   x   |   -   |   -   | [Portal](https://vdb.console.vngcloud.vn/relational/database)  |
| **MemoryStore**         |        |   x   |   x   |   x   |   -   |   -   | [Portal](https://vdb.console.vngcloud.vn/memorystore/database) |
| **Kafka**               |        |   x   |   -   |   -   |   -   |   -   | [Portal](https://vdb.console.vngcloud.vn/kafka/cluster)        |
| **OpenSearch**          |        |   x   |   -   |   -   |   -   |   -   | [Portal](https://vdb.console.vngcloud.vn/opensearch/cluster)   |

{% endtab %}

{% tab title="VKS" %}

### VKS (VNG Kubernetes Service)

| Service                      | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                        |
| ---------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | -------------------------------------------------------------------------------------------------- |
| **Kubernetes Cluster** |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://vks.console.vngcloud.vn/overview) \| [HAN](https://vks-han-1.console.vngcloud.vn/overview) |
| **Container Registry** |        |   x   |   x   |   x   |   -   |   x   | [HCM](https://vcr.console.vngcloud.vn/repository/list) \| [HAN](https://han-1.console.vngcloud.vn/vcr)   |

{% endtab %}

{% tab title="Backup Center" %}

### Backup Center

| Service                          | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                                        |
| -------------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Backup Center**          |        |   x   |   x   |   x   |   -   |   x   | [HCM](https://backupcenter.console.vngcloud.vn/backup-server/list) \| [HAN](https://backupcenter.console.vngcloud.vn/backup-server/list) |
| **Server Migration**       |        |   x   |   x   |   x   |   x   |   x   | [HCM](https://backupcenter.console.vngcloud.vn/server-migration) \| [HAN](https://backupcenter.console.vngcloud.vn/server-migration)     |
| **Disaster Recovery (DR)** |   x   |   x   |   x   |   x   |   -   |   -   | [Portal](https://backupcenter.console.vngcloud.vn/protected-server/list)                                                              |

{% endtab %}

{% tab title="vMonitor" %}

### vMonitor Platform

| Service                  | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                         |
| ------------------------ | :----: | :----: | :----: | :----: | :----: | :----: | ------------------------------------------------------------------- |
| **Metric**         |   x   |        |        |        |        |        | [Portal](https://vmonitor.console.vngcloud.vn/quota-usages/metric)     |
| **Log**            |   x   |        |        |        |        |        | [Portal](https://vmonitor.console.vngcloud.vn/log/project)             |
| **Synthetic Test** |   x   |        |        |        |        |        | [Portal](https://vmonitor.console.vngcloud.vn/synthetic-test/api-test) |
| **Notification**   |   x   |        |        |        |        |        | [Portal](https://vmonitor.console.vngcloud.vn/notification)            |

{% endtab %}

{% tab title="vCDN" %}

### vCDN

| Service                   | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                            |
| ------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ------------------------------------------------------ |
| **Web Accelerator** |   x   |        |        |        |        |        | [Portal](https://vcdn.vngcloud.vn/webacc/list.html)       |
| **Object Download** |   x   |        |        |        |        |        | [Portal](https://vcdn.vngcloud.vn/obj-download/list.html) |
| **Video On Demand** |   x   |        |        |        |        |        | [Portal](https://vcdn.vngcloud.vn/vod/list.html)          |
| **Live Streaming**  |   x   |        |        |        |        |        | [Portal](https://vcdn.vngcloud.vn/live-cdn/list.html)     |

{% endtab %}

{% tab title="Security & IAM" %}

### Security & IAM

| Service       | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                |
| ------------- | :----: | :----: | :----: | :----: | :----: | :----: | ------------------------------------------ |
| **IAM** |   x   |        |        |        |        |        | [Portal](https://iam.console.vngcloud.vn/)    |
| **KMS** |        |   -   |   -   |   -   |   -   |   x   | [HAN](https://han-1-kms.console.vngcloud.vn/) |

{% endtab %}

{% tab title="Marketplace & AI" %}

### Marketplace & AI

| Service                | Global | HCM-1A |   HCM-1B   |   HCM-1C   | BKK-1A | HAN-1A | Console URL                                                                                                        |
| ---------------------- | :----: | :----: | :---------: | :---------: | :----: | :----: | ------------------------------------------------------------------------------------------------------------------ |
| **vMarketplace** |        |   x   |      x      |      x      |   -   |   x   | [HCM](https://marketplace.console.vngcloud.vn/overview) \| [HAN](https://marketplace-han-1.console.vngcloud.vn/overview) |
| **vColo**        |   x   |        |            |            |        |        | [Portal](https://vcolo.console.vngcloud.vn/overview)                                                                  |
| **AI Platform**  |        |   x   | Coming Soon | Coming Soon |   -   |   -   | [Portal](https://aiplatform.console.vngcloud.vn/overview)                                                             |

{% endtab %}
{% endtabs %}

---

## Lưu ý khi chọn Region và AZ

1. **Độ trễ (Latency)**: Chọn region gần với người dùng cuối để giảm độ trễ
2. **Tuân thủ dữ liệu**: Một số quy định yêu cầu dữ liệu phải được lưu trữ trong một khu vực địa lý cụ thể
3. **Tính sẵn sàng cao**: Triển khai ứng dụng trên nhiều AZ để đảm bảo high availability
4. **Chi phí**: Giá dịch vụ có thể khác nhau giữa các region
