# Dashboard

### Overview <a href="#dashboard-tongquan" id="dashboard-tongquan"></a>

A Dashboard is a data visualization tool that helps users quickly find important information and better understand the data. A Dashboard in the vMonitor Platform is a group of charts used to monitor your resources from certain services, applications, or servers. The group of charts will clearly show you the health of the system.

On the vMonitor Platform, we define 2 types of Dashboards including:

* **Default Dashboard**: This type of Dashboard is automatically created by our system as soon as you enable monitoring for the services you're using or when you successfully set up monitoring for your hosts. The main characteristic of this Dashboard is that you can view, create copies, but cannot modify any parameters or Widgets within the Dashboard.
* **Custom Dashboard**: This type of Dashboard is created by you. The characteristics of this Dashboard are that you have full control to view, create new ones, duplicate, edit parameters, as well as add, remove, or arrange the Widgets within the Dashboard as you wish.

***

### Dashboard Rule <a href="#dashboard-phamvigioihandashboard" id="dashboard-phamvigioihandashboard"></a>

**Dashboard naming rules**

The following rules apply to naming Dashboards in the vMonitor Platform:

* The Dashboard name must be between 1 (minimum) and 50 (maximum) characters in length.
* The Dashboard name can only include uppercase letters, lowercase letters (a-z, A-Z), numbers (0-9), dots (.), underscores (\_), hyphens (-), slashes (/) and the @ character.&#x20;
* The Dashboard name should not contain sensitive information (e.g., IP addresses, account names, login passwords,...).&#x20;
* The Dashboard name must be unique within a VNG Cloud account until it is deleted.&#x20;

Examples:

* Here are examples of valid and compliant Dashboard names following the proposed naming conventions:
  * monitor\_host@1
  * logproject-DashboardA
  * ...
* The following Dashboard names are valid but we do not recommend using them:
  * [docexamplewebsite.com](http://docexamplewebsite.com/)
  * 1.1.1.2/10
  * ...
* Examples of invalid Dashboard names are:
  * Report\_usage\_80\_% (chứa ký tự %)
  * Dashboard\&Report (chứa ký tự &)
  * ...

***

### Create a Dashboard <a href="#dashboard-khoitaodashboard" id="dashboard-khoitaodashboard"></a>

To initialize a Dashboard, you can use the vMonitor Platform following the instructions below:

1. Login into vMonitor Platform [tại đây.](https://hcm-3.console.vngcloud.vn/vmonitor)
2. Select the menu **Dashboard.**
3. Select **Create a Dashboard.**
4. The **Create Dashboard** screen is displayed. Enter **Dashboard name** and ensure it complies with our naming conventions for your Dashboard. Don't worry, after creating the Dashboard, you can change its name if needed.
5. Select **Create**.

***

### View list of Dashboard <a href="#dashboard-xemdanhsachdashboard" id="dashboard-xemdanhsachdashboard"></a>

To view the Dashboards, you can:

1. Login into vMonitor Platform.
2. Select the menu **Dashboard.**
3. On the **Dashboard** list display page, you can filter the **Dashboard** list according to the types of Dashboard and their meanings as described in the tables below:

<table data-header-hidden><thead><tr><th width="194"></th><th></th></tr></thead><tbody><tr><td><strong>Loại Dashboard</strong></td><td><strong>Description</strong></td></tr><tr><td>All Dashboards</td><td>All existing dashboards</td></tr><tr><td>All host</td><td>All Dashboards are automatically created by the vMonitor Platform when you set up a Host.</td></tr><tr><td>All integration</td><td>All Dashboards are automatically created by the vMonitor Platform when you set up integrated applications.</td></tr><tr><td>All VNG Cloud</td><td>All Dashboards are created by the vMonitor Platform system for VNG Cloud Products.</td></tr><tr><td>Created by you</td><td>Dashboards created by users</td></tr><tr><td>Favourite</td><td>Favorite Dashboards.</td></tr></tbody></table>

The **Dashboard** has not been successfully added to the favorites list. The **Dashboard** has been successfully added to the favorites list and vice versa when the icon <img src="../../../.gitbook/assets/image (105).png" alt="" data-size="line"> on the **Dashboard** is on each **Dashboard**. When the icon on the Dashboard is <img src="../../../.gitbook/assets/image (106).png" alt="" data-size="line">, you can mark a **custom Dashboard** as a favorite or remove it from the favorites list by re-selecting it.

***

### Change Dashboard Name <a href="#dashboard-thaydoitendashboard" id="dashboard-thaydoitendashboard"></a>

To change the name of the Dashboard you created earlier, follow the instructions below:

1. Login into vMonitor Platform.
2. Select the menu **Dashboard.**
3. In the **Dashboard** you want to rename, select the icon <img src="../../../.gitbook/assets/image (50) (1).png" alt="" data-size="line">
4. Select **Rename**.
5. Input the **Dashboard name**, Please enter a name that complies with our guidelines for your Dashboard.
6. Select **Save**.

You can only rename Dashboards created by yourself. For **default Dashboards** automatically generated by our system, you cannot rename them but can create a Dashboard copy.

***

### Clone a Dashboard <a href="#dashboard-taobansaodashboard" id="dashboard-taobansaodashboard"></a>

To create a copy of a Dashboard, follow the instructions below:

1. Login into vMonitor Platform.
2. Select the menu **Dashboard.**
3. On **Dashboard** which you wanna clone, chọn <img src="../../../.gitbook/assets/image (51) (1).png" alt="" data-size="line">
4. Select **Clone Dashboard.**
5. Input **Dashboard name**, Please enter a name that complies with our guidelines for your Dashboard.
6. Select **Clone.**

At this point, a new **Dashboard** with the same parameters as the initial **Dashboard** is created. On this new **Dashboard**, you can customize the parameters as well as configure additional settings or delete Widgets as desired.

***

### Delete a Dashboard <a href="#dashboard-xoadashboard" id="dashboard-xoadashboard"></a>

If you no longer need to use a custom **Dashboard**, you can delete it from the system following the instructions below:

1. Login into vMonitor Platform.
2. Select the menu **Dashboard.**
3. On **Dashboard** which you wanna delete, select <img src="../../../.gitbook/assets/image (52) (1).png" alt="" data-size="line">
4. Select **Delete**.
5. On the Delete Dashboard confirmation screen, select **Delete**.

After you successfully delete, your **Dashboard** will be completely removed from our system. You cannot restore a deleted **Dashboard**, so please use this feature cautiously.
