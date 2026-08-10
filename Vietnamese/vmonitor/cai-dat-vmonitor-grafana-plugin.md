# Cài đặt và sử dụng vMonitor Datasource Plugin cho Grafana

> Hướng dẫn này giúp bạn cài đặt vMonitor Datasource Plugin lên máy chủ Grafana self-hosted, thêm data source kết nối tới vMonitor, rồi query metric/log, dựng dashboard và thiết lập alerting.

---

## Điều kiện cần (Prerequisites)

- Máy chủ Grafana phiên bản **12.3.0** trở lên.
- Quyền `sudo` trên máy chủ Grafana.
- Một cặp **Service Account** key GreenNode IAM (`Client ID` + `Client Secret`) có quyền đọc vMonitor (tạo ở bước đầu tiên bên dưới).

---

## Tạo Service Account key pair

Plugin xác thực với vMonitor bằng cặp key của Service Account, không dùng username/password.

**Bước 1: Tạo Service Account**

1. Mở GreenNode IAM console.
2. Vào **Service Accounts** → **Create service account**.
3. Đặt tên và tạo Service Account.

**Bước 2: Gắn policy**

1. Gắn policy **vMonitorMetricReadOnlyAccess** cho Service Account (bắt buộc để query metric).
2. Nếu cần query log, gắn thêm policy **vMonitorLogReadOnlyAccess**.

**Bước 3: Tạo cặp key**

1. Trong Service Account vừa tạo, chọn tạo key pair.
2. Ghi lại **Access Key ID** — đây là `Client ID`.
3. Ghi lại **Secret Access Key** — đây là `Client Secret`.

{% hint style="warning" %}
Secret Access Key chỉ hiển thị **một lần**. Nếu mất, bạn phải tạo key pair mới.
{% endhint %}

---

## Cài đặt plugin trên máy chủ Grafana

Plugin là backend plugin chưa ký (unsigned build), nên Grafana cần được cho phép tải unsigned plugin.

**Bước 1: Tải plugin**

