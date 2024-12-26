# Getting Start with Metrics

### Step 1: Create a Metric quota <a href="#batdauvoimetrics-buoc1-khoitaometricquota" id="batdauvoimetrics-buoc1-khoitaometricquota"></a>

To start using the service, you need to create a Metric quota. A Metric quota is a term on the vMonitor Platform that represents a package for monitoring Metrics with a specific number of Resources and storage duration that you purchase on VNG Cloud. At any given time, you can own a Metric quota and use it to analyze data from your system.

Perform the purchase of Metric Quota by following these steps:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account yet, sign up for free at [here](https://register.vngcloud.vn/signup).
2. Choose **Quota & Usage**.
3. Choose **Buy metric quota.**
4. Choose the **Class** that you need. We offer you a choice of 1 in 2 classes including: Basic, Pro.
5. If you choose the **Basic** class, you won't be able to customize the package configuration. If you choose the **Pro** class, you can select the desired number of hosts by dragging and dropping or entering the number of resources you want in the Number of resources field. For more detailed information about the classes, please see [Metric Quota Class](../vmonitor-platform-la-gi/vmonitor-platform-metric-la-gi/metric-quota-class.md).
6. Choose **Buy Metric Quota**.
7. Choose **Period** if you are a prepaid user. We offer prepaid periods including: 1 month, 3 months, 6 months, 12 months, 24 months, 36 months.
8. Choose **Continue.**
9. Perform the steps to **Checkout** the cart, and after successful payment, the **Metric quota** will be created.

The method for calculating costs for each metric quota package is publicly available on the VNG Cloud homepage. Please refer to the Pricing Calculation.

***

### Step 2: Create a Service Account <a href="#batdauvoimetrics-buoc2-khoitaoserviceaccount" id="batdauvoimetrics-buoc2-khoitaoserviceaccount"></a>

Create a Service Account and attach the policy: <mark style="color:red;">**vMonitorMetricPush**</mark> to have sufficient rights to push Metrics to vMonitor (You can skip this step if it's already created)

To create a service account, you need to access the IAM Portal:

1. After successfully creating, you need to save the Client\_ID and Secret\_Key for the next step.
2. Find and select **Policy:** **vMonitorMetricPush**, then click "**Create a Service Account**" to create a Service Account. The Policy: vMonitorMetricPush created by VNG Cloud only contains the exact permissions to push metrics to the system.
3. Choose "**Create a Service Account**," enter a name for the Service Account, and click **Next Step** to assign permissions to the Service Account.

***

### Step 3: Install Metric Agent on Linux OS Server <a href="#batdauvoimetrics-buoc3-caidatmetricagenttrenlinuxosserver" id="batdauvoimetrics-buoc3-caidatmetricagenttrenlinuxosserver"></a>

To push metrics to vMonitor, you need to install the Metric Agent on the server. The vMonitor Platform uses Telegraf Agent to send metrics to the system. Currently, Telegraf Agent supports IAM Service Account for authentication and authorization. Follow the steps below to configure Telegraf Agent to send metrics to vMonitor.

After successfully creating the Service Account and storing the Client\_ID and Secret\_key, proceed to:

Use the Client\_ID and Secret\_Key you copied earlier to replace the **$IAM\_CLIENT\_ID** and **$IAM\_CLIENT\_SECRET** fields in the command below. Run this command on the server you want to monitor, making sure to do so with root user privileges (or add sudo before the command if not running as root). \*\*Replace the Client\_ID and Secret\_Key in the command below and run on the server to install

```
VMONITOR_SITE=monitoring-agent.vngcloud.vn \
IAM_CLIENT_ID=$IAM_CLIENT_ID \
IAM_CLIENT_SECRET=$IAM_CLIENT_SECRET \
IAM_URL=https://iamapis.vngcloud.vn/accounts-api/v2/auth/token \bash -c "$(curl -L 
https://raw.githubusercontent.com/vngcloud/vmonitor-metrics-agent/main/install.sh)"
```

***

### Step 4: View Metric's information through Dashboard <a href="#batdauvoimetrics-buoc4-xemthongtinmetricthongquadashboard" id="batdauvoimetrics-buoc4-xemthongtinmetricthongquadashboard"></a>

After installing the Metric Agent as guided in **Step 3: Install Metric Agent on Server** to push metrics to the vMonitor Platform, we will automatically create a **default Dashboard** for this **Host**. To view this default Dashboard, please follow the instructions below:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Choose **Infrastructure List/ Host.**

<figure><img src="../../.gitbook/assets/image (35) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2. Choose the **Hostname**. For example, if the device **LAP15839** is successfully configured with the Metric Agent to the vMonitor Platform, the default dashboard will be named: **LAP15839**. When you select the dashboard, it will display as shown in the image:

<figure><img src="../../.gitbook/assets/image (36) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

With this Default Dashboard, you will be able to view the metric information that we have pre-drawn for you, including charts on CPU, Memory, Load Avg, Disk, and Network information. On this **Default Dashboard**, you cannot add widgets or customize the dashboard. To make changes or customize the Dashboard, you need to create a new dashboard or **Create a copy** from this **Default Dashboard** and Edit. To create a Dashboard copy, follow the instructions below:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Choose **Dashboard.**
2. On the **Default Dashboard** you want to copy, select **Create Dashboard Copy**
3. Enter the **Dashboard Name**. According to our regulations, the Dashboard name must be between 1 (minimum) and 50 (maximum) characters long. The Dashboard name can include uppercase, lowercase letters (a-z, A-Z), numbers (0-9), period (.), underscore (\_), hyphen (-), at symbol (@), and slash (/).
4. Select **Create Copy**.

After a copy of the **Default Dashboard** is created, you can add, remove, customize, or change the position of Widgets in this copied Dashboard. For more information on working with Metrics and Metric Dashboards, please refer to Metrics.
