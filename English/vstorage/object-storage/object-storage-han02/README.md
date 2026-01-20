# Object storage (HAN02)

GreenNode introduces to you the new **HAN02** **Region** for vStorage services. The standout features of this region include:

* **High performance**: Region HAN02 is designed to handle high traffic volume, delivering exceptional performance that optimizes the operation of your applications and services.
* **Enhanced security**: The HCM04 Region offers encryption mechanisms such as SSE-S3 and SSE-C that ensure absolute safety for customer data.
* **Diverse packages:** In particular, at region HAN02, we offer a variety of storage packages such as Gold, Instant Archive, etc. to fully meet your storage needs.

Get started with vStorage in Region HAN02 by following these instructions.

***

### **Farm** <a href="#farm" id="farm"></a>

Farm is a term specifically used for vStorage, a farm is defined by us as a system that includes infrastructure, services, etc. deployed at a specific location within the 2 regions of Hanoi and Ho Chi Minh City with the purpose of providing vStorage storage services. For farm HAN02, the specific parameters are provided by us as follows:

| HAN02 | 5d10c8ba-7187-4acc-b8c5-2d67d71c9202 | https://han02.vstorage.vngcloud.vn | Multi-purpose server farm with high performance and shared storage in Hanoi Region. |
| ----- | ------------------------------------ | ---------------------------------- | ----------------------------------------------------------------------------------- |

***

## Resource quota

The tables below list the maximum values for storage resources on your vStorage.

### Bandwidth

<table data-full-width="true"><thead><tr><th width="113">Farm</th><th width="210">Download BW Domestic</th><th width="238">Download BW International</th><th width="198">Upload BW Domestic</th><th>Upload BW International</th></tr></thead><tbody><tr><td>HAN02</td><td>10Gbps shared</td><td>TBA</td><td>10Gbps shared</td><td>TBA</td></tr></tbody></table>

### Request per limit

* Per IP

<table data-full-width="true"><thead><tr><th width="167">Storage Class</th><th width="187.091064453125">Request all types</th><th width="174.45458984375">Put request</th><th width="188.364013671875">Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Gold</td><td>5000  request/s/IP</td><td>2000  request/s/IP</td><td>3000  request/s/IP</td><td>1000  request/s/IP</td></tr><tr><td>Instant Archive</td><td>2500  request/s/IP</td><td>1000  request/s/IP</td><td>1500  request/s/IP</td><td>500  request/s/IP</td></tr><tr><td>Archive</td><td>1000 request/s/IP</td><td>500 request/s/IP</td><td>500  request/s/IP</td><td>100  request/s/IP</td></tr></tbody></table>

* Per path

<table data-full-width="true"><thead><tr><th width="164.1817626953125">Storage Class</th><th width="203.13629150390625">Request all types</th><th width="194.9090576171875">Put request</th><th width="194.0906982421875">Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Gold</td><td>5000 request/s/path</td><td>2000 request/s/path</td><td>3000 request/s/path</td><td>1000 request/s/path</td></tr><tr><td>Instant Archive</td><td>2500 request/s/path</td><td>1000 request/s/path</td><td>1500 request/s/path</td><td>500 request/s/path</td></tr><tr><td>Archive</td><td>1000 request/s/path</td><td>500 request/s/path</td><td>500 request/s/path</td><td>100 request/s/path</td></tr></tbody></table>

### Other

<table data-full-width="true"><thead><tr><th>Item</th><th>Limit</th></tr></thead><tbody><tr><td>Maximum number of objects stored per bucket</td><td>600 million objects</td></tr><tr><td>Maximum number of buckets that can be created per project</td><td>Unlimited</td></tr></tbody></table>

***

## Storage class

Below is a table describing the specifications of each storage class we support:

<table data-full-width="true"><thead><tr><th>Item</th><th>Gold Class</th><th>Instant Archive</th><th data-hidden>Archive</th></tr></thead><tbody><tr><td><strong>Designed for</strong></td><td>For frequently accessed data that requires low latency and high throughput with retrieval in <strong>milliseconds (10m object/ 1H)</strong>.</td><td>For long-term storing data with retrieval in <strong>miliseconds (5m object/ 1H)</strong>.</td><td>For long-term data archiving that is accessed once or twice in a year with retrieval within <strong>hour (5m object/ 12H and 10m object/ 24H).</strong></td></tr><tr><td><strong>Durability</strong></td><td>99.999999999%</td><td>99.999999999%</td><td>99.999999999%</td></tr><tr><td><strong>Availability</strong></td><td>99.99%</td><td>99.99%</td><td>99.99%</td></tr><tr><td><strong>Min storage quota</strong></td><td>No</td><td>No</td><td>5 TB</td></tr><tr><td><strong>Min storage duration</strong></td><td>No</td><td>No</td><td>90 days</td></tr><tr><td><strong>Min billable object size</strong></td><td>0</td><td>0</td><td>128 KB</td></tr><tr><td><strong>Free traffic</strong></td><td>Quota x 10</td><td>Quota x 2</td><td>Quota x1</td></tr><tr><td><strong>Free request</strong></td><td>Free request on Gold Class performance</td><td>Free request on Instant Archive Class performance</td><td>Free request on Archive Class performance</td></tr></tbody></table>
