# Prepaid & Postpaid Users

Use this document to better understand the types of resource usage for different types of users. At the VGN Cloud Service level, we support two main types of users:&#x20;

* **Prepaid users:** Users who must pay for resource usage before they are allowed to use them. Payment for resource usage is based on the configuration and time they want to use (they need to determine the time to stop using resources).&#x20;
* **Postpaid users:** Users who are allowed to use resources first and pay later, based on the actual resource usage cost. The amount to be paid will be determined at the end of each month until the user stops using the resource.&#x20;

Let's take a look at some differences in concepts, rights, and functions between these two types of users for VNG Cloud services, such as:&#x20;

* Process actions on resources: Create, Resize, Renew, Recover, Delete.
* Resource provisioning process.
* Resource management.
* Invoice management.
* Payment management.

## Process actions on resources

**Prepaid users**

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Postpaid users**

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Resource provisioning process

* **Prepaid users:**
  * After successful payment confirmation, the Product team will provide resources according to the configuration requested by the user.&#x20;
  * During the resource provisioning process, if there is a process error, the system will refund the user's previously paid service fee. The refunded money will be converted into Credit and transferred to the VNG Cloud wallet.&#x20;
* **Postpaid users:**&#x20;
  * At the "Confirmation" step, the Product team will provide resources according to the user's requested configuration, and the system will record the start time of resource usage.

## Resource management&#x20;

Basically, the features that users can perform on resources are:

* **For prepaid users**: Create new resources Change configuration Renew resources Recover resources Auto-renew resources Delete resources.
* **For postpaid users:** Create new resources Change configuration Delete resources.

## Invoice management&#x20;

* **Prepaid users**
  * At the successful payment step, after successfully providing resources, the system will generate an invoice that corresponds to the user's resource usage, which is considered paid.
* **Postpaid users**&#x20;
  * Invoices for resources will be generated at the end of each month, based on the actual usage of the customer during that month.&#x20;
  * The generated invoice will be considered unpaid, and users can pay through the following two methods: Contact the Sales or Support team  or Access the user portal, go to Billing history, select the invoice to be paid and proceed with payment.

## Payment Management

* **Prepaid Users**
  * Payment history will appear immediately in the User Portal's Payment history section after the user makes a resource payment.&#x20;
* **Postpaid Users:** In general, postpaid users will have payment history in the following cases:
  * Automatic invoice payment system → Learn more about **automatic invoice payment**
  * Users proactively pay invoices at the User Portal

## How to switch from prepaid to postpaid and vice versa?

When users register a new account at VNG Cloud, the system will default to prepaid users. To switch to postpaid users, users need to proactively contact the Sales/Support department for assistance upon request. In case a postpaid user wants to switch back to prepaid, they can also proactively contact the Sales/Support department for assistance upon request.
