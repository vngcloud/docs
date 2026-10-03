# Resource Tagging

### Overview

**Why tag resources?**

* **Organize and manage resources efficiently:** Tagging resources helps you categorize and group them by various criteria such as owning department, purpose, environment (dev, test, prod), etc.
* **Easily search and filter resources:** Instead of manually searching for each resource, you can use tags to quickly filter and find resources that meet specific criteria.
* **Automate tasks:** You can use tags to automate resource management tasks such as backup, deletion, or applying different security policies to different resource groups.
* **Allocate costs:** Based on tags, you can allocate resource usage costs to different departments or projects.

**Benefits of using Resource Tagging:**

* **Improve productivity:** Reduce the time spent searching for and managing resources.
* **Increase accuracy:** Minimize risks from manual resource management.
* **Optimize costs:** Allocate resource usage costs appropriately.
* **Ensure security:** Apply suitable security policies to each resource group.

### Features

#### **1. Tag resources**

**Step 1:** Go to the resource statistics page here: [https://dashboard.console.greennode.ai/resource](https://dashboard.console.greennode.ai/resource)

**Step 2:** Select one or more resources you want to tag (see image below)

<figure><img src="https://3672463924-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FB0NrrrdJdpYOYzRkbWp5%2Fuploads%2Fgit-blob-f94830930d9312b600a56fc77e31bf40b8d4b2b6%2Fimage.png?alt=media" alt=""><figcaption></figcaption></figure>

**Step 3:** Click the "Manage tags" button or the tag icon in the table header.

A window will open allowing you to add or remove the resource's tag information, as follows:

<figure><img src="https://3672463924-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FB0NrrrdJdpYOYzRkbWp5%2Fuploads%2Fgit-blob-0788a5b0d83279fc2157fd5a87ba04ff4e2894db%2Fimage.png?alt=media" alt="" width="375"><figcaption></figcaption></figure>

1. **Default tag:** Resources are automatically tagged with `vng.createdBy`, whose value is the identifier of the IAM User or Root User who created the resource. This tag cannot be deleted.
2. **Custom tags:**
   * **Select a tag type:** You can choose from predefined tag types such as `Assignee`, `Company,Department`, `Environment`.
   * **Enter a value:** Enter a specific value for the tag (e.g. `Assignee=Sultu`, `Department=Engineering`). Click the "Add" button to confirm adding the tag

**Step 4:** Click the "Save" or "Apply" button to finish tagging.

#### **2. Search resources by tag**

**Step 1:** Go to the resource statistics page here: [https://dashboard.console.greennode.ai/resource](https://dashboard.console.greennode.ai/resource)

**Step 2:** Locate the search box as shown below:

<figure><img src="https://3672463924-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FB0NrrrdJdpYOYzRkbWp5%2Fuploads%2Fgit-blob-00372566592ba602b8d570b92b9b5313c591cca0%2Fimage.png?alt=media" alt=""><figcaption></figcaption></figure>

**Step 3:** Enter the value of the tag you want to search for (e.g. `Sultu`).

**Step 4:** The system will display a list of resources with a tag whose value is Sultu.

**Note:**

* **Tag values:** Tag values must be exact and follow the specified format.
* **Permissions:** Only the Root User can add or edit resource tags. IAM Users can only view them.

#### 3. Sync tag information to invoices

The tag-to-invoice sync feature closely links resource information with billing information. Specifically:

* **Purpose:** Ensures consistency between resource information and invoices, enabling more accurate cost tracking, management, and allocation.
* **How it works:**
  * When a new resource is created, the system automatically creates a corresponding invoice.
  * When you tag a resource, the tag information is **not synced immediately** to the invoice.
  * **End of the reconciliation period:** The system syncs tag information from the resource to the corresponding invoice only once.
  * **Note:** Only tags attached to the resource **before the end of the reconciliation period** are synced. Tags edited afterwards will not be updated on the invoice.

**To view tag information on an invoice:**

1. **Go to the billing report page:** [https://dashboard.console.greennode.ai/billing-report](https://dashboard.console.greennode.ai/billing-report)
2.  **Export invoice:** Click the "Export invoice" button to download a full copy of the invoice.

    <figure><img src="https://3672463924-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FB0NrrrdJdpYOYzRkbWp5%2Fuploads%2Fgit-blob-78546b5c8c0b74128df5a0f350856ebc9d620782%2Fimage.png?alt=media" alt=""><figcaption></figcaption></figure>
3. **Check tag information:** In the exported invoice copy, you will find a section listing the tags attached to the resources related to that invoice.

**Note:**

* **Sync timing:** Tag information is synced at the end of the invoice's reconciliation period.
* **Synced data:** Only the resource's tag information at the end of the reconciliation period is synced.
* **Purposes of tag information on invoices:**
  * **Cost analysis:** Based on tags, you can analyze resource usage costs by criteria such as department, project, etc.
  * **Asset tracking:** Easily identify resources related to a specific invoice.
  * **Auditing:** Provides detailed information to support auditing.
