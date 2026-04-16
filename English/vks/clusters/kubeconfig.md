# Kubeconfig

**Kubeconfig** is a configuration file that allows the `kubectl` tool to authenticate and connect to your Kubernetes Cluster. Each kubeconfig file contains cluster information (API server address), authentication credentials (client certificate), and a context that identifies which cluster is being used.

On VKS, the kubeconfig file uses the **Client Certificate** mechanism for authentication. You can actively choose the certificate validity period when downloading, providing better security control.

***

## Download Kubeconfig

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2:** On the **Overview** screen, select the **Kubernetes Cluster** menu.

**Step 3:** At the Cluster you want to get the kubeconfig for, click the **Action** icon and select **Download Config File.**

**Step 4:** The system displays a confirmation popup. Here, select the **certificate validity period** for the kubeconfig:

| Validity Period | Description                                                                 |
| --------------- | --------------------------------------------------------------------------- |
| 30 days         | Suitable for staging, testing environments, or temporary access             |
| 90 days         | Suitable for production environments with periodic rotation cycles          |
| 365 days        | Suitable for cases requiring long-term kubeconfig, needs careful management |

<figure><img src="../../.gitbook/assets/Image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**Security notes:**

* The kubeconfig file grants **cluster-admin** privileges to the holder. Do not share this file with unauthorized individuals.
* If you need to **revoke the certificate** before it expires, please contact the VKS support team for assistance.
* If the kubeconfig file is compromised, contact the VKS support team immediately for timely handling.
{% endhint %}

**Step 5:** Click **Confirm** to download. The `config` file will be saved to your machine.

***

## Configure kubectl to Use Kubeconfig

After downloading the kubeconfig file, you need to place it in the correct location for `kubectl` to recognize.

**Step 1:** Create the `.kube` directory if it does not exist:

```bash
mkdir -p ~/.kube
```

**Step 2:** Move the downloaded kubeconfig file to the `.kube` directory and name it `config`:

```bash
mv <path_to_downloaded_file> ~/.kube/config
```

**Step 3:** Verify the connection to the Cluster:

```bash
kubectl get nodes
```

If the connection is successful, you will see the list of nodes in your Cluster.

{% hint style="info" %}
**Using multiple Clusters at once:**

If you need to manage multiple Clusters, you can place the kubeconfig file in a different location and specify the path when running the command:

```bash
kubectl --kubeconfig <path_to_kubeconfig> get nodes
```

Or set an environment variable:

```bash
export KUBECONFIG=<path_to_kubeconfig>
```
{% endhint %}

***

## Managing Certificate Validity

### View the current certificate expiry

**Method 1: View on Portal**

When clicking **Download Config File** on the Kubernetes Cluster screen, the system displays a kubeconfig information popup that includes the certificate validity period. You can view the expiry date directly here before downloading.

<figure><img src="../../.gitbook/assets/Image (5).png" alt=""><figcaption></figcaption></figure>

**Method 2: Check via command**

To check the validity period of the certificate in the kubeconfig file currently in use, run the following command:

```bash
kubectl config view --raw -o jsonpath='{.users[0].user.client-certificate-data}' \
  | base64 --decode \
  | openssl x509 -noout -dates
```

The output will display `notBefore` (start date) and `notAfter` (expiry date) of the certificate.

### Renew Certificate

When the certificate is about to expire (within 7 days), the VKS system will send you a notification. At that point, you can:

<figure><img src="../../.gitbook/assets/Image (6).png" alt=""><figcaption></figcaption></figure>

* **Automatic renewal:** The system automatically renews the certificate if conditions are met. You will receive a confirmation notification when the process is complete.
* **Manual renewal:** If the system cannot automatically renew, you will see a **Renew** button in the notification. Click **Renew** for the system to issue a new certificate.

{% hint style="info" %}
**Note:**

After renewal, you need to download the new kubeconfig file and replace the old one. The certificate will continue to work until the old one expires after renewal.
{% endhint %}

### Re-download New Kubeconfig

