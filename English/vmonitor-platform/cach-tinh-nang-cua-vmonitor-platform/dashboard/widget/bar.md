# Bar

### Overview

**Bar chart** is a type of chart used to compare values of different groups or categories. In the vMonitor Platform, a bar chart consists of multiple vertical bars, each representing a value of a group or data point.

<figure><img src="../../../../.gitbook/assets/image (58) (1).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (59) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For a bar chart, select **Bar** for the Style.

<figure><img src="../../../../.gitbook/assets/image (60) (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Graph your data

Select data type to draw Widget:

* **Metrics: No Support.**
* Logs: view Log Query to configure for the type of Logs data.

Alias: You can set an Alias for each query; this alias will be displayed on the graph and legend. This is very useful for long metric names, logs, or queries with extensive filters.

#### 3. Fixed time range

A fixed time range is an attribute of a Widget that you can set to filter data within the Widget based on a specific time range, independent of the Dashboard's time range. Each Widget can have its own Fixed time range settings, and you can select from the time ranges described in the table below. For example, if you select Global time, the data period displayed on the Widget will match the period selected on the Dashboard. Thus, changing the Dashboard's data period will also alter the Widget's data period accordingly. This option is recommended. If you choose Pass N minutes (N = 5, 10,...), the data period on the Widget remains fixed (unchanged) at 5, 10,...minutes prior.

#### 4. Configure graph

For each type of chart: Line, Bar, Stacked Area, Pie, you need to select the corresponding chart attributes. The attributes are described in the table below:

| **Parameter**     | **Options**                      |
| ----------------- | -------------------------------- |
| Graph legend      | Hidden, Top, Bottom, Left, Right |
| Connect nulls     | Enable, Disable                  |
| Y-axis lable      | Custom value                     |
| Y-axis scale type | Linear, Logarithmic              |
| Y-axis Max value  | Custom value                     |
| Y-axis Max value  | Custom value                     |

Select **Create** to create a Widget. If you need to change the widget name, you can edit it in Widget name.
