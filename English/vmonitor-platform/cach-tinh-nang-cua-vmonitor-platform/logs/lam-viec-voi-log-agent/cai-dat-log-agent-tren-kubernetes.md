# Install Log Agent on Kubernetes

Before installing the agent on the operating systems we support below, you need to download the certificate according to the instructions at [Initialize Certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/logs/lam-viec-voi-log-agent/khoi-tao-certificate) . Information on setting up the agent is in the readme file, and the instruction scripts are also in the downloaded certificate file. Use this information with the instructions below to complete Agent for Log setup.

**Setting**

You can install the agent using Kubectl.

The goal when deploying in a k8s environment is usually to push the logs of all other pods. Therefore, we should deploy the agent as [a daemon-set](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) .

**Kubectl**

* After initializing the Certificate, you will save the user authentication information to the k8s master node (or any machine that has kubectl and has execute rights on kubernetes).
* Move to the agent you want to install, k8s / kubectl folder. Run command:

| <p>Copy</p><pre><code>kubectl apply -f namespace.yml
kubectl apply -f configmap.yml
kubectl apply -f secret.yml
kubectl apply -f daemonset.yml
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ |

In order for the gent log to be able to read the logs of other pods, you need to repair your computer and disable selinux. On [the k8s home page](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) , it is also specified to disable selinux with centos. On k8s nodes, run the command:

| <p>Copy</p><pre><code>setenforce 0
</code></pre> |
| ------------------------------------------------ |

and go to the file `/etc/sysconfig/selinux`to edit `SELINUX=enforcing`and become `SELINUX=disabled`.

The configuration files below have been prepared by us in the script when downloading the certificate. The description below helps readers imagine what it would be like if we created a manual.

**Configuration**

You need to edit the {parts in brackets} in the files below to suit your environment:

Filebeat

| <ul><li>File<code>namespace.yml.</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre></td></tr></tbody></table><ul><li>File configmap.yml. For example, the configuration below will push all pod logs in <strong>the web-app namespace</strong> to the system</li><li><code>{$BOOTSTRAP_SERVERS}, {$TOPIC}</code>Read the <a href="http://info.md/">info.md</a> ​​file in the downloaded certificate folder.</li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
data:
  filebeat.yml: >-
    filebeat.inputs:
    - type: log
      paths:
        - /var/log/pods/*/*/*.log

    output.kafka:
      hosts: {$BOOTSTRAP_SERVERS}
      topic: {$TOPIC}
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
</code></pre></td></tr></tbody></table><ul><li>File<code>secret.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: filebeat
data:
  VNG.trust.pem: {$vng.trust.pem}
  user.cer.pem: {$user.cer.pem}
  user.key.pem: {$user.key.pem}
type: Opaque
</code></pre></td></tr></tbody></table><ul><li><code>$vng.trust.pem, $user.cer.pem, $user.key.pem</code> The content is md5 hash of the corresponding files in the certificate directory or create a secret with --from-file cert</li><li>File<code>daemonset.yml</code></li></ul><table data-header-hidden><thead><tr><th></th></tr></thead><tbody><tr><td><p>Copy</p><pre><code>apiVersion: apps/v1
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
</code></pre></td></tr></tbody></table> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Copy</p><pre><code>apiVersion: v1
kind: Namespace
metadata:
  name: agent-vmonitor-platform
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| <p>Copy</p><pre><code>apiVersion: v1
kind: ConfigMap
metadata:
  name: filebeat
  namespace: agent-vmonitor-platform
data:
  filebeat.yml: >-
    filebeat.inputs:
    - type: log
      paths:
        - /var/log/pods/*/*/*.log

    output.kafka:
      hosts: {$BOOTSTRAP_SERVERS}
      topic: {$TOPIC}
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
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| <p>Copy</p><pre><code>apiVersion: v1
kind: Secret
metadata:
  namespace: agent-vmonitor-platform
  name: filebeat
data:
  VNG.trust.pem: {$vng.trust.pem}
  user.cer.pem: {$user.cer.pem}
  user.key.pem: {$user.key.pem}
type: Opaque
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| <p>Copy</p><pre><code>apiVersion: apps/v1
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
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
