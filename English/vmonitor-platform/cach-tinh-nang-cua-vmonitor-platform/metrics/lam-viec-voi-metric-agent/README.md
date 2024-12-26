# Working with Metric Agent

### Overview

To push Metrics to vMonitor, you need to install the Metric Agent on your server. vMonitor uses the Telegraf Agent to push metrics to the system. Currently, the Telegraf Agent supports the IAM Service Account for authentication and authorization. Follow the steps below to set up the Telegraf Agent to push metrics to vMonitor.

***

### Installing Metric Agent on Server

* [Linux OS](cai-dat-metric-agent-tren-server/linux-os.md)
* [Linux OS has internet connection limitations](cai-dat-metric-agent-tren-server/linux-os-co-gioi-han-ket-noi-internet.md)
* [Window OS](cai-dat-metric-agent-tren-server/window-os.md)

***

### Viewing Information of Hosts Successfully Set Up with Metric Agent

Servers with the Metric Agent installed are called Hosts. After successfully installing on the servers, you can view the list of Hosts pushing metrics on the Infrastructure List/Host page by following these steps:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account, register for free [here](https://register.vngcloud.vn/signup).
2. Select the **Infrastructure List** folder.
3. Choose **Host**.
4. The system will display information about the hosts that you have successfully set up to push metrics. The displayed information includes:

* **Status**: Whether the server is pushing data (UP) or not (Undetermined).
* **Memory Available**: Available memory at the current time.
* **CPU Usage**: CPU usage at the current time.
* **Load**: Current load information.
* **Apps**: List of plugins that the Metric Agent has enabled.
* **Billing Status**: Monitoring status of the Host.

You can set up multiple hosts to push metrics to the vMonitor Platform using the same Service Account when configuring the Metric Agent. For example, two devices, LAPTOP-01 and LAPTOP-02, can use the same Service Account to push metrics to the vMonitor Platform. The number of hosts is defined as the number of resources when purchasing a Metric quota package.

When you click on a Host frame, a detailed page about that Host will open. The dashboard naming rule for the Host will be the hostname of the Host.

Additionally, clicking on the Host name will take you to the Dashboard page, where you can view the default dashboard for that Host.

{% hint style="info" %}
**Notice:**

* The vMonitor system will take an average time of less than 1 minute (in the worst case, up to 5 minutes) to update the new Host after you install the Metric Agent.
{% endhint %}

***

### Disabling a Host with Successfully Set Up Metric Agent

After successfully setting up the Metric Agent on your server, you have a certain number of hosts pushing metrics to the vMonitor Platform. If you want to temporarily stop a host from pushing metrics to our system without deleting the Metric Agent on that host, the Disable Host feature will help you achieve this. To disable a host with a successfully set up Metric Agent, follow the steps below:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account, register for free [here](https://hcm-3.console.vngcloud.vn/vmonitor).
2. Select the **Infrastructure list** folder.
3. Choose **Host**.
4. Select the icon  ![](<../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)  on the host you want to disable.
5. On the host disable confirmation screen, select **Disable**.
6. When the icon changes to ![](<../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>), the host has been successfully disabled.

When you disable a host, the Metric Agent configuration on the host remains unchanged, and you can re-enable host monitoring at any time following the instructions in Restore Disabled Host. From the moment you disable a host, its metrics will no longer be pushed, and the host will not be counted as a resource in the Metric quota configuration. If you no longer need to monitor metric data on a host, you can also completely delete the host information by following the instructions in Delete Host Information with Successfully Set Up Metric Agent.

***

### Restoring a Disabled Host

You have disabled a host from pushing metrics to our system, and the metric data from that host has been paused since the time of disabling. If you now need to resume monitoring these metrics, follow the instructions below to restore the disabled host:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account, register for free [here](https://hcm-3.console.vngcloud.vn/vmonitor).
2. Select the **Infrastructure list** folder.
3. Choose **Host**.
4. Select the icon ![](<../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>) on the host you want to restore.
5. On the host restore confirmation screen, select **Enable**.
6. When the icon changes to  ![](<../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)  , the host has been successfully restored. From this point, metrics will start being pushed again.

***

### Deleting Host Information with Successfully Set Up Metric Agent

To delete a host, you can:

1. Log in to [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account, register for free [here](https://register.vngcloud.vn/signup).
2. Select the **Infrastructure list** folder.
3. Choose **Host**.
4. On the host you want to delete, select **Delete**.
5. On the host deletion confirmation screen, select **Delete**.

{% hint style="info" %}
**Notice:**

* After you delete a host, it will be temporarily removed from your host list. However, if you do not uninstall the Metric Agent on the server, the monitor record for this host will automatically regenerate the next time.
{% endhint %}

To view the list of corresponding metrics for each product, please refer to the [Supported Metrics List](../danh-sach-metrics-ho-tro/).
