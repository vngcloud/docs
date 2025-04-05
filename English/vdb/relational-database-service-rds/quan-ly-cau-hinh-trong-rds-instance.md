# Managing Configuration Group in RDS Instance

#### Configuration Groups Overview

A **Configuration Group** is a set of configuration parameters for an RDS Instance's database service. Instead of manually editing configuration files and restarting services as in traditional methods, you can make changes quickly using Configuration Groups. Additionally, a Configuration Group can be applied to multiple RDS Instances, allowing you to configure once and apply to many.

You can access the vDBaaS service and navigate to the **Configuration Group** section to manage your Configuration Groups.

#### A - Creating a Configuration Group

To create a Configuration Group, click **CREATE CONFIGURATION GROUP**.

In the creation screen, you can configure the following:

* **Configuration Group Name**: The name for the Configuration Group.
* **Engine**: The database engine type that this Configuration Group can be applied to.
* **Engine Version**: The engine version that the Configuration Group can be applied to. Only RDS Instances with the compatible engine type and version can use this Configuration Group.
* **Description**: A description for the Configuration Group.

Once you confirm the information is correct, click **CREATE CONFIGURATION GROUP** at the top right, and the Configuration Group will be created.

To configure the values of the Configuration Group, click the name of the Configuration Group. You can then view all the configuration parameters, which include:

* **Name**: The parameter's name.
* **Value**: The current configuration value for the parameter. By default, VNG Cloud does not configure any parameters and keeps the database engine’s default values.
* **Allowed Values**: The allowed values for each parameter.
* **Data Type**: The data type of the value that can be applied to this configuration parameter.

#### B - Editing Configuration Parameters

To edit the configuration parameters, in the **Configuration Group** details screen, click **EDIT PARAMETER**.

Enter or select the value for the parameter you want to configure. You can search for parameters quickly using the **SEARCH** box.

After entering or selecting the value, you can click **Save** immediately, or click **Preview Changes** to see the changes first. If you're sure about the changes, click **Save Changes** to save them. To apply the changes to all RDS Instances linked to this Configuration Group, click **Apply Change**.

The configuration changes will be applied to all RDS Instances associated or about to be associated with this Configuration Group. You can go back to the **Database Management Screen** to monitor the configuration application process. If successful, the RDS Instance will show the status **ACTIVE**.

**Note**: In some cases, changing a configuration parameter may require restarting the database service on the RDS Instance. In this case, the RDS Instance status will change to **RESTART\_REQUIRED**. With VNG Cloud, you can control when to perform this action. After backing up the tasks on the RDS Instance, click **ACTION** and choose **RESTART** to complete the process.

#### C - Linking RDS Instances to Configuration Groups

To link an RDS Instance to an existing Configuration Group, you have two options:

1. Link the Configuration Group during the RDS Instance creation.
2. Modify the configuration of an existing RDS Instance.

**Option 1: Link During RDS Instance Creation**

Please refer to the **RDS Instance Creation Guide** for more information.

**Option 2: Modify Existing RDS Instance Configuration**

To link an RDS Instance to a Configuration Group, follow these steps:

1. Go to the **Database Management Screen**, select the RDS Instance, and click **EDIT DATABASE**.
2. In the RDS Instance configuration screen, scroll to the **CHANGE CONFIGURATION GROUP** section. In the **New Configuration Group** field, select the Configuration Group you created earlier.
3. Once the selection is correct, click **SAVE** at the top right. Wait for the configuration changes to be applied, and if successful, the RDS Instance will show the status **ACTIVE**.

**Note**: Similar to parameter editing, some configuration changes may require a **RESTART** of the database service on the RDS Instance. In this case, the status will change to **RESTART\_REQUIRED**. Once you have backed up the tasks on the RDS Instance, click **ACTION** and select **RESTART** to complete the process.
