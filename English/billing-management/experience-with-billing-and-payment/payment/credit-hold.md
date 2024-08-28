# Credit hold

## **Overview**

At VNG Cloud Service, certain resources/services are exclusively for postpaid users due to the following reasons:

* The cost of using the resource cannot be calculated immediately upon usage.
* The cost of using the resource can only be calculated based on the actual usage of the user.

Therefore, prepaid users cannot make payments to use these special resources (such as the vContainer service) immediately upon creation.

Recognizing the increasing demand for postpaid resources/services from prepaid users, VNG Cloud Service has introduced the Credit Hold feature:

**Applicable to:** Prepaid users

**Applicable resources/services:** Currently supports vContainer (K8s), Snapshot, Repository (vCR), and Bandwidth services

**Fund source:** VNG Cloud Credit

**Tasks:**

* Users select the desired resource configuration.
* Confirm the credit hold on the payment page.

**Results upon completion:**

* The system proceeds with the credit hold: The held credit cannot be used for other purposes.
* The system provides the resource according to the configured settings.
* An email notification is sent with resource information (depending on the specific characteristics of each resource).

## **Applicable services**

### 1. vContainer (K8s) service/product

After successful resource creation, at the end of each day, the system will automatically recalculate the actual usage cost for that day and proceed to hold the necessary credit for using the service in the next 3 days. Please refer to the following example:

| Action                                  | Estimated Usage for next 3 days (1) | Available credit (2) | Daily actual usage (3) | Số credit cần đặt cọc (4)                        | Số Credit khả dụng còn lại khi thực hiện tác vụ (5) |
| --------------------------------------- | ----------------------------------- | -------------------- | ---------------------- | ------------------------------------------------ | --------------------------------------------------- |
| Create (date n) with 2 nodes 4 volumes  | 1,800,000 VND                       | 50,000,000 VND       | N/A                    | 1,800,000 VND                                    | 50,000,000 - 1,800,000 = 48,200,000 VND             |
| Date n+1 (same configuration)           | 1,800,000 VND                       | 48,200,000 VND       | 600,000 VND            | 600,000 + 1,800,000 = 2,400,000 VND              | 50,000,000 - 2,400,000 = 47,600,000 VND             |
| Date n+2 (same configuration)           | 1,800,000 VND                       | 47,600,000 VND       | 600,000 VND            | 600,000\*2 + 1,800,000 = 3,000,000 VND           | 50,000,000 - 3,000,000 = 47,000,000 VND             |
| Date n+3, scale up to 3 nodes 6 volumes | 2,700,000 VND                       | 47,000,000 VND       | 600,000 VND            | 600,000\*3 + 2,700,000 = 4,500,000 VND           | 50,000,000 - 4,500,000 = 45,500,000 VND             |
| Date n + 4, (same configuration)        | 2,700,000 VND                       | 45,500,000 VND       | 900,000 VND            | 600,000\*3 + 900,000 + 2,700,000 = 5,400,000 VND | 50,000,000 - 5,400,000 = 44,600,000 VND             |
| Date n + 5, delete                      | 0                                   | 44,600,000 VND       | 900,000 VND            | 600,000\*3 + 900,000\*2 = 3,600,000 VND          | 50,000,000 - 3,600,000 = 46,400,000 VND             |

**Explanation:**

* (1) Estimated cost for using the service for 3 consecutive days, based on the current resource configuration.&#x20;
* (2) Available credit balance.&#x20;
* (3) Actual usage cost: The exact cost for one day of service usage, based on configuration changes (if any).&#x20;
* (4) Required credit deposit: This is the cumulative amount for actual service usage days, plus the estimated cost for the next 3 days. At the end of each month, this amount will be used to pay the service bill.&#x20;
* (5) Remaining available credit after performing the credit hold task = Total initial available credit - Total actual usage cost (calculated from the service creation date to the present) - Estimated service usage for the next 3 days (based on the current configuration).

**Note:**

Resource usage costs are calculated accurately to the minute at the time the user performs an action (creation, configuration change). The above is for reference only.

When a user deletes a K8s resource, the system will retain the actual usage amount (3,600,000 VND as in the example), which will be used to pay the bill at the end of the billing cycle.

### **2. Snapshot**

Please note that when activating the Snapshot service for the first time, users will not be charged any fees. Credit holding will only occur once a day if the user's account has created and stored snapshot data. Refer to the guide below for more information on implementing credit holding for the Snapshot service:

**Snapshot Pricing**

* **Formula:** The cost of creating a snapshot is calculated based on the size of the snapshot (in gigabytes) and its usage time (usually measured in hours).
* **Usage time:** Users will be charged for the duration of the snapshot's existence. This time is recorded by the hour.
* **Example:** If you have a 100GB snapshot and the unit price for the Snapshot Service is 7.7 VND per GB-hour, the cost will be calculated as follows:
  * By hour: 7.7 VND \* 100 GB = 770 VND per hour.&#x20;
  * By day: 770 VND \* 24 = 18,480 VND per day.&#x20;
  * By month: 18,480 \* 30 = 554,400 VND per month.

**Note:** The unit price provided is for reference only. The actual usage time of snapshots is recorded hourly based on the actual size of your snapshots.

**Usage Scenario**