Repeat the steps in the [Download Kubeconfig](kubeconfig.md#download-kubeconfig) section to get a new kubeconfig file with a valid certificate.

***

## Kubeconfig Security

Below are security recommendations when using kubeconfig on VKS:

* **Do not commit the kubeconfig file to a source code repository** (Git, GitLab, etc.). Add `~/.kube/config` to the project's `.gitignore`.
*   **Restrict file access permissions:** Ensure only the current user can read the kubeconfig file:

    ```bash
    chmod 600 ~/.kube/config
    ```
* **Choose an appropriate certificate validity period:** Avoid using 365-day certificates for all use cases. Prefer 30 or 90 days and rotate periodically.

***

## Create a Read-only Kubeconfig

The default kubeconfig downloaded from VKS grants **cluster-admin** — full privileges on the cluster. If you need to grant access to other users (developers, auditors, etc.) with **view-only** permissions and no edit rights, create a separate kubeconfig with `view` permissions.

The guide below creates a read-only kubeconfig for the user `readonly-user`. You can replace this name as needed.

### Step 1 — Generate private key and CSR

```bash
openssl genrsa -out readonly-user.key 2048
```

```bash
openssl req -new -key readonly-user.key -out readonly-user.csr -subj "/CN=readonly-user/O=read-only"
```

### Step 2 — Create a CertificateSigningRequest in Kubernetes

**Step 2a — Encode the CSR to base64**

```bash
CSR_BASE64=$(cat readonly-user.csr | base64 | tr -d '\n')
```

**Step 2b — Create the YAML file**

```bash
cat > csr.yaml <<EOF
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: readonly-user
spec:
  request: ${CSR_BASE64}
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 31536000
  usages:
  - client auth
EOF
```

**Step 2c — Apply the file**

```bash
kubectl apply -f csr.yaml
```

### Step 3 — Approve the CSR

```bash
kubectl certificate approve readonly-user
```

### Step 4 — Retrieve the signed certificate

```bash
kubectl get csr readonly-user -o jsonpath='{.status.certificate}' | base64 -d > readonly-user.crt
```

### Step 5 — Bind RBAC for the user

```bash
kubectl create clusterrolebinding readonly-user-binding \
  --clusterrole=view \
  --user=readonly-user
```

### Step 6 — Create the kubeconfig file

**Step 6a — Retrieve cluster information**

```bash
CLUSTER_SERVER=$(kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}')
CLUSTER_CA=$(kubectl config view --minify --raw -o jsonpath='{.clusters[0].cluster.certificate-authority-data}')
CERT_DATA=$(cat readonly-user.crt | base64 | tr -d '\n')
KEY_DATA=$(cat readonly-user.key | base64 | tr -d '\n')
```

**Step 6b — Create the kubeconfig file**

```bash
cat > readonly-kubeconfig.yaml <<EOF
apiVersion: v1
kind: Config
clusters:
- cluster:
    certificate-authority-data: ${CLUSTER_CA}
    server: ${CLUSTER_SERVER}
  name: my-cluster
contexts:
- context:
    cluster: my-cluster
    user: readonly-user
  name: readonly-context
current-context: readonly-context
users:
- name: readonly-user
  user:
    client-certificate-data: ${CERT_DATA}
    client-key-data: ${KEY_DATA}
EOF
```

> The user only needs one file: `readonly-kubeconfig.yaml`.

### Step 7 — Delete temporary files

```bash
rm readonly-user.key readonly-user.csr readonly-user.crt csr.yaml
```

{% hint style="warning" %}
The `.key` (private key) file has been embedded into `readonly-kubeconfig.yaml` as `client-key-data`. Delete the original `.key` file to prevent private key leakage.
{% endhint %}

### Step 8 — Verify

```bash
# Expected: list of pods is displayed normally
kubectl --kubeconfig=readonly-kubeconfig.yaml get pods -A
```

```bash
# Expected: command is rejected with a Forbidden error
kubectl --kubeconfig=readonly-kubeconfig.yaml delete pod some-pod
```

***

## Revoking Access

### Delete ClusterRoleBinding — required

```bash
kubectl delete clusterrolebinding readonly-user-binding
```

Deleting the ClusterRoleBinding → the user **immediately loses access**, even if the certificate is still valid.

### Delete CSR — optional (cleanup)

```bash
kubectl delete csr readonly-user
```

The CSR is only an object that stores the history of the certificate signing process. Deleting the CSR **does not affect** the signed certificate — it is only to avoid leaving residual objects in the cluster.

{% hint style="info" %}
**Important note:**

Kubernetes **does not have a certificate revocation mechanism**. If the user still holds the kubeconfig file, the certificate remains valid until it expires. Deleting the ClusterRoleBinding is the only way to immediately block access.
{% endhint %}

{% hint style="warning" %}
**Recommendation for customers:**

* **Do not delete the ClusterRoleBinding** of the cluster unless you are certain you want to permanently revoke access.
* If you **accidentally delete the ClusterRoleBinding** and cannot connect to the cluster, please **contact the VKS support team** for assistance in creating a new kubeconfig.
{% endhint %}

| Action                         | Delete ClusterRoleBinding | Delete CSR |
| ------------------------------ | ------------------------- | ---------- |
| User loses access immediately? | **Yes**                   | No         |
| Purpose                        | Revoke access             | Cleanup    |
| Required?                      | **Required**              | Optional   |
