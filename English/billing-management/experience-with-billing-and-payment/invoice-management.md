# Invoice management

Use this document as a guide to help you manage and control your invoices when using services at GreenNode Service.

Here, we provide users with a comprehensive and detailed view of how invoices are processed at the GreenNode Service level, such as Invoice initiation time, Invoice information, Invoice payment time, and View invoice list.

## Invoice initiation time

Invoices are initiated in the following cases:

* Prepaid users perform actions that generate/change resource usage costs such as:
  * Creating resources: Generate a new corresponding invoice for the initialized resource.
  * Resizing resource configuration: Update information on the old invoice, generate a new invoice with the new configuration.
  * Renewing resources: Generate a new invoice with the same resource configuration, but a different usage time.
  * Recovery resources: Generate a new invoice with the same resource configuration, but a different usage time.
* The system records users' resource usage information at the end of each month for postpaid users:
  * For postpaid users, one invoice will be generated for each resource to record the actual usage figures.
  * In the case of users having multiple resources, multiple corresponding invoices will be generated for each resource.

## Invoice information

**Invoice information** includes the main information corresponding to a specific resource:

* Invoice code
* Invoice creation date
* Resource usage time
* Detailed description: Detailed description of the resource and usage configuration.
* Money amount

**For prepaid users**

The amount on the invoice is the amount that the user needs to pay to use a specific resource, calculated on the factors:

* (1) Resource configuration.
* (2) Unit price according to configuration (Discounted or not): At the time of performing the action on the resource (including VAT).
* (3) Resource usage time: Start date, End date (calculated by the minute).
* (4) Coupon deduction (if any).

For example, the formula for calculating the invoice value when initiating a Server including information is:

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**For postpaid users**

* The amount on the invoice is the amount calculated based on the actual cost of using resources.
* The usage report will be exported at the end of the month on the user portal: [https://dashboard.console.greennode.ai/usage-report](https://dashboard.console.greennode.ai/usage-report).
* To understand more about how to calculate the cost of using resources in a month, please refer to this link.

## Payment due date

**For prepaid users**

The invoice will be generated immediately after the system successfully provides resources, and the invoice will be generated with a paid status at that time.

**For postpaid users**

After the service invoice is generated at the end of the month, users can pay in various forms:

* Exchange externally by transferring to the Sale Operation department.
* Pay directly on the user portal by depositing credit into the wallet.

## View invoice list

We provide a user portal website to help users manage usage invoices in the most efficient and effective way:

* Access the invoice management page here: [https://dashboard.console.greennode.ai/billing-report](https://dashboard.console.greennode.ai/billing-report)
* To see more instructions on how to use and the features of the invoice management page, please refer to this link
