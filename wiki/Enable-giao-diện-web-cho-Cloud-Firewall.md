 **Bước 1** :Sử dụng Terminal của Linux để kết nối đến vCF

ssh -p 22016 root@61.28.233.3

 **Bước 2** :Thực hiện các command để enable giao diện web

![](images/storage/worddav76b705858a95eadd1427965a65a0429b.png)


*  **1 -** Nhập "cli" để khởi động CLI
*  **2 -** Nhập "configure" để vô chế độ cài đặt
*  **3 -** Nhập "set system services web-management http interface fxp0.0" để cài đặt enable giao diện web
*  **4 -** Nhập "commit check" để kiểm tra thông tin config hợp lệ
*  **5 -** Nhập "commit" để apply enable giao diện web

 **Bước 3** :Truy cập web quản lý với link WebEndpoint (trong email khởi tạo) và điền thông tin user root, password tương ứng để login

VD: [http://61.28.233.3:28013](http://61.28.233.3:28013/)

![](images/storage/worddav22c7f03f9f74491dbdd4bbf7c38ab870.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
