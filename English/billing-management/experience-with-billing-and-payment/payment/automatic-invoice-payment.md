# Automatic invoice payment

Auto payment is a feature designed to support GreenNode users in paying their unpaid invoices.

**Target users**

* Prepaid and postpaid users having unpaid invoices.&#x20;
* The invoices to be paid have the status of "unpaid" or "partially paid".&#x20;

**Runtime:** Every day.

**Source of money:** GreenNode wallet (Credit wallet)&#x20;

**Tasks**&#x20;

* Filter out users with outstanding bills to be paid.&#x20;
* Check if there is an available balance in the wallet:&#x20;
  * If the available balance is greater than 0: Prioritize paying bills in order of older bills and bills with smaller amounts first.&#x20;
  * If the available balance is less than or equal to 0: Cancel the task.&#x20;

**Results upon completion of the task**

* Send an email to the user notifying them of the bill that has just been paid.&#x20;
* Generate transaction history on the user portal at:&#x20;
  * Billing history: [https://dashboard.console.vngcloud.vn/billing-report](https://dashboard.console.vngcloud.vn/billing-report).
  * Credit history: [https://dashboard.console.vngcloud.vn/credit-history](https://dashboard.console.vngcloud.vn/credit-history).
  * Payment history: [https://dashboard.console.vngcloud.vn/payment-history](https://dashboard.console.vngcloud.vn/payment-history).
