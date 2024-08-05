# Metrics

You can install the vMonitor Platform Metric Agent into your Kubernetes Cluster to collect and push metrics to the vMonitor Platform site, then use the features at vMonitor Platform to centrally manage resources and monitor unusual activity of your Kubernetes Cluster.

### **Cài đặt Metric Agent sử dụng Helm** <a href="#metrics-caidatmetricagentsudunghelm" id="metrics-caidatmetricagentsudunghelm"></a>

**Preparation steps before installation**

**Check Permissions Using kubectl Command:**

1. You need to install Helm on the server **with a kubeconfig having sufficient permissions** to interact with the Kubernetes Cluster.

**Install Helm on Debian/Ubuntu Server**

After successful creation, you need to save the **Client\_ID** and **Secret\_Key** for the next step.

Find and select **Policy:** **vMonitorMetricPush**, then click "**Create a Service Account**" to create the Service Account. The vMonitorMetricPush policy created by VNG Cloud contains only the precise permissions required to push metrics to the system.

Click "**Create a Service Account**", enter a name for the Service Account, and click **Next Step** to attach the policy to the Service Account, then follow these steps:

2. **Create a Service Account and Attach the vMonitorMetricPush Policy to Enable Metric Push to vMonitor**
   * Access the service account creation page here.
3. Check that you have the Metric Quota and that the quota has not reached its limit. If you do not have it, you need to purchase Metric Quota at:

```
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace default
kubectl auth can-i '*' '*'
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace chỉ định, sử dụng lệnh này khi bạn muốn cài đặt agent metric tại namespace khác
kubectl auth can-i -n <namespace_chỉ_định> '*' '*'
# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebinding
kubectl auth can-i create clusterrole
kubectl auth can-i create clusterrolebinding
```

* Execute the following commands:&#x20;

2\. Proceed with Helm installation If the result of the above commands is **YES**, then you have sufficient permissions.

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null 
sudo apt-get install apt-transport-https --yes 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list 
sudo apt-get update 
sudo apt-get install helm 
```

* Kiểm tra Helm đã cài đặt thành công

```
helm version
# Kết quả mong muốn của command 
# version.BuildInfo{Version:"v3.11.0", GitCommit:"472c5736ab01133de504a826bd9ee12cbe4e7904", GitTreeState:"clean", GoVersion:"go1.18.10"}
```

\\

Declare the environment variable: KUBECONFIG. For each helm command, add the --kubeconfig option: for example, `helm install --kubeconfig <path_to_kubeconfig>`. If you need to change the kubeconfig path, you can use two ways: Helm will use kubeconfig to interact with the cluster. By default, Helm will use the config in the path: `~/.kube/config`.

#### Additional Notes on Helm:

* Refer to detailed instructions here: Install Helm Through Package Managers
* Refer to installation guides here: Install Helm on Different Operating Systems

**Daemonset** Agent: collects metrics from each node in the k8s cluster (CPU, Memory usage, ...)

**Deployment** Agent kube-state-metrics: collects metrics from each resource of the k8s cluster (pod, daemonset, deployment, replicaset, ....)

By default, when installing vMonitor Platform Metric Agent, there will be 2 components:

Installing Metric Agent

1\. Add Helm vMonitor Platform Repo

```
helm repo add vmonitor-platform https://vngcloud.github.io/helm-charts-vmonitor
helm repo update
```

2\. Install chart

* Kiểm tra và xóa các resource liên quan trước khi cài đặt để tránh đụng độ

```
# Get Clusterrole vmonitor metric agent
kubectl get clusterrole | grep vmonitor-metric-agent
# Thực hiện xóa resource nếu có tồn tại
kubectl delete clusterrole vmonitor-metric-agent
```

* Cài đặt tại **namespace default** (thêm cờ **-n \<namespace\_chỉ\_định>** để cài đặt agent tại namespace khác)

```
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> 
```

* \<YOUR\_CLIENT\_ID\_XXXXXXXXXXXXXXXXXXX>, \<YOUR\_CLIENT\_SECRET\_XXXXXXXXXXXXXXX>: Thông tin service account đã tạo ở bước chuẩn bị
* \<CLUSTER\_NAME>: Thông tin này sẽ dùng để lọc các host của k8s cluster trong trường hợp có nhiều cluster để theo dõi
* Kiểm tra việc install agent thành công

```
# Chạy command và đảm bảo output là các pods ở trạng thái running
kubectl get pod | grep "vmonitor-metric-agent"
```

* Nếu các pods agent không ở trạng thái running, sử dụng command tương ứng để kiểm tra lỗi

```
# Chạy command nếu pod ở trạng thái Pending
kubectl describe pod <vmonitor-metric-agent-node-name>
# Chạy command nếu pod ở trạng thái CrashLoopBackOff and Error
kubectl logs <vmonitor-metric-agent-node-name>
# Sau đó kiểm tra logs xuất hiện tại agent
```

Execute the following command to remove the installed related k8s resources: Uninstall Metric Agent \*\*After the installation is complete, Kubernetes monitoring metrics will be sent to the vMonitor Platform site, where you can create dashboards and widgets.

```
helm uninstall vmonitor-metric-agent
```

Install in the **default namespace** (add the flag **-n \<specified\_namespace>** to install the agent in a different namespace) Install Metric Agent without using kube

```
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> \
 --set vmonitor.kubeStateMetricsEnabled=false \
 --set kubeStateMetricsAgent.enabled=false 
```
