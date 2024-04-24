# Linux OS

Để đẩy Metric về vMonitor, bạn cần cài đặt Metric Agent trên server, vMonitor sử dụng Telegraf Agent để đẩy metric về hệ thống, hiện tại Telegraf Agent hỗ trợ Service Account của IAM để xác thực và phân quyền, bạn thực hiện các bước bên dưới để thiết lập Telegraf Agent đẩy metrics về vMonitor

**Telegraf Agent với Service Account**

1. **Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor**

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts),

* Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
* Tìm và chọn **Policy:** **vMonitorMetricPush,** sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
* Sau khi tạo thành công bạn cần phải lưu lại Client\_ID và Secret\_Key để thực hiện bước tiếp theo

**2. Thay thế Client\_ID, Secret\_Key vào câu lệnh bên dưới và chạy trên server để cài đặt**

Bạn sử dụng Client\_ID và Secret\_Key đã sao chép ở trên, thay thế theo thứ tự vào các trường **$IAM\_CLIENT\_ID** và **$IAM\_CLIENT\_SECRET** của câu lệnh bên dưới và chạy trên server cần được monitor, lưu ý bạn cần chạy với quyền **root user** của server (nếu không bạn phải thêm sudo ở trước câu lệnh)

```
VMONITOR_SITE=monitoring-agent.vngcloud.vn \
IAM_CLIENT_ID=$IAM_CLIENT_ID \
IAM_CLIENT_SECRET=$IAM_CLIENT_SECRET \
IAM_URL=https://iamapis.vngcloud.vn/accounts-api/v2/auth/token \
bash -c "$(curl -L https://raw.githubusercontent.com/vngcloud/vmonitor-metrics-agent/main/install.sh)"
```

|   |
| - |

**3. Sau khi chạy câu lệnh và cài đặt thành công bạn sẽ thấy server ở trang Infrastructure List/Host**&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/63767148/image2021-5-17_16-49-13.png?version=1&#x26;modificationDate=1691480997000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Telegraf Agent với API\_KEY (deprecated**): không khuyến cáo sử dụng, sắp tới sẽ dừng hỗ trợ với phương thức này <a href="#linuxos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay" id="linuxos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay"></a>

* Đây là phương thức hỗ trợ cũ của Telegraf với API\_Key, sắp tới sẽ dừng hỗ trợ phương thức này.
* Truy cập vào **Integration/API Key** để tạo và lấy thông tin API Key. Chọn **"Create an API Key",** đặt tên cho API Key và nhấn **Create,** sau đó sao chép API Key để sử dụng
* Thay thế API Key đã sao chép ở trên vào trường **$API\_KEY** của câu lệnh bên dưới và chạy câu lệnh trên server
  
```
API_KEY=$API_KEY bash -c "$(curl -L https://raw.githubusercontent.com/vngcloud/vmonitor-metrics-agent/v1-stable/install.sh)"
```
* Sau khi chạy câu lệnh và cài đặt thành công bạn sẽ thấy server ở trang Infrastructure List/Host

<figure><img src="https://docs.vngcloud.vn/download/attachments/63767148/image2021-5-17_16-49-13.png?version=1&#x26;modificationDate=1691480997000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
