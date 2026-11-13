# Giới hạn outbound cho worker node VKS

Theo mặc định, worker node của cluster VKS được phép truy cập outbound tới mọi destination. Tài liệu này hướng dẫn cấu hình bộ outbound rule **tối thiểu để cluster VKS hoạt động ổn định**. Các destination mà ứng dụng của bạn truy cập không thuộc phạm vi bộ rule này; bạn cần tự bổ sung (xem lưu ý tại Bước 2).

- **Phạm vi áp dụng:** **private cluster** sử dụng CNI Cilium overlay. Với Calico hoặc Cilium native routing, các bước vẫn áp dụng được; chỉ khác các port giữa các node ở Bước 2 (cách xác định được nêu tại đó).
- **Không áp dụng cho public cluster:** node truy cập dịch vụ VNG Cloud qua public domain, IP address có thể thay đổi bất kỳ lúc nào nên không thể lọc bằng Security Group.
- **Chỉ cần giới hạn egress của pod:** sử dụng `CiliumNetworkPolicy` egress. Phương án này hỗ trợ lọc theo domain (FQDN) và không ảnh hưởng tới các system component.
- **Trách nhiệm:** bạn chịu trách nhiệm quản lý và duy trì bộ outbound rule. Thiếu rule có thể khiến node mới không join được cluster, không pull được image, không tạo được volume hoặc load balancer.

## Kiến thức cần nắm

- Outbound traffic của node được cho phép nếu **bất kỳ** Security Group (SG) nào gắn trên VM cho phép. Do đó cần loại bỏ rule outbound allow-all trên **tất cả** SG gắn trên node, không chỉ SG của cluster.
- SG hoạt động theo cơ chế stateful: chỉ cần khai báo rule theo chiều outbound, return traffic được tự động cho phép.
- Mỗi SG khi tạo mới đều có sẵn 2 default rule outbound allow-all: `any → 0.0.0.0/0` và `any → ::/0`.

Các SG thường gắn trên node VKS:

| SG | Định dạng tên | Thao tác cần thực hiện |
| --- | --- | --- |
| Node SG của cluster | `vks-user-<user ID>-k8s-<cluster ID>-…` | Thêm allow rule, xoá 2 default rule (Bước 2–3) |
| SG của load balancer | `vks-<cluster ID rút gọn>-<namespace>-<tên Service/Ingress>-…` | Tắt outbound bằng annotation (mục tiếp theo) |
| SG do bạn tự gắn | Theo tên bạn đặt | Xoá 2 default rule |

## Tắt outbound trên SG của load balancer

GreenNode LoadBalancer Controller tạo một SG cho mỗi Service `LoadBalancer` và Ingress, sau đó attach SG này lên node. Theo mặc định, SG này allow-all outbound; nếu xoá thủ công, controller sẽ tạo lại. Để tắt, thêm annotation sau vào **tất cả** Service `LoadBalancer` và Ingress:

```yaml
metadata:
  annotations:
    vks.vngcloud.vn/enable-default-egress: "false"
```

Controller sẽ gỡ 2 outbound rule khỏi SG tương ứng mà không gây downtime cho load balancer. Khi gỡ annotation, 2 rule này được tạo lại.

> **Không xoá outbound rule trực tiếp trên portal** đối với SG do controller quản lý: controller sẽ tạo lại các rule này ở lần đồng bộ định kỳ kế tiếp. Luôn dùng annotation.

Annotation yêu cầu GreenNode LoadBalancer Controller phiên bản `0.5.0` trở lên; nếu cluster đang chạy phiên bản cũ hơn, cần upgrade trước. Kiểm tra phiên bản hiện tại:

```bash
kubectl -n kube-system get deploy -l app.kubernetes.io/name=vngcloud-load-balancer-controller \
  -o jsonpath='{.items[0].spec.template.spec.containers[0].image}'; echo
```

**Áp dụng cho mọi Service/Ingress, kể cả các resource tạo mới sau này.** Chỉ cần một Service `LoadBalancer` hoặc Ingress thiếu annotation, outbound của toàn bộ node sẽ được mở lại. Liệt kê các resource còn thiếu annotation (output rỗng nghĩa là đã đầy đủ):

