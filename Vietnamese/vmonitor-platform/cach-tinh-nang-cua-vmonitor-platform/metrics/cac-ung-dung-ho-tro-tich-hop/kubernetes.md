# Kubernetes

### Cài đặt Metric Agent tại Kubernetes Cluster <a href="#kubernetes-caidatmetricagenttaikubernetescluster" id="kubernetes-caidatmetricagenttaikubernetescluster"></a>

Bạn có thể cài đặt vMonitor Platform Metric Agent vào Kubernetes Cluster để thu thập và đẩy metric về vMonitor Platform site, sau đó sử dụng các tính năng tại vMonitor Platform để quản lý tập trung tài nguyên và theo dõi hoạt động bất thường của Kubernetes Cluster.

#### **Cài đặt Metric Agent sử dụng Helm** <a href="#kubernetes-caidatmetricagentsudunghelm" id="kubernetes-caidatmetricagentsudunghelm"></a>

#### **Các bước chuẩn bị trước khi cài đặt** <a href="#kubernetes-cacbuocchuanbitruockhicaidat" id="kubernetes-cacbuocchuanbitruockhicaidat"></a>

&#x20;      1\. Kiểm tra bạn đã có Metric Quota và quota chưa chạm mức giới hạn, nếu chưa có bạn cần thực hiện mua Quota Metric tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555658).

&#x20;      **2. Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor**

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts), sau đó thực hiện các bước sau:

* Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
* Tìm và chọn **Policy:** **vMonitorMetricPush,** sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
* Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** để thực hiện bước tiếp theo.

#### Cài đặt helm tại Debian/Ubuntu server <a href="#kubernetes-caidathelmtaidebian-ubuntuserver" id="kubernetes-caidathelmtaidebian-ubuntuserver"></a>

&#x20;       1\. Bạn cần cài đặt Helm trên server **có kubeconfig chứa đủ quyền** để tương tác Kubernetes Cluster.

* Kiểm tra quyền bằng **command kubectl**:

Kube check permission

| `# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace defaultkubectl auth can-i '*'` `'*'# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace chỉ định, sử dụng lệnh này khi bạn muốn cài đặt agent metric tại namespace kháckubectl auth can-i -n <namespace_chỉ_định> '*'` `'*'# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebindingkubectl auth can-i create clusterrolekubectl auth can-i create clusterrolebinding` |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

* Nếu kết quả các command trên là **YES** thì bạn đã đủ quyền.

&#x20;       2\. Tiến hành cài đặt Helm

* Thực hiện những command sau:

