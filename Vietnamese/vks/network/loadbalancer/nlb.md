# Network Load Balancer (NLB)

## Tích hợp với NLB

Để tích hợp NLB với cụm Kubernetes, bạn có thể sử dụng Service với type LoadBalancer. Khi bạn tạo một Service như vậy, VNG Cloud LoadBalancer Controller sẽ tự động tạo một NLB để chuyển tiếp lưu lượng đến các pod trên node của bạn. Bạn cũng có thể sử dụng annotation để tùy chỉnh các thuộc tính của NLB, như cổng, giao thức,...

### Triển khai một NLB

#### Bước 1: Tạo Deployment, Service type LoadBalancer

```bash
kubectl create deployment httpbin --image=mccutchen/go-httpbin
kubectl expose deployment httpbin --name=httpbin-service --port=80 --target-port=8080 --type=LoadBalancer
```
