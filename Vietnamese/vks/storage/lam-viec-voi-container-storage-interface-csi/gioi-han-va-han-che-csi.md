# Giới hạn và hạn chế CSI

## Hạn chế <a href="#restrictionsandlimitations-hanche" id="restrictionsandlimitations-hanche"></a>

* Việc thay đổi tên hoặc kích thước (Rename, Resize Load Balancer, Extend Volume) các tài nguyên như Load Balancer hay Volumes trên vServer Portal có thể gây ra sự không tương thích với tài nguyên trên Kubernetes Cluster. Điều này có thể dẫn đến việc các tài nguyên không hoạt động trên Cluster, tài nguyên bị đồng bộ lại hoặc thông tin tài nguyên giữa vServer Portal và Cluster không khớp. Để ngăn chặn vấn đề này, hãy sử dụng `kubectl`để quản lý tài nguyên của Cluster.
