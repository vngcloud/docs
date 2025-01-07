# Application Load Balancer (ALB)

## Integrate with ALB

### Deploy a ALB

#### Step 1: Create Deployment, Service type NodePort

```bash
kubectl create deployment httpbin --image=mccutchen/go-httpbin                  
kubectl expose deployment httpbin --name=httpbin-service --port=80 --target-port=8080 --type=NodePort
```

#### Step 2: Check the Deployment and Service information just deployed

#### Step 3: Create Ingress Resource

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

New annotations for NLB and ALB:

- `vks.vngcloud.vn/is-poc`: `true` or `false` (default: `false`). If `true`, the LoadBalancer will be created in the POC.
- `vks.vngcloud.vn/enable-autoscale`: `true` or `false` (default: `false`). If `true`, the LoadBalancer will be created with autoscale.
- `vks.vngcloud.vn/ignore`: `true` or `false` (default: `false`). If `true`, the operator will not manage the resource `Service` and `Ingress`. Any changes to the resource will be ignored and LoadBalancer will not be updated.

New annotations for ALB only:

- `vks.vngcloud.vn/implementation-specific-params`:
- `vks.vngcloud.vn/header`: `string`, default: "".
- `vks.vngcloud.vn/client-certificate-id`: `string`, default: "".
