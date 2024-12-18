# Getting Start with Logs

### Step 1: Create a Log project <a href="#batdauvoilogs-buoc1-khoitaologproject" id="batdauvoilogs-buoc1-khoitaologproject"></a>

To start using the service, you need to create a Log project. A Log project is a term on the vMonitor Platform that represents a log monitoring package with specific capacity and duration that you purchase on VNG Cloud. At any given time, you can own one or multiple Log projects simultaneously and use them as a way to organize resources for different teams or departments for various purposes.

Implement project creation according to the steps below:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). If you don't have an account yet, sign up for free at here.
2. Select **Quota & Usage**.
3. Select **Create a log project.**
4. Enter **Log project Name**. According to our regulations, **Log project Name** must be 1 (minimum) to 63 (maximum) characters long. **Log project Name** can include lowercase letters (a-z), numbers (0-9), hyphens (-). **Log project Name** must start with a lowercase letter and end with a lowercase letter or a number.
5. Enter **Log project Description** if there is any. According to our regulations, **Description** can be from 0 (minimum) to 300 (maximum) characters long. **Description** can include uppercase letters, lowercase letters (a-z, A-Z), numbers (0-9), periods (.), underscores (\_), spaces ( ), or hyphens (-).
6. Choose the **Class** you need to use. We offer you a choice between 2 classes: Basic and Pro.
7. If you choose the **Basic** class, you will not be able to customize the package configuration. If you choose the **Pro** class, you can select the retention day and configure the desired log size per day by dragging or entering your desired log size in the Log size per day box. For more detailed information about the classes, please refer to the Log Project Class.
8. Select **Buy Log Quota.**
9. Perform the **Checkout** steps for the cart, and after successful payment, a **Log Project** will be initiated.

The cost calculation for each log project package is publicly available on the VNG Cloud homepage; please refer to the Pricing section.

***

### Step 2: Download Certificate and install Log Agent on Server <a href="#batdauvoilogs-buoc2-certificatevacaidatlogagenttrenserver" id="batdauvoilogs-buoc2-certificatevacaidatlogagenttrenserver"></a>

After purchasing a Log Project, the system will automatically generate a certificate for each Log Project. This certificate is used to authenticate the Log Agent with the vMonitor Platform.

Follow the steps below to download the certificate and installation scripts.

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Select **Integration.**
2. Select **Certificate.**
3. Select **Download** to download the certificate information to the server where you want to push logs.

After downloading, the folder will contain setup instructions for the agent in the readme file. The setup scripts are also included in the certificate file that was downloaded. Use this information along with the instructions below to complete the setup of the Agent for Log.

#### Install

Determine the type of agent you want to install and follow the instructions for that agent below. Here, we guide you through installing the Filebeat agent:

* If you use the pre-prepared script in the download folder, run the command

```
sudo chmod +x filebeat.sh
sudo ./filebeat.sh <path-to-file-log>
```

***

### Step 3: View Log through Log search <a href="#batdauvoilogs-buoc3-xemthongtinlogthongqualogsearch" id="batdauvoilogs-buoc3-xemthongtinlogthongqualogsearch"></a>

To perform log search and analysis, follow the steps below:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Select **Log.**
2. Select **Log search**.
3. Select the **Log project** you need to view and analyze logs from. The location for selecting the log project is shown in the image below:

<figure><img src="../../.gitbook/assets/image (37) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4. Continue to perform log search and analysis.
