# Log search

### Overview

A summary table chart is a type of chart that displays calculated values from a dataset, rather than showing the raw numbers. Typically, this type of chart should be used when you want to group data over time using the Group by feature.

<figure><img src="../../../../.gitbook/assets/image (73) (1).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (74) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For the table chart, in this section, you select Style as **Log search**

<figure><img src="../../../../.gitbook/assets/image (75) (1).png" alt="" width="563"><figcaption></figcaption></figure>

#### 2. Graph your data

Select data type to draw Widget:

* **Metrics: No Support.**
* Logs: refer to Log Query for configuring the Logs data type.

**By default, log data is displayed in Full content view**. If you only want to display a certain number of log fields on the chart, select the log fields at

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Alias: You can set an Alias for each query. This alias will be displayed on the graph and legend, which is useful for long metric names, logs, or queries with extensive filters.

#### 3. Fixed time range

A fixed time range is an attribute of a Widget that you can set to filter data on the Widget according to a fixed time range, independent of the Dashboard's time range. Each Widget can have its own Fixed time range setting. You can choose one of the time ranges described in the table below. For example, if you select Global time, the data retrieval period displayed on the Widget will match the period you selected on the Dashboard. This means that changing the data retrieval time on the Dashboard will also change the Widget's data retrieval time. This option is recommended. If you select Pass N minutes (N = 5,10,...), the data retrieval period on the Widget will be fixed (unchanged) at 5, 10,... minutes before.

Select **Create** to make a Widget. If you need to change the widget name, you can edit it in \*\*Widget name
