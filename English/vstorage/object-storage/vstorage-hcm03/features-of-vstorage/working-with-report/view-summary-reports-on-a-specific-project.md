# View summary reports on a specific project

To generate a summary report for specific projects in a particular region, you can follow these steps:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).\
2\. Select **Reports**.\
3\. Choose the desired **region** and **project** for which you want to view the report.\
4\. Select the time period you want to consolidate the data for the report. By default, we display the report for the current day. However, you can adjust the time range to view reports for up to 3 months. You have three options to choose from:

* Select a predefined option from the **Quick** section.
* Enter a relative time range (usually in hours, minutes, or seconds) in the **Relative** section.
* Specify the exact start and end time (usually in days, hours, or minutes) in the **Absolute** section.

5\. On the report page, you will find detailed parameters for the selected project in the specified region. These include:

* **General information**: Provides general information, including:
  * Maximum storage capacity used: The maximum storage capacity used within the selected time period.
    * Total traffic: The total access traffic within the selected time period.
    * Maximum quota: The maximum quota value purchased during the selected time period.
    * Total number of requests: Includes the total number of requests for HET, HEAD, PUT, POST, DELETE methods within the selected time period.
    * Storage capacity usage breakdown by storage package (Gold, Silver, Archive) within the selected time period.
    * Access traffic breakdown by internal traffic, international traffic, and domestic traffic within the selected time period.
    * Number of GET/HEAD requests breakdown by storage package (Gold, Silver, Archive) within the selected time period.
    * Number of PUT/POST/DELETE requests breakdown by storage package (Gold, Silver, Archive) within the selected time period.
* **Detailed information**: Provides detailed information, including:
  * Traffic access report: Breaks down traffic access by internal traffic, international traffic, and domestic traffic within the selected time period. Additionally, we provide line, bar, and data table charts for you to track traffic access on a daily basis.
  * Request count report: Breaks down the number of requests for HET, HEAD, PUT, POST, DELETE methods within the selected time period. Similarly, we offer line, bar, and data table charts to track the request count on a daily basis.
  * Storage capacity usage report: Breaks down storage capacity usage by storage package (Gold, Silver, Archive) within the selected time period. You can also track storage capacity usage on a daily basis using line, bar, and data table charts.
  * Quota report: Provides the current quota value for the project. We also offer line, bar, and data table charts to track the quota on a daily basis.

**Warning:**&#x20;

* The parameters of each project are consolidated into reports that we generate twice a day at fixed time frames: 7:00 AM and 12:00 PM. For example, if you create a project, create a container, upload files, or perform PUT/DELETE object actions at 04:00 PM on January 1, 2023, the data will be updated after 12:00 PM on the same day. This means that from January 2, 2023, these parameters will be fully updated in the reports.
* To provide a long-term perspective for your reports, we support viewing these reports with a 3-month cycle. For example, you can choose to view report data from January 1, 2023, to March 31, 2023.
