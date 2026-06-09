# User Tags

### 1. Tổng Quan

**User Tags** cho phép gắn một tập nhãn dạng key/value lên toàn bộ tài nguyên bao gồm server và volume thuộc một **Node Group**. **User Tags** sẽ được tự động tạo trên:

* Toàn bộ **Server** của **Node Group**.
* Toàn bộ **Block Volume** do **VKS** quản lý gắn vào các **Server** đó — gồm root disk, data disk và volume **CSI** cấp động qua **PVC**.

Bạn có thể dùng **User Tags** để:

* **Phân bổ chi phí (cost allocation)** — gắn tag theo phòng ban / dự án / môi trường để bóc tách hoá đơn.
* **Quản trị & tra cứu** — lọc tài nguyên trên **vServer** console theo tags.
* **Tự động hoá** — công cụ nội bộ của bạn dựa vào tags để phân loại tài nguyên.

#### Cách hoạt động

* **User Tags** được duy trì liên tục — nếu ai sửa/xoá **User Tags** do **VKS** quản lý trên **vServer** console, hệ thống **VKS** tự khôi phục lại các **User Tags** này.
* **Volume gắn sau** (**PVC** tạo qua **CSI**) cũng sẽ được hệ thống **VKS** gắn tags tự động.
* **User Tags** sẽ được hệ thống **VKS** tự động cập nhật tối đa 15 phút sau khi **Server**/**Volume** được tạo.

{% hint style="info" %}
**Lưu ý cho account IAM-user:**

IAM ser cần được cấp đầy đủ các quyền dưới đây (admin nên cấp một lần trước khi sử dụng):
{% endhint %}

| Quyền                      | Mục đích                                           | Dùng tại bước                |
| -------------------------- | -------------------------------------------------- | ---------------------------- |
| `UpdateNodegGroupMetadata` | Cập nhật metadata (Label/Taint/Tag) cho Node Group | Cập nhật metadata Node Group |

### 2. Hướng dẫn cấu hình

#### Tạo User Tags

**User Tags** cho **Node Group** được cấu hình khi tạo **Cluster/Node Group**, tại section Default Node Group Configuration → Node Group Metadata Setting (Optional).

**Bước 1**:&#x20;

1. Truy cập [VKS Console](https://vks.console.vngcloud.vn/overview).
2. Nhấn Create a Kubernetes **Cluster**/**Node Group**.

**Bước 2**: Điền tag tại **Node Group** Metadata Setting

1. Mở mục Node Group Metadata Setting (Optional).
2. Nhấn Add Tag để thêm mới.
3. Điền Key và Value cho mỗi tag.
4. Lặp lại để thêm nhiều tag.

#### Cập nhật User Tags

**Bước 1**: Mở **Cluster** Detail

1. Truy cập [VKS Console](https://vks.console.vngcloud.vn/overview).
2. Chọn **Cluster** chứa **Node Group** cần chỉnh sửa tag.

**Bước 2**: Chọn action **Edit Metadata**

1. Chọn tab **Node Group**.
2. Tại **Node Group** cần chỉnh sửa, nhấn vào menu **Action**.
3. Chọn **Edit Metadata**.

**Bước 3**: Thêm, sửa hoặc xóa **User Tags**

**Bước 4**: Lưu thay đổi

1. Kiểm tra lại danh sách **User Tags**.
2. Nhấn **Save** để áp dụng.

### 3. Tag hệ thống (VKS Managed)

Ngoài **User Tags** của bạn, hệ thống **VKS** luôn tự gắn 3 tag sau lên mọi tài nguyên của node group:

| Key                   | Ý nghĩa                   |
| --------------------- | ------------------------- |
| `vng.vks.cluster.id`  | Định danh cluster         |
| `vng.vpc.id`          | Mạng (VPC) của tài nguyên |
| `vng.billing.product` | `vks` (phục vụ tính cước) |

* Bạn **không cần** và **không thể** tự cấu hình các tag này.
* Nếu các tag này bị xoá thủ công trên console, hệ thống **VKS** sẽ tự gắn lại.

#### Prefix dành riêng (không được dùng)

Để tránh ghi đè marker hệ thống, bạn **không được** đặt key bắt đầu bằng các prefix sau:

```
vng.vks.    vng.vpc.    vng.billing.    vks-    vks-mgmt-
```

Tag dùng các prefix này sẽ **bị bỏ qua** (không được áp dụng).

### 4. Các hành vi cần biết

**4.1 Giữ nguyên tag bạn tự gắn**

Nếu bạn tự gắn tag trực tiếp trên **vServer** console — thì những tag đó được giữ nguyên, hệ thống **VKS** không xoá. Hệ thống **VKS** chỉ quản lý đúng những tag bạn khai báo qua **VKS** portal.

**4.2 Tự khôi phục khi bị sửa**

* Nếu ai đó đổi value của một tag (do **VKS** quản lý) trên **vServer** console → hệ thống sẽ khôi phục về giá trị bạn đã cấu hình.
* Nếu một tag hệ thống bị xoá trên **vServer** console → hệ thống **VKS** sẽ tự động gắn lại.

**4.3 Chỉ tag volume do VKS quản lý**

Hệ thống chỉ gắn tag lên volume do **VKS** quản lý (root disk, data disk, volume **CSI**). Nếu bạn tự gắn một volume khác vào **Server** (không thuộc quản lý của **VKS**), **Volume** này sẽ không được gắn **User Tags** của Node Group.

### 5. Giới hạn số lượng User Tags (Quota)

**vServer** giới hạn số tag tối đa trên mỗi tài nguyên (`TAG_PER_RESOURCE` quota). Lưu ý:

* Mỗi tài nguyên đã có **3 tag hệ thống** chiếm chỗ trong quota.
* Nếu tổng số tag (hệ thống + của bạn) **vượt quota**, việc đồng bộ tag cho tài nguyên đó sẽ **thất bại**.

Khi điều này xảy ra, bạn sẽ thấy thông báo cảnh báo dạng:

```
Exceeded TAG_PER_RESOURCE quota on N resource(s): ...
Please reduce the number of User Tags, or request a tag quota increase on vServer
```

**Cách xử lý:** giảm bớt số tag, hoặc liên hệ để nâng quota tag trên **vServer**.

### 6. Theo dõi & thông báo

Hệ thống **VKS** hỗ trợ các sự kiện (**event**) liên quan, hiển thị qua **Cluster events** trên portal:

| Loại                    | Khi nào                                     | Ý nghĩa                                                                                                        |
| ----------------------- | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `UserTagsUpdated`       | Khi bạn đổi User Tags và đồng bộ thành công | Xác nhận tag mới đã được áp dụng — message liệt kê tag hiện tại (hoặc "Removed all User Tags" nếu bạn xoá hết) |
| `UserTagsQuotaExceeded` | Khi có tài nguyên vượt quota tag            | Cảnh báo cần giảm tag hoặc nâng quota                                                                          |

