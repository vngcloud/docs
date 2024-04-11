# View summary reports across all regions

After you have created projects to store data, we provide you with statistical reports on various metrics within each project. This allows you to manage, control, and evaluate the efficiency of your storage usage. The attributes we use throughout the reports include:

* Quota
* Traffic
* Storage usage
* Request count

To view summary reports across all regions, you can:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Select **Reports** and then choose the desired time range for data aggregation in the report. By default, we display reports for the current day. You can adjust the time range to view reports for up to 3 months by:

\- Selecting a predefined option under **Quick**.\
\- Entering a relative time range that you wish to view data for (usually in hours, minutes, seconds) under **Relative**.\
\- Selecting the Absolute start and end time that you want to view data for (usually in days, hours, minutes) under **Absolute**.

3\. On the report page, you can view detailed metrics for all projects across all regions. The attributes for each project include:

* **General Information**: Provides general information including:
  * Region.
  * Number of projects used in each region.
  * Total quota of projects in each region.
  * Total storage usage of projects in each region.
  * Maximum storage usage: The highest storage usage within the selected time range.
  * Total traffic: The total access traffic within the selected time range.
  * Maximum quota: The highest quota value that you have purchased within the selected time range.
  * Total request count: Includes the total number of requests for HET, HEAD, PUT, POST, DELETE methods within the selected time range.
* **Detailed Information**: Provides detailed information including:
  * Storage usage breakdown by storage packages (Gold, Silver, Archive) within the selected time range.
  * Access traffic breakdown by internal traffic, international traffic, domestic traffic within the selected time range.
  * Number of GET/HEAD requests breakdown by storage packages (Gold, Silver, Archive) within the selected time range.
  * Number of PUT/POST/DELETE requests breakdown by storage packages (Gold, Silver, Archive) within the selected time range.

**Warning:**&#x20;

* The metrics for each project are aggregated into reports that we generate twice a day at fixed time intervals: 7:00 AM and 12:00 PM. For example, if you create a project, create a container, upload files, or perform PUT/DELETE object actions at 04:00 PM on January 1, 2023, these data will be updated after 12:00 PM on the same day. From January 2, 2023, these metrics will be fully reflected in the reports.
* To provide a long-term perspective for your reports, we support viewing these reports with a 3-month cycle. For example, you can choose to view report data from January 1, 2023, to March 31, 2023.
