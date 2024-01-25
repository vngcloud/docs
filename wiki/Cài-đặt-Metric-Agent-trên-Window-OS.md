Để đẩy Metric về vMonitor, bạn cần cài đặt Metric Agent trên server, vMonitor sử dụng Telegraf Agent để đẩy metric về hệ thống, hiện tại Telegraf Agent hỗ trợ Service Account của IAM để xác thực và phân quyền, bạn thực hiện các bước bên dưới để thiết lập Telegraf Agent đẩy metrics về vMonitor

Lưu ý bạn cần có Quota Metric, nếu chưa có bạn cần thực hiện mua Quota Metric tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555658). Ngoài ra đối với những khách hàng trước đó đã sử dụng Telegraf Agent với phương thức xác thực là API Key cũng có thể thực hiện theo hướng dẫn bên dưới để cài lại Telegraf Agent với Service Account.

 **Telegraf Agent với Service Account** 
1.  **Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor** 

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts):


* Chọn " **Create a Service Account** ", điền tên cho Service Account và nhấn  **Next Step ** để gắn quyền cho Service Account
* Tìm và chọn ** Policy:**   **vMonitorMetricPush, ** sau đó nhấn " **Create a Service Account** " để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
* Sau khi tạo thành công bạn cần phải lưu lại Client_ID và Secret_Key để thực hiện bước tiếp theo

2.  **Tải bản cài  Agent Installer cho Windows** 


* Truy cập vào link để thực hiện tải agent installer cho Windows : [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly_windows_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly_windows_amd64.exe)

3. **Cài đặt installer với Client_ID và Secret_Key đã sao chép ở trên** 


* Chạy agent installer đã tải ở trên
* Sau khi nhận thông báo, chọn  **More Info** 

![](images/storage/worddav78ab72ef870b0249d8f6a626cf0dd070.png)


* Sau đó chọn  **Run anyway** , để bắt đầu cài agent

![](images/storage/worddav468312982544d0b0ef8edc2cd437560c.png)


* Chọn  **Next**  để tiếp tục

![](images/storage/image2023-6-27_16-32-56.png)




* Nhập 2 thông tin  **Client_ID**  và  **Secret_Key**  đã sao chép ở trên vào 2 trường:  **IAM_CLIENT_ID**  và  **IAM_CLIENT_SECRET** : 

![](images/storage/image2023-6-27_16-33-25.png)


* Để mặc định, chọn Next để tiếp tục, hoặc nếu bạn muốn thay đổi thư mục cài đặt thì thực hiện thay đổi

![](images/storage/image2023-6-27_16-34-49.png)


* Chọn  **Accept the license,**  sau đó chọn  **Next**  để tiếp tục

![](images/storage/image2023-6-27_16-35-6.png)


* Để mặc định, chọn  **Next**  để tiếp tục, hoặc bạn có thể tùy chỉnh shortcut menu name cho agent

![](images/storage/image2023-6-27_16-35-30.png)


* Chọn  **Install**  để thực hiện cài đặt

![](images/storage/image2023-6-27_16-36-10.png)


* Chọn  **Yes**  để thực hiện grant quyền cho agent hoạt động

![](images/storage/worddav0578afc8e639abf0bcb73033219454af.png)


* Sau khi quá trình cài đặt hoàn tất, chọn  **Finish** 

![](images/storage/image2023-6-27_16-36-50.png)

4.  **Sau khi cài đặt thành công bạn sẽ thấy server ở trang Infrastructure List/Host ** 




##  **Telegraf Agent với API_KEY (deprecated** ): không khuyến cáo sử dụng, sắp tới sẽ dừng hỗ trợ với phương thức này vào ngày 15/11
B1: Tạo API Key (nếu chưa thực hiện tạo bất kỳ API Key nào trước đó )


* Truy cập vào portal vMonitor Platform Product: [https://hcm-3.console.vngcloud.vn/vmonitor/](https://hcm-3.console.vngcloud.vn/vmonitor/)
* Chọn  **Intergration**  => sau đó chọn phần  **API Key** 

![](images/storage/worddav11a7182e3ab02771b39bbb182406ca04.png)


* Chọn  **Create an API Key** , để thực hiện tạo mới (nếuchưatạobấtkỳ API Key nàotrướcđó)

![](images/storage/worddav26be19225d998762cf92c40c98d65e73.png)

B2: Download Agent Installer


* Truy cập vào link để thực hiện tải agent installer: [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly_windows_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly_windows_amd64.exe)

B3: Install Agent


* Chạy agent installer
* Sau khi nhận thông báo, chọn  **More Info** 

![](images/storage/worddav78ab72ef870b0249d8f6a626cf0dd070.png)


* Sau đó chọn  **Run anyway** , để bắt đầu install agent

![](images/storage/worddav468312982544d0b0ef8edc2cd437560c.png)


* Chọn  **Next**  để tiếp tục

![](images/storage/worddavd9a5116c4051f0a01984feeda26d0c46.png)


* Quay về Portal vMonitor Platform, ở phần API Key,  **chọn**  **biểu**  **tượng copy** , để copy thông tin API Key

![](images/storage/worddavbeffd4f0c2a21218bf241b5c5127a8e0.png)


* Paste thông tin API Key vào phần nhập  **Credentials** 

![](images/storage/worddavd52772f6e56d94fc0d6fe1ffc19e44cb.png)


* Có thể tùy chỉnh installation folder

![](images/storage/worddava9617c685b7a4cb8766d9f5bc361f4f8.png)


* Chọn  **Accept the license,**  sau đó chọn  **Next**  để tiếp tục

![](images/storage/worddavd8994f5442c991b06590a64f47b544ff.png)


* Có thể tùy chỉnh shortcut menu name cho agent, sau đó chọn  **Next**  để tiếp tục

![](images/storage/worddav2d58db8601c5d1d03a289c53098ae4c2.png)


* Chọn  **Install**  để thực hiện cài đặt

![](images/storage/worddav0c5a1caef45759f913ddeeeb188274da.png)


* Chọn Yes để thực hiện grant quyền cho agent hoạt động

![](images/storage/worddav0578afc8e639abf0bcb73033219454af.png)


* Sau khi quá trình cài đặt hoàn tất, chọn  **Finish** 

![](images/storage/worddav41555652043df0ea78adcc129cca4687.png)


## B4: Kiểm tra agent đã hoạt động

* Truy cập vào portal vMonitor Platform, chọn  **Infrastructure list**  => chọn  **Host,**  sau đó kiểm tra hostname của VM đã xuất hiện trong danh sách

![](images/storage/worddav6f233f581f0b5be25d8454b400712038.png)


* Chọn vào tên  **Hostname** , để kiểm tra dashboard monitor

![](images/storage/worddav3b6eb48193a6bf5cc95600036f1d83fe.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
