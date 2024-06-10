# Pie

### Overview

**Pie chart** is a type of circular chart used to compare values (usually in percentage form) with the overall level. Each section in the chart represents data for a specific item and is distinguished by different colors or symbols. Pie charts are commonly used when there are few components, and you want to focus on the differences between them.

<figure><img src="../../../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For a pie chart, select **Pie** as the Style.

<figure><img src="../../../../.gitbook/assets/image (66).png" alt="" width="563"><figcaption></figcaption></figure>

#### 2. Graph your data

Select data type to render Widget:

* **Metrics: No Support.**
* Logs: view Log Query to configure for the type of Logs data.

Alias: You can set an alias for each query. This alias will be displayed on the graph and legend, which is very useful for metric names, logs, or queries with long filters.

#### 3. Fixed time range

Fixed time range is an attribute of a Widget that you can set to filter data on the Widget according to a fixed time frame, independent of the Dashboard's time range. Each Widget can have its own Fixed time range, chosen from the options described in the table below. For example, if you select Global time, the data displayed on the Widget will match the time range selected on the Dashboard. This means that changing the data time range on the Dashboard will also change the data time range of the Widget. This option is recommended. If you choose Past N minutes (N = 5,10,...), the data time range on the Widget will be fixed at 5, 10,... minutes prior and will not change.

#### 4. Configure graph

In each type of chart—Line, Bar, Stacked Area, Pie—you need to select the corresponding chart attributes. The attributes are described in the table below:

| **Parameter** | **Options**                      |
| ------------- | -------------------------------- |
| Graph legend  | Hidden, Top, Bottom, Left, Right |
| Data Lable    | Enable/ Disable                  |

Select **Create** to create a widget. If you need to change the widget name, you can do so in **Widget name**.
