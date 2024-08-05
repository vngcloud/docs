# Apply coupon at payment step

A Coupon is a discount code provided by VNG Cloud. The Coupon can only be used for the vServer, vStorage, vCDN, vDB, vMonitor, and vWAF products when paying for services from these products.&#x20;

To use a Coupon, simply follow these steps:

* Step 1: Configure resources on the product page (vServer, vStorage, vServer).&#x20;
* Step 2: Confirm the use of resources to proceed to the payment page.&#x20;
* Step 3: Enter the coupon code on the payment page to apply the discount. Users will receive notification of an invalid coupon code in cases where the coupon has expired or is not applicable to the service being paid for, etc.&#x20;
* Step 4: Click on the payment confirmation to complete the purchase.

**How the coupon value is calculated for a single payment**&#x20;

* In cases where users use a Coupon when paying for an order with multiple resources, the Coupon value will be divided among the resources based on the value of the resources on the total order.
* Below is an example of applying a 150,000 VND Coupon for a single payment consisting of multiple resources:

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

→ **The total initial order amount** is 1,500,000 VND.&#x20;

→ **Percentage of coupon value applied:**&#x20;

* Server = 1,000,000/1,500,000 = 2/3 coupon value.
* Project storage = 500,000/1,500,000 = 1/3 coupon value.

From the example above, the user needs to pay 900,000 + 450,000 = 1,350,000 VND in one transaction for the 2 resources purchased at the same time. At the same time, the system will generate 2 invoices recording the price information of each corresponding resource (after applying the coupon).
