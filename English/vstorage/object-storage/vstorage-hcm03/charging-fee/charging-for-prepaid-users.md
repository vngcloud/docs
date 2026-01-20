# Charging for prepaid users

#### Users prepaid create a project <a href="#chargingforprepaidusers-usersprepaidcreateaproject" id="chargingforprepaidusers-usersprepaidcreateaproject"></a>

When you create a project, if you are a prepaid user, the default amount to be paid is the amount you need to pay to use a specific resource, calculated based on the following factors:

* Resource configuration (storage quota).
* Unit price according to the configuration (with or without discount): at the time of action on the resource (including VAT).
* Resource usage time: Start date, End date (down to the minute).
* Coupon deduction (if any).

For example, the formula for calculating the amount you need to pay when initializing a project is as follows:

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Quota Default</th><th>Price per Quota Default (include VAT) (2)</th><th>Periods (3)</th><th>Coupon Value (4)</th><th>Total = (2) * (3) - (4)</th></tr></thead><tbody><tr><td>Gold</td><td>30GB</td><td>33,000 VND / 1 month</td><td>1 month</td><td>20,000 VND</td><td>13,000 VND</td></tr><tr><td>Silver</td><td>30GB</td><td>19,800 VND / 1 month</td><td>1 month</td><td>None</td><td>19,800 VND</td></tr><tr><td>Archive</td><td>30GB</td><td>33,660 VND/ 6 month</td><td>6 month</td><td>10,000 VND</td><td>23,660 VND</td></tr><tr><td><p>When you change the quota limit, the storage package price will be adjusted accordingly. Each storage package has its own specifications regarding usage capacity and the number of requests. For more information, please refer to What is vStorage?</p><p>Similarly, when you renew a project or increase/decrease the size of the storage package, we will calculate the additional amount you need to pay or the amount that may be refunded. For details, please refer to Invoice, cost &#x26; resource management on GreenNode.</p></td><td></td><td></td><td></td><td></td><td></td></tr></tbody></table>

***

#### Users prepaid renew or set auto-renew a project <a href="#chargingforprepaidusers-usersprepaidreneworsetauto-renewaproject" id="chargingforprepaidusers-usersprepaidreneworsetauto-renewaproject"></a>

When you renew a project as a pre-paid user, the default amount to be paid is the difference calculated based on the chosen renewal period. We offer storage renewal cycles of 1 month, 3 months, 6 months, 12 months, 24 months, and 36 months. When you select a renewal cycle, the system automatically calculates the effective time of the new storage cycle and the total amount you need to pay for the project renewal. The calculation of the payment difference is based on the following factors:

* t\_start: the start time of the service (Start time).
* t\_end: the end time of the service (End time).
* t\_resize: the time of resizing the project (Time of resizing).
* p\_original: the initial price (Billing Price).
* p\_new: the price after modification (Resizing Price).

For example, the formula for calculating the amount you need to pay when renewing a project is as follows:

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Old Price</th><th>Start time</th><th>End time</th><th>Renew time</th><th>Renew period</th><th>New End time</th><th>New Price</th></tr></thead><tbody><tr><td>Silver</td><td>19,800 VND / 1 month</td><td>06-03-2023</td><td>05-04-2023</td><td>08-03-2023</td><td>1 month</td><td>05-05-2023</td><td>19,800 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 month</td><td>06-03-2023</td><td>05-04-2023</td><td>08-03-2023</td><td>3 month</td><td>04-07-2023</td><td>59,400 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 month</td><td>06-03-2023</td><td>05-04-2023</td><td>08-03-2023</td><td>6 month</td><td>02-10-2023</td><td>118,800 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 month</td><td>06-03-2023</td><td>05-04-2023</td><td>08-03-2023</td><td>12 month</td><td>30-03-2024</td><td>237,600 VND</td></tr><tr><td>Silver</td><td>19,800 VND / 1 month</td><td>06-03-2023</td><td>05-04-2023</td><td>08-03-2023</td><td>24 month</td><td>25-03-2025</td><td>475,200 VND</td></tr></tbody></table>

***

#### Users prepaid resize a project <a href="#chargingforprepaidusers-usersprepaidresizeaproject" id="chargingforprepaidusers-usersprepaidresizeaproject"></a>

When you increase or decrease the storage size (resize) of a project, if you are a user who pays in advance, the default amount to be paid is the amount calculated based on the size of the storage package you choose. You can increase or decrease the quota to the minimum or maximum level that we provide. When you choose the renewal period, the system will automatically calculate the total amount you need to pay for the storage quota change. The rule for calculating the differential payment amount is based on the following factors:

* Current storage package.
* Current quota.
* Unit price on the current quota (1).
* New quota.
* Unit price on the new quota (2).

An example formula for calculating the amount you need to pay when increasing or decreasing the storage quota of a project is as follows:

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Start time</th><th>End time</th><th>Current Quota</th><th>New Quota</th><th>Price Unit/ Current Quota</th><th>Resize time</th><th>Money refund (1)</th><th>Price Unit/ New Quota (2)</th><th>Total days use in New Quota(3)</th><th>Total = (2)/30*(3) - (1)</th></tr></thead><tbody><tr><td>Silver</td><td>06-03-2023</td><td>05-04-2023</td><td>30 GB</td><td>80 GB</td><td>19,800 VND/ 1 month</td><td>31/03/2023</td><td>3,300 VND</td><td>52,800 VND/ 1 month</td><td>5</td><td>5,500 VND</td></tr></tbody></table>

***

#### Users prepaid delete a active project <a href="#chargingforprepaidusers-usersprepaiddeleteaactiveproject" id="chargingforprepaidusers-usersprepaiddeleteaactiveproject"></a>

When you delete an active project, if you are a user who pays in advance, by default, you will receive a refund amount calculated based on the actual number of days you have not used the storage package. The rule for calculating the differential payment amount is based on the following factors:

* t\_start: The time of initiating the service (Start time)
* t\_end: The time of ending the service (End time)
* t\_delete: The time of performing the configuration return (Time of deletion)
* p: The amount of money (Billing Price)

An example formula for calculating the amount you will be refunded when deleting a project is as follows:

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Storage Class</td><td>Start Time</td><td>End Time (1)</td><td>Current Quota</td><td><p>Delete Time</p><p>(2)</p></td><td>Origin Price (3)</td><td>Days refund (4) = (1) - (2)</td><td>Total refund = (3) * (4) * 24 *60 / (30 * 24 * 60)</td></tr><tr><td>Silver</td><td>01-01-2023</td><td>01-02-2023</td><td>30 GB</td><td>08-01-2023</td><td>19,800 VND</td><td>24 ngày</td><td>15,840 VND</td></tr></tbody></table>
