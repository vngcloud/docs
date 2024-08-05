# Manage MDS Config Group

Configuration Groups are collections of configuration variables for MDS Instance database services. Instead of manually editing configuration files and restarting services, you can make changes quickly and easily with Configuration Groups. Even better, a single Configuration Group can be applied to multiple MDS Instances, allowing you to configure once and apply to many.

To access Configuration Groups, go to the MemoryStore database service and switch to the Configuration Group section: https://vdb.console.vngcloud.vn/memorystore/config-group

**A. Creating a Configuration Group**

To create a Configuration Group, click "Create Configuration Group." On the creation screen, you can configure:

* **Configuration Group Name:** The name of the Configuration Group.
* **Engine:** The type of Database Engine that can apply this Configuration Group.
* **Engine Version:** The type of Engine Version that can apply this Configuration Group. Only MDS Instances with the matching Database Engine & Version can apply this Configuration Group.
* **Descriptions:** Description for this Configuration Group.

After ensuring the information is correct, click "Create" in the upper right corner, and you will see the created Configuration Group.

**B. Editing Configuration Variables**

To configure the values of a Configuration Group, left-click on the name of the Configuration Group. Here, you can view all the configuration variables of this group. Each variable includes:

* **Name:** Variable name.
* **Value:** The current configuration value of the variable. By default, VNG Cloud does not configure any variables and keeps the default values of the Database Engine.
* **Allowed Values:** Allowed configuration values for each variable.
* **Data Type:** The data type of the value that can be applied to this configuration variable.

To edit configuration variables:

1. On the Configuration Group details screen, click "Edit parameter."
2. You can quickly search for variables in the "Search" box. At the variable you want to configure, enter or select the desired value.
3. After entering or selecting the value, you can click "Save" immediately or click "Preview Changes" to preview the changes. If you are sure, click "Save" to save the changes.
4. For the system to actually apply the changes, click "Apply Change" to apply the changes to all MDS Instances linked to this Configuration Group.

The linked or to-be-linked MDS Instances will be applied with these new values. You can go back to the Database management screen to see the process of applying the new configuration. If the application is successful, the MDS Instance will have the status "Active."

Note: In some cases, configuration variables may require restarting the Database service on the MDS Instance. The status of the MDS Instance will then be "Restart\_required." With VNG Cloud, you can proactively choose the time to perform this operation. After backing up tasks on the MDS Instance, click "Action" and choose "Restart" to complete the process.

**C. Linking MDS Instances with Configuration Groups**

To link an MDS Instance with an existing Configuration Group, you have two options:

1. Link it immediately when the MDS Instance is created.
2. Modify the MDS Instance configuration.

For option 1, please refer to the instructions on Creating an MDS Instance.

For option 2, you can do the following:

1. Go to the Database management screen at: https://vdb.console.vngcloud.vn/memorystore/database
2.  Select the MDS Instance and click "Edit Configuration Group."&#x20;

    <figure><img src="../../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure>
3. On the change screen, select the Configuration Group you want to apply.
4. When all selections are correct, click the "SAVE" button in the upper right corner. Wait for a while for the configuration variables to be applied to the MDS Instance. If the change is successful, the MDS Instance will have the status "Active."

Note: In some cases, configuration variables may require restarting the Database service on the MDS Instance. The status of the MDS Instance will then be "Restart\_required." With VNG Cloud, you can proactively choose the time to perform this operation. After backing up tasks on the MDS Instance, click "Action" and choose "Restart" to complete the process.

**D. Delete Configuration Group**
