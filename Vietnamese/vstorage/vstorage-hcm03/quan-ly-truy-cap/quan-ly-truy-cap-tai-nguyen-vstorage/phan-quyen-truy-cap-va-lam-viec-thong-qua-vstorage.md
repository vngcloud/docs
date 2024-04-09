# Phân quyền truy cập và làm việc thông qua vStorage

rên hệ thống vStorage, chúng tôi cung cấp cho bạn các tính năng phân quyền truy cập riêng lẻ tới từng container hoặc object được mô tả qua sơ đồ bên dưới. Chi tiết bao gồm:

<figure><img src="https://www.vngcloud.vn/documents/20126/1455799/vng-cloud-product-vstorage-acl-vi-01-slideshow.jpg" alt=""><figcaption></figcaption></figure>

<details>

<summary>Chuyển chế độ công khai container</summary>

Bạn có thể chuyển chế độ của container từ riêng tư thành công khai để cho phép bất kỳ ai cũng có thể truy cập vào container để xem, tải xuống, tải lên tất cả tệp tin, object thuộc container được công khai. Để biết thêm thông tin, hãy xem tại [Chuyển chế độ công khai container](phan-quyen-truy-cap-va-lam-viec-thong-qua-vstorage.md#chuyen-che-do-cong-khai-container).

</details>

<details>

<summary>Chuyển chế độ riêng tư container</summary>

Bạn có thể chuyển chế độ của container từ công khai thành riêng tư để dừng việc chia sẻ công khai container trên môi trường điện toán đám mây. Bạn sẽ không thể truy cập vào container thông qua đường dẫn URL mà cần chứng thực quyền truy cập. Để biết thêm thông tin, hãy xem tại [Chuyển chế độ riêng tư container](phan-quyen-truy-cap-va-lam-viec-thong-qua-vstorage.md#chuyen-che-do-rieng-tu-container).

</details>

<details>

<summary>Phân quyền truy cập ACLs container</summary>

Bạn có thể cấp quyền Đọc, Ghi hoặc Đọc và Ghi cho 1 hoặc tất cả Root user khác. (Root user được cấp quyền truy cập qua ACLS phải là tài khoản được cấp quyền trên hệ thống VNG Cloud của chúng tôi). Để biết thêm thông tin, hãy xem tại [Phân quyền truy cập ACLs container](../../cac-tinh-nang-cua-vstorage/lam-viec-voi-container/phan-quyen-truy-cap-acls-container.md).

</details>

<details>

<summary>Chia sẻ tài nguyên CORS</summary>

Bạn có thể cho phép một website truy cập vào tài nguyên trên container. Để biết thêm thông tin, hãy xem tại [Chia sẻ tài nguyên CORS container](../../cac-tinh-nang-cua-vstorage/lam-viec-voi-container/chia-se-tai-nguyen-cors-container.md).

</details>

<details>

<summary>Chia sẻ object qua TempURL</summary>

Bạn có thể chia sẻ việc truy cập vào 1 hoặc nhiều object thông qua đường dẫn TempURL. Để biết thêm thông tin, hãy xem tại [Chia sẻ object](../../cac-tinh-nang-cua-vstorage/lam-viec-voi-directory-va-object/chia-se-object.md).

</details>
