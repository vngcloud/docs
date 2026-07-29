# Access Management

## Overview <a href="#tong-quan" id="tong-quan"></a>

The secondary authorization system allows customers to manage access and operations on CDN services flexibly and in detail. Through GreenNode's Portal interface, customers can authorize administration to any account that already exists on the system with customized permissions.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

1. **Authorized Account Type**
   * Customers can authorize the Root User Account as their own IAM User Account to interact with your CDN service.
2. **Type of permission granted:**
   * **Full:** Full rights, allows to perform all operations on the CDN system (configuration, management, deletion, addition, etc.).
   * **Read Only:** Only allowed to view information and status of CDN service, cannot make changes.
   * **Deny:** Default permission, prevents any access or manipulation to the system.
3. **Authorized objects:**
   * Authorization can be applied to each type of object on the CDN system, including:
     * **Analytic Resources:**
       * Dashboard
       * Report
     * **Product Management:**
       * Web Accelerator
       * Live Entrypoint
       * Object Download
       * Live Streaming
       * Video On Demand
       * Certificate
       * Purge Cache
     * **System Management:**
       * Profile
       * API Key
       * Activity Logs

***

## **How to grant permission** <a href="#quy-trinh-thuc-hien-phan-quyen" id="quy-trinh-thuc-hien-phan-quyen"></a>

**Step 1:** Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)

**Step 2:** Select **IAM** , then select **Add new.**

**Step 3:** Enter the email address of an account that already exists on the GreenNode system.

**Step 4:** At the object that needs to be authorized, select the type of authority that suits your needs. In which:

* **Full:** Full rights, allows to perform all operations on the CDN system (configuration, management, deletion, addition, etc.).
* **Read Only:** Only allowed to view information and status of CDN service, cannot make changes.
* **Deny:** Default permission, prevents any access or manipulation to the system.

**Step 5:** Select **Save** to apply the changes.

<figure><img src="../.gitbook/assets/image (378).png" alt="" width="371"><figcaption></figcaption></figure>
