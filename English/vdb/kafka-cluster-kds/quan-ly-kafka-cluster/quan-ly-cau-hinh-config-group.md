# Manage Configuration (Config Group)

## What is a Kafka Config Group?

A Kafka Config Group is a collection of Kafka configuration parameters. You can create multiple different Config Groups to manage configurations for different environments (development, staging, production) or different applications.

## Manage Kafka Config Group

**1. Create New Config Group**

* **Access Kafka Config Group:** Log in to vDB and select the Config Group page here: [https://vdb.console.vngcloud.vn/kafka/config-group](https://vdb.console.vngcloud.vn/kafka/config-group)
* **Click "Create New" button:** Click the "Create Config Group" button to start creating a new Config Group.
* **Set name and description:** Enter a name for the Config Group and a brief description (optional).
* **Add configuration parameters:** Add the necessary Kafka parameters to the Config Group. You can use the graphical interface or enter parameters directly as text.
* **Save Config Group:** Click the "Save" button to create the new Config Group.

**2. Create New Version from Config Group**

* **Select Config Group:** From the Config Groups list, select the Config Group for which you want to create a new version.
* **Click "Create Version" button:** Find and click the "Create Version" button.
* **Select source version (optional):**
  * By default, the new version will copy the configuration from the latest version.
  * You can also select a specific version to copy the configuration from. This helps you easily apply similar configurations to different Kafka clusters and minimize risk when adjusting.
* **Edit parameters (if needed):** If you want to change the configuration, edit the parameters in this new version.
* **Save new version:** Click the "Save" button to create the new version of the Config Group.

**3. Apply Config Group to Kafka Cluster**

* **Select Kafka Cluster:** Select the Kafka cluster you want to apply the configuration to.
* **Select "Configuration" section:** In the Kafka cluster management interface, find and select the "Configuration" section.
* **Select Config Group:** From the Config Groups list, select the Config Group you want to apply.
* **Select version:** If the Config Group has multiple versions, select the specific version you want to apply.
* **Confirm and apply:** Review the changes and click the "Apply" button to update the configuration for the Kafka cluster.

**4. Delete Version or Config Group**

* **Select Version or Config Group:** From the list, select the Version or Config Group you want to delete.
* **Check deletion conditions:** The system will check whether that Version or Config Group is currently applied to any Kafka cluster.
* **Confirm and delete:** If no Kafka cluster is using it, you can click the "Delete" button to delete the Version or Config Group. If it is in use, you will receive a notification and cannot delete until it is removed from the related Kafka clusters.

**Important Notes:**

* Changing configurations may affect the operation of the Kafka cluster. Make sure you understand the parameters thoroughly before applying.
* It is recommended to create a new version of the Config Group before making major changes, so you can easily revert to the old version if needed.
* Always thoroughly test changes in a testing environment before applying to the production environment.
