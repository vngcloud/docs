# Usage Report

The **Usage Report** in vConsole provides reports and cost statistics for GreenNode Service products (vServer, vMonitor, vStorage, vCDN, etc.), broken down by individual resource. Here, users can track how long each resource has been used, as well as any configuration changes (if applicable).

Access the **Usage Report** page [**here**](https://dashboard.console.greennode.ai/usage-report)**.**

On the **Usage Report** page, users will see the main data table, which includes the following components:

#### **1. Search toolbar** <a href="#usagereport-1.searchtoolbar" id="usagereport-1.searchtoolbar"></a>

***

**Search resource usage information using multiple criteria:**

* **Product type:** Search resource usage information by specific product:
  * **All:** Default when accessing the page; searches resource usage across all products
  * **vServer:** Search resource usage for vServer
  * **vStorage:** Search resource usage for vStorage
  * **vMonitor:** Search resource usage for vMonitor
  * **vCDN:** Search resource usage for vCDN
* **Usage period:** Defaults to the previous month; only data within a single month can be searched
* **Keyword:** Search by _Invoice ID, Resource name, Resource ID, Product, Service, Item, Coupon code._

_Finally, click the **"Magnifying glass"** icon to view the search results based on the criteria above._

**Export reports based on search criteria:**

_To export payment history data:_

* Click the **"Export report"** icon next to the **"Magnifying glass"** icon to export the full payment history based on the search results.
* Supported format: Excel (.xlsx)
* Save location: By default, the file is saved to the "Downloads" folder or according to your web browser settings.

#### **2. Search results** <a href="#usagereport-2.searchresults" id="usagereport-2.searchresults"></a>

***

Search results are displayed based on the criteria applied in the "Search toolbar" and include the following key information:

* **Invoice ID:** Invoice identifier
* **Created date:** Date the invoice was issued
* **Status:** Invoice status (Paid / Partial\_Paid / Unpaid)
* **Resource name:** Name of the resource used
* **Resource ID:** Resource identifier
* **Product name:** The product type the resource belongs to (vServer, vStorage, vMonitor, vCDN)
* **Service name:** The service type the resource belongs to
* **Item:** The item the resource corresponds to
* **Unit:** The unit used to price the item. **E.g.: GB is the unit for the VPC-Bandwidth service of the vServer product**
* **Reconciliation period in month:** The period during which the resource was used with the same configuration (start and end time)
* **Unit price (VND):** Price per unit
* **Quantity:** Number of items used in a resource
* **Discount (%):** Percentage discount applied to an item at the time the resource was purchased
* **Tax rate (%):** Tax applied at the time the resource was purchased
* **Coupon value (VND):** Coupon value applied at the time the resource was purchased
* **Coupon code:** Coupon code applied at the time the resource was purchased
* **Total amount (VND):** Total cost of resource usage for the month

#### **3. FAQ** <a href="#usagereport-3.faq" id="usagereport-3.faq"></a>

***

**How is the total monthly resource usage cost calculated?**

* **Total cost before tax** = \[**Reconciliation period in month** (in minutes) \* **Unit price** \* **Quantity** \* (**1 - Discount/100**) / (**30\*24\*60**)]
* **Tax amount** = **Total cost before tax** \* **Tax rate** / 100
* **Total monthly usage cost** = **Total cost before tax + Tax amount** - **Coupon value**
* Note: The formula above is an example where the **Unit** is based on 30 days, with (30\*24\*60) converting it into minutes.

**How do I view resource usage that spans more than one month?**

* The Usage Report page only supports viewing resource usage within a single month.
* If a resource's usage spans multiple months, change the month you want to view in the search toolbar.
* The displayed Coupon value is also divided evenly across the months of usage. For example:
  * At the time of purchase, a Coupon value of 100,000 VND was applied. The resource was used from 01/2023 to 02/2023, so:
    * The Coupon value displayed for 01/2023 is 50,000 VND
    * The Coupon value displayed for 02/2023 is 50,000 VND

**How do I view resource configuration changes within a month?**

* When a resource's configuration changes, an additional invoice line is generated to map to the resource's new configuration.
* This means multiple invoice lines may be linked to the same resource if its configuration has been changed several times.

**The data table contains too much information. How can I view only the columns I need?**

* You can show or hide data columns as needed by clicking the **Settings icon** in the top right corner of the data table.
