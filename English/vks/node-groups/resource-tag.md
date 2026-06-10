# Resource Tag

### 1. Overview

**Resource Tag** lets you attach a set of key/value labels to all resources — including servers and volumes — that belong to a **Node Group**. **Resource Tag** is automatically applied to:

* All **Servers** in the **Node Group**.
* All **Block Volumes** managed by **VKS** that are attached to those servers — including root disks, data disks, and **CSI** volumes dynamically provisioned through a **PVC**.

You can use **Resource Tag** to:

* **Cost allocation** — tag resources by department / project / environment to break down billing.
* **Administration & lookup** — filter resources in the **vServer** console by tags.
* **Automation** — let your internal tools rely on tags to classify resources.

#### How it works

* **Resource Tag** is continuously enforced — if someone edits or deletes a VKS-managed **Resource Tag** in the **vServer** console, the **VKS** system automatically restores it.
* **Volumes attached later** (a **PVC** created through **CSI**) are also tagged automatically by the **VKS** system.
* **Resource Tag** is applied automatically by the **VKS** system within up to 15 minutes after a **Server** / **Volume** is created.

> **Note for IAM users**
>
> An IAM user must be granted the permission below (an admin should grant it once before use):

| Permission                | Purpose                                                | Used at step                 |
| ------------------------- | ------------------------------------------------------ | ---------------------------- |
| `UpdateNodeGroupMetadata` | Update metadata (Label / Taint / Tag) for a Node Group | Updating Node Group metadata |

### 2. Configuration Guide

#### Create Resource Tag

**Resource Tag** for a **Node Group** is configured when you create a **Cluster / Node Group**, under the section **Default Node Group Configuration → Node Group Metadata Setting (Optional)**.

**Step 1:**

1. Go to the [VKS Console](https://vks.console.vngcloud.vn/overview).
2. Click **Create a Kubernetes Cluster / Node Group**.

**Step 2:** Enter tags under **Node Group Metadata Setting**

1. Open the **Node Group Metadata Setting (Optional)** section.
2. Click **Add Tag** to add a new one.
3. Enter a **Key** and **Value** for each tag.
4. Repeat to add multiple tags.

#### Update Resource Tag

**Step 1:** Open the **Cluster** detail page

1. Go to the [VKS Console](https://vks.console.vngcloud.vn/overview).
2. Select the **Cluster** that contains the **Node Group** whose tags you want to edit.

**Step 2:** Choose the **Edit Metadata** action

1. Select the **Node Group** tab.
2. On the **Node Group** you want to edit, click the **Action** menu.
3. Choose **Edit Metadata**.

**Step 3:** Add, edit, or delete **Resource Tag**.

**Step 4:** Save your changes

1. Review the list of **Resource Tags**.
2. Click **Save** to apply.

### 3. System Tags (VKS Managed)

In addition to your **Resource Tag**, the **VKS** system always attaches the following three tags to every resource in a node group:

| Key                   | Meaning                      |
| --------------------- | ---------------------------- |
| `vng.vks.cluster.id`  | Cluster identifier           |
| `vng.vpc.id`          | The resource's network (VPC) |
| `vng.billing.product` | `vks` (used for billing)     |

* You **do not need to** and **cannot** configure these tags yourself.
* If these tags are deleted manually in the console, the **VKS** system re-applies them automatically.

#### Reserved prefixes (not allowed)

To avoid overwriting system markers, you **must not** create keys that start with the following prefixes:

```
vng.vks.    vng.vpc.    vng.billing.    vks-    vks-mgmt-
```

Tags using these prefixes will be **ignored** (not applied).

### 4. Behaviors to Be Aware Of

**4.1 Tags you apply yourself are preserved**

If you apply tags directly in the **vServer** console, those tags are kept and the **VKS** system does not delete them. The **VKS** system only manages the tags you declare through the **VKS** portal.

**4.2 Self-healing when modified**

* If someone changes the value of a VKS-managed tag in the **vServer** console → the system restores it to the value you configured.
* If a system tag is deleted in the **vServer** console → the **VKS** system re-applies it automatically.

**4.3 Only VKS-managed volumes are tagged**

The system only tags volumes managed by **VKS** (root disks, data disks, **CSI** volumes). If you attach a different volume to a **Server** yourself (one not managed by **VKS**), that volume will not receive the Node Group's **Resource Tag**.

### 5. Resource Tag Quota

**vServer** limits the maximum number of tags per resource (the `TAG_PER_RESOURCE` quota). Note that:

* Each resource already has **3 system tags** taking up quota.
* If the total number of tags (system + yours) **exceeds the quota**, tag synchronization for that resource will **fail**.

When this happens, you will see a warning message such as:

```
Exceeded TAG_PER_RESOURCE quota on N resource(s): ...
Please reduce the number of Resource Tags, or request a tag quota increase on vServer
```

**How to resolve:** reduce the number of tags, or contact support to increase the tag quota on **vServer**.

### 6. Monitoring & Notifications

The **VKS** system supports related events, surfaced through **Cluster events** in the portal:

| Type                    | When                                           | Meaning                                                                                                                          |
| ----------------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `UserTagsUpdated`       | When you change Resource Tag and sync succeeds | Confirms the new tags were applied — the message lists the current tags (or "Removed all Resource Tags" if you removed them all) |
| `UserTagsQuotaExceeded` | When a resource exceeds the tag quota          | Warns that you need to reduce tags or increase the quota                                                                         |
