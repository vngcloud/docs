# Metrics

You can install vMonitor Platform Metric Agent into your Kubernetes Cluster to collect and push metrics to the vMonitor Platform site, then use the features at vMonitor Platform to centrally manage resources and monitor unusual activity of your Kubernetes Cluster. .

## **Install Metric Agent using Helm** <a href="#metrics-caidatmetricagentsudunghelm" id="metrics-caidatmetricagentsudunghelm"></a>

**Preparation steps before installation**

1\. Check that you have the Metric Quota and that your quota has not reached the limit. If you do not have it, you need to buy the Metric Quota [here](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555658) .

**2. Create a Service Account and attach policy: vMonitorMetricPush to have enough rights to push Metric to vMonitor**

To create a service account, go here [,](https://hcm-3.console.vngcloud.vn/iam/service-accounts) then perform the following steps:

* Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
* Find and select **Policy: vMonitorMetricPush,** then click " **Create a Service Account** " to create a Service Account, Policy: vMonitorMetricPush created by VNG Cloud only contains the correct permission to push metrics to the system.
* After successful creation, you need to save **the Client\_ID** and **Secret\_Key** to perform the next step.

**Install helm on Debian/Ubuntu server**

1\. You need to install Helm on a server **with kubeconfig containing enough permissions** to interact with the Kubernetes Cluster.

* Check permissions with **kubectl command** :

Kube checks permission

```
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace default
kubectl auth can-i '*' '*'
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace chỉ định, sử dụng lệnh này khi bạn muốn cài đặt agent metric tại namespace khác
kubectl auth can-i -n <namespace_chỉ_định> '*' '*'
# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebinding
kubectl auth can-i create clusterrole
kubectl auth can-i create clusterrolebinding
```

* If the result of the above commands is **YES** , then you have enough rights.

2\. Proceed to install Helm

* Execute the following commands:

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null 
sudo apt-get install apt-transport-https --yes 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list 
sudo apt-get update 
sudo apt-get install helm 
```

* Check that Helm has been installed successfully

```
helm version
# Kết quả mong muốn của command 
# version.BuildInfo{Version:"v3.11.0", GitCommit:"472c5736ab01133de504a826bd9ee12cbe4e7904", GitTreeState:"clean", GoVersion:"go1.18.10"}
```

Install Helm in other operating systems

Refer to the installation instructions here: [Install Helm Through Package Managers](https://helm.sh/docs/intro/install/#through-package-managers)

3\. Some additional notes about Helm: (see details at: [helm docs](https://helm.sh/docs/helm/helm/) )

* Helm will use kubeconfig to interact with the cluster, by default helm will use config in the path: "\~/.kube/config"
* If we need to change the path to kubeconfig we can use 2 ways:
  * For each helm command, add the --kubeconfig option: for example, helm install --kubeconfig \<path\_to\_kubeconfig>
  * Declare environment variable: KUBECONFIG

**Install Metric Agent**

By default, when installing vMonitor Platform Metric Agent, there will be 2 components:

* **Deployment** Agent kube-state-metrics: collect metrics for each resource of k8s cluster (pod, daemonset, deployment, replicaset, ....)
* **Daemonset** Agent: collect metrics for each k8s cluster node (CPU, Memory usage, ...)

1\. Add Helm vMonitor Platform Repo

```
helm repo add vmonitor-platform https://vngcloud.github.io/helm-charts-vmonitor
helm repo update
```

2\. Install charts

* Check and delete related resources before installation to avoid conflicts

```
# Get Clusterrole vmonitor metric agent
kubectl get clusterrole | grep vmonitor-metric-agent
# Thực hiện xóa resource nếu có tồn tại
kubectl delete clusterrole vmonitor-metric-agent
```

* Install at **default namespace** (add flag **-n \<namespace\_specified>** to install agent at another namespace)

```
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> 
```

* \<YOUR\_CLIENT\_ID\_XXXXXXXXXXXXXXXXXXX>, \<YOUR\_CLIENT\_SECRET\_XXXXXXXXXXXXXXX>: Service account information created in the preparation step
* \<CLUSTER\_NAME>: This information will be used to filter hosts of k8s cluster in case there are many clusters to monitor
* Check that the agent installation was successful

```
# Chạy command và đảm bảo output là các pods ở trạng thái running
kubectl get pod | grep "vmonitor-metric-agent"
```

* If the pods agent is not in running state, use the corresponding command to check for errors

```
# Chạy command nếu pod ở trạng thái Pending
kubectl describe pod <vmonitor-metric-agent-node-name>
# Chạy command nếu pod ở trạng thái CrashLoopBackOff and Error
kubectl logs <vmonitor-metric-agent-node-name>
# Sau đó kiểm tra logs xuất hiện tại agent
```

**After the installation is complete, kubernetes tracking metrics have been pushed to the vMonitor Platform site, you can proceed to vMonitor to draw dashboards and widgets.**

**Uninstall Metric Agent**

Execute the following command to delete the installed related k8s resources:

```
helm uninstall vmonitor-metric-agent
```

**Metric Agent installation does not use kube-state-metrics**

* Install at **default namespace** (add flag **-n \<namespace\_specified>** to install agent at another namespace)

```
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> \
 --set vmonitor.kubeStateMetricsEnabled=false \
 --set kubeStateMetricsAgent.enabled=false 
```
