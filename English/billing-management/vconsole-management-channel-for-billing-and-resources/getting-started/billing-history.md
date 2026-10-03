# Billing History

The **Billing History** page in vConsole provides reports and cost statistics for GreenNode Service products (vServer, vMonitor, vStorage, vCDN, etc.). vConsole offers two types of reports (Overview and Detailed) to suit different user needs:

* Pie chart: Statistics of GreenNode Service usage costs, categorized by product, over a specific period.
* Bar chart: Statistics of invoice payments by amount and payment status over a specific period.

Access the **Billing History** page [**here**](https://dashboard.console.greennode.ai/billing-report)**.**

On the **Billing History** page, users will see two main sections:

#### **1. Usage history** <a href="#billinghistory-1.usagehistory" id="billinghistory-1.usagehistory"></a>

***

Here, users can view the total payments for GreenNode Service products (_vServer, vStorage, vMonitor, vCDN_) by selecting a time range in the **time box (in months)**:

* **Quick**: Options include _This month, Last month, Last 2 months, Last 3 months, Last 6 months_
* **Relative**: Enter any number of months counting back from the current time. For example: if the current month is **12/2022** and you enter 5 in the "From" field, the applied time range is from **07/2022** to **12/2022**. If you also enter 2 in the "To" field, the applied time range is from **07/2022** to **10/2022.** Click the **"View this range"** button to apply the selected time range.
* **Absolute:** Enter the specific time range ("From" → "To") you want to view, then click the **"View this range"** button to apply the selected time range.

Based on the applied time range, you will see two types of reports/statistics:

* **Pie chart**: Statistics of _invoiced service usage costs_ within the time range selected in the **time box,** including:
  * Total cost of all services: Displayed in the center of the chart
  * Costs by product: **vMonitor**, **vCDN**, **vStorage**, **vServer.** Users can select/deselect one or more products to view their figures on the chart. To map data from the Pie chart to the Bar chart, click a specific product on the Pie chart
* **Bar chart**: Statistics of invoice payment status (Paid and Unpaid) by month, within the time range selected in the **time box.** Users can choose to view Paid invoices, Unpaid invoices, or both.

To view the invoice payment status of a specific product, select that product on the Pie chart. The Bar chart will then display the payment status out of the total invoices for that product.

* Example: The **Pie chart** is displaying invoice costs for two products, **vServer and vMonitor**. Click **vServer** on the **Pie chart** to view monthly invoice payment information for **vServer** in the **Bar chart**, and click **vServer** again to view data for **All** products. Follow the same steps for other products.

#### **2. Billing report** <a href="#billinghistory-2.billingreport" id="billinghistory-2.billingreport"></a>

***

Here, users can view detailed invoice statistics, including: _Invoice ID, Service, Created date, Invoice details, Status **(Paid / Unpaid / Partially paid)**, Total amount (VND)_

Along with key features such as:

* **Search:** Search invoices using multiple criteria
  1. **By product / service**: Search invoices by GreenNode Service product/service. vConsole currently supports filtering by 04 main products/services: _vServer, vStorage, vMonitor, vCDN._
  2. **By time**: Search by day.
  3. **By keyword:** Search by _Invoice ID / Invoice details / Invoice status_

_Finally, click the **"Magnifying glass"** icon to view the search results based on the criteria above._

* **Export report:** Click the **"Export report"** icon next to the **"Magnifying glass"** icon to export all invoice information based on the search results (supported formats: .pdf, .xlsx).

#### **3. FAQ** <a href="#billinghistory-3.faq" id="billinghistory-3.faq"></a>

***

**Why does an invoice have the status Partially paid / Partial\_Paid?**

* An invoice has the status Partially paid / Partial\_Paid when the user does not have sufficient balance to pay the full invoice. In this case, the invoice is partially paid, and the user is notified by email with the invoice information, including:
  * Invoice information
  * Invoice total
  * Amount paid
  * Amount unpaid
