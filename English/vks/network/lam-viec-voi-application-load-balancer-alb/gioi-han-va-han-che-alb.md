# ALB Limitation

### Note <a href="#restrictionsandlimitationsalb-gioihan" id="restrictionsandlimitationsalb-gioihan"></a>

A few notes about the limitations of ingressing an ALB into a cluster:

* A cluster can have multiple Ingresses, each Ingress containing resource information for a single ALB.
* One ALB can be used for many Ingress. From there, one ALB can be used for many clusters but must ensure these clusters have the same **Subnet** .
* An ALB can include many listeners, many pools, and many policies. For limits on the number of listeners, number of pools, number of policies, please refer to \[Resource limit]

***

### Limit <a href="#restrictionsandlimitationsalb-hanche" id="restrictionsandlimitationsalb-hanche"></a>

* Ingress controller manager needs to configure annotations to specify ALB properties, such as protocol, port,... These annotations may vary depending on the cloud service provider, currently with **vngcloud ingress controller** is being used. provides a reference annotation list at [Configuration for an Application Load Balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/network/lam-viec-voi-application-load-balancer-alb/cau-hinh-cho-mot-application-load-balancer) . We will further upgrade this part in the next release versions.
* Currently, vLB does not support the strip path feature in Load Balancer Layer 7, we will soon integrate this feature in the future.
* Changing the name or size (Rename, Resize) of the Load Balancer resource on vServer Portal can cause incompatibility with resources on the Kubernetes Cluster. This can lead to resources becoming inactive on the Cluster, or resources being resynchronized, or resource information between vServer Portal and the Cluster not matching. To prevent this problem, use `kubectl`Cluster resource management.
