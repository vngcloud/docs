# Cài đặt Log Agent trên Kubernetes

Trước khi thực hiện cài đặt agent trên các hệ điều hành mà chúng tôi hỗ trợ bên dưới, bạn cần phải tải xuống certificate theo hướng dẫn tại [Khởi tạo Certificate](khoi-tao-certificate.md). Thông tin hướng dẫn thiết lập agent nằm trong file readme, các script hướng dẫn cũng nằm trong tệp tin certificate được tải về. Sử dụng thông tin này với các hướng dẫn bên dưới để hoàn thành việc thiết lập Agent for Log.

#### Cài đặt

Bạn có thể cài đặt agent sử dụng Kubectl.

Mục tiêu khi triển khai trong môi trường k8s thường là để đẩy log của tất cả các pods khác. Do vậy ta nên triển khai agent dưới dạng [daemon-set](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

#### Kubectl

* [Tải certificate ](https://vngctech.atlassian.net/wiki/spaces/VP/pages/847970312)lấy thông tin xác thực user, lưu vào vào k8s master node (hoặc bất kỳ máy nào lưu đang có kubectl và có quyền excute trên kubernetes).
* Di chuyển vào agent muốn cài, thư mục k8s / kubectl. Chạy lệnh:

| <pre><code>kubectl apply -f namespace.yml
kubectl apply -f configmap.yml
kubectl apply -f secret.yml
kubectl apply -f daemonset.yml
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |

Để log gent có thể dọc được log của các pod khác bạn cần sửa máy bạn cần disable selinux. Trên [trang chủ k8s ](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)cũng chỉ định disable selinux với centos\
Trên các k8s node chạy lệnh:

| <pre><code>setenforce 0
</code></pre> |
| ------------------------------------- |

và vào file `/etc/sysconfig/selinux` để sửa `SELINUX=enforcing` và thành `SELINUX=disabled`.

Các file cấu hình dưới đều đã được chúng tôi chuẩn bị sẵn tại script khi tải certificate về, mô tả dưới đây giúp người đọc hình dung được nếu tạo manual sẽ thế nào.

#### Cấu hình

| <ul><li>File <code>namespace.yml.</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre></td></tr></tbody></table><ul><li>File configmap.yml. Ví dụ như cấu hình dưới đây sẽ đẩy tất cả log của pod trong <strong>namespace web-app</strong> về hệ thống</li><li><code>$BOOTSTRAP_SERVERS, $TOPIC</code> đọc tại file <a href="http://info.md/">info.md</a> thư mục certificate đã tải về.</li></ul><p><br></p><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
data:
  filebeat.yml: >-
    filebeat.inputs:
    - type: log
      paths:
        - /var/log/pods/web-app*/*/*.log

    output.kafka:
      hosts: ${BOOTSTRAP_SERVERS}
      topic: ${TOPIC}
      partition.round_robin:
        reachable_only: false
      required_acks: 1
      compression: gzip
      max_message_bytes: 1000000
      ssl.certificate_authorities:
        - /usr/share/filebeat/VNG.trust.pem
      ssl.certificate: /usr/share/filebeat/user.cer.pem
      ssl.key: /usr/share/filebeat/user.key.pem
      ssl.verification_mode: "none"
    logging.level: info
    logging.to_files: true
    logging.files:
      path: /var/log/filebeat
      name: filebeat
      keepfiles: 7
      permissions: 0644
</code></pre></td></tr></tbody></table><p><br></p><ul><li>File <code>secret.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: filebeat
data:
  VNG.trust.pem: $vng.trust.pem
  user.cer.pem: $user.cer.pem
  user.key.pem: $user.key.pem
type: Opaque
</code></pre></td></tr></tbody></table><ul><li><code>$vng.trust.pem, $user.cer.pem, $user.key.pem</code> có nội dung là md5 hash các file tương ứng tại thư mục certificate hoặc tạo secret bằng --from-file cert</li><li>File <code>daemonset.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
  labels:
    app: filebeat
spec:
  selector:
    matchLabels:
      app: filebeat
  template:
    metadata:
      name: filebeat
      labels:
        app: filebeat
    spec:
      containers:
        - name: filebeat
          image: docker.elastic.co/beats/filebeat:8.7.0
          imagePullPolicy: IfNotPresent
          volumeMounts:
            - name: config
              mountPath: /usr/share/filebeat/filebeat.yml
              subPath: filebeat.yml
            - name: certificate
              mountPath: /usr/share/filebeat/VNG.trust.pem
              subPath: VNG.trust.pem
            - name: certificate
              mountPath: /usr/share/filebeat/user.cer.pem
              subPath: user.cer.pem
            - name: certificate
              mountPath: /usr/share/filebeat/user.key.pem
              subPath: user.key.pem
            - name: varlog
              mountPath: /var/log/
              readOnly: true
            - name: varlibdockercontainers
              mountPath: /var/lib/docker/containers
              readOnly: true
          resources:
            limits:
              cpu: '1'
              memory: 2Gi
      volumes:
        - name: varlog
          hostPath:
            path: /var/log/
        - name: varlibdockercontainers
          hostPath:
            path: /var/lib/docker/containers

        - name: config
          configMap:
            name: filebeat
            items:
              - key: filebeat.yml
                path: filebeat.yml

        - name: certificate
          secret:
            secretName: filebeat
            items:
              - key: VNG.trust.pem
                path: VNG.trust.pem
              - key: user.cer.pem
                path: user.cer.pem
              - key: user.key.pem
                path: user.key.pem
      securityContext:
        runAsUser: 0
      restartPolicy: Always
      tolerations:
        - key: vmonitor-log
          operator: Equal
          value: 'true'
          effect: NoSchedule
</code></pre></td></tr></tbody></table><p><br></p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| <pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
data:
  filebeat.yml: >-
    filebeat.inputs:
    - type: log
      paths:
        - /var/log/pods/web-app*/*/*.log

    output.kafka:
      hosts: ${BOOTSTRAP_SERVERS}
      topic: ${TOPIC}
      partition.round_robin:
        reachable_only: false
      required_acks: 1
      compression: gzip
      max_message_bytes: 1000000
      ssl.certificate_authorities:
        - /usr/share/filebeat/VNG.trust.pem
      ssl.certificate: /usr/share/filebeat/user.cer.pem
      ssl.key: /usr/share/filebeat/user.key.pem
      ssl.verification_mode: "none"
    logging.level: info
    logging.to_files: true
    logging.files:
      path: /var/log/filebeat
      name: filebeat
      keepfiles: 7
      permissions: 0644
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| <pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: filebeat
data:
  VNG.trust.pem: $vng.trust.pem
  user.cer.pem: $user.cer.pem
  user.key.pem: $user.key.pem
type: Opaque
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <pre><code>apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
  labels:
    app: filebeat
spec:
  selector:
    matchLabels:
      app: filebeat
  template:
    metadata:
      name: filebeat
      labels:
        app: filebeat
    spec:
      containers:
        - name: filebeat
          image: docker.elastic.co/beats/filebeat:8.7.0
          imagePullPolicy: IfNotPresent
          volumeMounts:
            - name: config
              mountPath: /usr/share/filebeat/filebeat.yml
              subPath: filebeat.yml
            - name: certificate
              mountPath: /usr/share/filebeat/VNG.trust.pem
              subPath: VNG.trust.pem
            - name: certificate
              mountPath: /usr/share/filebeat/user.cer.pem
              subPath: user.cer.pem
            - name: certificate
              mountPath: /usr/share/filebeat/user.key.pem
              subPath: user.key.pem
            - name: varlog
              mountPath: /var/log/
              readOnly: true
            - name: varlibdockercontainers
              mountPath: /var/lib/docker/containers
              readOnly: true
          resources:
            limits:
              cpu: '1'
              memory: 2Gi
      volumes:
        - name: varlog
          hostPath:
            path: /var/log/
        - name: varlibdockercontainers
          hostPath:
            path: /var/lib/docker/containers

        - name: config
          configMap:
            name: filebeat
            items:
              - key: filebeat.yml
                path: filebeat.yml

        - name: certificate
          secret:
            secretName: filebeat
            items:
              - key: VNG.trust.pem
                path: VNG.trust.pem
              - key: user.cer.pem
                path: user.cer.pem
              - key: user.key.pem
                path: user.key.pem
      securityContext:
        runAsUser: 0
      restartPolicy: Always
      tolerations:
        - key: vmonitor-log
          operator: Equal
          value: 'true'
          effect: NoSchedule
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

\


| <ul><li>File <code>namespace.yml.</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre></td></tr></tbody></table><ul><li>File <code>configmap.yml.</code> Ví dụ như cấu hình dưới đây sẽ đẩy tất cả log của pod trong <strong>namespace web-app</strong> về hệ thống</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: logstash
  namespace: agent-vmonitor-platform
data:
  logstash.conf: >-
    input {
        file {
            start_position => "beginning"
            path => [ "/var/log/pods/web-app*/*/*.log"]
        }
    }

    output {
          kafka {
            codec => json
            bootstrap_servers => "$BOOTSTRAP_SERVER"
            topic_id => "$TOPIC"
            security_protocol => "SSL"
            ssl_truststore_location => "/usr/share/logstash/VNG.trust"
            ssl_truststore_password => "$TRUTSTORE_PASS"
            ssl_keystore_location => "/usr/share/logstash/user.key"
            ssl_keystore_password => "$USER_PASS"
            ssl_key_password => "$USER_PASS"
            ssl_endpoint_identification_algorithm => ""
          }
    }
</code></pre></td></tr></tbody></table><ul><li><code>$BOOTSTRAP_SERVERS, $TOPIC, $TRUTSTORE_PASS, $USER_PASS</code> đọc tại file <a href="http://info.md/">info.md</a> thư mục certificate đã tải về</li></ul><ul><li>File <code>secret.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: logstash
data:
  VNG.trust: $vng.trust
  user.key: $user.key
type: Opaque
</code></pre></td></tr></tbody></table><ul><li><code>$vng.trust</code> và <code>$user.key</code> có nội dung là md5 hash các file tương ứng tại thư mục certificate</li></ul><ul><li>File <code>daemonset.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><pre><code>apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: logstash
  namespace: agent-vmonitor-platform
  labels:
    app: logstash
spec:
  selector:
    matchLabels:
      app: logstash
  template:
    metadata:
      name: logstash
      labels:
        app: logstash
    spec:
      containers:
        - name: logstash
          image: docker.elastic.co/logstash/logstash-oss:8.6.2
          imagePullPolicy: IfNotPresent
          volumeMounts:
            - name: config
              mountPath: /usr/share/logstash/pipeline/logstash.conf
              subPath: logstash.conf
            - name: certificate
              mountPath: /usr/share/logstash/VNG.trust
              subPath: VNG.trust
            - name: certificate
              mountPath: /usr/share/logstash/user.key
              subPath: user.key

            - name: varlog
              mountPath: /var/log/
              readOnly: true
            - name: varlibdockercontainers
              mountPath: /var/lib/docker/containers
              readOnly: true
          resources:
            limits:
              cpu: '1'
              memory: 2Gi
      volumes:
        - name: varlog
          hostPath:
            path: /var/log/
        - name: varlibdockercontainers
          hostPath:
            path: /var/lib/docker/containers

        - name: config
          configMap:
            name: logstash
            items:
              - key: logstash.conf
                path: logstash.conf

        - name: certificate
          secret:
            secretName: logstash
            items:
              - key: VNG.trust
                path: VNG.trust
              - key: user.key
                path: user.key
      securityContext:
        runAsUser: 0
      restartPolicy: Always
</code></pre></td></tr></tbody></table><p><br></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| <pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: logstash
  namespace: agent-vmonitor-platform
data:
  logstash.conf: >-
    input {
        file {
            start_position => "beginning"
            path => [ "/var/log/pods/web-app*/*/*.log"]
        }
    }

    output {
          kafka {
            codec => json
            bootstrap_servers => "$BOOTSTRAP_SERVER"
            topic_id => "$TOPIC"
            security_protocol => "SSL"
            ssl_truststore_location => "/usr/share/logstash/VNG.trust"
            ssl_truststore_password => "$TRUTSTORE_PASS"
            ssl_keystore_location => "/usr/share/logstash/user.key"
            ssl_keystore_password => "$USER_PASS"
            ssl_key_password => "$USER_PASS"
            ssl_endpoint_identification_algorithm => ""
          }
    }
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: logstash
data:
  VNG.trust: $vng.trust
  user.key: $user.key
type: Opaque
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| <pre><code>apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: logstash
  namespace: agent-vmonitor-platform
  labels:
    app: logstash
spec:
  selector:
    matchLabels:
      app: logstash
  template:
    metadata:
      name: logstash
      labels:
        app: logstash
    spec:
      containers:
        - name: logstash
          image: docker.elastic.co/logstash/logstash-oss:8.6.2
          imagePullPolicy: IfNotPresent
          volumeMounts:
            - name: config
              mountPath: /usr/share/logstash/pipeline/logstash.conf
              subPath: logstash.conf
            - name: certificate
              mountPath: /usr/share/logstash/VNG.trust
              subPath: VNG.trust
            - name: certificate
              mountPath: /usr/share/logstash/user.key
              subPath: user.key

            - name: varlog
              mountPath: /var/log/
              readOnly: true
            - name: varlibdockercontainers
              mountPath: /var/lib/docker/containers
              readOnly: true
          resources:
            limits:
              cpu: '1'
              memory: 2Gi
      volumes:
        - name: varlog
          hostPath:
            path: /var/log/
        - name: varlibdockercontainers
          hostPath:
            path: /var/lib/docker/containers

        - name: config
          configMap:
            name: logstash
            items:
              - key: logstash.conf
                path: logstash.conf

        - name: certificate
          secret:
            secretName: logstash
            items:
              - key: VNG.trust
                path: VNG.trust
              - key: user.key
                path: user.key
      securityContext:
        runAsUser: 0
      restartPolicy: Always
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |



Trước khi thực hiện cài đặt tác nhân trên các hệ điều hành mà chúng tôi hỗ trợ bên dưới, bạn cần tải xuống chứng chỉ theo hướng dẫn tại Khởi tạo Chứng chỉ. Thông báo hướng dẫn tác nhân thiết lập nằm trong tệp readme, hướng dẫn tập lệnh cũng nằm trong tệp tin chứng chỉ được tải về. Sử dụng thông tin này với các hướng dẫn bên dưới để hoàn thành việc thiết lập Agent for Log.
