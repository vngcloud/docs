# Create a Certificate

After purchasing Log Project, the system will automatically generate a certificate for each Log Project, this certificate is used to authenticate Log Agent with the vMonitor Platform system. To create or download a certificate, follow the steps below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor) .
2. Select **Integration -> c** select **Certificate.**
3. If you have not created any Log project, select **New cert** to create a new Certificate. If you have successfully created the Log project from [Create Log project](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-project-quota) , in this Log project, select **New cert.**
4. We start creating a certificate for your Log project. When the certificate status is **ACTIVE,** it means this certificate is ready for you to use.
5. Select **Download** to download certificate information to your device or select **Delete** to delete the newly created Certificate.

After downloading and unpacking, you will see certificate files and installation instructions for each environment and agent type to help you easily set up the initial steps:

| <pre><code>/Linux
│   ├── Filebeat               // Bộ cài cho agent filebeat , môi trường Linux
│   |   ├── VNG.trust.pem      // các file pem để  xác thực người dùng
│   |   ├── user.cer.pem       
│   |   ├── user.key.pem
│   |   ├── filebeat.sh        // script cài khởi đầu
│   |   ├── info.md            // thông tin endpoint gửi dữ liệu
│   |   ├── readme.md          // hướng dẫn sơ bộ
│   ├── Logstash               // Bộ cài cho agent logstash , môi trường Linux
/Windows                       // Bộ cài cho môi trường Windows
│   ├── ...                    // tương tự cũng có các file .pem như trên
/Docker                        // Bộ cài cho môi trường Docker
/Kubernetes                    // Bộ cài cho môi trường Kubernetes
</code></pre> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