| `curl https://baltocdn.com/helm/signing.asc \| gpg --dearmor \| sudo tee /usr/share/keyrings/helm.gpg > /dev/null sudo apt-get install apt-transport-https --yes echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg]` [`https://baltocdn.com/helm/stable/debian/`](https://baltocdn.com/helm/stable/debian/) `all main"` `\| sudo tee /etc/apt/sources.list.d/helm-stable-debian.list sudo apt-get update sudo apt-get install helm`  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* Kiểm tra Helm đã cài đặt thành công

| `helm version# Kết quả mong muốn của command# version.BuildInfo{Version:"v3.11.0", GitCommit:"472c5736ab01133de504a826bd9ee12cbe4e7904", GitTreeState:"clean", GoVersion:"go1.18.10"}` |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\


Cài đặt Helm tại các hệ điều hành khác

&#x20;       Tham khảo hướng dẫn cài đặt tại đây: [Install Helm Through Package Managers](https://helm.sh/docs/intro/install/#through-package-managers)

&#x20;       3\. Một số lưu ý thêm về Helm: (tham khảo chi tiết tại: [helm docs](https://helm.sh/docs/helm/helm/))

* Helm sẽ dùng kubeconfig để tương tác với cluster, mặc định helm sẽ dùng config ở đường dẫn: "\~/.kube/config"
* Nếu cần thay đổi đường dẫn tới kubeconfig ta có thể sử dụng 2 cách:
  * Với mỗi command helm ta thêm option --kubeconfig: ví dụ helm install --kubeconfig \<path\_to\_kubeconfig>
  * Khai báo biến môi trường: KUBECONFIG

#### Cài đặt Metric Agent <a href="#kubernetes-caidatmetricagent" id="kubernetes-caidatmetricagent"></a>

&#x20;       Mặc định khi cài đặt vMonitor Platform Metric Agent sẽ có 2 thành phần:

* **Deployment** Agent kube-state-metrics: thu thập metric từng resource của k8s cluster (pod, daemonset, deployment, replicaset, ....)
* **Daemonset** Agent: thu thập metrics từng node k8s cluster (CPU, Memory usage, ...)

&#x20;       1\. Thêm Helm vMonitor Platform Repo

| `helm repo add vmonitor-platform https://vngcloud.github.io/helm-charts-vmonitorhelm repo update` |
| ------------------------------------------------------------------------------------------------- |

&#x20;       2\. Cài đặt chart

* Cài đặt tại **namespace default** (thêm cờ **-n \<namespace\_chỉ\_định>** để cài đặt agent tại namespace khác)

| `helm install` `vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent` `\ --set` `vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \ --set` `vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \ --set` `vmonitor.clusterName=<CLUSTER_NAME>` |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* \<YOUR\_CLIENT\_ID\_XXXXXXXXXXXXXXXXXXX>, \<YOUR\_CLIENT\_SECRET\_XXXXXXXXXXXXXXX>: Thông tin service account đã tạo ở bước chuẩn bị
* &#x20;\<CLUSTER\_NAME>: Thông tin này sẽ dùng để lọc các host của k8s cluster trong trường hợp có nhiều cluster để theo dõi
* Kiểm tra việc install agent thành công

| `# Chạy command và đảm bảo output là các pods ở trạng thái runningkubectl get pod \| grep "vmonitor-metric-agent"` |
| ------------------------------------------------------------------------------------------------------------------ |

&#x20;     **Sau khi cài đặt hoàn tất, metric theo dõi kubernetes đã được đẩy về vMonitor Platform site , bạn có thể tiến hành lên vMonitor để vẽ các dashboard, widget.**

#### Gỡ cài đặt Metric Agent <a href="#kubernetes-gocaidatmetricagent" id="kubernetes-gocaidatmetricagent"></a>

Thực hiện command sau để xóa các k8s resources liên quan đã cài đặt:

| `helm uninstall vmonitor-metric-agent` |
| -------------------------------------- |

#### Cài đặt Metric Agent không sử dụng kube-state-metrics <a href="#kubernetes-caidatmetricagentkhongsudungkube-state-metrics" id="kubernetes-caidatmetricagentkhongsudungkube-state-metrics"></a>

* Cài đặt tại **namespace default** (thêm cờ **-n \<namespace\_chỉ\_định>** để cài đặt agent tại namespace khác)

| `helm install` `vmonitor-metric-agent vmonitor-platform/vmonitor-metric-agent` `\ --set` `vmonitor.iamClientID=<YOUR_CLIENT_ID_XXXXXXXXXXXXXXXXXXX> \ --set` `vmonitor.iamClientSecret=<YOUR_CLIENT_SECRET_XXXXXXXXXXXXXXX> \ --set` `vmonitor.clusterName=<CLUSTER_NAME> \ --set` `vmonitor.kubeStateMetricsEnabled=false` `\ --set` `kubeStateMetricsAgent.enabled=false` |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

***

### Monitor Kubernetes(k8s) tại vMonitor Platform  <a href="#kubernetes-monitorkubernetes-k8s-taivmonitorplatform" id="kubernetes-monitorkubernetes-k8s-taivmonitorplatform"></a>

Để thực hiện monitor Kubernetes(k8s) tại vMonitor Platform, vui lòng thực hiện theo hướng dẫn bên dưới:

**Bước 1**: Cài đặt helm từ APT đối với **hệ điều hành Debian/Ubuntu,** bạn nên cài đặt Helm trên máy có kubeconfig và có đủ quyền để truy cập lên Kubernetes Cluster bạn cần theo dõi

* Thực hiện những command sau&#x20;

| `curl https://baltocdn.com/helm/signing.asc \| gpg --dearmor \| sudo tee /usr/share/keyrings/helm.gpg > /dev/null sudo apt-get install apt-transport-https --yes echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg]` [`https://baltocdn.com/helm/stable/debian/`](https://baltocdn.com/helm/stable/debian/) `all main"` `\| sudo tee /etc/apt/sources.list.d/helm-stable-debian.list sudo apt-get update sudo apt-get install helm`  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Đối với những hệ điều hành khác** có thể tham khảo hướng dẫn cài đặt tại đây: [Install Helm Through Package Managers](https://helm.sh/docs/intro/install/#through-package-managers)&#x20;

* Kiểm tra helm đã được cài đặt thành công bằng command&#x20;

| `helm version`  |
| --------------- |

**Bước 2**: Kiểm tra quyền tương tác với cluster k8s

* Một số lưu ý về helm: (tham khảo chi tiết tại: [helm docs](https://helm.sh/docs/helm/helm/))
  * Helm sẽ dùng kubeconfig để tương tác với cluster, mặc định helm sẽ dùng config ở đường dẫn: "\~/.kube/config"
  * Nếu cần thay đổi đường dẫn tới kubeconfig ta có thể sử dụng 2 cách:
    * Với mỗi command helm ta thêm option --kubeconfig: ví dụ helm install --kubeconfig \<path\_to\_kubeconfig>
    * Khai báo biến môi trường: KUBECONFIG
* Kiểm tra quyền:
  * Sử dụng command kubectl:

Kube check permission

| `# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace defaultkubectl auth can-i '*'` `'*'# Lệnh dùng để kiểm tra quyền tương tác tất cả resource tại namespace kube-systemkubectl auth can-i -n kube-system '*'` `'*'# Lệnh dùng để kiểm tra quyền tạo clusterrole và clusterrolebindingkubectl auth can-i create clusterrolekubectl auth can-i create clusterrolebinding` |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Nếu kết quả các command trên ra YES thì bạn đã đủ quyền để thực hiện các bước tiếp theo

**Bước 3**: Cài đặt kube-state-metrics bằng helm

\* **Lưu ý**: hiện tại vMonitor metric agent chỉ hỗ trợ kube-state-metrics version <= v2.7.0

| `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts helm repo update helm install -n kube-system kube-state-metrics prometheus-community/kube-state-metrics --set image.tag="v2.7.0"`  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* Kiểm tra install kube-state-metrics thành công

| `# Chạy command và đảm bảo output là các pods ở trạng thái runningkubectl get pod -n kube-system \| grep kube-state-metrics` |
| ---------------------------------------------------------------------------------------------------------------------------- |

\


**Bước 4**: Cài đặt vmonitor metric agent bằng helm&#x20;

Mặc định, vMonitor metric agent sẽ có 2 thành phần: deployment dùng để thu thập kube-state-metrics và thành phần daemonset để thu thập metrics từng node k8s&#x20;

* Thêm vMonitor helm repository

| `helm repo add vmonitor https://vngcloud.github.io/helm-charts-vmonitor/helm repo update`  |
| ------------------------------------------------------------------------------------------ |

* Cài đặt vmonitor-metric-agent từ helm repository, mặc định sẽ được cài đặt ở namespace:default, nếu bạn muốn cài ở namespace khác, thì thêm option –n ở command bên dưới, để lấy **API\_Key** bạn tham khảo hướng dẫn: [Hướng dẫn tạo và lấy API\_KEY](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555663), bạn có thể thay đổi tên **vng-vmonitor-metric-agent** thành bất kì tên nào bạn muốn và đổi **k8s-cluster-name** thành tên Kubernetes Cluster của bạn

| `helm install vmonitor-metric-agent --set vmonitor.apiKey=<API_KEY> --set vmonitor.clusterName=k8s-cluster vmonitor/vmonitor-metric-agent`  |
| ------------------------------------------------------------------------------------------------------------------------------------------- |

* Kiểm tra việc install agent thành công

| `# Chạy command và đảm bảo output là các pods ở trạng thái runningkubectl get pod \| grep "vmonitor-metric-agent"` |
| ------------------------------------------------------------------------------------------------------------------ |

\


**Bước 5: sau khi cài đặt xong tất cả metric theo dõi kubernetes đã được đẩy về, bạn có thể tiến hành lên vMonitor để vẽ các dashboard, widget.**

(Optional) Nếu không còn nhu cầu sử dụng vmonitor metric agent bạn có thể thực hiện gỡ cài đặt bằng command bên dưới

| `helm uninstall vmonitor-metric-agent` |
| -------------------------------------- |

**Lưu ý**&#x20;

* Khi monitor Kubernetes với vMonitor, hiện tại bạn chỉ bị tính tiền số lượng Host vào Quota, số lượng Host sẽ được tính bằng số lượng kubelet worker node bạn đang có cộng thêm 1. Số lượng Container trên mỗi Host sẽ chưa được tính vào thời điểm này.&#x20;
