# Bước 3: Sử dụng Kubeclt để access vào Container đã khởi tạo

Sau khi khởi tạo thành công Kubernetes Cluster, bạn cần sử dụng Kubectl để access vào Container đã tạo theo các bước sau đây:

### **Bước 1. Download file Config Container trên VNG CLOUD portal**  <a href="#buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc1.downloadfileconfigcontainertrenvngcloudportal" id="buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc1.downloadfileconfigcontainertrenvngcloudportal"></a>

1. Truy cập vào bảng điều khiển Kubernetes Cluster tại: [https://hcm-3.console.vngcloud.vn/vserver/container/cluster](https://hcm-3.console.vngcloud.vn/vserver/container/cluster)
2. Sau đó chỉ định Cluster và chọn **Action**
3. Chọn **Lấy file config**

<figure><img src="../../../../../.gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

***

### **Bước 2. Copy file Configure vào file configure của Kubectl trên PC/Laptop hệ điều hành MacOS** <a href="#buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc2.copyfileconfigurevaofileconfigurecuakubectltr" id="buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc2.copyfileconfigurevaofileconfigurecuakubectltr"></a>

1. Đầu tiên, bạn cần mở Terminal trên máy tính của bạn.
2.  Chuyển đến thư mục gốc của tài khoản người dùng:\


    | `cd ~/` |
    | ------- |
3.  Tạo một thư mục có tên .kube trong thư mục gốc của tài khoản người dùng. Thư mục này sẽ chứa tệp cấu hình của Kubernetes

    | `mkdir .kube` |
    | ------------- |
4.  Chuyển đến thư mục .kube mà bạn vừa tạo

    | `cd .kube` |
    | ---------- |
5.  Mở tệp với tên config bằng trình soạn thảo văn bản Vim. Tệp config chính là tệp cấu hình của kubectl để thực hiện các lệnh truy vấn và quản lý Kubernetes.\


    | `vim config` |
    | ------------ |
6.  Copy File Config trên Portal download về vào file config trên MAC OS: \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650173/Screen%20Shot%202021-05-24%20at%2010.34.41.png?version=1&#x26;modificationDate=1681382380000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (467).png" alt=""><figcaption></figcaption></figure>

***

### **Bước 2. Copy file Configure vào file configure của Kubectl trên PC/Laptop hệ điều hành Window** <a href="#buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc2.copyfileconfigurevaofileconfigurecuakubectltr" id="buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc2.copyfileconfigurevaofileconfigurecuakubectltr"></a>

1. cd \~/
2. mkdir .kube
3. cp \~/Downloads/config.txt \~/.kube/config
4.  cd. kube\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650173/image2023-8-10_15-19-54.png?version=1&#x26;modificationDate=1691655596000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### **Bước 3. Kiểm tra kết nối từ Kubectl lên VNG CLOUD Containter:** <a href="#buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc3.kiemtraketnoitukubectllenvngcloudcontainter" id="buoc3-sudungkubecltdeaccessvaocontainerdakhoitao-buoc3.kiemtraketnoitukubectllenvngcloudcontainter"></a>

1.  Sau đó dùng lệnh sau để liệt kê tất cả các node trong cluster Kubernetes của bạn:\


    | `kubectl get nodes` |
    | ------------------- |
2.  Giao diện sẽ trả về kết quả như sau:\
    \
    \
    \
    Như vậy đã hoàn thành việc khởi tạo Containers và kết nối lên Container đó ngay tại PC hoặc Laptop của mình.

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650173/Screen%20Shot%202021-05-24%20at%2010.40.43.png?version=1&#x26;modificationDate=1681382380000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
