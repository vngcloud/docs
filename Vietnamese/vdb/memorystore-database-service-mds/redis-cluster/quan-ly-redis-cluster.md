# Quản lý Redis Cluster

Sau khi tạo Redis Cluster, bạn có thể quản lý topology, thay đổi số replica, thực hiện backup thủ công và xóa cluster trực tiếp từ trang chi tiết.

---

## Điều kiện tiên quyết

* Đã có ít nhất 1 Redis Cluster ở trạng thái Available.
* Quyền quản lý database trên tài khoản vDB.

---

## Lọc danh sách Database

Trang danh sách Database hỗ trợ lọc nhanh theo loại deployment bằng các tab ở đầu trang:

| Tab           | Hiển thị                                  |
| ------------- | ------------------------------------------- |
| All Databases | Tất cả database (Single-node và Cluster) |
| Single-node   | Chỉ Single-node database                   |
| Cluster       | Chỉ Cluster database                       |

Số lượng database hiển thị dạng badge bên cạnh mỗi tên tab. Quick filter kết hợp với tính năng tìm kiếm: khi đang ở tab Cluster, kết quả tìm kiếm chỉ trả về Cluster databases.

---

## Xem Topology

Tab Topology trong trang chi tiết cluster hiển thị toàn bộ cấu trúc master–replica của cluster.

![](../../../.gitbook/assets/Redis-cluster/redis-cluster-detail.png)

Để xem Topology:

1. Truy cập trang chi tiết Redis Cluster.
2. Chọn tab Topology.

Tab này hiển thị:

* Master node: Icon database màu xanh lá với nhãn "Master".
* Replica nodes: Các icon bên dưới, hiển thị tối đa 2, phần còn lại được gộp thành "+N".
* Summary: Số lượng Master, Replica và tổng số nodes.

---

## Thay đổi số Replica (Edit Nodes)

Bạn có thể scale up hoặc scale down số Replica của cluster sau khi tạo mà không gây downtime.

![](../../../.gitbook/assets/Redis-cluster/redis-edit-node.png)

Để thay đổi số Replica:

1. Tại trang chi tiết cluster, chọn tab Topology.
2. Chọn Edit nodes.
3. Trong dialog Edit Cluster, chọn Number of nodes mới — UI chỉ hiển thị 2 lựa chọn: current−1 hoặc current+1.
4. Kiểm tra phần Cost Summary bên phải để xem chi phí thay đổi:
   * CURRENT CONFIGURATION: Cấu hình và giá hiện tại.
   * NEW CONFIGURATION: Cấu hình và giá mới.
   * Total: Chênh lệch chi phí (xanh = tăng, đỏ = giảm).
5. Chọn SAVE để áp dụng.

{% hint style="info" %} Mỗi lần edit chỉ được thay đổi ±1 node. Để đạt số node mong muốn, lưu và lặp lại thao tác. Cơ chế này đảm bảo sync hoàn tất trước mỗi bước, tránh lỗi replication. {% endhint %}

---

## Backup thủ công (Back up now)

Nút Back up now nằm trực tiếp trên header trang chi tiết cluster, cho phép tạo Full Snapshot ngay lập tức mà không cần vào submenu.

Để tạo Manual Backup:

1. Tại header trang chi tiết cluster, chọn Back up now.
2. Xác nhận trong dialog
3. Chọn Back up now.

Hệ thống sẽ hiển thị thông báo và backup mới xuất hiện trong tab Backup .

![](../../../.gitbook/assets/Redis-cluster/redis-backup-now.png)

{% hint style="warning" %}

* Nút Back up now bị vô hiệu hóa khi đang có backup job đang chạy (Auto hoặc Manual). Tooltip sẽ hiển thị: "A backup job is currently in progress".
* Khi tài khoản hết quota, hệ thống trả lỗi `<span attribution="{"id":"huyenttn3@vng.com.vn","name":"Huyền. Trần Thị Ngọc (3)","timestamp":1778229000000,"email":"huyenttn3@vng.com.vn","oid":"15e1faed-f48a-4412-b344-1ef30f492985","dataSource":0}">QuotaExceeded</span>` và không tự động retry.
* Chỉ hỗ trợ Full Snapshot — không hỗ trợ Incremental backup thủ công. {% endhint %}

---

## Xem thông tin Backup

Tab Backup trong trang chi tiết cluster cho phép bạn theo dõi trạng thái backup và lịch sử backup.

Để xem thông tin Backup:

1. Tại trang chi tiết cluster, chọn tab Backup.

![](../../../.gitbook/assets/Redis-cluster/redis-detail-tab-backup.png)

Tab này hiển thị:

* Backup Information: Description, Created Date, Latest Record, Backup Size, Backup Policy, Backup Location.
* Backup List: Danh sách các bản backup với các cột: Backup DB Point ID, Backup Size (GB), Backup Type, Schedule Type, Backup Location, Backup Point, Status, Action.

Chọn View full backup details → để mở trang chi tiết backup của cluster này trong Backup Center (mở tab mới).

---

## Quản lý Backup tại Backup Center

Trang Backup của vDB (menu: Memory Store > Backup) hiển thị tổng quan danh sách backup. Để thực hiện các thao tác đầy đủ (Restore, Delete, quản lý Policy), bạn cần vào Backup Center.

| Trạng thái      | Hành động                                                      |
| ----------------- | ----------------------------------------------------------------- |
| Chưa có backup  | ChọnCreate a Backupđể chuyển đến Backup Center tạo mới.   |
| Đã có backup   | ChọnGo to vBackupđể mở Backup Center (filter theo Vault vDB). |
| Click tên backup | Mở trang chi tiết backup trong Backup Center (tab mới).        |

