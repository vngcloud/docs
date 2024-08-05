# NLB Limitation

### Limit <a href="#restrictionsandlimitationsnlb-gioihan" id="restrictionsandlimitationsnlb-gioihan"></a>

A few notes about the limitations of integrating an NLB into a cluster:

* One NLB can be used for many clusters but must ensure these clusters have the same **Subnet** .
* An NLB can include many listeners, many pools, and many policies. For limits on the number of listeners, number of pools, number of policies, please refer to [Resource Limits](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59802094) .

***

### Limit <a href="#restrictionsandlimitationsnlb-hanche" id="restrictionsandlimitationsnlb-hanche"></a>

* Changing the name or size (Rename, Resize) of the Load Balancer resource on vServer Portal can cause incompatibility with resources on the Kubernetes Cluster. This can lead to resources becoming inactive on the Cluster, or resources being resynchronized, or resource information between vServer Portal and the Cluster not matching. To prevent this problem, use `kubectl`Cluster resource management.
