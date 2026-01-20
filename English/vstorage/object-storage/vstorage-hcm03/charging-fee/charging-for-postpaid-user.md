# Charging for postpaid user

When you create a project, if you are a postpaid user, you can purchase the project by default without having to pay the storage package price at the time of purchase. At the end of each month, we will provide you with an invoice containing information on resource usage and costs incurred on the resources that you actually use.

Resource usage information includes:

* Invoice code: Invoice ID
* Creation date: Invoice creation date
* Status: Invoice status (Paid / Partial\_Paid / Unpaid)
* Resource name: Name of the resource used
* Resource ID: Resource ID
* Product name: Indicates the type of product to which the resource belongs (vServer, vStorage, vMonitor, vCDN)
* Service name: Indicates the type of service to which the resource belongs
* Item: Indicates which item the resource is using
* Unit: Indicates the unit used to calculate the price of the item. For example, the unit is GB for the VPC-Bandwidth service of the vServer product)
* Reconciliation period in the month: Indicates the period of time the resource was used with the same configuration (start and end time)
* Unit price (VND): Indicates the price to be paid per unit
* Quantity: Indicates the number of items used in a resource
* Discount (%): Indicates the percentage of the price that is discounted on an item at the time the resource is purchased
* Tax rate (%): Tax applicable at the time of purchase of the resource
* Coupon value (VND): Coupon value applied at the time of purchase of the resource
* Coupon code: Coupon code applied at the time of purchase of the resource
* Total amount (VND): Total cost of using the resource in the month
* You can view the resource usage report at: [https://dashboard.console.vngcloud.vn/usage-report](https://dashboard.console.vngcloud.vn/usage-report)

**The total amount you need to pay at the end of each month is calculated based on the following formula:**

* Total cost before tax: \[Reconciliation period in the month (in minutes) \* Unit price \* Quantity \* (1 - Discount / 100) / (30 \* 24 \* 60)]
* Tax amount: Total cost before tax \* Tax rate / 100
* Total cost of use in the month: Total cost before tax + Tax amount - Coupon value
* The above formula is an example in the case of Unit calculated on 30 days, (30 \* 24 \* 60) converted to minutes.

**Similarly, when you renew a project, increase/decrease the size of the storage package, we will also calculate the additional price you need to pay or the price that you can be refunded. For details, please refer to Invoice, cost & resource management on GreenNode.**
