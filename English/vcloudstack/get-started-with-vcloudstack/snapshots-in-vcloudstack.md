# Snapshots in vCloudStack

### Overview <a href="#tong-quan" id="tong-quan"></a>

Snapshots are a key component of any storage system. They provide the ability to create and manage backup versions of your virtual disk data at specific points in time, providing important benefits in protecting data, optimizing resources, and ensuring data recovery should the need arise.

Each snapshot contains all the information needed to restore your data to the state it was in when the snapshot was created. When you create a new drive based on a snapshot, the new drive starts as an exact copy of the original drive used to create the snapshot. The copying process is done in the background so you can start using it immediately. If you access data that isn't loaded yet, the drive automatically loads the required data from the system, then continues loading the rest of the drive's data in the background.

Snapshots also support end-to-end data encryption, ensuring the security of stored data and helping to comply with security and privacy requirements. You can create snapshots of encrypted drives and create new drives from encrypted snapshots.

vCloudStack supports creating Snapshots for both Servers and Volumes, simplifying the Snapshot creation process and adapting to your needs. Once you have created a Snapshot for your virtual server and virtual disk, you can use our Roll Back feature to restore the state of your virtual machine and virtual disk to the time the Snapshot was created.

**The drive you want to create a Snapshot on is in In Use** or **Not Attached** state . Note the following:

* If the disk is in **the In Use state:** make sure that the instance the disk is mounted on is in the Running or Stopped state.
* If the disk is in **Not Attached state:** make sure the disk was attached to a Server at some point. It is not possible to create snapshots for cloud disks that have never been attached to a VM.

***

#### **Create Snapshot** <a href="#taosnapshot-taosnapshotchovolumetrenbangdieukhien" id="taosnapshot-taosnapshotchovolumetrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Snapshot page.

**Step 2:** Select create **Snapshot**

**Step 3:** On the Snapshot creation information entry page, you need to complete the following items:

* **Snapshot Type** – Default by Server.
* **Snapshot Name** – The system automatically generates it based on the VM name and the time the Snapshot was created.
* **Select Volume** – Select the type of resource you want to backup, here is the list of Servers and Volumes attached to it.
* **Policy Settings:** Select **the Policy** you want to apply to the snapshot.

**Step 4: Enter notes** for your backups to create a reminder

**Step 5:** Select the **Create** button to confirm the initialization. The Status field displays **Creating** when the Snapshot is created. This action prompts the cloud infrastructure to start collecting data from the selected drive.

***

#### **Restore virtual server using Snapshot on dashboard** <a href="#khoiphucmaychuaobangbansnapshot-khoiphucmaychuaobangsnapshottrenbangdieukhien" id="khoiphucmaychuaobangbansnapshot-khoiphucmaychuaobangsnapshottrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Snapshot page.

**Step 2:** Select create **Snapshot**

**Step 3:** Select the Snapshot of the Boot Volume on the list page, then select **Action** , click Rollback Server **.**

#### **Create Server using Snapshot on Create Server Screen** <a href="#khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhtaoserversnapshotcreateserve" id="khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhtaoserversnapshotcreateserve"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack.

**Step 2:** In the navigation pane, select **Servers** ;

**Step 3:** Select the " Create a **Server** " button to navigate to the Create Server screen;

**Step 4:** To configure Create Server using snapshot. In " **Basic configuration/Image** " section, select " **My snapshot** " tab;

**Step 5:** User can choose the appropriate snapshot to recreate the Server at the corresponding time.

{% hint style="info" %}
**Note:** When configuring to create a new Server using Snapshot, the user still performs configuration operations in other items (Configuration type, volume, Network settings, Other settings) as usual, see instructions in [Initializing VM on vCloudstack](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/bat-dau-voi-vcloudstack/khoi-tao-vm-tren-vcloudstack) .
{% endhint %}

#### **Create Server using Snapshot on Snapshot Screen** <a href="#khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhsnapshot" id="khoiphucmaychuaobangbansnapshot-taomaychu-server-bangsnapshottrenmanhinhsnapshot"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Snapshot page.

**Step 2:** At the Snapshot list screen, User **clicks on a Snapshot Server** to navigate to the detailed information screen.

**Step 3:** At the Snapshot Server detail screen, User selects the " **Restore Point** " Tab.

**Step 4:** Then select the corresponding Snapshot version you want to create the Server for, by clicking on the action button, select " **Create server** ".

**Step 5:** Navigate to the Create Server screen with the Snapshot file option selected, and continue the same operation as "Create Server using Snapshot on the Create Server Screen" above.

#### **Restore virtual drive using Snapshot on console** <a href="#khoiphucodiaaobangbansnapshot-khoiphucodiaaobangsnapshottrenbangdieukhien" id="khoiphucodiaaobangbansnapshot-khoiphucodiaaobangsnapshottrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack.

**Step 2:** In the navigation pane, select **Snapshot** ;

**Step 3:** Select Snapshot of the Data Volume on the list page, then select **Action** , click Rollback Volume **.**

#### **Delete Snapshot Volume in Snapshot list page on dashboard** <a href="#xoasnapshot-xoasnapshotvolumetaitrangdanhsachsnapshottrenbangdieukhien" id="xoasnapshot-xoasnapshotvolumetaitrangdanhsachsnapshottrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack.

**Step 2:** In the navigation pane, select **Snapshot** ;

**Step 3:** Select the Snapshot to delete, then select **Action** , click **Delete Snapshot.**

#### **Delete Snapshot Volume on Volume details page on dashboard** <a href="#xoasnapshot-xoasnapshotvolumetaitrangchitietvolumetrenbangdieukhien" id="xoasnapshot-xoasnapshotvolumetaitrangchitietvolumetrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack.

**Step 2:** In the navigation pane, select **Volume** ;

**Step 3:** Click on the Volume name to go to the Volume details page

**Step 4:** Switch to the **Associated Snapshot Tab**

**Step 5:** Select the Snapshot Volume to delete and select **Delete Snapshot Volume Point**

#### **Delete Server Snapshot on Server details page on dashboard** <a href="#xoasnapshot-xoasnapshotservertaitrangchitietservertrenbangdieukhien" id="xoasnapshot-xoasnapshotservertaitrangchitietservertrenbangdieukhien"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack.

**Step 2:** In the navigation pane, select **Server** ;

**Step 3:** Click on the Server name to go to the Server details page

**Step 4:** Switch to the **Associated Snapshot Tab**

**Step 5:** Select the Snapshot Server to delete and select **Delete Snapshot Volume Point.**
