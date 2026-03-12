# Manage Access to OpenSearch Cluster

In the **GreenNode** **vDB OpenSearch** service, you can access OpenSearch in two ways:

* **Log in to OpenSearch Dashboard** to manage and analyze data.
* **Push logs to OpenSearch Cluster** for log storage and processing.

We provide **two endpoints with different ports**, but **share the same Master User account** to perform both tasks.

## Access OpenSearch Dashboard

To log in to the OpenSearch management interface, use the following information:

* **Endpoint:** `https://your-cluster-name-hcm03.vdb-opensearch.vngcloud.vn`
* **Port:** `443`
* **Username:** `master-user`
* **Password:** (The password you set up)

Use a browser to access the URL above and log in with the Master User account.

## Push Logs to OpenSearch Cluster

To send logs to the OpenSearch system, use the following information:

* **Endpoint:** `https://your-cluster-name-hcm03.vdb-opensearch.vngcloud.vn`
* **Port:** `9200`
* **Username:** `master-user`
* **Password:** (The password you set up)

{% hint style="info" %}
**Note:**

* Currently, we only support **1 public endpoint mode**, which means by default if you do not set up Allowed CIDRs, **anyone with the Master User account information** can access the cluster. To limit access, you can **configure the allowed IP list (Allow CIDRs)** on the cluster following the guide below.
{% endhint %}

## Control access to OpenSearch Dashboard / push logs to OpenSearch Cluster

You can control access... by:

* When initializing an OpenSearch Cluster, in the Network setting section, enter the CIDRs you want to allow access to the Dashboard or push logs. CIDRs can be separated by commas, for example 10.192.168.8/16, 10.192.160.10/24
* When an OpenSearch Cluster has already been initialized, you can edit by going to the detail of a Cluster, in the Connectivity & Security section, select the Edit button at the Allowed CIDRs field for each Dashboard or Receive Logs section

Below is the complete guide, with additional information on how to control OpenSearch access clearly and easily:

### **Set Up CIDRs When Initializing Cluster**

When creating a new OpenSearch Cluster, you can configure CIDRs by:

* In the **Network Setting** section of the cluster initialization interface, **enter the list of CIDRs** that you want to grant access to the **Dashboard** or **Receive Logs**. CIDRs are separated by commas (`,`). For example: `10.192.168.8/16, 10.192.160.10/24`.

**Complete the Cluster creation process**, these CIDRs will be applied immediately.

### **Edit CIDRs After Cluster Has Been Initialized**

If you want to change the CIDRs list after the cluster has been initialized:

**Step 1: Access** the OpenSearch Cluster you want to edit.

**Step 2: Go to the** `Connectivity & Security` tab.

**Step 3: In the Accessibility section:**

* Select **Edit** at the **Dashboard** field to edit CIDRs for management interface access.
* Select **Edit** at the **Receive Logs** field to edit CIDRs for the log receiving endpoint.

**Step 4: Enter new CIDRs** in valid format. CIDRs are separated by commas (`,`). For example: `10.192.168.8/16, 10.192.160.10/24`.

**Step 5: Press Save** to update the changes.
