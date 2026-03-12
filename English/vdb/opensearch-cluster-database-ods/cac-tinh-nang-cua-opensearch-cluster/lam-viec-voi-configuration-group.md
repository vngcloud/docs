# Working with Configuration Group

In **GreenNode's** **vDB OpenSearch**, we support configuring your DB operating parameters **through Configuration Group**, helping you easily manage and optimize performance for your OpenSearch Cluster.

## **Default Configuration Group**

* When you create an **OpenSearch Cluster**, the system will automatically assign a **Default Configuration Group** based on the OpenSearch version you select.
* Currently, we provide **2 Default Configuration Groups** corresponding to:
  * **OpenSearch v2.15**
  * **OpenSearch v2.17**
* You **cannot edit or delete** these Default **Configuration Groups**.

## **Create & Attach Custom Configuration Group**

If you want to customize configuration parameters, create **a new Configuration Group** and attach it to your OpenSearch Cluster.

### **Initialize a Configuration Group**

**Step 1:** Access [https://vdb.console.vngcloud.vn/](https://vdb.console.vngcloud.vn/)

**Step 2:** Select **Configuration group** under the **OpenSearch** section.

**Step 3:** Select **Create a Configuration group".** The create new configuration group screen appears, where you need to:&#x20;

Enter the required information:

* **Configuration Name**:
  * Only allows characters: `a-z`, `A-Z`, `0-9`, `_`, `-`, `.`, `@` and spaces.
  * Must start with a letter.
  * Length from **5 to 50 characters**.
* **Description** (Brief description of the Configuration Group).
* **OpenSearch Version**: Select the version compatible with your OpenSearch Cluster.

**Step 4:** Select **Create** to complete the Configuration Group creation.

### Edit parameters in a Configuration Group

After a Configuration Group is created, you can edit parameters in this Configuration Group by:

**Step 1:** Select the **Configuration group** you have created

**Step 2:** Select **Edit parameters**

**Step 3:** Select/Enter parameter values according to the specified **Allowed Values** and **Data Type**.

**Step 4:** Select **Preview and Save** then review the changes you have updated

**Step 5:** Agree that **Edit parameter** may affect your DB

**Step 6**: Select **Apply**

### **Attach Configuration Group to OpenSearch Cluster**

**Step 1: Select** the icon <img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" data-size="line"> on the cluster where you want to change the configuration group

**Step 2:** Select **Edit Configuration group**

**Step 3:** Select a **Configuration Group** that you want to apply.

**Step 4: Select Save** to complete.

{% hint style="info" %}
**Note:**

* Each OpenSearch Cluster must always have at least one Configuration Group.
* One Configuration Group can be attached to multiple OpenSearch Clusters simultaneously.
* You can create multiple custom Configuration Groups to suit different usage purposes
{% endhint %}
