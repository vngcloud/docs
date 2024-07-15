# Charging for prepaid users

#### Users prepaid create a project <a href="#chargingforprepaidusers-usersprepaidcreateaproject" id="chargingforprepaidusers-usersprepaidcreateaproject"></a>

When you create a project, if you are a prepaid user, the default amount to be paid is the amount you need to pay to use a specific resource, calculated based on the following factors:

* Resource configuration (storage quota).
* Unit price according to the configuration (with or without discount): at the time of action on the resource (including VAT).
* Resource usage time: Start date, End date (down to the minute).
* Coupon deduction (if any).

For example, the formula for calculating the amount you need to pay when initializing a project is as follows:

| Storage Class                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Quota Default | Price per Quota Default (include VAT) (2) | Periods (3) | Coupon Value (4) | Total = (2) \* (3) - (4) |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ----------------------------------------- | ----------- | ---------------- | ------------------------ |
| Gold                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | 30GB          | 33,000 VND / 1 month                      | 1 month     | 20,000 VND       | 13,000 VND               |
| Silver                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 30GB          | 19,800 VND / 1 month                      | 1 month     | None             | 19,800 VND               |
| Archive                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 30GB          | 33,660 VND/ 6 month                       | 6 month     | 10,000 VND       | 23,660 VND               |
| <p>When you change the quota limit, the storage package price will be adjusted accordingly. Each storage package has its own specifications regarding usage capacity and the number of requests. For more information, please refer to What is vStorage?</p><p>Similarly, when you renew a project or increase/decrease the size of the storage package, we will calculate the additional amount you need to pay or the amount that may be refunded. For details, please refer to Invoice, cost &#x26; resource management on VNG Cloud.</p> |               |                                           |             |                  |                          |

***

#### Users prepaid renew or set auto-renew a project <a href="#chargingforprepaidusers-usersprepaidreneworsetauto-renewaproject" id="chargingforprepaidusers-usersprepaidreneworsetauto-renewaproject"></a>

When you renew a project as a pre-paid user, the default amount to be paid is the difference calculated based on the chosen renewal period. We offer storage renewal cycles of 1 month, 3 months, 6 months, 12 months, 24 months, and 36 months. When you select a renewal cycle, the system automatically calculates the effective time of the new storage cycle and the total amount you need to pay for the project renewal. The calculation of the payment difference is based on the following factors:

* t\_start: the start time of the service (Start time).
* t\_end: the end time of the service (End time).
* t\_resize: the time of resizing the project (Time of resizing).
* p\_original: the initial price (Billing Price).
* p\_new: the price after modification (Resizing Price).

For example, the formula for calculating the amount you need to pay when renewing a project is as follows:

| Storage Class | Old Price            | Start time  | End time   | Renew time | Renew period | New End time | New Price   |
| ------------- | -------------------- | ----------- | ---------- | ---------- | ------------ | ------------ | ----------- |
| Silver        | 19,800 VND / 1 month | 06-03-2023  | 05-04-2023 | 08-03-2023 | 1 month      | 05-05-2023   | 19,800 VND  |
| Silver        | 19,800 VND / 1 month | 06-03-2023  | 05-04-2023 | 08-03-2023 | 3 month      | 04-07-2023   | 59,400 VND  |
| Silver        | 19,800 VND / 1 month | 06-03-2023  | 05-04-2023 | 08-03-2023 | 6 month      | 02-10-2023   | 118,800 VND |
| Silver        | 19,800 VND / 1 month | 06-03-2023  | 05-04-2023 | 08-03-2023 | 12 month     | 30-03-2024   | 237,600 VND |
| Silver        | 19,800 VND / 1 month | 06-03-2023  | 05-04-2023 | 08-03-2023 | 24 month     | 25-03-2025   | 475,200 VND |

\


***

#### Users prepaid resize a project <a href="#chargingforprepaidusers-usersprepaidresizeaproject" id="chargingforprepaidusers-usersprepaidresizeaproject"></a>

When you increase or decrease the storage size (resize) of a project, if you are a user who pays in advance, the default amount to be paid is the amount calculated based on the size of the storage package you choose. You can increase or decrease the quota to the minimum or maximum level that we provide. When you choose the renewal period, the system will automatically calculate the total amount you need to pay for the storage quota change. The rule for calculating the differential payment amount is based on the following factors:

* Current storage package.
* Current quota.
* Unit price on the current quota (1).
* New quota.
* Unit price on the new quota (2).

An example formula for calculating the amount you need to pay when increasing or decreasing the storage quota of a project is as follows:

| Storage Class | Start time  | End time   | Current Quota | New Quota | Price Unit/ Current Quota | Resize time | Money refund (1) | Price Unit/ New Quota (2) | Total days use in New Quota(3) | Total = (2)/30\*(3) - (1) |
| ------------- | ----------- | ---------- | ------------- | --------- | ------------------------- | ----------- | ---------------- | ------------------------- | ------------------------------ | ------------------------- |
| Silver        | 06-03-2023  | 05-04-2023 | 30 GB         | 80 GB     | 19,800 VND/ 1 month       | 31/03/2023  | 3,300 VND        | 52,800 VND/ 1 month       | 5                              | 5,500 VND                 |

***

#### Users prepaid delete a active project <a href="#chargingforprepaidusers-usersprepaiddeleteaactiveproject" id="chargingforprepaidusers-usersprepaiddeleteaactiveproject"></a>

When you delete an active project, if you are a user who pays in advance, by default, you will receive a refund amount calculated based on the actual number of days you have not used the storage package. The rule for calculating the differential payment amount is based on the following factors:

* t\_start: The time of initiating the service (Start time)
* t\_end: The time of ending the service (End time)
* t\_delete: The time of performing the configuration return (Time of deletion)
* p: The amount of money (Billing Price)

An example formula for calculating the amount you will be refunded when deleting a project is as follows:

| Storage Class | Start Time | End Time (1) | Current Quota | <p>Delete Time</p><p>(2)</p> | Origin Price (3) | Days refund (4) = (1) - (2) | Total refund = (3) \* (4) \* 24 \*60 / (30 \* 24 \* 60) |
| ------------- | ---------- | ------------ | ------------- | ---------------------------- | ---------------- | --------------------------- | ------------------------------------------------------- |
| Silver        | 01-01-2023 | 01-02-2023   | 30 GB         | 08-01-2023                   | 19,800 VND       | 24 ngày                     | 15,840 VND                                              |
