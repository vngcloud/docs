# Kubernetes

## Install Metric Agent at Kubernetes Cluster <a href="#kubernetes-caidatmetricagenttaikubernetescluster" id="kubernetes-caidatmetricagenttaikubernetescluster"></a>

You can install vMonitor Platform Metric Agent into your Kubernetes Cluster to collect and push metrics to the vMonitor Platform site, then use the features at vMonitor Platform to centrally manage resources and monitor unusual activity of your Kubernetes Cluster. .

***

## **Install Metric Agent using Helm**

### **Preparation steps before installation**

1\. Check that you have the Metric Quota and that your quota has not reached the limit. If you do not have it, you need to buy the Metric Quota [here](https://vmonitor.console.vngcloud.vn/quota-usages/metric) .

**2. Create a Service Account and attach policy: vMonitorMetricPush to have enough rights to push Metric to vMonitor Platform.** To create a service account, go here [,](https://iam.console.vngcloud.vn/service-accounts) then perform the following steps:

* Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
* Find and select **Policy: vMonitorMetricPush,** then click " **Create a Service Account** " to create a Service Account, Policy: vMonitorMetricPush created by GreenNode only contains the correct permission to push metrics to the system.
* After successful creation, you need to save **the Client\_ID** and **Secret\_Key** to perform the next step.

### **Install helm on Debian/Ubuntu server**

1\. You need to install Helm on a server **with kubeconfig containing enough permissions** to interact with the Kubernetes Cluster.

* Check permissions with **kubectl command** :

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

**To install Helm on other operating systems, please refer to the installation instructions here:** [**Install Helm Through Package Managers**](https://helm.sh/docs/intro/install/#through-package-managers) **.**

3\. Some additional notes about Helm: (see details at: [helm docs](https://helm.sh/docs/helm/helm/) )

* Helm will use kubeconfig to interact with the cluster, by default helm will use config in the path: "\~/.kube/config"
* If we need to change the path to kubeconfig we can use 2 ways:
  * To each helm command you can add the --kubeconfig option: for example helm install --kubeconfig \<path\_to\_kubeconfig>
  * Declare environment variable: KUBECONFIG

***

## **Install Metric Agent**

By default, when installing vMonitor Platform Metric Agent, there will be 2 components:

* **Deployment Agent kube-state-metrics** : collect metrics for each resource of k8s cluster (pod, daemonset, deployment, replicaset, ....)
* **Daemonset Agent** : collect metrics for each k8s cluster node (CPU, Memory usage, ...)

1\. Add Helm vMonitor Platform Repo as command

```
helm repo add vmonitor-platform https://vngcloud.github.io/helm-charts-vmonitor
helm repo update
```

2\. Install charts

* Install at **default namespace** (add flag **-n \<namespace\_specified>** to install agent at another namespace)

```
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> 
```

* In there:
  * \<YOUR\_CLIENT\_ID\_XXXXXXXXXXXXXXXXXXX>, \<YOUR\_CLIENT\_SECRET\_XXXXXXXXXXXXXXX>: Service account information created in the preparation step
  * \<CLUSTER\_NAME>: This information will be used to filter hosts of k8s cluster in case there are many clusters to monitor
* Check the successful installation of the agent via command

```
# Chạy command và đảm bảo output là các pods ở trạng thái running
kubectl get pod | grep "vmonitor-metric-agent"
```

**After installation is complete, kubernetes tracking metrics have been pushed to the vMonitor Platform site, you can proceed to vMonitor Platform to draw dashboards and widgets.**

***

## **Uninstall Metric Agent**

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

***

## Monitor Kubernetes (K8S) at vMonitor Platform <a href="#kubernetes-monitorkubernetes-k8s-taivmonitorplatform" id="kubernetes-monitorkubernetes-k8s-taivmonitorplatform"></a>

To perform a Kubernetes (K8S) monitor at vMonitor Platform, please follow the instructions below:

**Step 1** : Install helm from API for **Debian/Ubuntu operating system,** you should install Helm on the machine with kubeconfig and have enough rights to access the Kubernetes Cluster you need to monitor

* Execute the following commands

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null 
sudo apt-get install apt-transport-https --yes 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list 
sudo apt-get update 
sudo apt-get install helm 
```

**For other operating systems** , you can refer to the installation instructions here: [Install Helm Through Package Managers](https://helm.sh/docs/intro/install/#through-package-managers)

* Check that helm has been installed successfully with the command

```
helm version 
```

**Step 2** : Check permissions to interact with k8s cluster

* Some notes about helm: (see details at: [helm docs](https://helm.sh/docs/helm/helm/) )
  * Helm will use kubeconfig to interact with the cluster, by default helm will use config in the path: "\~/.kube/config"
  * If we need to change the path to kubeconfig we can use 2 ways:
    * For each helm command, add the --kubeconfig option: for example, helm install --kubeconfig \<path\_to\_kubeconfig>
    * Declare environment variable: KUBECONFIG
* Check permissions:
  * Use the kubectl command:

```
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace default
kubectl auth can-i '*' '*'
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace kube-system
kubectl auth can-i -n kube-system '*' '*'
# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebinding
kubectl auth can-i create clusterrole
kubectl auth can-i create clusterrolebinding
```

If the results of the above commands are YES, then you have enough rights to perform the next steps

**Step 3** : Install kube-state-metrics using helm

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts 
helm repo update 
helm install -n kube-system kube-state-metrics prometheus-community/kube-state-metrics --set image.tag="v2.7.0" 
```

* Check that the installation of kube-state-metrics was successful

```
# Chạy command và đảm bảo output là các pods ở trạng thái running
kubectl get pod -n kube-system | grep kube-state-metrics
```

**Attention:**

* Currently vMonitor metric agent only supports kube-state-metrics version <= v2.7.0.

**Step 4** : Install vmonitor metric agent using helm

By default, vMonitor metric agent will have 2 components: deployment used to collect kube-state-metrics and daemonset component to collect metrics for each k8s node

* Add vMonitor helm repository

```
helm repo add vmonitor https://vngcloud.github.io/helm-charts-vmonitor/
helm repo update 
```

* Install vmonitor-metric-agent from the helm repository, by default it will be installed in namespace:default, if you want to install in another namespace, add the –n option in the command below, you can change the name **vng-vmonitor- metric-agent** to whatever name you want and change **k8s-cluster-name** to your Kubernetes Cluster name

```
helm install vmonitor-metric-agent --set vmonitor.apiKey=<API_KEY> --set vmonitor.clusterName=k8s-cluster vmonitor/vmonitor-metric-agent 
```

* Check that the agent installation was successful

```
# Chạy command và đảm bảo output là các pods ở trạng thái running
kubectl get pod | grep "vmonitor-metric-agent"
```

**Step 5: After installing all kubernetes tracking metrics have been pushed, you can proceed to vMonitor to draw dashboards and widgets.**

* If you no longer need to use vmonitor metric agent, you can uninstall it with the command below

```
helm uninstall vmonitor-metric-agent
```

{% hint style="info" %}
**Attention:**

* When monitoring Kubernetes with vMonitor Platform, you are currently only charged for the number of Hosts into the Quota, the number of Hosts will be calculated by the number of kubelet worker nodes you have plus 1. The number of Containers per Host will not be counted. this moment.
{% endhint %}