1. Tải file ZIP mới nhất (v1.0.0) từ trang **[Releases](https://github.com/GreenNodeHub/vmonitor-grafana-plugin/releases)** của repo `GreenNodeHub/vmonitor-grafana-plugin`.

**Bước 2: Giải nén**

1. Tạo thư mục plugin nếu chưa có (mặc định `/var/lib/grafana/plugins`).
2. Giải nén archive vào thư mục con tên `greennode-vmonitor-datasource`.

{% hint style="info" %}
Tìm đường dẫn plugin bằng cách xem khoá `plugins` dưới `[paths]` trong `/etc/grafana/grafana.ini`. Khi nâng cấp, xoá thư mục plugin cũ trước khi giải nén bản mới.
{% endhint %}

**Bước 3: Phân quyền**

1. Grafana chạy với user `grafana`. Cấp ownership cho toàn bộ thư mục plugin:

```bash
sudo chown -R grafana:grafana /var/lib/grafana/plugins
```

**Bước 4: Cho phép unsigned plugin**

1. Mở `/etc/grafana/grafana.ini`.
2. Thêm ID plugin vào section `[plugins]`:

```ini
[plugins]
allow_loading_unsigned_plugins = greennode-vmonitor-datasource
```

ID plugin nằm trong `plugin.json` của thư mục plugin. Nhiều unsigned plugin phân tách bằng dấu phẩy.

**Bước 5: Khởi động lại và kiểm tra**

1. Khởi động lại Grafana server.
2. Kiểm tra log: thành công sẽ có dòng "Plugin registered". Hai cảnh báo về unsigned plugin là bình thường.
3. Vào **Administration → Plugins and data → Plugins**, plugin **GreenNode vMonitor** xuất hiện trong danh sách.

{% hint style="warning" %}
Khởi động lại Grafana sẽ gián đoạn phiên làm việc hiện tại. Thực hiện ngoài giờ cao điểm nếu cần.
{% endhint %}

---

## Thêm data source và import dashboard

**Bước 1: Thêm data source**

1. Vào **Administration → Plugins and data → Plugins**.
2. Tìm "GreenNode vMonitor" và thêm data source mới.

**Bước 2: Điền thông tin**

| Trường | Bắt buộc | Mô tả |
|---|---|---|
| API URL | Không | vMonitor API base URL; để trống dùng mặc định |
| Client ID | Có | Access Key ID của Service Account key |
| Client Secret | Có | Secret Access Key; lưu mã hoá, chỉ backend đọc |
| Token URL | Không | IAM token-exchange endpoint; để trống dùng mặc định |

**Bước 3: Lưu và kiểm tra**

1. Nhấn **Save & test**.
2. Backend đổi cặp key lấy **Bearer token** và cache đến khi hết hạn.

{% hint style="info" %}
Client Secret không bao giờ gửi lên browser; chỉ backend giữ và dùng để đổi token.
{% endhint %}

**Bước 4: Import dashboard**

1. Vào **Connections → Data sources**, mở data source vừa tạo.
2. Chuyển sang tab **Dashboards** và import từng dashboard mong muốn.

---

## Truy vấn Metric

**Bước 1: Chọn mode**

1. Chọn data source GreenNode vMonitor.
2. Chọn **Metric** mode.

**Bước 2: Cấu hình query**

| Trường | Mô tả |
|---|---|
| Metric | Tên metric, ví dụ `net.if.in.bytes_sec` |
| Statistic | Hàm tổng hợp: `avg`, `min`, `max`, `sum`, `count`, `rate_1s`, `rate_1m`, `rate_5m` |
| Filter by | Dimension filter, kết hợp bằng AND |
| Group by | Tách thành nhiều series theo giá trị dimension |
| Alias | Tên hiển thị, dùng cú pháp `{{dimension}}` |

**Bước 3: Thêm function (nếu cần)**

Nhấn **Add Function** để thêm:

| Function | Mô tả | Giới hạn |
|---|---|---|
| Rollup | Tổng hợp trên cửa sổ thời gian cố định (avg/min/max/sum/count) | Không dùng với `rate_*` |
| Rate | Chuyển counter tích lũy thành rate (per_second/per_minute/per_hour) | Không dùng với `rate_*` |
| Timeshift | Chồng cùng metric từ khoảng thời gian trước đó | Không dùng với `rate_*` |
| Rank | Giữ top N (topk) hoặc bottom N (bottomk) series tại mỗi điểm | Series bị loại có gap |
| Reduce | Rút gọn series về 1 giá trị (last/avg/min/max/sum) cho Stat/Top List panel | — |

{% hint style="info" %}
Các statistic `rate_1s`, `rate_1m`, `rate_5m` không hỗ trợ function Rollup, Rate, Timeshift. Trong alert rule dùng Rank, hãy thêm **Resample** trước **Reduce** để xử lý gap.
{% endhint %}

**Bước 4: Ví dụ**

- **Top 5 vServer theo CPU:** Metric `cpu.usage_user`, statistic `avg`, filter `product = vserver`, group by `resource_id`, Rank topk 5, alias `{{resource_id}}`.
- **Network throughput so với tuần trước:** Query A với metric và statistic `avg`; Query B cùng metric kèm Timeshift 1 tuần.

---

## Truy vấn Log

**Bước 1: Chọn Log project**

1. Chọn data source, chuyển sang **Logs** mode.
2. Chọn **Log project** (chỉ liệt kê project ở trạng thái ACTIVE).

**Bước 2: Chọn định dạng xuất**

| Định dạng | Dùng cho | Hiển thị |
|---|---|---|
| logs | Explore, Logs panel | Dòng log kèm histogram số lượng, mỗi dòng mở rộng được |
| table | Table panel | 1 dòng mỗi entry, 1 cột mỗi field |
| timeseries | Graph panel, Alerting | Số lượng log theo thời gian |

Trong Alert mode, định dạng tự đặt thành `timeseries`.

**Bước 3: Lọc log**

| Operator | Input | Ý nghĩa |
|---|---|---|
| is | 1 giá trị | Khớp chính xác |
| is not | 1 giá trị | Không khớp |
| is one of | Nhiều giá trị | Khớp bất kỳ |
| is not one of | Nhiều giá trị | Không khớp giá trị nào |
| is between | from, to | Trong khoảng [from, to) |
| is not between | from, to | Ngoài khoảng |
| exists | — | Field có mặt |
| does not exist | — | Field vắng mặt |

Grafana variable được hỗ trợ trong giá trị filter, ví dụ `$selected_host`.

**Bước 4: Group by (chỉ timeseries)**

1. Chọn field keyword aggregatable để tách số lượng log thành nhiều series.
2. Mỗi tổ hợp giá trị duy nhất thành 1 series; tối đa 20 giá trị cho mỗi field.

---

## Thiết lập Alert và Notification

Alerting và notification do **Grafana** xử lý: bạn dựng Grafana alert rule trên các query metric/log của vMonitor, rồi Grafana gửi cảnh báo qua notification policy và contact point của chính Grafana (email, Slack, Webhook...). Plugin không dùng Alarm hay Notification của vMonitor.

**Alert trên metric:** Dựng metric query, rồi trong alert rule thêm **Reduce** + **Threshold**. Nếu dùng Rank, thêm **Resample** trước **Reduce** để xử lý gap.

**Alert trên số lượng log:** Dùng log query định dạng `timeseries`, thêm filter, rồi gắn **Reduce** + **Threshold** để kích hoạt khi số lượng log vượt ngưỡng.

{% hint style="info" %}
Trong thời gian yên tĩnh, số lượng log báo về `0` thay vì thiếu dữ liệu, nên rule cũng có thể kích hoạt khi log ngừng xuất hiện.
{% endhint %}

**Group by trong alert log:** Mỗi giá trị group tạo một alert instance Grafana riêng. Group không có log trong kỳ đánh giá sẽ không sinh instance.

---

## Template variables

| Function | Trả về |
|---|---|
| `metrics()` | Tất cả tên metric |
| `dimensions(metricName)` | Các dimension key của metric |
| `dimensionValues(metricName, key)` | Giá trị của dimension key |
| `infrastructure(product[, region])` | Resource của một loại product |
| `regions(product)` | Các region khả dụng cho product nhận region |

Product hỗ trợ bởi `infrastructure()`: `host`, `vserver`, `vlb`, `vstorage`, `vstorage-bucket`, `vdb`, `vdb-kafka`, `vdb-cluster`, `vbackup`.

---

## Khắc phục sự cố

| Triệu chứng | Nguyên nhân & khắc phục |
|---|---|
| Plugin không có trong danh sách Plugins | Build chưa ký; kiểm tra bước cho phép unsigned, xem log lỗi chữ ký |
| Thư mục plugin bị bỏ qua | Lỗi ownership; chạy lại `chown` ở bước phân quyền |
| Plugin unavailable khi query | Backend binary không khởi động; đảm bảo `plugin.json` nằm trực tiếp trong thư mục plugin, không lồng |
| Lỗi version | Plugin yêu cầu Grafana **12.3.0+** |
| 401 Unauthorized khi **Save & test** | Sai Client ID hoặc Client Secret |
| Connection refused khi **Save & test** | Sai API URL hoặc vấn đề mạng |
| Query không trả data | Kiểm tra time range, dimension filter và quyền đọc IAM |
| Dropdown Log project rỗng | IAM key thiếu quyền đọc log, hoặc project không ở trạng thái ACTIVE |

---

## Kết quả

Sau khi hoàn tất, bạn có một data source GreenNode vMonitor trong Grafana, có thể query metric/log, dùng các dashboard dựng sẵn và thiết lập alerting từ dữ liệu vMonitor.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Xem các bản cập nhật vMonitor | [Announcements and Updates](../overview/product-updates-all/) |
| Tìm hiểu về vMonitor Platform | [vMonitor Platform](README.md) |
