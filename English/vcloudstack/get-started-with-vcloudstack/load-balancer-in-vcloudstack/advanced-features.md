# Advanced Features

Let's learn more about how Load Balancer works and its advanced features below:

### **View Load Balancer List** <a href="#manageloadbalancer-2.xemdanhsachloadbalancer" id="manageloadbalancer-2.xemdanhsachloadbalancer"></a>

Use this guide to view a list of all available Load Balancers in the system.

**Access the Load Balancer list**

1. Go to the Load Balancer homepage;
2. On the Load Balancer home page, a list of Load Balancers will appear including information such as:
   * Load Balancer Name and Identifier: Load Balancer identifier duplication is supported;
   * Load Balancer Status: Indicates the current status of the Load Balancer
   * Other information such as: Endpoint, Type (Application/Network), Package used, Date created.

**Filter and Sort Load Balancer**

Users can sort the Load Balancer list as needed by clicking on the column name to be sorted in the Load Balancer list table such as: Sort by Name, Status, Endpoint, Load balancer type.

**Search Load Balancer**

To search for exactly one/many Load Balancers with the same/similar name, users can enter the Load Balancer name in the search box at the top right corner of the Load Balancer list table.

***

### **Manage Load Balancer details** <a href="#manageloadbalancer-3.quanlythongtinchitietloadbalancer" id="manageloadbalancer-3.quanlythongtinchitietloadbalancer"></a>

Access Load Balancer to view and manage details

**Access Load Balancer details**

1. Click on the Load Balancer to view details on the Load Balancer list screen.
2. Instructions for viewing Load Balancer information: The Load Balancer detail screen is divided into 3 main parts.
   * **Availability statistics**
     * Statistics of total number of Listeners in Load Balancer
     * Total Pool Statistics in Load Balancer
     * Statistics of number of active Pools / Total Pools
     * Statistics of number of Pools that are not working properly / Total number of Pools
   * **General information of Load Balancer**
     * Load Balancer name and identification information
     * Private subnet & Endpoint
     * Load Balancer Package Information: Connections, Data Transfer, Package name
   * **Details**
     * Listener: List and details of each Listener
     * Pool: List and details of each Pool
     * Monitor: List of Metrics and Logs

***

### **Change Load Balancer Package (Resize)** <a href="#manageloadbalancer-4.thaydoigoiloadbalancer-resize" id="manageloadbalancer-4.thaydoigoiloadbalancer-resize"></a>

The "Change Load Balancer Plan" feature is an important part of managing your Load Balancer. It allows you to customize and update service plans to suit both the financial and operational needs of a Load Balancer such as:

* Increase or decrease Connection and Data Transfer to accommodate changing traffic loads.
* Optimize the Load Balancer package configuration to suit actual needs after long-term use.

**How to change Load Balancer package**

1. Resize Load Balancer in 2 ways:
   * On the Load Balancer list screen: Click on **the "three dots" icon** at the end of each Load Balancer information row, a list of actions will appear, click on the **"Resize" action**
   * On the Load Balancer detail screen: Click on **the "Resize" action** in the upper right corner of the detail screen
2. After clicking "Resize", an interface window appears, including a list of available Load Balancer packages, **click to select the package to use** .
3. Check and Compare 2 Plans: After selecting a plan, users can **compare the current plan information and the new plan** in the information section on the right side of the pop-up window.
4. Confirm changes: Once you are sure, click **the "Resize Load Balancer" button** at the bottom right corner of the pop-up window to finish the Resize process.

Note

**Some notes to know when performing Resize:**

* The Resize process will take a certain amount of time, so your Load Balancer will be interrupted during this time and will resume normal operation after the process is complete.
* After successfully Resizing, users need to check the actual parameters/data of the Load Balancer in the Monitor tab, to ensure that the new Load Balancer package can meet actual usage needs.

***

### **Duplicate Load Balancer** <a href="#manageloadbalancer-5.duplicateloadbalancer" id="manageloadbalancer-5.duplicateloadbalancer"></a>

The "Duplicate Load Balancer" feature is an important part of managing your Load Balancer. It allows you to create an exact copy of an existing Load Balancer to use for different purposes or to ensure redundancy of your system.

**Why Duplicate Load Balancer?**

There are several reasons why you might want to replicate a Load Balancer:

* Ensure application redundancy and availability.
* Create a test or development environment that does not affect the current application.
* Create copies of tested and proven configurations to deploy to new applications.

**How to Implement Duplicate Load Balancer**

1. Resize Load Balancer in 2 ways:
   * On the Load Balancer list screen: Click on **the "three dots" icon** at the end of each Load Balancer information row, a list of actions will appear, click on the **"Duplicate" action**
   * On the Load Balancer details screen: Click on **the "Duplicate" action** in the upper right corner of the details screen
2. After clicking "Duplicate", an interface window appears allowing you to configure the necessary information, including:
   * **Load Balancer Name**
   * **Load Balancer Package**
   * **Listener Information:** To suit actual usage needs, the Duplicate feature allows the editor to edit the Listener information when Duplicate as
     * Add/Delete/Edit Certificate, SNI for Listener
     * Remove unnecessary Listeners for the new Load Balancer
3. Check Load Balancer package information: Configuration information on the right side of the pop-up window
4. Confirm Duplicate: Once you are sure, click **the "Duplicate Load Balancer" button** at the bottom right corner of the pop-up window to finish the Duplicate process.

Note

**A few things to know when performing Duplicate:**

* Duplicate ensures that the new Load Balancer is created with 100% exact configuration from the selected Load Balancer (unless the Load Balancer and Listener packages are changed).
* Duplicate Load Balancer will take a certain amount of time, the more complex the configuration of the Load Balancer selected for Duplicate, the longer it will take to provide service.

***

### **Delete Load Balancer** <a href="#manageloadbalancer-6.xoaloadbalancer" id="manageloadbalancer-6.xoaloadbalancer"></a>

Before deleting the Load Balancer, users need to consider carefully, because once deleted, the Load Balancer cannot be restored.

**How to delete a Load Balancer**

1. There are 2 ways to delete a Load Balancer:
   * On the Load Balancer list screen: Click on **the "three dots" icon** at the end of each Load Balancer information row, a list of actions will appear, click on the **"Delete" action**
   * On the Load Balancer details screen: Click **the "Delete" action** at the top right corner of the details screen
2. After clicking "Delete", a delete interface window appears to confirm the user's action to delete the Load Balancer.
3. Click "Delete" to complete the deletion of the Load Balancer.

**How to delete multiple Load Balancers**

1. Access the Load Balancer list screen
2. Select the Load Balancer to delete in the check box at the top of each Load Balancer information row.
3. Click the "Delete" button in the upper left corner of the Load Balancer list table
4. A delete interface window pops up to confirm the user's action to delete the Load Balancer.
5. Click "Delete" to complete the deletion of the selected Load Balancers.
