# Metric query

When creating a **Widget** for **metric** data, in the **Graph your data** section, compose your data query by selecting **Add a query**. Each query will be represented by a line, a stacked area, or a number on the chart. The components of a query for metric data include:

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

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

<table data-header-hidden><thead><tr><th width="135"></th><th width="183"></th><th></th></tr></thead><tbody><tr><td><strong>Statistics</strong></td><td><strong>Meaning</strong></td><td><strong>Examples</strong></td></tr><tr><td>avg</td><td>Giá trị trung bình của kết quả metric sinh ra.</td><td><p>Metric A mỗi 30s lại sinh ra 1 điểm dữ liệu như bên dưới:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>Nếu độ mịn dữ liệu được tự động tính toán khi hiển thị dữ liệu là 60s cho một điểm ,thì điểm dữ liệu trả về cho metric A này theo phép toán avg là:</p><ul><li>01-01-2023 07:01:00 value = 1.5</li><li>01-01-2023 07:02:00 value = 2</li></ul></td></tr><tr><td>count</td><td>Đếm số lượng kết quả metric sinh ra.</td><td><p>Metric A mỗi 30s lại sinh ra 1 điểm dữ liệu như bên dưới:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>Nếu độ mịn dữ liệu được tự động tính toán khi hiển thị dữ liệu là 60s cho một điểm ,thì điểm dữ liệu trả về cho metric A này theo phép toán count là:</p><ul><li>01-01-2023 07:01:00 value = 2</li><li>01-01-2023 07:02:00 value = 2</li></ul></td></tr><tr><td>max</td><td>Giá trị lớn nhất của kết quả metric sinh ra.</td><td><p>Metric A mỗi 30s lại sinh ra 1 điểm dữ liệu như bên dưới:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>Nếu độ mịn dữ liệu được tự động tính toán khi hiển thị dữ liệu là 60s cho một điểm ,thì điểm dữ liệu trả về cho metric A này theo phép toán max là:</p><ul><li>01-01-2023 07:01:00 value = 2</li><li>01-01-2023 07:02:00 value = 3</li></ul></td></tr><tr><td>min</td><td>Giá trị nhỏ nhất của kết quả metric sinh ra.</td><td><p>Metric A mỗi 30s lại sinh ra 1 điểm dữ liệu như bên dưới:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>Nếu độ mịn dữ liệu được tự động tính toán khi hiển thị dữ liệu là 60s cho một điểm ,thì điểm dữ liệu trả về cho metric A này theo phép toán min là:</p><ul><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:02:00 value = 1</li></ul></td></tr><tr><td>sum</td><td>Tổng các giá trị của kết quả metric sinh ra.</td><td><p>Metric A mỗi 30s lại sinh ra 1 điểm dữ liệu như bên dưới:</p><ul><li>01-01-2023 07:00:00 value = 1</li><li>01-01-2023 07:00:30 value = 2</li><li>01-01-2023 07:01:00 value = 1</li><li>01-01-2023 07:01:30 value = 3</li></ul><p>Nếu độ mịn dữ liệu được tự động tính toán khi hiển thị dữ liệu là 60s cho một điểm ,thì điểm dữ liệu trả về cho metric A này theo phép toán sum là:</p><ul><li>01-01-2023 07:01:00 value = 3</li><li>01-01-2023 07:02:00 value = 4</li></ul></td></tr></tbody></table>

#### 7. Group by

**Group by**: bạn có thể nhóm dữ liệu theo các dimension tương ứng của metric. Ví dụ khi bạn chọn dimension host, nếu metric của bạn đang có 5 hosts khác nhau, hệ thống sẽ tự động vẽ ra 5 dòng tương ứng với 5 hosts trên Widget.

#### 8. Limit to

**Limit to**: giới hạn số series hiển thị trên biểu đồ theo nhóm Top hoặc Bottom. Ví dụ khi bạn sử dụng tính năng group by nếu Metric của bạn đang có 10 hosts khác nhau, hệ thống sẽ tự động vẽ ra 10 dòng tương ứng với 10 hosts trên widget. Nếu bạn tiếp tục sử dụng Top 5, hệ thống chỉ vẽ ra 5 dòng có điểm dữ liệu lớn nhất trong thời điểm đó.

#### 9. Alias

**Alias**: tên gợi nhớ dễ hiểu widget hơn. Nếu bạn không nhập Alias, chúng tôi tự động sinh ra tên query là **Statistic:metricname(dimension)**. Khi có thêm timeshift 5 phút thì Alias sẽ là **timeshift(statistic:metricname{dimension}, 5 minutes)**. Khi bạn có chọn group by thì Alias chỉ hiện thị dimension thôi, ví dụ bạn có một query với điều kiện group by cpu, thì Alias sẽ là cpu0, cpu1,...

Bạn có thể tham khảo cách tạo một graph với metric dựa trên video bên dưới

<figure><img src="../../../../.gitbook/assets/3%20(1).gif" alt=""><figcaption></figcaption></figure>
