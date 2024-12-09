# Table

### Overview

Summary statistic table charts are a type of chart that displays calculated figures from a data set, instead of showing the original numbers. Typically, this kind of chart should be used when you want to group data over time using the Group by feature.

<figure><img src="../../../../.gitbook/assets/image (70) (1).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (71) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For table charts, at this section, choose Style as **Table**.

<figure><img src="../../../../.gitbook/assets/image (72) (1).png" alt="" width="563"><figcaption></figcaption></figure>

#### 2. Graph your data

Select data type to render Widget:

* **Metrics: No Support.**
* Logs: see Log Query to configure for the type of Logs data.

Alias: You can set an Alias for each query; this alias will be displayed on the graph and legend. This is very helpful for metric names, logs, or queries with long filters.

#### 3. Fixed time range

Fixed time range is an attribute of a Widget that you can configure to filter data on the Widget according to a fixed time range, independent of the Dashboard's time range. Each Widget can have its own Fixed time range setting, and you can choose from the time ranges described in the table below. For instance, if you select Global time, the data retrieval period displayed on the Widget will match the time range you selected on the Dashboard. This means that changing the data retrieval time on the Dashboard will also change the Widget's data retrieval time. It is recommended to use this option. If you choose Pass N minutes (N = 5,10,...), the data retrieval period on the Widget will be fixed (unchanged) and will always be 5, 10,... minutes ago.

Select **Create** to generate a Widget. If you need to change the widget's name, you can edit it in Widget name.
