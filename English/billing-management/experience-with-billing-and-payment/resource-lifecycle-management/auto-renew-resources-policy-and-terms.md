# Auto-renew resources - policy & terms

Use this document to learn more about the auto-renewal feature. It will detail the steps involved in **auto-renewing resources and the costs associated** with auto-renewing resources. Other steps are simplified and only mentioned as part of the process.

**1. The automatic resource renewal policy only applies to:**

* **Target:** Prepaid users
* **Resources** : All resources are auto-renewable and are in use
* **Funding source** : VNG Cloud Credit

**2. Instructions to enable/disable the "Automatic renewal" feature**

**2.1 For vStorage service products:** [**https://docs.vngcloud.vn/vng-cloud-document/vstorage/object-storage/vstorage-hcm03/charging-fee/charging-for-prepaid-users**](https://docs.vngcloud.vn/vng-cloud-document/vstorage/object-storage/vstorage-hcm03/charging-fee/charging-for-prepaid-users)

**2.2 For vServer products and services**

*   **Enable "Auto-Renew" on initialization**

    * Step 1: Configure service information on the product page → Click " **Initialize** " to go to the payment page
    * Step 2: On the payment page, tick " **Auto-renew** " to enable auto-renewal feature

    <figure><img src="../../../.gitbook/assets/image (11) (3).png" alt=""><figcaption></figcaption></figure>
* **Turn on/off during service use**
  * Step 1: Navigate to the Resource Billing page in the vServer service: [https://hcm-3.console.vngcloud.vn/vserver/billing](https://hcm-3.console.vngcloud.vn/vserver/billing)
  * Step 2: Click on the three dots icon at the location of the resource that needs to be changed. See image below
    * Select **"Auto-Renew"** to enable auto-renew if not enabled at creation
    * Select **"Update auto-renewal"** to adjust the resource usage time applied when the system performs auto-renewal
    * Select **"Turn off auto-renewal"** to turn off auto-renewal if not needed.

<figure><img src="../../../.gitbook/assets/image (446).png" alt=""><figcaption></figcaption></figure>

**2.3 For vMonitor products and services**

* **Enable "Auto-Renew" on initialization**
  * Step 1: Configure service information on the product page → Click "Initialize" to go to the payment page
  * Step 2: On the payment page, tick "Auto-renew" to enable auto-renewal

<figure><img src="../../../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

_Note: Currently, services in vMonitor products do not support turning off automatic renewal when users turn it on at initialization. To turn off automatic renewal when not needed, please contact the 247 team for further support._

**3. Automatic resource renewal process**

Automatic resource renewal is **a system feature** that helps users' resource usage not be interrupted at the end of the resource period (users need to continue using it but forget to renew it on the system for some reason).

**Terms applicable to the "Automatic renewal" feature on VNG Cloud are as follows:**

* Send email notification of required resources **7 days in advance** , from the end of the resource. The purpose is for users to prepare enough credit balance.
* Resources are **renewed by default for 1 month** from the end date.
* Users need to prepare enough available credit balance as notified so that the system can proceed with the renewal.
* The official system will renew **3 days in advance** , calculated from the end of the resource.
  * The pricing for automatic renewal is no different from when the user actively renews the resource. See more [here.](https://docs.vngcloud.vn/vng-cloud-document/billing-management/experience-with-billing-and-payment/resource-lifecycle-management/renew-resource)
  * The system sends information about the resource being renewed successfully/failed to the user.
  * The system generates invoices corresponding to the extended period.
* For expired resources, automatic renewal will not be applied. This means that when the resource is enabled for automatic renewal, but the automatic renewal process fails due to lack of credits, resulting in the resource expiring, in this case the user needs to proactively restore the resource to continue using the service. Refer to the Resource Restoration [guide](https://docs.vngcloud.vn/vng-cloud-document/billing-management/experience-with-billing-and-payment/resource-lifecycle-management/recover-resource)
