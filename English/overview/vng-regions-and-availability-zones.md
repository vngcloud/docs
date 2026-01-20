---
description: Information about GreenNode Regions and Availability Zones
---

# VNG Regions and Availability Zones

## Overview

### What is a Region?

A Region is an independent geographic area where GreenNode deploys its infrastructure. Each region is designed to operate independently, ensuring your data is stored in the location you choose.

### What is an Availability Zone (AZ)?

An Availability Zone is one or more discrete data centers within a region, equipped with independent power, networking, and connectivity. Deploying applications across multiple AZs increases availability and fault tolerance.

### Naming Convention

* **Region**: Named by geographic location (e.g., HCM - Ho Chi Minh, HAN - Ha Noi, BKK - Bangkok)
* **AZ**: Combines region name + sequence number + letter (e.g., HCM-1A, HCM-1B, HAN-1A, BKK-1A)

***

## VNG Regions List

| Region Code | Region Name | Availability Zones             | Console URL                                                                                                                        |
| ----------- | ----------- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| HCM         | Ho Chi Minh | HCM-1A, HCM-1B, HCM-1C, BKK-1A | https://hcm-3.console.vngcloud.vn                                                                                                  |
| HAN         | Ha Noi      | HAN-1A                         | [https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server](https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server) |

{% hint style="info" %}
As of December 15, 2025, GreenNode supports 2 regions: Ho Chi Minh and Ha Noi.
{% endhint %}

***

## Service Availability by Region

{% hint style="info" %}
**Legend:**

* x : Service available in this zone
* \- : Service not available in this zone
* Coming Soon: Service will be supported soon
{% endhint %}

{% hint style="warning" %}
Service URLs within the same region are identical.
{% endhint %}

***

{% tabs %}
{% tab title="vServer" %}
#### vServer