---

## Cấu hình tham số (Configuration Group)

Redis Cluster áp dụng cấu hình tham số qua **DB Configuration Group**: bạn tạo group, gắn vào cluster và chỉnh sửa tham số ngay trên portal thay vì sửa file cấu hình thủ công. Cách tạo, chỉnh sửa và gắn group cho MDS Instance được mô tả chi tiết ở trang [Quản lý cấu hình MDS Instance (Configuration Group)](../quan-ly-cau-hinh-mds-instance.md).

### Xem và tạo Configuration Group

1. Mở trang **Configuration group** trên vpB portal.
2. Tìm group theo tên hoặc ID, hoặc tạo group mới bằng **Create a Configuration group**.

![Danh sách Configuration group](../../../.gitbook/assets/vdb-redis-cluster-config-group-list.png)

Khi tạo group cho Redis Cluster: đặt **Configuration name** và mô tả, chọn **Engine** là Redis, **Deployment type** là Cluster, rồi chọn **Engine version** phù hợp với cluster.

![Dialog Create Configuration group](../../../.gitbook/assets/vdb-redis-cluster-config-group-create.png)

### Gắn group vào Redis Cluster

1. Mở trang chi tiết Redis Cluster và chọn **Edit Configuration Group** trên header. Hành động này cũng có trong Action Menu (⋮) của cluster ở danh sách Database.
2. Trong dialog, mở dropdown **DB configuration group** và chọn group muốn gắn. Danh sách chỉ liệt kê các group cùng engine với cluster; nhấn biểu tượng làm mới nếu group mới tạo chưa xuất hiện.
3. Chọn **Save** để cập nhật group cho cluster.

![Dialog Edit Configuration Group](../../../.gitbook/assets/vdb-redis-cluster-config-group-edit-configuration-group.png)

### Sửa tham số

Mở Configuration Group đang gắn với cluster — trang chi tiết hiển thị bảng tham số với **Name**, **Values**, **Allowed values** và **Data type**.

![Trang chi tiết Configuration group với bảng tham số](../../../.gitbook/assets/vdb-redis-cluster-config-group-detail.png)

Chọn **Edit parameters** để chuyển sang chế độ chỉnh sửa, thay đổi các tham số trong khoảng **Allowed values** cho phép, rồi chọn **Preview and Save**.

![Chế độ Edit parameters](../../../.gitbook/assets/vdb-redis-cluster-config-group-edit-parameters.png)

Trong dialog **Preview changes and apply**: đối chiếu thay đổi ở bảng **Current value** / **New value**, tick checkbox xác nhận việc sửa tham số sẽ ảnh hưởng tới các database đang gắn group, rồi chọn **Apply**.

![Dialog Preview changes and apply](../../../.gitbook/assets/vdb-redis-cluster-config-group-edit-parameters-preview.png)

{% hint style="info" %}
**Hành vi khi bỏ một parameter khỏi Configuration Group**: Với Redis Cluster, khi bạn bỏ một parameter khỏi Configuration Group đang gắn với cluster, parameter đó **giữ nguyên giá trị đang có** và **không** trở về giá trị mặc định của Database Engine. Điều này khác với Redis Single node, nơi parameter bị bỏ sẽ trở về giá trị mặc định của Database Engine.

Mỗi lần chỉnh sửa, bạn có thể thay đổi một hoặc nhiều parameter. Các parameter không được thay đổi trên portal sẽ giữ nguyên giá trị đang có.
{% endhint %}

---

## Xóa Redis Cluster

{% hint style="warning" %} Thao tác xóa cluster không thể hoàn tác. Toàn bộ dữ liệu sẽ bị xóa vĩnh viễn. {% endhint %}

Để xóa cluster:

1. Tại trang chi tiết cluster, chọn biểu tượng More Actions (⋮).
2. Chọn Delete.
3. Trong dialog xác nhận:
   * (Tùy chọn) Chọn Create final backup? để tạo snapshot cuối trước khi xóa (chỉ khả dụng nếu cluster còn Backup Database trong vBackup).
   * Chọn I acknowledge... để xác nhận mất quyền truy cập vào các bản backup.
   * Nhập chữ delete vào ô xác nhận.
4. Chọn Delete (màu đỏ) để hoàn tất.

{% hint style="info" %} Nếu Backup Database của cluster đã bị xóa khỏi vBackup, checkbox Create final backup? sẽ bị vô hiệu hóa và hệ thống hiển thị ghi chú: "No backup database found. Final backup is unavailable." {% endhint %}

---

## Action Menu

Từ trang danh sách Database, chọn biểu tượng Action (⋮) bên cạnh một Redis Cluster để thực hiện nhanh:

| Action                   | Mô tả                                                     |
| ------------------------ | ----------------------------------------------------------- |
| Edit configuration group | Chỉnh sửa Redis configuration parameters.                 |
| Edit DB settings         | Chỉnh sửa tên, backup policy và các database settings. |
| Delete                   | Xóa cluster (có dialog xác nhận).                       |

---

## Tiếp theo

* [Xem giới hạn và hạn chế khi dùng Redis Cluster](https://loop.cloud.microsoft/p/gioi-han-redis-cluster.md)
* [Tìm hiểu kiến trúc và so sánh với Single-node](https://loop.cloud.microsoft/p/redis-cluster.md)
