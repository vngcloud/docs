# Line

### Overview

**Line chart** is a type of chart used to display data changes over time. A line chart is created by plotting a series of points and connecting them with straight lines.

<figure><img src="../../../../.gitbook/assets/image (55) (3).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (56) (3).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For a line chart, select **Line** as the Style in this section.

<figure><img src="../../../../.gitbook/assets/image (57) (3).png" alt=""><figcaption></figcaption></figure>

To change the line's weight and transparency, you can adjust using the following options:

| **Parameter** | **Options**         |
| ------------- | ------------------- |
| Style         | Solid, Dot, Dash    |
| Stroke        | Normal, Thin, Thick |

#### 2. Graph your data

Choose data type to draw Widget:

* Metrics: See Metric Query to configure for the Metrics data type.
* Logs: refer to Log Query to configure for Logs data.

Alias: You can set an alias for each query. This alias will be displayed on the graph and legend, which is very useful for metric names, logs, or lengthy queries with filters.

#### 3. Fixed time range

Fixed time range is a property of a Widget that you can set to filter data on the Widget according to a fixed time range, independent of the Dashboard's time range. Each Widget can have its own Fixed time range setting, and you can select from the time ranges described in the table below. For example, if you choose Global time, the time range for data displayed on the Widget will match the time range you select on the Dashboard. This means that changing the time range on the Dashboard will also change the time range for data on the Widget. It is recommended to use this option. If you choose Pass N minutes (N = 5,10,...), the data time range on the Widget will be fixed (unchanging) to always be the previous 5, 10,... minutes.

#### 4. Configure graph

For each chart type - Line, Bar, Stacked Area, and Pie - you need to select the corresponding chart attributes. The attributes are described in the table below:

| **Parameter**     | **Options**                      |
| ----------------- | -------------------------------- |
| Graph legend      | Hidden, Top, Bottom, Left, Right |
| Connect nulls     | Enable, Disable                  |
| Y-axis lable      | Custom value                     |
| Y-axis scale type | Linear, Logarithmic              |
| Y-axis Max value  | Custom value                     |
| Y-axis Max value  | Custom value                     |

Select **Create** to generate a Widget. If you need to change the widget name, you can edit it under Widget name.
