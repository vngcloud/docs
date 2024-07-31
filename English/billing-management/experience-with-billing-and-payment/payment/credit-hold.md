# Credit hold

At VNG Cloud Service, there are some resources/services specifically designed for postpaid users for the following reasons:&#x20;

* It is impossible to calculate the cost of resource usage at the time of occurrence.&#x20;
* The cost of using resources can only be calculated based on the actual usage of users.&#x20;
* Therefore, prepaid users cannot pay for the cost of using these special resources (such as vContainer service) at the time of initialization.&#x20;

## Overview

Recognizing the increasing demand for postpaid resources/services from prepaid users, VNG Cloud Service has introduced a Credit Hold feature:

* Target audience: Prepaid users.
* Applicable resources/services: Currently supporting vContainer (K8s), Snapshot, vCR (Container Registry).
* Source of money: VNG Cloud wallet (Credit wallet).
* Tasks:&#x20;
  * Users select the configuration of resources they want to use.&#x20;
  * Confirm the credit hold transaction on the payment page.&#x20;
* Results upon completion of the task:&#x20;
  * The system will temporarily hold the credit.&#x20;
  * The amount of credit held by the user will not be used for other purposes. The system will provide resources according to the user's configuration.&#x20;
  * Send an email notification of resource information.

## Continue to use resources after successful initialization

After successfully initializing the resources, the system will automatically calculate the actual amount of money used each day and hold the necessary amount of credit for the user to use the service in the next three days. Refer to the following example **the use of vContainer (K8s) Service**:

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## Insufficient available credit balance to hold credit&#x20;

If the user does not have the minimum available credit balance to hold credit, the system will:&#x20;

* Continue to hold the remaining available credit.&#x20;
* Send an email notification to the user about the amount of credit that needs to be added.&#x20;
* Users will need to actively add credit to their wallet for the system to hold credit the following day (including the temporary credit hold debt).&#x20;
* If the user owes credit for five consecutive days, VNG Cloud will take action to stop providing services to the customer.

## Stopping resource

If the customer proactively stops using resources, the system will:&#x20;

* Generate an invoice based on actual resource usage.
* Proceed to pay the invoice
  * Prioritize using the credit currently on hold for payment, if any excess remains it will be returned as the available credit balance.
  * If the credit on hold is not enough to pay the invoice, the remaining balance will be deducted from the available credit balance. If the available credit balance is still not enough to pay the entire invoice, the invoice status will be recorded as partially paid.