```bash
kubectl get svc -A -o jsonpath='{range .items[?(@.spec.type=="LoadBalancer")]}{.metadata.namespace}/{.metadata.name} {.metadata.annotations.vks\.vngcloud\.vn/enable-default-egress}{"\n"}{end}' | awk '$2!="false"'
kubectl get ingress -A -o jsonpath='{range .items[*]}{.metadata.namespace}/{.metadata.name} {.spec.ingressClassName}{.metadata.annotations.kubernetes\.io/ingress\.class} {.metadata.annotations.vks\.vngcloud\.vn/enable-default-egress}{"\n"}{end}' | awk '$2=="vngcloud" && $3!="false"'
```

## Bước 1: Thu thập thông số cluster

IP address khác nhau giữa các cluster, vì vậy cần thu thập thông số riêng cho từng cluster. Tạo một debug pod trên node (yêu cầu kubectl 1.28 trở lên; lệnh sử dụng image Cilium có sẵn trên node do private cluster thường không truy cập được Docker Hub):

```bash
NODE=$(kubectl get nodes -o jsonpath='{.items[0].metadata.name}')
IMG=$(kubectl -n kube-system get ds cilium -o jsonpath='{.spec.template.spec.containers[0].image}')
kubectl debug node/$NODE -it --profile=sysadmin --image=$IMG -- chroot /host bash -c '
  echo "## control plane"; grep "server:" /etc/kubernetes/kubelet.conf
  echo "## endpoints"; for h in iamapis.vngcloud.vn hcm-3.api.vngcloud.vn hcm03.vstorage.vngcloud.vn vcr.vngcloud.vn; do
    getent ahosts $h | cut -d" " -f1 | sort -u | sed "s/^/$h /"; done
  echo "## dns";   resolvectl status | grep -E "DNS Servers|Current DNS"
  echo "## ntp";   timedatectl show-timesync -p ServerAddress -p SystemNTPServers
  echo "## dhcp";  networkctl status eth0 | grep "DHCP4 via"'
kubectl get pods -o name | grep node-debugger | xargs kubectl delete
```

Ghi nhận các giá trị sau:

| Thông số | Ví dụ | Nguồn |
| --- | --- | --- |
| VPC CIDR | `10.0.0.0/16` | Portal VPC (CIDR của VPC, không phải của subnet) |
| Control plane IP | `10.0.1.3` | Mục `## control plane`. Nếu là hostname, chạy `getent ahosts <hostname>` trên node và lấy toàn bộ IP |
| Private endpoint IP | `10.0.1.6` … `10.0.1.9` | Mục `## endpoints`: IAM (`iamapis…`), vServer API (`…api…`), vStorage (`…vstorage…`), vCR (`vcr…`). Cluster multi-AZ có một IP cho mỗi zone, cần lấy toàn bộ. Domain trong lệnh là của region HCM; region khác xem trang Private Service Endpoint trên portal |
| DNS resolver | `8.8.8.8` | Mục `## dns`, lấy toàn bộ IP |
| NTP server | IP NTP server nội bộ | Mục `## ntp`. Nếu là public pool (ví dụ `ntp.ubuntu.com`), IP thay đổi liên tục: chuyển sang NTP server nội bộ hoặc mở `UDP 123 → 0.0.0.0/0` |
| DHCP server | `10.0.1.2` | Mục `## dhcp` |

## Bước 2: Tạo bộ outbound rule

Thêm các rule dưới đây vào **node SG**: trên portal vServer, vào **Security Groups**, chọn SG có tên dạng `vks-user-<user ID>-k8s-<cluster ID>-…`, mở danh sách rule **Outbound** và thêm rule. Giá trị trong `< >` lấy từ Bước 1, mỗi IP tương ứng một rule dạng `/32`. Cột "Type" là rule type cần chọn trên portal. Lưu ý: type **DNS** trên portal chỉ mở TCP, vì vậy cần thêm một rule **Custom UDP** cho DNS.

**Phương án 1 (khuyến nghị): allow toàn bộ traffic trong VPC, chặn traffic ra ngoài VPC.**

| # | Type | Port | Destination | Mục đích |
| --- | --- | --- | --- | --- |
| 1 | All Traffic | – | `<VPC CIDR>` | Control plane, private endpoint, DHCP, traffic giữa các node |
| 2 | HTTP | 80 | `169.254.169.254/32` | Metadata service, dùng khi node bootstrap và khi CSI/LB controller khởi động |
| 3 | DNS **và** Custom UDP | 53 | `<DNS resolver>/32` | DNS resolution |
| 4 | Custom UDP | 123 | `<NTP server>/32` | Time sync |

