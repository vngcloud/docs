# Liên kết tài khoản Service Account với policy tương ứng

Sau khi bạn đã khởi tạo Service Account và Policy mong muốn, tiếp theo bạn cần liên kết tài khoản Service Account vào policy theo hướng dẫn bên dưới:&#x20;

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/) với tài khoản Root User Account.
2. Chọn menu **Service Account.**&#x20;
3. Chọn **Service Account** muốn thực hiện gán quyền.&#x20;
4. Chọn **Attach policies**.
5. Chọn các **policy** mà bạn mong muốn. Hệ thống vIAM hỗ trợ bạn gán nhiều policy vào một tài khoản Service Account. Nếu các policy này chứa các quyền hạn độc lập thì chúng sẽ bổ sung cho nhau (tức là danh sách quyền hạn được hợp lại). Ngược lại nếu các policy này chứa các quyền hạn trái ngược thì bạn sẽ không thể truy cập vào tài nguyên tương ứng theo danh sách quyền hạn này (tức là danh sách quyền được hợp lại và khi trái ngược thì sẽ triệt tiêu nhau).
6. Chọn **Attach**.

Sau khi bạn thực hiện 6 bước bên trên, lúc này bạn đã có thể sử dụng Service Account để truy cập vào tài nguyên vStorage. Để biết thêm thông tin, hãy xem tại [Truy cập tài nguyên sử dụng tài khoản Service Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648950).
