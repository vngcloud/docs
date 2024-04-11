# View summary reports on a specific region

To generate a summary report for projects in a specific region, you can follow these steps:

&#x20;Use vStorage Portal

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select **Reports**.
3. Choose the desired **region** to view the report.
4. Select the desired time range for data aggregation in the report. By default, the report will display data for the current day. You can adjust the time range to view data for up to 3 months using one of the following options:
   * Choose a pre-defined option provided under the **Quick** section.
   * Enter a relative time range in hours, minutes, and seconds under the **Relative** section.
   * Specify an Absolutestart and end time in days, hours, and minutes under the **Absolute** section.
5. On the report page, you can view detailed metrics for all projects in the selected region, including the following attributes:

* **General Information**: Provides general information, including:
  * Maximum storage usage: The highest storage usage within the selected time range.
  * Total traffic: The total access traffic within the selected time range.
  * Maximum quota: The maximum quota value purchased within the selected time range.
  * Total number of requests: Includes the total number of requests for HET, HEAD, PUT, POST, DELETE methods within the selected time range.
* **Detailed Information**: Provides detailed information, including:
  * Storage usage breakdown by storage packages (Gold, Silver, Archive) within the selected time range.
  * Access traffic breakdown by internal traffic, international traffic, and domestic traffic within the selected time range.
  * Number of GET/HEAD requests breakdown by storage packages (Gold, Silver, Archive) within the selected time range.
  * Number of PUT/POST/DELETE requests breakdown by storage packages (Gold, Silver, Archive) within the selected time range.

**Warning:**&#x20;

* The parameters of each project are consolidated into reports that we generate twice a day at fixed times: 7:00 AM and 12:00 PM. For example, if you create a project, create a container, upload files, or perform PUT/DELETE object actions at 04:00 PM on January 1, 2023, the data will be updated after 12:00 PM on the same day. This means that from January 2, 2023, these parameters will be fully updated in the reports.
* To provide a long-term perspective for your reports, we support viewing these reports on a 3-month cycle. For example, you can choose to view report data from January 1, 2023, to March 31, 2023.
