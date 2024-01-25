Trong trường hợp Load balancer (LB) của chúng ta đang chạy HTTPS và muốn tất cả traffic HTTP tới LB chuyển sang HTTPS. Chúng ta phải tạo một listener chạy HTTP để hứng tất cả traffic từ HTTP, sau đó tạo một policy sử dụng action  **Redirect to URL ** để forward traffic sang listener chạy HTTPS. Các bước thực hiện như sau:

 **1. Tạo Listener chạy giao thức HTTP** 

 _Nếu đã có listener chạy giao thức HTTP, thì bạn bỏ qua bước này và thực hiện bước số 2 (thêm policy redirect)._ 

![](images/storage/http_https1.jpg)

 **Step 1: ** Chọn tab Load Balancers (LB).

 **Step 2: ** Chọn LB name cần cấu hình.

 **Step 3: ** Chọn tab  **LISTENER** .

 **Step 4: ** Chọn  **ADD LISTENER** .



Thêm các thông tin sau:


* Friendly name: đặt tên cho listener.
* Protocol: chọn giao thức HTTP.
* Port: chọn port 80 (hoặc port mong muốn).
* Action: để default (không ảnh hưởng cho mục đích tạo redirect).

 **2. Thêm Policy redirect cho Listener chạy giao thức HTTP** 

![](images/storage/http_https.jpg)

 **Step 1: ** Chọn tab  **Load Balancers** (LB).

 **Step 2: ** Chọn LB name cần cấu hình.

 **Step 3: ** Chọn tab  **LISTENER**  và chọn Listener name cần cấu hình.

 **Step 4: ** Chọn  **ADD POLICY** .

![](images/storage/https.jpg)

Thêm các thông tin sau:


* Information:  **_Policy name_**  đặt tên cho policy.
* Condition: mệnh đề  **_if_**  chọn  **_HOST_** , mệnh còn lại chọn  **_contains_** .
    *  **_Text box_**  nhập tên domain cần redirect.

    
* Action: chọn  **_Redirect to URL_** .
    *  **_URL to direct_**  nhập đường dẫn cần redirect.

    

Sau khi hoàn tất chọn  **ADD POLICY** .



*****

[[category.storage-team]] 
[[category.confluence]] 