Xác nhận control plane IP, 4 private endpoint IP và DHCP server đều thuộc `<VPC CIDR>`. IP nào nằm ngoài range này cần thêm rule riêng theo bảng của Phương án 2. Nếu DNS resolver và NTP server thuộc VPC thì không cần rule 3 và 4.

<details>
<summary>Phương án 2: chỉ mở các port cần thiết (thay cho rule 1)</summary>

| Type | Port | Destination | Mục đích |
| --- | --- | --- | --- |
| Custom TCP | 6443 | `<Control plane IP>/32` | Kubernetes API server |
| Custom TCP | 8132 | `<Control plane IP>/32` | `kubectl logs/exec`, admission webhook |
| HTTPS | 443 | `<IAM endpoint IP>/32` | Authentication cho CSI và LB controller |
| HTTPS | 443 | `<vServer API endpoint IP>/32` | Attach volume, tạo load balancer |
| HTTPS | 443 | `<vCR endpoint IP>/32` | Pull system image |
| HTTPS | 443 | `<vStorage endpoint IP>/32` | vStorage |
| Custom UDP | 67 | `<DHCP server>/32` | DHCP lease renewal. Thiếu rule này, node vẫn nhận IP khi khởi động nhưng không renew lease định kỳ được |
| Custom UDP | 8472 | `<VPC CIDR>` | VXLAN tunnel giữa các node (pod-to-pod traffic) |
| Custom TCP | 4240 | `<VPC CIDR>` | Cilium health check |
| All ICMP | – | `<VPC CIDR>` | Health check, Path MTU Discovery |
| Custom TCP | 10250 | `<VPC CIDR>` | Kubelet API giữa các node |
| Custom TCP | 4244 | `<VPC CIDR>` | Hubble |

Bốn rule cuối với destination `<VPC CIDR>` áp dụng cho Cilium overlay. Với CNI khác, sao chép các inbound rule mà VKS đã tạo trên node SG sang chiều outbound (cùng protocol, cùng port, destination `<VPC CIDR>`).

</details>

> **Lưu ý về destination của ứng dụng.** Bộ rule trên chỉ đáp ứng nhu cầu của cluster VKS. Sau khi xoá default outbound rule, mọi connection từ ứng dụng tới destination **ngoài VPC** (với Phương án 2 là cả destination trong VPC) sẽ bị chặn nếu không có rule tương ứng, ví dụ: database hoặc API ngoài VPC, image registry private hoặc public (Docker Hub, ghcr.io…), Git, logging/monitoring backend, dịch vụ SaaS. Hãy rà soát và bổ sung rule cho các destination này trước khi apply.
>
> Các destination sử dụng CDN (Docker Hub, ghcr.io, quay.io và phần lớn dịch vụ SaaS) thay đổi IP liên tục, nên rule theo IP sẽ mất hiệu lực sau một thời gian ngắn. Khuyến nghị mirror image về vCR, và truy cập dịch vụ SaaS qua proxy hoặc `CiliumNetworkPolicy` `toFQDNs`.

## Bước 3: Apply

Nguyên tắc: thêm allow rule trước, xoá rule allow-all sau cùng. Thực hiện trên cluster dev/staging có cùng cấu hình trước khi apply cho production.

1. Backup cấu hình hiện tại: danh sách SG trên từng VM node và toàn bộ rule của các SG đó.
2. Thêm toàn bộ rule ở Bước 2, cùng các rule cho destination của ứng dụng, vào node SG. Chưa xoá rule nào.
3. Thêm annotation `enable-default-egress: "false"` vào tất cả Service `LoadBalancer` và Ingress (xem mục "Tắt outbound trên SG của load balancer"). Bước này phải thực hiện **sau** bước 2: nếu node SG còn thiếu rule và cluster đang hoạt động nhờ outbound của SG load balancer, việc tắt outbound này sẽ gây downtime ngay lập tức.
4. Trong maintenance window (khung giờ thấp điểm), xoá 2 default outbound rule (`::/0` trước, `0.0.0.0/0` sau) trên node SG và các SG bạn tự gắn.
5. Verify ngay theo Bước 4. Nếu phát sinh lỗi, rollback trước rồi mới điều tra nguyên nhân.

