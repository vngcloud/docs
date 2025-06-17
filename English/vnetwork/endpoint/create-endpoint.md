---
description: >-
  VNG Cloud Endpoint is the private connection point between VPC and VNG Cloud
  services
---

# Create Endpoint



{% hint style="danger" %}
**Important**

* Within the same region, users can create **multiple Endpoints within a single VPC**.
* If the option **“Enable Private DNS”** is selected during Endpoint creation, **manual host file configuration is not required** — DNS resolution is handled automatically.
* If **Private DNS is not enabled**, users must **manually add host entries** on each server in order to access the Endpoint Service.
{% endhint %}

#### **Endpoint Creation Process**

1. **Log in** to the VNG Cloud console at:\
   [https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list](https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list)
   * Ensure that the selected **region is HCM**.
2. From the left-hand navigation panel, click on the **“Endpoint”** menu.
3. Click **“Create an Endpoint”** to begin the setup process.
4. Enter the required information for the Endpoint:
   * **Endpoint Name**: Provide a name for the new Endpoint.
   * **Select Region/Zone**: Choose the appropriate region and availability zone (e.g., HCM-1A, HCM-1B, etc.).
   * **Select Service**: Choose a VNG Cloud service to connect to from the supported list:\
     **vServer, vStorage, vMonitor, vCR, IAM**.
   * **Service Package**: The Endpoint is provisioned with the default **Standard** package.
     * No manual selection is required.
5. **Select the VPC and Subnet** to connect to the VNG Cloud service via the service Endpoint.
6. **Private DNS Configuration**:
   * If the selected VPC supports DNS, the **“Enable Private DNS”** option will be available.
     * When enabled, domain names will automatically resolve to internal IPs — **no manual host entries are required**.
   * If the VPC **does not support DNS**, the option will be **disabled by default**.
     * In this case, users **must manually configure host entries** to access the service.
7. Review service pricing and configuration details in the **“Summary”** section.
8. Click **“CREATE ENDPOINT”** to proceed.
9. The system will begin provisioning the Endpoint.
   * Once creation is complete, the new Endpoint will appear in the **Endpoint list view**.

### **How to Use the Endpoint**

#### **For Endpoints Created in VPCs Without DNS Support**

When the VPC does **not** support DNS, the **"Enable Private DNS"** option will be **unavailable** during Endpoint creation.\
As a result, **DNS name resolution will not be applied automatically**, and users will **not be able to access the Endpoint Service** directly after creation.

#### **Manual Configuration Steps:**

To configure private access from your server to the Endpoint Service, follow these steps:

1. **Open the Endpoint Management Page**
   * Navigate to the list of created Endpoints.
   * Select the Endpoint you wish to configure.
2. **Identify Key Information**\
   On the Endpoint detail page, the system will display two important items:
   * **Endpoint URL**: The public domain name for accessing the service via the Endpoint.
   * **Endpoint IP**: The internal IP address assigned to the Endpoint.
3.  **Configure the Host File on Your Server**\
    On each server that needs to access the service, add a host entry:

    * For **Linux/macOS**: `/etc/hosts`
    * For **Windows**: `C:\Windows\System32\drivers\etc\hosts`

    **Entry format:**

    ```php
    <Endpoint IP>    <Endpoint URL>
    ```

    **Example:**

    ```php
    10.0.5.123    service.example.internal
    ```
4. **Save changes** and verify that domain name resolution points to the correct Endpoint IP.

> ✅ **Note:** Host entry configuration is only required on servers located within the same VPC or that have a valid network route to the Endpoint Service.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Endpoint List</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption><p>Endpoint Detail</p></figcaption></figure>

Add host entries on servers that need to access the service via the Endpoint Service.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Add host</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

#### **Using Endpoint Service with “Enable Private DNS” Enabled**

When an Endpoint is created with the **“Enable Private DNS”** option enabled, the DNS system automatically resolves the service domain name. This eliminates the need for users to manually configure host records on their servers and ensures seamless and simplified access to the service.

**Key Behaviors:**

* Within each VPC, only **one Endpoint with “Enable Private DNS” enabled** is allowed per specific service.
* When this option is enabled:
  * The system **automatically overrides the public DNS record** of the service domain with a corresponding **private IP address** within the VPC.
  * All DNS queries from resources inside the VPC to the service domain will be **routed through the internal Endpoint**, rather than using the public IP.

> ⚠️ **Note:**\
> The DNS override mechanism is **only effective within the VPC**. It does **not affect DNS resolution from outside the internal network**.
