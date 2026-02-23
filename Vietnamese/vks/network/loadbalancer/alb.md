# Application Load Balancer (ALB)

## Tích hợp với ALB

### Triển khai một ALB

#### Bước 1: Tạo Deployment, Service type NodePort

```bash
kubectl create deployment httpbin --image=mccutchen/go-httpbin
kubectl expose deployment httpbin --name=httpbin-service --port=80 --target-port=8080 --type=NodePort
```

#### Bước 2: Kiểm tra thông tin Deployment và Service vừa triển khai

#### Bước 3: Tạo Ingress Resource

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
spec:
  ingressClassName: "vngcloud"
  defaultBackend:
    service:
      name: httpbin-service
      port:
        number: 80
  rules:
    - http:
        paths:
          - path: /4
            pathType: Exact
            backend:
              service:
                name: httpbin-service
                port:
                  number: 80
```

Các annotation mới cho NLB và ALB:

- `vks.vngcloud.vn/is-poc`: `true` hoặc `false` (mặc định: `false`). Nếu `true`, LoadBalancer sẽ được tạo trong POC.
- `vks.vngcloud.vn/enable-autoscale`: `true` hoặc `false` (mặc định: `false`). Nếu `true`, LoadBalancer sẽ được tạo với autoscale.
- `vks.vngcloud.vn/ignore`: `true` hoặc `false` (mặc định: `false`). Nếu `true`, operator sẽ không quản lý resource `Service` và `Ingress`. Mọi thay đổi trên resource sẽ bị bỏ qua và LoadBalancer sẽ không được cập nhật.

Các annotation mới chỉ dành cho ALB:

- `vks.vngcloud.vn/implementation-specific-params`:
- `vks.vngcloud.vn/header`: `string`, mặc định: "".
- `vks.vngcloud.vn/client-certificate-id`: `string`, mặc định: "".
