# Create resource

Use this document as a guide to initialize resources. The document will describe in detail the processing steps related to resource management during initialization. Other steps will be simplified and only referred to as part of the process.&#x20;

Resource initialization feature applies to:&#x20;

* Target user: Prepaid and postpaid users&#x20;
* Source of money: GreenNode wallet or other sources (performed through payment gateway).
* Resources: All resources belonging to GreenNode products.

## Prepaid user initializes resources

### Resource initialization process

* Step 1: Configure resources&#x20;
  * 1.1 Access the vServer, vStorage, vMonitor product page.
  * 1.2 Select the resources and configurations to use on the product page.
  * 1.3 Confirm the use of resources to proceed to payment: At this point, the system will redirect the user to the resource payment page.
* Step 2: Pay for resources See detailed instructions here.
* Step 3: Check resource and payment information&#x20;
  * 3.1 Check resource information on the product page.
  * 3.2 Check payment information, and invoices at User Portal: [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/)
* Step 4: System Implementation&#x20;
  * Email notification of the resource information just initialized.
  * Generate corresponding invoices: Refer to how to calculate the amount and invoice information here.

### Resource pricing guide

The price displayed at the resource payment step is also the price displayed on the corresponding invoice for that resource.&#x20;

Below is a guide to calculate the price when initializing a Server, users can apply the formula to calculate similarly for other resources in the GreenNode Service system.&#x20;

_An example formula for calculating the invoice value when initializing a Server includes information:_&#x20;

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Postpaid user initializes resources&#x20;

### Resource initialization process

* Step 1: Configure resources on the product page
  * 1.1 Access the vServer, vStorage, vMonitor product page&#x20;
  * 1.2 Select the resources and configuration to be used on the product page&#x20;
  * 1.3 Confirm the use of resources.
  * 1.4 Check resource information.
* Step 2: The system sends confirmation information to the user Email notification of newly initialized resources Record the start time of resource usage for calculating the usage price at the end of the month.
