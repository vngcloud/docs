# Automatically manage Certificates in VKS with Nginx Ingress Controller, Cert-Manager, and Let's Encr

## Necessary conditions <a href="#dieu-kien-can" id="dieu-kien-can"></a>

* You have initialized the Cluster on the VKS system according to the instructions here [and](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer4) the VNGCloud LoadBalancer Controller has been installed on your cluster **.**
* Next, make sure you have a **domain** registered and in use.
* Finally, you need an **email** address to perform the Certificate management test.
* Next, you need to install nginx-ingress-controller with the command:

```bash
helm install nginx-ingress-controller oci://ghcr.io/nginxinc/charts/nginx-ingress --namespace kube-system
```

***

## **Install Cert-Manager** <a href="#cai-dat-cert-manager" id="cai-dat-cert-manager"></a>

**Cert-Manager** is responsible for automatically issuing and renewing certificates from **Let's Encrypt.**

* Use **Helm** to install Cert-Manager via command:

```bash
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.16.2 \
  --set crds.enabled=true
```

***

## **Steps to follow** <a href="#cac-buoc-thuc-hien" id="cac-buoc-thuc-hien"></a>

### **Deploy sample app** <a href="#deploy-sample-app" id="deploy-sample-app"></a>

Let's deploy a sample app, for example:

```bash
kubectl create deployment echo-server --image=mccutchen/go-httpbin
kubectl expose deployment echo-server --name=clusterip --port=80 --target-port=8080 --type=ClusterIP
```

### **Issuer Configuration** <a href="#cau-hinh-issuer" id="cau-hinh-issuer"></a>

Issuer is the component that helps Cert-Manager communicate with Let's Encrypt to issue certificates.

<details>

<summary>Testing on STAGING environment</summary>

1.  Create file `letsencrypt-issuer.yaml`:

    ```yaml
    apiVersion: cert-manager.io/v1
    kind: Issuer
    metadata:
      name: letsencrypt-staging
    spec:
      acme:
        server: https://acme-staging-v02.api.letsencrypt.org/directory
        email: ______________________ # Change to your email
        privateKeySecretRef:
          name: letsencrypt-staging
        solvers:
          - http01:
              ingress:
                ingressClassName: nginx
    ```
2.  Create Issuer on VKS cluster via command:

    ```bash
    kubectl apply -f letsencrypt-issuer.yaml
    ```
3.  Check Issuer via command:

    ```bash
    kubectl describe issuer letsencrypt-staging
    ```
4.  The results returned are as follows:

    ```bash
    Status:
      Acme:
        Uri:  https://acme-staging-v02.api.letsencrypt.org/acme/acct/...
      Conditions:
        Last Transition Time:  ...
        Message:               The ACME account was registered with the ACME server
        Reason:                ACMEAccountRegistered
        Status:                True
        Type:                  Ready
    ```
5.  Continue to deploy ingress, change your domain in the yaml file below:

    ```bash
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: go-httpbin
      annotations:
        cert-manager.io/issuer: "letsencrypt-staging"
        acme.cert-manager.io/http01-edit-in-place: "true"
    spec:
      ingressClassName: nginx
      tls:
      - hosts:
        - ______________________ # Change to your domain
        secretName: quickstart-example-tls
      rules:
      - host: ______________________ # Change to your domain
        http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: clusterip
                port:
                  number: 80
    ```
6.  Check certificate via command:

    ```bash
    kubectl get certificate

    NAME                     READY   SECRET                   AGE
    quickstart-example-tls   True    quickstart-example-tls   16m # Ready should be True
    ```
7.  Check certificate details:

    ```bash
    kubectl describe certificate quickstart-example-tls

    Name:         quickstart-example-tls
    Namespace:    default
    Labels:       <none>
    Annotations:  <none>
    API Version:  cert-manager.io/v1
    Kind:         Certificate
    Metadata:
      Cluster Name:
      Creation Timestamp:  2018-11-17T17:58:37Z
      Generation:          0
      Owner References:
        API Version:           networking.k8s.io/v1
        Block Owner Deletion:  true
        Controller:            true
        Kind:                  Ingress
        Name:                  kuard
        UID:                   a3e9f935-ea87-11e8-82f8-42010a8a00b5
      Resource Version:        9295
      Self Link:               /apis/cert-manager.io/v1/namespaces/default/certificates/quickstart-example-tls
      UID:                     68d43400-ea92-11e8-82f8-42010a8a00b5
    Spec:
      Dns Names:
        www.example.com
      Issuer Ref:
        Kind:       Issuer
        Name:       letsencrypt-staging
      Secret Name:  quickstart-example-tls
    Status:
      Acme:
        Order:
          URL:  https://acme-staging-v02.api.letsencrypt.org/acme/order/...
      Conditions:
        Last Transition Time:  2018-11-17T18:05:57Z
        Message:               Certificate issued successfully
        Reason:                CertIssued
        Status:                True
        Type:                  Ready
    Events:
      Type     Reason          Age                From          Message
      ----     ------          ----               ----          -------
      Normal   CreateOrder     9m                 cert-manager  Created new ACME order, attempting validation...
      Normal   DomainVerified  8m                 cert-manager  Domain "www.example.com" verified with "http-01" validation
      Normal   IssueCert       8m                 cert-manager  Issuing certificate...
      Normal   CertObtained    7m                 cert-manager  Obtained certificate from ACME server
      Normal   CertIssued      7m                 cert-manager  Certificate issued Successfully
    ```
8.  Check connection to domain via command:

    ```bash
    curl -kivL -H 'Host: ______DOMAIN______' 'http://_____IP_____'
    ```
9.  You can also delete test resources via the command:

    ```bash
    kubectl delete ingress go-httpbin
    kubectl delete issuer letsencrypt-staging
    kubectl delete secret quickstart-example-tls
    kubectl delete secret letsencrypt-staging
    ```

</details>

<details>

<summary>Execute on PRODUCTION environment</summary>

1.  Create file `letsencrypt-issuer.yaml`:

    ```yaml
    apiVersion: cert-manager.io/v1
    kind: Issuer
    metadata:
      name: letsencrypt-prod
    spec:
      acme:
        server: https://acme-v02.api.letsencrypt.org/directory
        email: ______________________ # Change to your email
        privateKeySecretRef:
          name: letsencrypt-prod
        solvers:
          - http01:
              ingress:
                ingressClassName: nginx
    ```
2.  Create Issuer on VKS cluster via command:

    ```bash
    kubectl apply -f letsencrypt-issuer.yaml
    ```
3.  Check Issuer via command:

    ```bash
    kubectl describe issuer letsencrypt-prod
    ```
4.  Continue to deploy ingress, change your domain in the yaml file below:

    ```bash
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: go-httpbin
      annotations:
        cert-manager.io/issuer: "letsencrypt-prod"
        acme.cert-manager.io/http01-edit-in-place: "true"
    spec:
      ingressClassName: nginx
      tls:
      - hosts:
        - ______________________ # Change to your domain
        secretName: quickstart-example-tls
      rules:
      - host: ______________________ # Change to your domain
        http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: clusterip
                port:
                  number: 80
    ```

</details>
