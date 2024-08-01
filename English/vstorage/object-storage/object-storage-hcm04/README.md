# Object storage (HCM04)

VNGCloud introduces to you the new **HCM04** **Region** for vStorage services. The standout features of this region include:

* **High performance**: The HCM04 Region is designed to meet the needs of processing large traffic volumes with a speed of 10,000 requests per second per IP, providing exceptional performance that optimizes the operation of your applications and services.
* **Enhanced security:** The HCM04 Region offers encryption mechanisms such as SSE-S3 and SSE-C that ensure absolute safety for customer data.
* **New pricing plan - Instant Archive**: Notably, in the HCM04 region, we introduce the new Instant Archive pricing plan with lower costs, helping customers save on long-term data storage without incurring hidden fees while still fully meeting the criteria for backup storage..

***

## **Farm** <a href="#farm" id="farm"></a>

Farm is a term specifically used for vStorage, a farm is defined by us as a system that includes infrastructure, services, etc. deployed at a specific location within the 2 regions of Hanoi and Ho Chi Minh City with the purpose of providing vStorage storage services. For the 2 farms HCM03, HAN01, the specific parameters for each farm are provided by us as follows:

<table data-full-width="true"><thead><tr><th width="115">Farm</th><th width="255">Farm ID</th><th width="309">vStorage endpoint</th><th>Mục đích sử dụng</th></tr></thead><tbody><tr><td>HCM04</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9204</td><td>https://hcm04.vstorage.vngcloud.vn</td><td>Farm phục vụ đa mục đích với hiệu suất cao và được dùng chung cho dữ liệu lưu trữ tại Region Hồ Chí Minh.</td></tr></tbody></table>

***

## Resource quota <a href="#han-muc-tai-nguyen" id="han-muc-tai-nguyen"></a>

The tables below list the maximum values for storage resources on your vStorage.

#### Bandwidth <a href="#bandwidth" id="bandwidth"></a>

<table data-full-width="true"><thead><tr><th>Farm</th><th>Download BW Domestic</th><th>Download BW International</th><th>Upload BW Domestic</th><th>Upload BW International</th></tr></thead><tbody><tr><td>HCM04</td><td>10Gbps shared</td><td>TBA</td><td>10Gbps shared</td><td>TBA</td></tr></tbody></table>

#### Request per limit <a href="#request-per-limit" id="request-per-limit"></a>

* Per IP

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Request all types</th><th>Put request</th><th>Get request</th></tr></thead><tbody><tr><td>Instant Archive</td><td>TBA</td><td>TBA</td><td>TBA</td></tr></tbody></table>

* Per path

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Request all types</th><th>Put request</th><th>Get request</th></tr></thead><tbody><tr><td>Instant Archive</td><td>TBA</td><td>TBA</td><td>TBA</td></tr></tbody></table>

#### Others <a href="#cac-han-muc-khac" id="cac-han-muc-khac"></a>

<table data-full-width="true"><thead><tr><th>Item</th><th>Limit</th></tr></thead><tbody><tr><td>Number of object per container/ bucket</td><td>600 millions</td></tr><tr><td>Number of container/ bucket per project</td><td>Unlimited</td></tr></tbody></table>
