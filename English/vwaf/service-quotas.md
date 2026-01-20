# Service Quotas

### Overview

The **Quota** page displays the usage limits applied to WAF features within your account.\
These quotas define how many rules or resources can be configured and help ensure stable and fair usage of the service.

Depending on the resource type, quotas may apply **per application** or **based on the total number of applications**.

***

### Quota Scope

#### Per-Application Quotas

The following quotas are applied **to each individual application**:

#### Rate Limit Rules

* Maximum number of **Rate Limiting rules per application**: **2**
* Each application has its own independent rate-limit quota.
* Rate limit rules created for one application do not affect other applications.

***

#### Allow & Deny Rules

* Maximum number of **Allow & Deny rules per application**: **10**
* Each application maintains its own Allow & Deny rule quota.
* Rules configured for one application do not consume quota from other applications.

***

#### Certificate Quotas (Application-Based)

Certificate quotas are calculated **based on the number of applications**.

This applies to:

* **Uploaded certificates**
* **Free certificates**

***

### Certificate Quota Behavior

Certificate quotas follow these rules:

* Each application can be associated with **one certificate**\
  (either an uploaded certificate or a free certificate).
* The **total number of certificates** you can upload or request equals the **number of applications you have created**.
* Uploaded certificates and free certificates **share the same quota scope**, based on application count.

#### Example

If you create **10 applications**, you can:

* Upload up to **10 certificates**, or
* Request up to **10 free certificates**, or
* Use any combination of uploaded and free certificates within that total limit.

***

### Notes

* Rate Limit rule quota: **2 rules per application**
* Allow & Deny rule quota: **10 rules per application**
* Certificate quotas are **counted across all applications**