* Step 1: Activate Snapshot for the first time (free). Example: Activation at 9 AM.
* Step 2: Create and store snapshots as needed. For example:
  * 10 AM: Create a 10GB snapshot.&#x20;
  * 1 PM: Create an additional 10GB, total Snapshot Size is 20GB.
* Step 3: The system records the snapshot usage capacity every hour.
* Step 4: Hold Credit daily based on actual usage. Specifically:
  * System runtime: 9 AM the next day
  * 10GB Snapshot Size for 3 hours of use (from 10 AM to 1 PM) = 7.7 \* 10 \* 3 = 231 VND&#x20;
  * 20GB Snapshot Size for 20 hours of use (from 1 PM to 9 AM the next day) = 7.7 \* 20 \* 20 = 3,080 VND&#x20;
  * Total actual cost for 1 day = 231 VND + 3,080 VND = 3,311 VND&#x20;
  * Total amount to hold = Actual cost + Estimated usage for the next 3 days = 3,311 + (7.7 VND \* 20GB \* 24h \* 3 days) (_) = 14,399 VND_&#x20;

_**Note (\***_**)**

* The system needs to hold both the actual usage and the estimated usage for the next 3 days to ensure the safety and continuity of service usage.
* The formula for estimating usage for the next 3 days is: T**otalSnapshotSize \* Unit price VND \* 24h \* 3 days**

### **3. Container Registry (vCR)**

Credit holding occurs once a day only if the user account has created and stored data in the repositories. Refer to the guide below for more information on implementing credit holding for the Container Repository (vCR) service:

**Repository Pricing**

* **Formula:** The cost of repositories is calculated based on actual storage capacity (in gigabytes) and usage time (usually measured in hours).
* **Usage time:** Users will be charged for the duration of the stored data (usually container images) in the repository. This time is recorded by the hour.
* **Example:** If you have a repository with a current storage capacity of 100GB and the unit price for the Repository Service is 7.7 VND per GB-hour, the cost will be calculated as follows:
  * By hour: 7.7 VND \* 100 GB = 770 VND per hour.&#x20;
  * By day: 770 VND \* 24 = 18,480 VND per day.&#x20;
  * By month: 18,480 \* 30 = 554,400 VND per month.

**Note:** The unit price provided is for reference only. The actual storage time of data (container images) in repositories is recorded hourly based on the actual size of your snapshots.

**Usage Scenario**

* Step 1: Create a Repository for data storage.
* Step 2: Push/Pull container images as needed. For example:
  * 10 AM: Push 1 image container of 10GB -> total capacity is 10GB.&#x20;
  * 1 PM: Push another 10GB image container -> total storage capacity is 20GB.
* Step 3: The system records the storage capacity in the Repository every hour.
* Step 4: Hold Credit daily based on actual usage. Specifically:
  * System runtime: 9 AM the next day
  * 10GB storage for 3 hours of use (from 10 AM to 1 PM) = 7.7 \* 10 \* 3 = 231 VND&#x20;
  * 20GB storage for 20 hours of use (from 1 PM to 9 AM the next day) = 7.7 \* 20 \* 20 = 3,080 VND&#x20;
  * Total actual cost for 1 day = 231 VND + 3,080 VND = 3,311 VND&#x20;
  * Total amount to hold = Actual cost + Estimated usage for the next 3 days = 3,311 + (7.7 VND \* 20GB \* 24h \* 3 days) (_) = 14,399 VND_&#x20;

_**Note (\***_**)**

* The system needs to hold both the actual usage and the estimated usage for the next 3 days to ensure the safety and continuity of service usage.
* The formula for estimating usage for the next 3 days is: **TotalSize \* Unit price VND \* 24h \* 3 days**

### **4. Bandwidth**

When users consume Pay-as-you-go bandwidth during a billing cycle, the system will reserve credit corresponding to the actual usage.

**Example:** Assuming the billing cycle ends on the last day of the month and the service price is 1,000 VND/1GB. When users consume Pay-as-you-go bandwidth for 2 IP addresses, as in the example below:

| IP Address    | Time   | Usage Recorded      | Usage Charged | Credit Hold   |
| ------------- | ------ | ------------------- | ------------- | ------------- |
| 103.245.251.6 | Day 10 | 5.56 GB             | 5 GB          | 5,000 credit  |
| 103.245.251.6 | Day 15 | Adding 8.25 GB more | 13 GB         | 13,000 credit |
| 103.245.251.6 | Day 17 | Adding 3 GB more    | 16 GB         | 16,000 credit |
| 116.118.95.65 | Day 1  | 5 GB                | 5 GB          | 5,000 credit  |
| 116.118.95.65 | Day 15 | Adding 7.75 GB more | 12 GB         | 12,000 credit |
| 116.118.95.65 | Day 20 | Adding 3 GB more    | 15 GB         | 15,000 credit |

Currently, the total credit held based on the usage of IP addresses is as follows:

* Total credit held = usage on IP 103.245.251.6 + usage on IP 116.118.95.65 = 16,000 + 15,000 = 31,000 credits.

At the end of the billing cycle, the system will generate a corresponding invoice and deduct it from the previously held amount. During usage, if the credit is insufficient, the system will stop providing the service according to the service policy.

## **Credit shortage handling**

In case the user does not have enough available credit balance after making the credit deposit, the system will:

* Send an email notification to the user about the required credit hold (including the total credit and the amount needed to top up).
* The user must proactively top up the credit to avoid exceeding the allowed threshold, which may affect the service usage.