Các connection đang mở có thể tiếp tục hoạt động; chỉ các connection **mới** bị chặn. Cần monitor ít nhất một chu kỳ nghiệp vụ. Cluster tạo mới hoặc tạo lại sẽ có node SG mới, cần thực hiện lại từ Bước 1.

## Bước 4: Verify

- [ ] **Xác nhận outbound đã bị chặn:** connection tới một destination không có trong rule phải bị timeout: `kubectl run egresstest --rm -it --restart=Never --image=<image có curl> -- curl -m 5 -sS https://1.1.1.1`. Nếu VPC không có route ra internet, phép thử này luôn timeout và không có ý nghĩa; khi đó hãy thử với một destination trong VPC chưa được mở rule.
- [ ] Tất cả node ở trạng thái `Ready`; `kubectl logs`, `kubectl exec` hoạt động bình thường.
- [ ] DNS resolution trong pod hoạt động với cả internal domain của cluster và external domain mà ứng dụng sử dụng.
- [ ] Pull được image mới (deploy thử với `imagePullPolicy: Always`).
- [ ] Restart CSI và LB controller, các pod chuyển sang `Running`: `kubectl -n kube-system get deploy,ds -o name | grep -E 'csi|load-balancer' | xargs -n1 kubectl -n kube-system rollout restart`
- [ ] Tạo được PVC và mount vào pod.
- [ ] Tạo được Service `LoadBalancer` có annotation và nhận được external address; thực hiện lại phép thử ở mục đầu tiên: kết quả vẫn timeout.
- [ ] DHCP lease renewal thành công: trong debug pod ở Bước 1, chạy `networkctl renew eth0`; sau vài giây, `ip -4 addr show eth0` hiển thị `valid_lft` trở về gần lease time đầy đủ (thường là 86400s).
- [ ] Scale node group thêm 1 node: node mới chuyển sang `Ready` trong thời gian bình thường. Sau đó scale về như cũ.
- [ ] Ứng dụng hoạt động đúng nghiệp vụ: database connection, API call, đẩy log và metric, scheduled job.

## Rollback

Thêm lại rule sau vào node SG để đưa cluster về trạng thái ban đầu, không cần restart node hay pod:

| Type | Port | Destination |
| --- | --- | --- |
| All Traffic | – | `0.0.0.0/0` |

Pod gặp lỗi trong thời gian thiếu rule sẽ tự retry. Node được tạo trong thời gian thiếu rule (ví dụ khi scale) không tự phục hồi sau khi thêm rule rollback; cần thay thế node đó. Sau khi xác định và bổ sung rule còn thiếu, xoá rule rollback.

## Troubleshooting

| Symptom | Nguyên nhân thường gặp |
| --- | --- |
| Node mới không chuyển sang `Ready`, liên tục bị thay thế | Thiếu rule tới metadata service `169.254.169.254`, control plane (6443), vCR hoặc DNS |
| CSI hoặc LB controller ở trạng thái `CrashLoopBackOff` | Thiếu rule tới metadata service, IAM hoặc vServer API |
| Pod trên các node khác nhau không kết nối được với nhau, node `NotReady` | Thiếu rule giữa các node (UDP 8472, TCP 4240, ICMP) |
| `kubectl logs/exec` bị timeout | Thiếu rule TCP 8132 tới control plane |
| `ImagePullBackOff` | Thiếu rule tới vCR (system image) hoặc registry chứa image của ứng dụng |
| PVC ở trạng thái `Pending`, Service `LoadBalancer` không nhận được external address | Thiếu rule tới IAM hoặc vServer API |
| Lỗi TLS certificate "not yet valid"/"expired" sau vài ngày | Thiếu rule tới NTP server |
| `networkctl renew eth0` trên node không renew được lease | Thiếu rule DHCP (UDP 67) |
| Đã xoá rule nhưng node vẫn truy cập được internet | Còn SG khác allow outbound, thường là SG của Service/Ingress thiếu annotation `enable-default-egress: "false"` |
| Ứng dụng không kết nối được tới database, API, registry… ngoài VPC | Thiếu rule cho destination của ứng dụng (xem lưu ý tại Bước 2) |
