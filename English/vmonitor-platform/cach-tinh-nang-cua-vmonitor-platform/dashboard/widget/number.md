# Number

### Overview

**Number chart** with a summary index is a type of chart that displays numbers calculated from a dataset, rather than showing the original numbers.

<figure><img src="../../../../.gitbook/assets/image (67) (2).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (68) (2).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For a number chart, at this section, select Style as **Number.**

<figure><img src="../../../../.gitbook/assets/image (69) (2).png" alt="" width="563"><figcaption></figcaption></figure>

#### 2. Graph your data

Select data type to draw Widget:

* Metrics: View Metric query to configure the type of Metrics data.
* Logs: see Log Query for configuration of the Logs data type.

Alias: You can set an Alias for each query. This alias will be displayed on the graph and legend, which is very useful for metrics names, logs, or queries with long filters.

#### 3. Fixed time range

A fixed time range is an attribute of a Widget that allows you to filter data within the Widget for a set period, independent of the Dashboard's time range. Each Widget can have its own Fixed time range configuration, from the options described in the table below. For example, if you select Global time, the data displayed on the Widget will match the time range chosen on the Dashboard. This means that altering the data time range on the Dashboard will update the Widget's data time range accordingly. This option is recommended. If you select Pass N minutes (N = 5,10,...), the data displayed on the Widget will be fixed to the last 5, 10, etc., minutes, regardless of changes in the Dashboard.

Select **Create** to create a Widget. If you need to change the widget name, you can edit it at Widget name
