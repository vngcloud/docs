# Linux OS has internet connection limitations

The [installing Metric agent on Server](./) guide for the agent requires an HTTPS internet connection to several endpoints to download the necessary resources for installation. Therefore, the installation may not succeed on a server with restricted internet access.

{% hint style="info" %}
**Notice:**

* Please note that you need to have a Metric Quota. If you do not have one, you need to purchase a Metric Quota [here](../../lam-viec-voi-metric-quota.md).
{% endhint %}

### In the case of a server with restricted internet access

#### Check and ensure the connection to the vMonitor Site

{% hint style="info" %}
**Allow by Endpoints:**

* [https://iamapis.vngcloud.vn/accounts-api/v2/auth/token](https://iamapis.vngcloud.vn/accounts-api/v2/auth/token)
* [https://monitoring-agent.vngcloud.vn/\*](https://monitoring-agent.vngcloud.vn/\*)

**Allow by IP and Port:**

* IP: 116.118.93.14, Port: 443 - Protocol: HTTPS ( [iamapis.vngcloud.vn](http://iamapis.vngcloud.vn) )
* IP: 116.118.93.158, Port: 443 - Protocol: HTTPS ( [monitoring-agent.vngcloud.vn](http://monitoring-agent.vngcloud.vn) )
{% endhint %}

#### **2. Create Service Account**

You need to create a Service Account and attach the policy: vMonitorMetricPush to have sufficient permissions to push Metrics to vMonitor (You can skip this step if it has already been created).

To create a service account, visit [here](https://iam.console.vngcloud.vn/service-accounts),

* Select **"Create a Service Account,**" enter a name for the Service Account, and click **Next Step** to assign permissions to the Service Account.
* Find and select the **Policy: vMonitorMetricPush**, then click "**Create a Service Account**" to create the Service Account. The Policy: vMonitorMetricPush, created by VNG Cloud, contains the exact permissions needed to push metrics to the system.
* After successfully creating the Service Account, you need to save the Client\_ID and Secret\_Key for the next step.

#### **3.** Proceed with the installation:

3.1 Download the installation package from another server: Choose one of the following packages depending on the OS

* RPM package: [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.2/telegraf-nightly.x86\_64.rpm](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.2/telegraf-nightly.x86\_64.rpm)
* Deb package: [https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.2/telegraf\_nightly\_amd64.deb](https://github.com/vngcloud/vmonitor-metrics-agent/releases/download/1.26.0-2.0.2/telegraf\_nightly\_amd64.deb)

3.2 Transfer the installation package to the server: You can use tools to transfer or copy the installation package to the server (e.g., scp, rsync, etc.).

3.3 Create credentials

```
echo -e "IAM_CLIENT_ID=YOUR_IAM_CLIENT_ID_XXXXXXXX\nIAM_CLIENT_SECRET=YOUR_IAM_CLIENT_SECRET_XXXXXXXX\nIAM_URL=https://iamapis.vngcloud.vn/accounts-api/v2/auth/token\nVMONITOR_SITE=monitoring-agent.vngcloud.vn" | sudo tee /etc/default/telegraf
```

3.4 Install the package: Run the following command based on the OS

* OS: **Centos** - **yum** package manager

```
sudo yum localinstall /<path_to_file>/telegraf-nightly.x86_64.rpm 
```

* OS: **Ubuntu, Debian** - **apt** or **dpkg** package manager

```
# use 1 of 2 commands following:
sudo apt install /<path_to_file>/telegraf_nightly_amd64.deb
# or
sudo dpkg -i /<path_to_file>/telegraf_nightly_amd64.deb

```

3.5 Start metric agent

* **SystemD** service manager

```
sudo systemctl restart telegraf
```

* **SysVInit** is the classic initialization process

```
sudo service telegraf restart
```

.
