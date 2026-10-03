# Cost Explorer

The **Cost Explorer** in vConsole provides statistics, analysis, and forecasts of GreenNode service usage costs across **multiple data dimensions** (by product, by resource type, and by individual resource), with various time granularities and flexible data filtering.

Access the **Cost Explorer** page [**here**](https://dashboard.console.greennode.ai/cost-explorer)**.**

**Cost Explorer only supports cost forecasting for the following products/services:**

| Product      | Typical resource types                   | Cost statistics / forecasting supported in Cost Explorer |
| ------------ | ---------------------------------------- | -------------------------------------------------------- |
| **vServer**  | `instance`, `volume`, `load balancer`, … | Yes                                                      |
| **vStorage** | `object-storage`, `backup-location`, …   | Yes                                                      |
| **vMonitor** | `monitor-platform-log`, …                | Yes                                                      |
| **AI Base**  | <p><code>ai-runtime</code>, …<br></p>    | Yes                                                      |

{% hint style="info" %}
The table above lists only **some typical resource types** for each product; the full list may expand per product. Users can view all resource types incurring costs via the **Resource type** filter in the interface. Resource types with zero cost during the period are still listed for complete tracking.
{% endhint %}

#### **1.** Filters and data scope <a href="#costexplorer-1.filtersanddatascope" id="costexplorer-1.filtersanddatascope"></a>

***

The filter bar at the top of the page lets users customize the displayed data. The available options change according to the selected **view mode (View by)**.

| Filter                    | Description                                                                                                                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **View by**               | Data analysis mode, with 3 options: **Product**, **Resource type**, **Resource ID**. This filter determines how data is aggregated and displayed across the entire page.                           |
| **Product**               | Filter by a specific product or **All products**.                                                                                                                                                  |
| **Resource type**         | Filter by a specific resource type or **All types**. _(Displayed in the Resource type and Resource ID view modes.)_                                                                                |
| **Resource name**         | Search by resource name.                                                                                                                                                                           |
| **Resource ID**           | Search by resource ID. _(In Resource ID mode, the search box is combined as "Search by resource name or ID".)_                                                                                     |
| **Granularity**           | Time-based data grouping level, with 4 options: **Hourly**, **Daily**, **Weekly**, **Monthly**. The chart's time axis and the table columns change accordingly.                                    |
| **Start date / End date** | Statistics period, **fixed to the current month** (from the beginning of the month to the time of access). This field is displayed for reference only; users cannot select a different time range. |
| **Apply**                 | Apply all filter conditions to update the chart, tables, and overview metrics.                                                                                                                     |

{% hint style="info" %}
**Flexible granularity:** Users can switch the data grouping level between **Hourly / Daily / Weekly / Monthly** to view costs at different time resolutions within the current month.<br>
{% endhint %}

#### **2.** Overview metrics <a href="#costexplorer-2.overviewmetrics" id="costexplorer-2.overviewmetrics"></a>

***

The left-hand area displays overview metric cards. The card content changes according to the view mode.

**Current month cost**

* Total service usage cost (only for products supported by Cost Explorer) within the selected time range.
* Displays the **change compared to the previous period** (percentage increase/decrease), compared against the immediately preceding period of the same length.
* Convention:
  * Percentage ≥ 0: **Increase** compared to the previous period.
  * Otherwise: **Decrease** compared to the previous period.

**Forecast month cost**

* Forecasts the total cost through the end of the current month, based on service usage trends from the beginning of the month to the time of access.
* _(Displayed in the Product view mode.)_

**Top resource type**

* The resource type with the highest cost in the period, along with its value and **share (%)** of the total cost.
* _(Displayed in the Resource type view mode.)_

**Breakdown by product / by type**

* A ranking of the cost share of each product (Product mode) or each resource type (Resource type mode), with a visual proportion bar and the corresponding cost value.

**Overview cards in Resource ID mode**

| Card                        | Meaning                                                    |
| --------------------------- | ---------------------------------------------------------- |
| **Total resource cost**     | Total cost of all resources in the period.                 |
| **Resources in period**     | Number of resources incurring costs during the time range. |
| **Average cost / resource** | Average cost per resource in the period.                   |

#### 3. Product view mode

***

Aggregates costs by **product** (vserver, vstorage, ai base, vmonitor…).

* **Overview metrics:** Current month cost, Forecast month cost, Breakdown by product.
* **"Cost details — by Product" chart:** each color represents a product.
* **"Cost details — by Product" table:**
  * Columns: **Product**, **Total (VND)**, and daily costs within the selected range.
  * The first row, **Total cost**, sums all products; each subsequent row represents one product.

#### 4. Resource type view mode

***

Aggregates costs by **resource type** (instance, volume, object-storage, ai-runtime, backup-location, monitor-platform-log, snapshot, etc.).

* **Overview metrics:** Current month cost, Top resource type, Breakdown by type.
* **"Cost details — by Resource type" chart:** each color represents a resource type.
* **"Cost details — by Resource type" table:**
  * Columns: **Resource type**, **Total (VND)**, **% of total** (share of total cost), and daily costs.
  * The first row is **Total cost**; each subsequent row represents one resource type.

#### 5. Resource ID view mode

***

Lists detailed costs down to each individual **resource** — the most detailed view level.

* **Overview metrics:** Total resource cost, Resources in period, Average cost / resource.
* **"Resources in period" table:**

| Column            | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| **Resource ID**   | Unique identifier of the resource (click to view details). |
| **Resource name** | Display name of the resource.                              |
| **Product**       | The product the resource belongs to.                       |
| **Resource type** | The resource's type.                                       |
| **Total (VND)**   | Total cost of the resource in the period.                  |
| **Daily average** | Average daily cost of the resource.                        |
| **Start date**    | Date the resource started incurring costs in the period.   |

* **Click a row** to view that resource's details.
* Supports selecting the number of rows displayed (**Show**) and pagination.

#### 6. Charts and statistical tables

***

* **Supported chart types:**
  * **Bar:** compares costs across time points.
  * **Line:** shows cost trends over time. _(New)_
  * **Stacked:** compares the contribution share of each component within the same bar.
* The chart's time axis and the table columns are determined by the selected **Granularity** (Hourly / Daily / Weekly / Monthly), within the current month.
* Chart and table data are always synchronized with the overview metrics and the applied filters.

#### Notes (\*)

* Figures in Cost Explorer are **forecasts / estimates** and are not 100% accurate, because:
  * Data in vConsole is not real-time and is subject to update delays.
  * Data only covers products/resource types supported by Cost Explorer (see the table at the top of the page).
* Costs are calculated using the **current price list**, so the figures are **most accurate for postpaid users**. For **prepaid users**, discrepancies may occur if the price list changes between the payment date and the time Cost Explorer is accessed.
* The **Forecast month cost** metric is based on usage trends from the beginning of the month to date and is for reference only.

<br>
