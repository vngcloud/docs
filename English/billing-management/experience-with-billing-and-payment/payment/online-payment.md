# Online payment

Online payment is one of the main payment methods at GreenNode Service. Currently, online payment method applies to:&#x20;

* **Target audience:** Prepaid users.
* **Source of funds:**&#x20;
  * GreenNode Wallet (Credit Wallet).
  * Online payment gateway: MoMo, ZaloPay, etc.&#x20;
* **Tasks:**&#x20;
  * Users choose the payment method and confirm the payment.
  * The system performs the payment.
    * Successful payment: Resources are provided according to the configuration, and transaction occurs in Payment History and Credit History (if using credit).
    * Payment failed: Cancel the task.
  * Provide resources according to the configuration:&#x20;
    * Success: Generate invoice history in Billing History.
    * Failure: Refund (generate refund transaction in Credit History), Cancel the task.
* **Result when completing the task:**&#x20;
  * Send an email notification with resource configuration information.
  * Generate transaction histories in Credit History, Payment History, and Billing History.

**Currently, the online payment feature at GreenNode supports the following payment methods:**

* **Payment with GreenNode Wallet (Credit)**&#x20;
  * Pay the entire order with Credit (if the available balance is sufficient).
  * In case of insufficient Credit balance, users can choose **Top up & Pay**: Use the entire available credit balance, and the remaining amount will be topped up via the online payment gateway
* **Pay through the payment gateway:** Pay the full value of the order through the online payment gateway without affecting the Credit Wallet (currently supporting payment methods such as MoMo, Zalo Pay, etc.).

In addition, when selecting the payment method through the payment gateway, GreenNode Service provides another payment method called Payment on Behalf.

* **Payment on Behalf**

Payment on Behalf is generated to support business or individual customers who are prepaid users and need to use GreenNode Service resources but depend on the financial aspect of other individuals/businesses.&#x20;

Payment on Behalf is only available when users choose to pay through the online payment gateway.&#x20;

At the step of confirming the deduction, instead of pressing Pay, users **click Share**, with the purpose of authorizing the payment:&#x20;

* Step 1: Click Share.
* Step 2: Enter the email of the authorized person to make payment, and click Confirm After clicking confirm, the system will send an email including the URL to the order payment page, the URL is valid for 3 days from the time of receiving the email.
* Step 3: The authorized person accesses the URL sent in the email (provided the URL is still valid).
* Step 4: The authorized person confirms the order payment.
* Step 5: The system will provide the resources after the successful confirmation of payment.&#x20;
* Step 6: After successfully providing resources, the system generates a corresponding invoice for the user (the person who requested the payment on behalf). In case of errors in the process, the task will be cancelled, and a refund will be issued

