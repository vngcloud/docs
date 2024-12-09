# Stack area

### Overview

**Stacked area** chart is a type of graph that shows the change in value over time through stacked regions. A stacked area chart usually comprises multiple regions, each with a different color. The height of the stack at the top line corresponds to the total value when all the stacked groups are combined.

<figure><img src="../../../../.gitbook/assets/image (61) (1).png" alt=""><figcaption></figcaption></figure>

***

### Widget Configuration

<figure><img src="../../../../.gitbook/assets/image (62) (1).png" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style

For a stacked area chart, select Style as Stacked area

<figure><img src="../../../../.gitbook/assets/image (63) (1).png" alt="" width="563"><figcaption></figcaption></figure>

#### 2. Graph your data

Choose data type to create Widget:

* Metrics: View the Metric query to configure for the Metrics data type.
* Logs: See Log Query to configure for the Logs data type.

Alias: You can assign an Alias to each query; this alias will be displayed on the graph and legend. This is very useful for long metric names, logs, or queries with extensive filters.

#### 3. Fixed time range

Fixed time range is a property of a Widget that you can set to filter data on the Widget according to a fixed time frame, independent of the time range of the Dashboard. Each Widget can have its own Fixed time range setting, and you can choose one of the time frames described in the table below. For example, if you select Global time, the data period displayed on the Widget will match the period you choose on the Dashboard. This means that when you change the data period on the Dashboard, the Widget’s data period will change accordingly. It is recommended to use this option. If you select Pass N minutes (N = 5, 10, ...), the data period on the Widget will always be fixed at the past 5, 10, ... minutes, respectively.

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

Select **Create** to create a Widget. If you need to change the widget's name, you can edit it in Widget name.
