# Metric query

When creating a **Widget** for **metric** data, in the **Graph your data** section, compose your data query by selecting **Add a query**. Each query will be represented by a line, a stacked area, or a number on the chart. The components of a query for metric data include:

<figure><img src="../../../../.gitbook/assets/image (76) (1).png" alt=""><figcaption></figcaption></figure>

In which:

#### 1. Hide/ Unhide query

The query result toggle icon on the chart can be shown/hidden. To show or hide the query result on the chart, simply click on this icon. When the icon is green (like 'a' in the image), it means the query result is displayed on the chart. When the icon is gray, the query result is not displayed on the chart.

#### 2. Color

**Color**: Choose colors for the chart based on the query results.

#### 3. Query Type

Type of query: data type selection box. To plot a chart for the metric, you need to select the Metric here.

#### 4. Metric name

**Metric**: Select a **metric** by searching and choosing it from the list of metrics. You can view this list in the **Metric Information** section. For more details, refer to Working with Metric Information.

#### 5. Filter

**Filter**: The metric you select can be filtered by **dimensions** (e.g., host, device,...) from the displayed list of **dimensions**. You can select multiple **dimensions** here. Besides selecting fixed-value dimensions for the metric, you can also use **variables** for more dynamic filtering. These **variables** are defined in the **Dashboard** where you want to create the **Widget**. To learn more about **variables**, please refer to Variable, Save Querying, and View. For example, in the image below, we select the metric win\_swap.Percent\_Usage and apply two dimension filters: host = ThuyVT2-PC and objectname = Paging\_File.

#### 6. Statistics

**Statistics**: the operation to aggregate data. The vMonitor Platform stores a large amount of data points and in most cases cannot display all of them on the chart. Therefore, we use the time-based data aggregation feature to address this issue by combining data points into time groups, called data granularity. Data granularity is automatically calculated based on the time range you select, with the auto-calculation rules shown below (or on the page). There are 5 aggregation methods you can use to combine your data in each time group: avg, count, max, min, sum as described in the table below:

<table data-header-hidden><thead><tr><th width="135"></th><th width="183"></th><th></th></tr></thead><tbody><tr><td><strong>Statistics</strong></td><td><strong>Meaning</strong></td><td><strong>Examples</strong></td></tr><tr><td>avg</td><td>Average value of the generated metric results.</td><td><p>Metric A generates 1 data point every 30s as below:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>If the data granularity is automatically calculated to be 60 seconds per data point, the data points returned for metric A using the avg operation are:</p><ul><li>01-01-2023 07:01:00 value = 1.5</li><li>01-01-2023 07:02:00 value = 2</li></ul></td></tr><tr><td>count</td><td>Count the number of generated metric results.</td><td><p>Metric A generates 1 data point every 30s as below:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>If the data granularity is automatically calculated to be 60 seconds per data point, the data points returned for metric A using the avg operation are:</p><ul><li>01-01-2023 07:01:00 value = 2</li><li>01-01-2023 07:02:00 value = 2</li></ul></td></tr><tr><td>max</td><td>The highest value of the resulting generated metric.</td><td><p>Metric A generates 1 data point every 30s as below:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>If the data granularity is automatically calculated to be 60 seconds per data point, the data points returned for metric A using the avg operation are:</p><ul><li>01-01-2023 07:01:00 value = 2</li><li>01-01-2023 07:02:00 value = 3</li></ul></td></tr><tr><td>min</td><td>The minimum value of the resulting metric.</td><td><p>Metric A generates 1 data point every 30s as below:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>If the data granularity is automatically calculated to be 60 seconds per data point, the data points returned for metric A using the avg operation are:</p><ul><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:02:00 value = 1</li></ul></td></tr><tr><td>sum</td><td>Total values of generated metric results.</td><td><p>Metric A generates 1 data point every 30s as below:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>If the data granularity is automatically calculated to be 60 seconds per data point, the data points returned for metric A using the avg operation are:</p><ul><li>01-01-2023 07:01:00 value = 3</li><li>01-01-2023 07:02:00 value = 4</li></ul></td></tr></tbody></table>

#### 7. Group by

**Group by**: You can group data according to the dimensions corresponding to the metric. For example, when you select the host dimension, if your metric has 5 different hosts, the system will automatically draw 5 lines corresponding to the 5 hosts on the Widget.

#### 8. Limit to

**Limit to**: restrict the number of series displayed on the chart by Top or Bottom groups. For example, when using the group by feature, if your Metric has 10 different hosts, the system will automatically plot 10 lines corresponding to the 10 hosts on the widget. If you then use Top 5, the system will display only the 5 lines with the largest data points at that time.

#### 9. Alias

**Alias**: an easy-to-understand widget name. If you don't input an Alias, the system will automatically generate a name as **Statistic:metricname(dimension)**. With a 5-minute timeshift, the Alias will be **timeshift(statistic:metricname{dimension}, 5 minutes)**. If you select group by, the Alias will display only the dimension, e.g., for a group by condition on cpu, the Alias will be cpu0, cpu1, etc.
