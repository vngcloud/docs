# Restrictions and limitations

## Hạn chế <a href="#restrictionsandlimitations-hanche" id="restrictionsandlimitations-hanche"></a>

* Hiện tại, chúng tôi chưa cung cấp cho bạn tính năng resize IOPS, nếu bạn muốn resize IOPS vui lòng liên hệ chúng tôi thông qua việc mở 1 ticket trên hệ thống VNG Cloud.
* Ngoài mục Kubernetes Cluster, các mục khác như Load Balancer, Volumes cũng được liệt kê bên ngoài mục Kubernetes Cluster, cụ thể là các mục Load Balancer, Volumes trong vServer Portal. Nếu bạn đổi tên hoặc sửa đổi các tài nguyên này (Load Balancer, Volumes) trong vServer Portal, bạn có thể khiến chúng không sử dụng được cho Cluster hoặc khiến cho tài nguyên trên vServer Portal và tài nguyên trên Cluster không được đồng nhất. Để tránh điều này, hãy quản lý tài nguyên cluster của bạn với kubectl.
