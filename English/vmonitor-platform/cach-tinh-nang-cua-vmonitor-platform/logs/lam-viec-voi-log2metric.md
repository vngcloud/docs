# Working with Log2metric

## Overview <a href="#lamviecvoilog2metric-tongquan" id="lamviecvoilog2metric-tongquan"></a>

Log2metric is a feature that allows you to create real-time metrics from logs. This approach helps you optimize log storage without sacrificing any important data. So your costs will be reduced. You can start using log2metric by setting up a simple query and we'll evaluate the value every **60** seconds. For example, you want to count the number of log lines with an error status, or you want to know the average request response time in your web server's logs, just use Log2metric. These output metrics are similar to other metrics you can use to draw dashboards and create alarms.

***

## Log2metric limited range <a href="#lamviecvoilog2metric-phamvigioihanlog2metric" id="lamviecvoilog2metric-phamvigioihanlog2metric"></a>

**Metric name naming rules:**

The following rules apply to metric naming in vStorage:

* The metric name must be between 3 (minimum) and 50 (maximum) characters long.
* The metric name must have the first character alphanumerics (az, AZ) or underscores (\_). The following characters are alphanumerics (az, 0-9), underscores (\_), minuses (-), periods (.) or slashes ( / ).
* The metric name should not contain sensitive information (eg IP address, account name, login password,...).
* The metric name must be unique on a GreenNode account until that metric is deleted.

**Illustration**

* The following example metric names are valid and follow recommended naming guidelines:
  * cpu.time\_system
  * mem.active
  * disk.free
  * ...

***

## Initialize metrics <a href="#lamviecvoilog2metric-khoitaometric" id="lamviecvoilog2metric-khoitaometric"></a>

To generate a metric from your log, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/) .
2. **Select the Log** folder , then select the **Log2metric** menu .
3. Select **Create a Metric** .
4. Enter **Metric name** . Metric names must comply with our rules, detailed above.
5. Create **Query Definition** by:
   * Search and select a **Log Project** you want to convert log to metric. The screen will display the logs in **the Log project** within 15 minutes for you to preview.
   * Create **Log Filter** to search for logs, select operations ( **Operator** ), select data grouping conditions ( **Group by** ), refer to [Search logs](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-search/search-logs) for details .
6. Select **Advanced query** if you want to set up advanced metrics including: **Event timestamp field, Event timestamp format, Default metric value** in which:
   * Select **Event timestamp field** : This field is used to read the time **the event** occurred. If you do not select it, we will take the **processing time** .
   * Select **Event timestamp format** : if you have selected **the Event timestamp field** before, this field is used to format the corresponding time of **the Event timestamp field** . If you choose **the Event timestamp format** that is not correct for the data type of **the Event timestamp field , the metric** result may not be correct.
   * Enter **Default metric value** : enter the default value of **the metric** if there is no calculated data based on the conditions entered above. You can enter real numbers from 0 to 100,000,000,000,000.

6\. Select **Create new** . **The metric** is created with the metric name and **log** based on the new creation condition you selected/entered. When the status of log2metric is **ACTIVE** , you can now continue to use this generated **metric in** [the Dashboard](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/dashboard) and [Metric Alarm](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/alarm/metric-alarm) .

The **data points** for the newly created Log2metric are periodically generated at 60s intervals **.** You can create multiple **metrics** for a **log project** with different **metric names** . The first time you initialize a metric from the log, the initialization process may take some time because we need to set up a lot of necessary configuration. Don't worry because from the next metric initializations, this process will be much faster.

***

## Edit metrics <a href="#lamviecvoilog2metric-chinhsuametric" id="lamviecvoilog2metric-chinhsuametric"></a>

To edit metrics that were previously created from logs, follow the instructions below:

1. Log in to vMonitor Platform [here.](https://hcm-3.console.vngcloud.vn/vmonitor)
2. **Select the Log** folder , then select the **Log2metric** menu .
3. At **the Metric** you want to edit, select **Edit** .
4. Edit the chart parameters as you desire. Parameters that you can edit include: **Log filter, Advanced query** . This editing is similar to when you create a new Widget.
5. Select **Save.**

***

## Delete metrics <a href="#lamviecvoilog2metric-xoametric" id="lamviecvoilog2metric-xoametric"></a>

You have initialized a metric from a corresponding log project. This metric has been used by you in vMonitor Dashboard, vMonitor Alarm. Currently you do not need to use this metric. We recommend that you delete this metric to optimize Metric quota costs.

To delete a project, follow these instructions:

1\. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/) .

**2. Select the Log** folder , then select the **Log2metric** menu .

3\. In the list of existing **metrics**![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLYHslWyx45GFqWXwFOpi%252Fimage.png%3Falt%3Dmedia%26token%3D68527325-aa58-43e6-af78-6a146e85c8ba\&width=35\&dpr=4\&quality=100\&sign=406fbad6\&sv=1) , select **the metric** you want to delete, then select **Delete** .

4\. Select **Delete** .

After you complete the 4 steps above to delete metrics, we will start the process of deleting your metrics. The status of the metric is currently Deleting. At this time, metrics have not been updated or deleted in vMonitor Dashboard or vMonitor Alarm. By the time we notify you that the metric has been successfully deleted, the metric will be deleted on the Log2Metric side but that metric name still exists on the vMonitor Platform - Metric system side. Therefore, if the Widget using the metric is deleted, the chart drawn from the metric will not have new data (the chart will retain its current status, features and old data before deleting the metric) and you can still add more. new Widget other than this removed metric.
