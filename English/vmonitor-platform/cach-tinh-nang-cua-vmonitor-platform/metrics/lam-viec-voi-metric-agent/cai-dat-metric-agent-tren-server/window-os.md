# Window OS

To push Metrics to vMonitor, you need to install the Metric Agent on your server. vMonitor uses the Telegraf Agent to push metrics to the system. Currently, the Telegraf Agent supports the IAM Service Account for authentication and authorization. Follow the steps below to set up the Telegraf Agent to push metrics to vMonitor.

### **Telegraf Agent with Service Account** <a href="#windowos-telegrafagentvoiserviceaccount" id="windowos-telegrafagentvoiserviceaccount"></a>

1. **Create a Service Account and attach the policy: vMonitorMetricPush to have sufficient permissions to push Metrics to vMonitor.**

To create a service account, visit [here](https://iam.console.vngcloud.vn/service-accounts).

* Select "**Create a Service Account**", enter a name for the Service Account, and click **Next Step** to assign permissions to the Service Account.
* Find and select the **Policy: vMonitorMetricPush**, then click "**Create a Service Account**" to create the Service Account. The Policy: vMonitorMetricPush, created by GreenNode, contains the exact permissions needed to push metrics to the system.
* After successfully creating the Service Account, you need to save the Client\_ID and Secret\_Key for the next step.

2\. **Download the Agent Installer for Windows**

* Access this link to load agent installer forWindows : [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly\_windows\_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.1/telegraf-nightly_windows_amd64.exe)

3\. Install the installer using the Client\_ID and Secret\_Key you copied above.

* Run the agent installer you downloaded above. A
* fter receiving the notification, select **More Info**.

<figure><img src="../../../../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

* Then select **Run anyway** to start installing the agent.

<figure><img src="../../../../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

* Chosse **Next** to continue

<figure><img src="../../../../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

* Enter the two pieces of information, **Client\_ID** and **Secret\_Key**, you copied above into the fields: **IAM\_CLIENT\_ID** and **IAM\_CLIENT\_SECRET:**

<figure><img src="../../../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

* Keep the default settings and select Next to continue, or if you want to change the installation directory, make the necessary changes.

<figure><img src="../../../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

* Select "**Accept the license**," then click **Next** to continue.

<figure><img src="../../../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

* Keep the default settings and select **Next** to continue, or you can customize the shortcut menu name for the agent.

<figure><img src="../../../../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

* Select **Install** to begin the installation.

<figure><img src="../../../../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

* Select **Yes** to grant permissions for the agent to operate.

<figure><img src="../../../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

* After the installation process is complete, select **Finish**.

<figure><img src="../../../../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

4.**After successful installation, you will see the server on the Infrastructure List/Host page**.

<figure><img src="../../../../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

### **Telegraf Agent với API\_KEY (deprecated**) <a href="#windowos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay" id="windowos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay"></a>

{% hint style="info" %}
**Notice:**

* We do not recommend using this method, as our system will soon stop supporting these API Keys.
{% endhint %}

Step 1: Create an API Key (if you have not created any API Key before).

* Access the vMonitor Platform Product portal: [https://hcm-3.console.vngcloud.vn/vmonitor/](https://hcm-3.console.vngcloud.vn/vmonitor/)
* Select **Integration** => then choose **API Key**.

<figure><img src="../../../../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

* Select **Create an API Key** to create a new one (if you have not created any API Key before).

<figure><img src="../../../../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

Step 2: Download Agent Installer

* Access the link to download the agent installer:: [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly\_windows\_amd64.exe](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.23.0-1.4.0/telegraf-nightly_windows_amd64.exe)

Step 3: Install Agent

* Run the agent installer.
* After receiving the notification, select **More Info**.

<figure><img src="../../../../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

* Then select **Run anyway** to start installing the agent.

<figure><img src="../../../../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

* Select **Next** to continue.

<figure><img src="../../../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

* Return to the vMonitor Platform portal, in the API Key section, select the **copy icon** to copy the API Key information.

<figure><img src="../../../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

* Paste the API Key information into the **credentials** entry field.

<figure><img src="../../../../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

* You can customize the installation folder if needed.

<figure><img src="../../../../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

* Select **Accept the license**, then click **Next** to continue.

<figure><img src="../../../../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

* You can customize the shortcut menu name for the agent, then select **Next** to continue.

<figure><img src="../../../../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

* Select **Install** to begin the installation.

<figure><img src="../../../../../.gitbook/assets/image (132) (1).png" alt=""><figcaption></figcaption></figure>

* Select **Yes** to grant permissions for the agent to operate.

<figure><img src="../../../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

* After the installation process is complete, select **Finish**.

<figure><img src="../../../../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

#### Step 4: Verify Agent Operated <a href="#windowos-b4-kiemtraagentdahoatdong" id="windowos-b4-kiemtraagentdahoatdong"></a>

* Access the vMonitor Platform portal, select **Infrastructure list** => choose **Host**, then check if the hostname of the VM has appeared in the list.

<figure><img src="../../../../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

* Click on the **hostname** to check the monitoring dashboard.

<figure><img src="../../../../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>
