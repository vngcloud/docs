# Linux OS

To push Metrics to vMonitor, you need to install the Metric Agent on your server. vMonitor uses the Telegraf Agent to push metrics to the system. Currently, the Telegraf Agent supports the IAM Service Account for authentication and authorization. Follow the steps below to set up the Telegraf Agent to push metrics to the vMonitor Platform.

{% hint style="info" %}
**Chú ý:**

* Please note that you need to have a Metric Quota. If you do not have one, you need to purchase a Metric Quota [here](../../lam-viec-voi-metric-quota.md).
{% endhint %}

### Telegraf Agent with Service Account

1. **Creating a Service Account and Attaching policy: the vMonitorMetricPush to Push Metrics to vMonitor.**

To create a service account, visit [this link](https://hcm-3.console.vngcloud.vn/vmonitor).

* Select **Create a Service Account**, enter a name for the Service Account, and click **Next Step** to assign permissions to the Service Account.
* Find and select the policy: **vMonitorMetricPush**, then click **Create a Service Account**. This policy, created by VNG Cloud, contains the exact permissions needed to push metrics to the system.
* After successfully creating the Service Account, save the **Client\_ID** and **Secret\_Key** for the next step.

2. **Replacing Client\_ID, Secret\_Key into the inline command and running on the server to install:**

Use the Client\_ID and Secret\_Key you copied above, replacing them in the corresponding **$IAM\_CLIENT\_ID** and **$IAM\_CLIENT\_SECRET** fields in the command below. Run this command on the server that needs to be monitored, making sure to execute it with **root user** privileges (if not, prepend sudo to the command).

```
VMONITOR_SITE=monitoring-agent.vngcloud.vn \
IAM_CLIENT_ID=$IAM_CLIENT_ID \
IAM_CLIENT_SECRET=$IAM_CLIENT_SECRET \
IAM_URL=https://iamapis.vngcloud.vn/accounts-api/v2/auth/token \
bash -c "$(curl -L https://raw.githubusercontent.com/vngcloud/vmonitor-metrics-agent/main/install.sh)"
```

3. **After running the command and completing the installation, you will see the server in the Infrastructure List/Host page.**

<figure><img src="../../../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

### **Telegraf Agent with API\_KEY (deprecated**) <a href="#linuxos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay" id="linuxos-telegrafagentvoiapi_key-deprecated-khongkhuyencaosudung-saptoisedunghotrovoiphuongthucnay"></a>

{% hint style="info" %}
**Notice:**

* We do not recommend using this method as our system will soon discontinue support for API Keys.
{% endhint %}

* This is an older method supported by Telegraf with API\_Key, which will soon be deprecated.
* Visit the Integration/API Key page to create and obtain an API Key.Select **Create an API Key**, name the API Key, click **Create**, and then copy the API Key for use.
* Replace the copied API Key in the command below and run it on the server:

```
API_KEY=$API_KEY bash -c "$(curl -L https://raw.githubusercontent.com/vngcloud/vmonitor-metrics-agent/v1-stable/install.sh)"
```

* After running the command and completing the installation, you will see the server in the **Infrastructure List/Host** page.

<figure><img src="../../../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image%20(114).png" alt=""><figcaption></figcaption></figure>
