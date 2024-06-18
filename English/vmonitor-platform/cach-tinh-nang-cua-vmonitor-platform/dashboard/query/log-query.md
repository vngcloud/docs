# Log query

When creating a **Widget** for **logs** data, in the **Graph your data** section, create your data query by selecting **Add a query**. Each query will be represented by a line, bar, stacked area, pie, number, table, or a log search interface on the chart. The components that make up a query for log data include:

<figure><img src="../../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

Including:

### 1. Hide/ Unhide query

Query result indicator is toggled on/off on the chart. To hide or show the query results, simply click on this icon. When the icon is green (like 'a' in the image), the query results are displayed on the chart. When the icon is gray, the query results are not shown on the chart.

### 2. Color

**Color**: choose a color for the chart drawn from the query results.

### 3. Loại query

**Query Type**: data type selection box. To plot a chart for **logs**, you need to select **Log** here.

### 4. Log project

**Log project**: Select a **log project** by searching and choosing from the list of log projects. You can view this list in the **Log/Log project** section. For detailed information, refer to Working with Log Project.

### 5. Search log

**Search log**: This is where you can perform data log searches based on your desired conditions. For more details on how to search logs, please refer to Log search.

### 6. Alias

**Alias**: A memorable, easy-to-understand name for the widget. Our system will automatically create an Alias for your chart, but if you want to create your own Alias, please edit this field.

### 7. Statistics

**Statistics**: methods for summarizing data. There are 7 aggregation methods you can use to combine your log data within each time group: count, count unique, sum, avg, min, max, percentiles, described in the table below:

<table data-header-hidden><thead><tr><th width="210"></th><th></th></tr></thead><tbody><tr><td><strong>Operations</strong></td><td><strong>Meaning</strong></td></tr><tr><td>count</td><td>Count the number of generated log records.</td></tr><tr><td>count unique</td><td>Count the number of unique log records generated based on the selected field.</td></tr><tr><td>sum</td><td>Sum of numerical values from a selected field in the generated logs.</td></tr><tr><td>min</td><td>Find the minimum value in the numerical fields of a selected field from the generated logs.</td></tr><tr><td>max</td><td>The highest value among the numerical values of a selected field generated in the logs.</td></tr><tr><td>percentiles</td><td>Calculate the percentile for a numerical value of a selected field from the generated logs.</td></tr></tbody></table>

### 8. Statistics field

**Field**: select the information field on which you want to perform the operation. For the **Count** operation, you don't need to select any field. For other operations, you must select a field with a **Number** data type available in the log project to perform the operation on its value.

### 9. Group by

**Group by**: you can group data according to the information fields available in the log project.

### 10. Interval

**Interval**: an attribute that allows you to determine the time period for which the widget will display values (data granularity). You can select values like Second, Minute, Day, etc., from the preset values we provide, or you can directly input the desired Interval value.

You can add multiple queries to a chart, we support creating up to 10 queries for a single chart. If you have more than 2 queries in one chart, ensure each query is assigned a distinct color and the data intervals between queries are not too disparate. This will help make your chart more vibrant.
