# Traffic / Request Billing Policy

### 1. Overview

This document describes:

* How traffic and request quotas are allocated
* How quotas are added and deducted
* Service suspension conditions
* Billing model for prepaid and postpaid customers

### 2. Quota Model (Traffic Pool & Request Pool)

The system uses two shared pools:

<table><thead><tr><th width="240.93359375">Pool</th><th>Description</th></tr></thead><tbody><tr><td>Traffic Pool</td><td>Total traffic volume (GB)</td></tr><tr><td>Request Pool</td><td>Total number of requests</td></tr></tbody></table>

#### Principles

* Each customer has:
  * One Traffic Pool
  * One Request Pool
* Pools are shared across all applications
* No per-application quota isolation

#### Adding quota to pools

Quota is added in the following cases:

1. Application creation:
   * +300 GB traffic
   * +3,000,000 requests
2. Monthly allocation
3. Purchasing additional quota:
   * Traffic → Traffic Pool
   * Requests → Request Pool

#### Pool usage

* All applications consume from shared pools
* Any usage deducts directly from the pool

### 3. Prepaid Customers

#### 3.1. Default quota

Each newly created application is granted:

<table><thead><tr><th width="240.9765625">Resource</th><th>Value</th></tr></thead><tbody><tr><td>Traffic</td><td>300 GB</td></tr><tr><td>Request</td><td>3,000,000</td></tr></tbody></table>

Notes:

* Quota is granted per application
* All quota is added to the shared pool
* No per-application isolation

#### 3.2. Monthly quota allocation

The system automatically adds free quota at the beginning of each month (e.g. 00:05).

Details:

* Each active application (domain) receives:
  * 300 GB traffic
  * 3,000,000 requests
* Quota is granted per application and added to the shared pool

Conditions:

1. Application must be Active
2. Application must have existed for at least 15 days

Formula:

Allocation time – creation time ≥ 15 days

Notes:

* Applications not meeting conditions will not receive quota
* If multiple applications are eligible, quota is granted per application

#### 3.3. Deduction mechanism

Checked every 10 minutes:

* If traffic ≥ 10 MB:
  * Deduct immediately
* If traffic < 10 MB:
  * Accumulate and deduct next day

#### 3.4. Out-of-quota handling

When either pool (traffic or request) reaches 0:

**Case A – With usage history**

Condition:

* Previous month usage exists

Behavior:

* Not suspended immediately
* Allows over-usage

Limits:

* Traffic: up to 50% of previous month traffic
* Requests: up to 50% of previous month requests

If either limit is exceeded:

* All applications are suspended

**Case B – No usage history**

Applies when:

* New customers
* Insufficient data

Thresholds:

* Traffic > 1000 GB
* Request > 10,000,000

If either threshold is exceeded:

* All applications are suspended

#### 3.5. Early deletion

If an application is deleted before 15 days:

* Reclaim from pool:
  * 300 GB traffic
  * 3,000,000 requests

### 4. Postpaid Customers

#### 4.1. Billing principle

* Calculated monthly
* T = number of applications

System generates T bills (1 application = 1 bill)

#### 4.2. Total usage

* m1: total traffic
* m2: total requests

#### 4.3. Free quota

<table><thead><tr><th width="241.29296875">Resource</th><th>Formula</th></tr></thead><tbody><tr><td>Traffic</td><td>T × 300 GB</td></tr><tr><td>Request</td><td>T × 3,000,000</td></tr></tbody></table>

#### 4.4. Traffic overage

N1 = m1 − (T × 300 GB)

* If N1 ≤ 0: no charge
* If N1 > 0:

Cost = N1 × price per GB

#### 4.5. Request overage

N2 = m2 − (T × 3,000,000)

* If N2 ≤ 0: no charge
* If N2 > 0:

Cost = (N2 / 1,000,000) × price per million requests

#### 4.6. Units

* 1 KB = 1000 Bytes
* 1 MB = 1000 KB
* 1 GB = 1000 MB

### 5. Best Practices

* Monitor shared pools regularly
* Avoid frequent app creation/deletion
* Use postpaid for variable workloads