| Service                             | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                                                                                                                  |
| ----------------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Server**                          |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) \| [HAN](https://han-1.console.vngcloud.vn/vserver/v-server/cloud-server)                                                             |
| **Volume**                          |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/volumes)                                                                 |
| **Image**                           |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/images) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/images)                                                                   |
| **Snapshot**                        |    -   |    x   |    x   |    x   |    -   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/block-store/snapshot/overview) \| [HAN](https://han-1.console.vngcloud.vn/vserver/block-store/snapshot/overview)                                             |
| **Network Interface**               |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/external-interface/external-interface-group) \| [HAN](https://han-1.console.vngcloud.vn/vserver/network/external-interface/external-interface-group) |
| **VPC, DHCP, VIP, Peering**         |    -   |    x   |    x   |    x   |    x   |    -   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/vpc)                                                                                                                                                 |
| **Bandwidth**                       |    -   |    x   |    x   |    x   |    -   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/network/bandwidth/list) \| [HAN](https://han-1.console.vngcloud.vn/vserver/network/bandwidth/list)                                                           |
| **vLB (Load Balancer)**             |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb) \| [HAN](https://han-1.console.vngcloud.vn/vserver/load-balancer/vlb)                                                                     |
| **GLB (Global Load Balancer)**      |    x   |    -   |    x   |    -   |    -   |    -   | [Portal](https://glb.console.vngcloud.vn/overview)                                                                                                                                                           |
| **vDCI (Dedicated Cloud Instance)** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vdci.console.vngcloud.vn)                                                                                                                                                                   |
{% endtab %}

{% tab title="vNetwork" %}
#### vNetwork

| Service                               | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                      |
| ------------------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ---------------------------------------------------------------------------------------------------------------- |
| **Endpoint, NAT, VPN, Cross Connect** |    -   |    x   |    x   |    x   |    -   |    x   | [HCM](https://hcm-3-vnetwork.console.vngcloud.vn/overview) \| [HAN](https://han-1-vnetwork.console.vngcloud.vn/) |
| **vDNS**                              |    x   |    -   |    x   |    x   |    -   |    -   | [Portal](https://vdns.console.vngcloud.vn/hosted-zones)                                                          |
| **Global View**                       |    x   |    -   |    x   |    x   |    x   |    -   | [Portal](https://regionview.console.vngcloud.vn/resource-region)                                                 |
{% endtab %}

{% tab title="vStorage" %}
#### vStorage

| Service          | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                          |
| ---------------- | :----: | :----: | :----: | :----: | :----: | :----: | -------------------------------------------------------------------------------------------------------------------- |
| **Storage**      |    -   |    x   |    -   |    -   |    -   |    x   | [HCM](https://vstorage.console.vngcloud.vn/storage/list) \| [HAN](https://vstorage.console.vngcloud.vn/storage/list) |
| **File Storage** |    -   |    x   |    x   |    x   |    -   |    -   | [HCM](https://efs.console.vngcloud.vn/overview)                                                                      |
| **Data Sync**    |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://datasync.console.vngcloud.vn/overview)                                                              |
{% endtab %}

{% tab title="vDB" %}
#### vDB (Database Service)

| Service                 | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                    |
| ----------------------- | :----: | :----: | :----: | :----: | :----: | :----: | -------------------------------------------------------------- |
| **Relational Database** |    -   |    x   |    x   |    x   |    -   |    -   | [Portal](https://vdb.console.vngcloud.vn/relational/database)  |
| **MemoryStore**         |    -   |    x   |    x   |    x   |    -   |    -   | [Portal](https://vdb.console.vngcloud.vn/memorystore/database) |
| **Kafka**               |    -   |    x   |    -   |    -   |    -   |    -   | [Portal](https://vdb.console.vngcloud.vn/kafka/cluster)        |
| **OpenSearch**          |    -   |    x   |    -   |    -   |    -   |    -   | [Portal](https://vdb.console.vngcloud.vn/opensearch/cluster)   |
{% endtab %}

{% tab title="VKS" %}
#### VKS (VNG Kubernetes Service)

| Service                | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                              |
| ---------------------- | :----: | :----: | :----: | :----: | :----: | :----: | -------------------------------------------------------------------------------------------------------- |
| **Kubernetes Cluster** |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://vks.console.vngcloud.vn/overview) \| [HAN](https://vks-han-1.console.vngcloud.vn/overview) |
| **Container Registry** |    -   |    x   |    x   |    x   |    -   |    x   | [HCM](https://vcr.console.vngcloud.vn/repository/list) \| [HAN](https://han-1.console.vngcloud.vn/vcr)   |
{% endtab %}

{% tab title="Backup Center" %}
#### Backup Center

| Service                    | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                                                                                              |
| -------------------------- | :----: | :----: | :----: | :----: | :----: | :----: | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Backup Center**          |    -   |    x   |    x   |    x   |    -   |    x   | [HCM](https://backupcenter.console.vngcloud.vn/backup-server/list) \| [HAN](https://backupcenter.console.vngcloud.vn/backup-server/list) |
| **Server Migration**       |    -   |    x   |    x   |    x   |    x   |    x   | [HCM](https://backupcenter.console.vngcloud.vn/server-migration) \| [HAN](https://backupcenter.console.vngcloud.vn/server-migration)     |
| **Disaster Recovery (DR)** |    x   |    x   |    x   |    x   |    -   |    -   | [Portal](https://backupcenter.console.vngcloud.vn/protected-server/list)                                                                 |
{% endtab %}

{% tab title="vMonitor" %}
#### vMonitor Platform

| Service            | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                                            |
| ------------------ | :----: | :----: | :----: | :----: | :----: | :----: | ---------------------------------------------------------------------- |
| **Metric**         |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vmonitor.console.vngcloud.vn/quota-usages/metric)     |
| **Log**            |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vmonitor.console.vngcloud.vn/log/project)             |
| **Synthetic Test** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vmonitor.console.vngcloud.vn/synthetic-test/api-test) |
| **Notification**   |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vmonitor.console.vngcloud.vn/notification)            |
{% endtab %}

{% tab title="vCDN" %}
#### vCDN

| Service             | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                               |
| ------------------- | :----: | :----: | :----: | :----: | :----: | :----: | --------------------------------------------------------- |
| **Web Accelerator** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vcdn.vngcloud.vn/webacc/list.html)       |
| **Object Download** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vcdn.vngcloud.vn/obj-download/list.html) |
| **Video On Demand** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vcdn.vngcloud.vn/vod/list.html)          |
| **Live Streaming**  |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://vcdn.vngcloud.vn/live-cdn/list.html)     |
{% endtab %}

{% tab title="Security & IAM" %}
#### Security & IAM

| Service | Global | HCM-1A | HCM-1B | HCM-1C | BKK-1A | HAN-1A | Console URL                                   |
| ------- | :----: | :----: | :----: | :----: | :----: | :----: | --------------------------------------------- |
| **IAM** |    x   |    -   |    -   |    -   |    -   |    -   | [Portal](https://iam.console.vngcloud.vn/)    |
| **KMS** |    -   |    -   |    -   |    -   |    -   |    x   | [HAN](https://han-1-kms.console.vngcloud.vn/) |
{% endtab %}

{% tab title="Marketplace & AI" %}
#### Marketplace & AI

| Service          | Global | HCM-1A |    HCM-1B   |    HCM-1C   | BKK-1A | HAN-1A | Console URL                                                                                                              |
| ---------------- | :----: | :----: | :---------: | :---------: | :----: | :----: | ------------------------------------------------------------------------------------------------------------------------ |
| **vMarketplace** |    -   |    x   |      x      |      x      |    -   |    x   | [HCM](https://marketplace.console.vngcloud.vn/overview) \| [HAN](https://marketplace-han-1.console.vngcloud.vn/overview) |
| **vColo**        |    x   |    -   |      -      |      -      |    -   |    -   | [Portal](https://vcolo.console.vngcloud.vn/overview)                                                                     |
| **AI Platform**  |    -   |    x   | Coming Soon | Coming Soon |    -   |    -   | [Portal](https://aiplatform.console.vngcloud.vn/overview)                                                                |
| **AI Gateway**   |    x   |    -   |      -      |      -      |    -   |    -   | [Portal](https://aigateway.console.vngcloud.vn)                                                                          |
| **MaaS**         |    x   |    -   |      -      |      -      |    -   |    -   | [Portal](https://aiplatform.console.vngcloud.vn/models)                                                                  |
{% endtab %}
{% endtabs %}

***

## Considerations When Choosing Region and AZ

1. **Latency**: Choose a region close to your end users to reduce latency
2. **Data Compliance**: Some regulations require data to be stored in a specific geographic area
3. **High Availability**: Deploy applications across multiple AZs to ensure high availability
4. **Cost**: Service pricing may vary between regions
