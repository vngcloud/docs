# Working with reports

vStorage provides you with storage statistics and project activity reports, you can view this information over the desired time period through the different chart formats we provide.

{% hint style="info" %}
**Attention:**

* The parameters of each project are aggregated into reports that we aggregate twice a day at two fixed time frames: 7:00 AM and 12:00 PM. For example, when you create a project, create a bucket, upload a file or perform PUT/DELETE object actions at 04:00 PM on January 1, 2023, after 12:00 PM on the same day, this data will be updated. That is, from January 2, 2023, these parameters will be fully updated on the reports.
* To provide a long-term perspective for your reports, we support you to view these reports on a 3-month cycle. For example, you can choose to view report data from 01/01/2023 to 31/03/2023.
{% endhint %}

## View summary reports on a specific region <a href="#xem-bao-cao-tom-tat-tren-mot-region-cu-the" id="xem-bao-cao-tom-tat-tren-mot-region-cu-the"></a>

To report a summary of projects in a specific region, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the Region** you want to view the report\*\*.\*\*

3\. Select **the Time range** you want to summarize data on the report. By default, we will display the report within the month. You can adjust the report viewing period up to 3 months through

* Choose an option we provide in the **Quick** section .
* Enter the relative time period you want to view data for (usually in hours, minutes, seconds) in the **Relative** field .
* Select the exact start and end times you want to view data for (usually in days, hours, minutes) in the **Absolute section.**

4\. On the detailed parameters report page of all projects **in** a **region,** you can view the properties for the project including:

* **General information** : provides general information including:
  * **Max Usage** : the maximum usage during the time period you select.
  * **Total Traffic** : total traffic during the time period you select.
  * **Max Quota** : the maximum quota value you can purchase within the time period you choose.
  * **Total requests** : includes the total number of requests in the types HET, HEAD, PUT, POST, DELETE in the time period you select.
* **Details** : provide information including:
  * Usage is calculated according to each Gold, Silver, Archive storage package for the period of time you choose.
  * Traffic is divided into internal traffic, international traffic, domestic traffic in the time period you choose.
  * Number of GET/HEAD requests divided by Gold, Silver, Archive storage packages during the time period you choose.
  * Number of PUT/ POST/ DELETE requests divided by Gold, Silver, Archive storage packages during the time period you choose.

## View summary reports on a specific project <a href="#xem-bao-cao-tom-tat-tren-mot-project-cu-the" id="xem-bao-cao-tom-tat-tren-mot-project-cu-the"></a>

To report a summary of projects in a specific region, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the Region** you want to view the report\*\*.\*\*

3\. Select **the Project** to view the report\*\*.\*\*

3\. Select **the Time range** you want to summarize data on the report. By default, we will display the report within the month. You can adjust the report viewing period up to 3 months through

* Choose an option we provide in the **Quick** section .
* Enter the relative time period you want to view data for (usually in hours, minutes, seconds) in the **Relative** field .
* Select the exact start and end times you want to view data for (usually in days, hours, minutes) in the **Absolute section.**

4\. On the detailed parameters report page of a **project** in a **region,** you can view the properties for the project including:

* **General information** : provides general information including:
  * **Max Usage** : the maximum usage during the time period you select.
  * **Total Traffic** : total traffic during the time period you select.
  * **Max Quota** : the maximum quota value you can purchase within the time period you choose.
  * **Total Requests** : includes the total number of requests in the types HET, HEAD, PUT, POST, DELETE in the time period you select.
  * Usage is calculated according to each Gold, Silver, Archive storage package for the period of time you choose.
  * Traffic is divided into internal traffic, international traffic, domestic traffic in the time period you choose.
  * Number of GET/HEAD requests divided by Gold, Silver, Archive storage packages during the time period you choose.
  * Number of PUT/ POST/ DELETE requests divided by Gold, Silver, Archive storage packages during the time period you choose.
* **Details** : provide information including:
  * **Traffic Report** : divided by internal traffic, international traffic, domestic traffic in the period you choose. Besides, we support you to track traffic by day through line charts, columns and data tables.
  * **Request Report** : divided by the number of requests in the types HET, HEAD, PUT, POST, DELETE in the time period you choose. Besides, we support you to track the number of requests by day through line charts, columns and data tables.
  * **Usage Report** : divided by storage package in Gold, Silver, Archive types within the period you choose. Besides, we support you to track storage capacity by day through line charts, columns and data tables.
  * **Quota Report** : current quota value of the project. Besides, we support you to track quota by day through line chart, column chart and data table.
