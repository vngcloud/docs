# Restoring RDS Instance

GreenNode vDB allows you to restore a new RDS Instance from a previous backup. This restore process is independent of the backup type (Full Backup or Incremental Backup) or how the backup was created (Manual Backup or Automatic Daily Backup).

#### To initiate the restore process:

1. Access the **Backup Management Screen** for vDB Relational at the provided link.
2. Select the backup you want to restore, and then choose **Action Restore**.

The restore process is similar to creating a new RDS Instance.

#### Steps for restoring:

**Step 1: Basic Configuration**

* You can assign a name for the new RDS Instance.

**Step 2: Technical Specifications**

* Customize the configuration, including **Flavor (CPU/Memory)**, **Storage Type**, and **Storage Size**.

**Step 3: Network and Security**

* Choose the **Cloud Network** and enable/disable **Public Accessibility** (Internet access). The Cloud Network can be the same or different from the old RDS Instance.

**Step 4: DB Options**

* In the **DB Options** section, you can select a **DB Configuration Group** (Optional) for the new RDS Instance. This could be the same or different from the old RDS Instance.

**Step 5: Backup Settings**

* Configure the **Automatic Backup** settings, including **Backup Retention Period** and **Backup Time**.

After confirming that all information is correct, click the **Restore Backup** button.

Once completed, return to the **Database Management Screen**, where you will see the new RDS Instance being restored.

The status of the RDS Instance will change from **Building/Build** to **Active** if the restoration is successful.

The **Master User** and **Database Name** information will remain unchanged.
