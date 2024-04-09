# Window OS

Để đẩy Metric về vMonitor, bạn cần cài đặt Metric Agent trên server, vMonitor sử dụng Telegraf Agent để đẩy metric về hệ thống, hiện tại Telegraf Agent hỗ trợ Service Account của IAM để xác thực và phân quyền, bạn thực hiện các bước bên dưới để thiết lập Telegraf Agent đẩy metrics về vMonitor

### **Telegraf Agent với Service Account** <a href="#windowos-telegrafagentvoiserviceaccount" id="windowos-telegrafagentvoiserviceaccount"></a>

1. **Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor**

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts):

* Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
* Tìm và chọn **Policy:** **vMonitorMetricPush,** sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
* Sau khi tạo thành công bạn cần phải lưu lại Client\_ID và Secret\_Key để thực hiện bước tiếp theo

2\. **Tải bản cài  Agent Installer cho Windows**

* Truy cập vào link để thực hiện tải agent installer cho Windows : [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly\_windows\_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly\_windows\_amd64.exe)

3\. **Cài đặt installer với Client\_ID và Secret\_Key đã sao chép ở trên**

* Chạy agent installer đã tải ở trên
* Sau khi nhận thông báo, chọn **More Info**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav78ab72ef870b0249d8f6a626cf0dd070.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Sau đó chọn **Run anyway**, để bắt đầu cài agent

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav468312982544d0b0ef8edc2cd437560c.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Next** để tiếp tục

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-32-56.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Nhập 2 thông tin **Client\_ID** và **Secret\_Key** đã sao chép ở trên vào 2 trường: **IAM\_CLIENT\_ID** và **IAM\_CLIENT\_SECRET**:&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-33-25.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Để mặc định, chọn Next để tiếp tục, hoặc nếu bạn muốn thay đổi thư mục cài đặt thì thực hiện thay đổi



<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-34-49.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Accept the license,** sau đó chọn **Next** để tiếp tục\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-35-6.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Để mặc định, chọn **Next** để tiếp tục, hoặc bạn có thể tùy chỉnh shortcut menu name cho agent



<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-35-30.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Install** để thực hiện cài đặt

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-36-10.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Yes** để thực hiện grant quyền cho agent hoạt động

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav0578afc8e639abf0bcb73033219454af.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Sau khi quá trình cài đặt hoàn tất, chọn **Finish**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2023-6-27_16-36-50.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

4\. **Sau khi cài đặt thành công bạn sẽ thấy server ở trang Infrastructure List/Host**&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/image2021-5-17_16-49-13.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Telegraf Agent với API\_KEY (deprecated**): không khuyến cáo sử dụng, sắp tới sẽ dừng hỗ trợ với phương thức này <a href="#windowos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay" id="windowos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay"></a>

B1: Tạo API Key (nếu chưa thực hiện tạo bất kỳ API Key nào trước đó )

* Truy cập vào portal vMonitor Platform Product: [https://hcm-3.console.vngcloud.vn/vmonitor/](https://hcm-3.console.vngcloud.vn/vmonitor/)
* Chọn **Intergration** => sau đó chọn phần **API Key**

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav11a7182e3ab02771b39bbb182406ca04.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Create an API Key**, để thực hiện tạo mới (nếu chưa tạo bất kỳ API Key nào trước đó)

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav26be19225d998762cf92c40c98d65e73.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

B2: Download Agent Installer

* Truy cập vào link để thực hiện tải agent installer: [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly\_windows\_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly\_windows\_amd64.exe)

B3: Install Agent

* Chạy agent installer
* Sau khi nhận thông báo, chọn **More Info**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav78ab72ef870b0249d8f6a626cf0dd070.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Sau đó chọn **Run anyway**, để bắt đầu install agent

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav468312982544d0b0ef8edc2cd437560c.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Next** để tiếp tục

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddavd9a5116c4051f0a01984feeda26d0c46.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Quay về Portal vMonitor Platform, ở phần API Key, **chọn** **biểu** **tượng copy**, để copy thông tin API Key

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddavbeffd4f0c2a21218bf241b5c5127a8e0.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Paste thông tin API Key vào phần nhập **Credentials**

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddavd52772f6e56d94fc0d6fe1ffc19e44cb.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Có thể tùy chỉnh installation folder

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddava9617c685b7a4cb8766d9f5bc361f4f8.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Accept the license,** sau đó chọn **Next** để tiếp tục

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddavd8994f5442c991b06590a64f47b544ff.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Có thể tùy chỉnh shortcut menu name cho agent, sau đó chọn **Next** để tiếp tục

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav2d58db8601c5d1d03a289c53098ae4c2.png?version=1&#x26;modificationDate=1691481028000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn **Install** để thực hiện cài đặt

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav0c5a1caef45759f913ddeeeb188274da.png?version=1&#x26;modificationDate=1691481029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn Yes để thực hiện grant quyền cho agent hoạt động

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav0578afc8e639abf0bcb73033219454af.png?version=1&#x26;modificationDate=1691481027000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Sau khi quá trình cài đặt hoàn tất, chọn **Finish**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav41555652043df0ea78adcc129cca4687.png?version=1&#x26;modificationDate=1691481029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### B4: Kiểm tra agent đã hoạt động <a href="#windowos-b4-kiemtraagentdahoatdong" id="windowos-b4-kiemtraagentdahoatdong"></a>

* Truy cập vào portal vMonitor Platform, chọn **Infrastructure list** => chọn **Host,** sau đó kiểm tra hostname của VM đã xuất hiện trong danh sách

<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav6f233f581f0b5be25d8454b400712038.png?version=1&#x26;modificationDate=1691481029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Chọn vào tên **Hostname**, để kiểm tra dashboard monitor

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59803970/worddav3b6eb48193a6bf5cc95600036f1d83fe.png?version=1&#x26;modificationDate=1691481029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
