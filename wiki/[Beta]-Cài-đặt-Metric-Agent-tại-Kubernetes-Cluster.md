Bạn có thể cài đặt vMonitor Platform Metric Agent vào Kubernetes Cluster để thu thập và đẩy metric về vMonitor Platform site, sau đó sử dụng các tính năng tại vMonitor Platform để quản lý tập trung tài nguyên và theo dõi hoạt động bất thường của Kubernetes Cluster.

             * [Cài đặt helm tại Debian/Ubuntu server](#cài-đặt-helm-tại-debian/ubuntu-server)
    * [Gỡ cài đặt Metric Agent](#gỡ-cài-đặt-metric-agent)
    * [Cài đặt Metric Agent không sử dụng kube-state-metrics](#cài-đặt-metric-agent-không-sử-dụng-kube-state-metrics)


 **Cài đặt Metric Agent sử dụng Helm**  **Các bước chuẩn bị trước khi cài đặt**        1. Kiểm tra bạn đã có Metric Quota và quota chưa chạm mức giới hạn, nếu chưa có bạn cần thực hiện mua Quota Metric tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555658).

 **       2. Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor** 

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts), sau đó thực hiện các bước sau:


* Chọn " **Create a Service Account** ", điền tên cho Service Account và nhấn  **Next Step ** để gắn quyền cho Service Account
* Tìm và chọn **Policy:**  **vMonitorMetricPush,** sau đó nhấn " **Create a Service Account** " để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
* Sau khi tạo thành công bạn cần phải lưu lại  **Client_ID**  và  **Secret_Key**  để thực hiện bước tiếp theo.


### Cài đặt helm tại Debian/Ubuntu server
        1. Bạn cần cài đặt Helm trên server  **có kubeconfig chứa đủ quyền**  để tương tác Kubernetes Cluster.


* Kiểm tra quyền bằng  **command kubectl** :


```
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace default
kubectl auth can-i '*' '*'
# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace chỉ định, sử dụng lệnh này khi bạn muốn cài đặt agent metric tại namespace khác
kubectl auth can-i -n <namespace_chỉ_định> '*' '*'
# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebinding
kubectl auth can-i create clusterrole
kubectl auth can-i create clusterrolebinding
```

* Nếu kết quả các command trên là  **YES**  thì bạn đã đủ quyền.

        2. Tiến hành cài đặt Helm


* Thực hiện những command sau:


```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null 
sudo apt-get install apt-transport-https --yes 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list 
sudo apt-get update 
sudo apt-get install helm 
```

* Kiểm tra Helm đã cài đặt thành công


```bash
helm version
# Kết quả mong muốn của command 
# version.BuildInfo{Version:"v3.11.0", GitCommit:"472c5736ab01133de504a826bd9ee12cbe4e7904", GitTreeState:"clean", GoVersion:"go1.18.10"}
```




Cài đặt Helm tại các hệ điều hành khác        Tham khảo hướng dẫn cài đặt tại đây: [Install Helm Through Package Managers](https://helm.sh/docs/intro/install/#through-package-managers)

        3. Một số lưu ý thêm về Helm: (tham khảo chi tiết tại: [helm docs](https://helm.sh/docs/helm/helm/))


* Helm sẽ dùng kubeconfig để tương tác với cluster, mặc định helm sẽ dùng config ở đường dẫn: "~/.kube/config"
* Nếu cần thay đổi đường dẫn tới kubeconfig ta có thể sử dụng 2 cách:
    * Với mỗi command helm ta thêm option --kubeconfig: ví dụ helm install --kubeconfig <path_to_kubeconfig>
    * Khai báo biến môi trường: KUBECONFIG

    

Cài đặt Metric Agent        Mặc định khi cài đặt vMonitor Platform Metric Agent sẽ có 2 thành phần: 


*  **Deployment**  Agent kube-state-metrics: thu thập metric từng resource của k8s cluster (pod, daemonset, deployment, replicaset, ....)
*  **Daemonset**  Agent: thu thập metrics từng node k8s cluster (CPU, Memory usage, ...)

        1. Thêm Helm vMonitor Platform Repo


```bash
helm repo add vmonitor-platform https://vngcloud.github.io/helm-charts-vmonitor
helm repo update
```
        2. Cài đặt chart


* Kiểm tra và xóa các resource liên quan trước khi cài đặt để tránh đụng độ


```bash
# Get Clusterrole vmonitor metric agent
kubectl get clusterrole | grep vmonitor-metric-agent
# Thực hiện xóa resource nếu có tồn tại
kubectl delete clusterrole vmonitor-metric-agent
```

* Cài đặt tại  **namespace default ** (thêm cờ **-n <namespace_chỉ_định>**  để cài đặt agent tại namespace khác)


```bash
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> 
```

* <YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX>, <YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX>: Thông tin service account đã tạo ở bước chuẩn bị


*  <CLUSTER_NAME>: Thông tin này sẽ dùng để lọc các host của k8s cluster trong trường hợp có nhiều cluster để theo dõi




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
 **     Sau khi cài đặt hoàn tất, metric theo dõi kubernetes đã được đẩy về vMonitor Platform site , bạn có thể tiến hành lên vMonitor để vẽ các dashboard, widget.** 


### Gỡ cài đặt Metric Agent
Thực hiện command sau để xóa các k8s resources liên quan đã cài đặt:


```bash
helm uninstall vmonitor-metric-agent
```

### Cài đặt Metric Agent không sử dụng kube-state-metrics

* Cài đặt tại  **namespace default ** (thêm cờ **-n <namespace_chỉ_định>**  để cài đặt agent tại namespace khác)


```bash
helm install vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent \
 --set vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \
 --set vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \
 --set vmonitor.clusterName=<CLUSTER_NAME> \
 --set vmonitor.kubeStateMetricsEnabled=false \
 --set kubeStateMetricsAgent.enabled=false 
```




*****

[[category.storage-team]] 
[[category.confluence]] 
