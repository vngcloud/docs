# Network Load Balancer (NLB)

## Integrate with NLB

To integrate a NLB with a Kubernetes cluster, you can use a Service with type [LoadBalancer](loadbalancerhttps://www.airplane.dev/blog/kubernetes-load-balancer) . When you create such a Service, GreenNode LoadBalancer Controller will automatically create an NLB to forward traffic to pods on your [node](nhttps://www.airplane.dev/blog/kubernetes-load-balancer) . You can also use annotations to customize NLB properties, such as port, protocol,...

### Deploy a NLB

#### Step 1: Create Deployment, Service type LoadBalancer

```bash
kubectl create deployment httpbin --image=mccutchen/go-httpbin                  
kubectl expose deployment httpbin --name=httpbin-service --port=80 --target-port=8080 --type=LoadBalancer
```
