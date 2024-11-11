# Backup Location

**Backup Location** is an important concept in data backup services. It represents a specific storage area designated to store backups (Backup Server Point) of a server or application. Using Backup Location effectively helps users manage, protect and restore data flexibly and securely.

## Outstanding features <a href="#tinh-nang-noi-bat" id="tinh-nang-noi-bat"></a>

1. **Cross-region Backup:**
   * **Meaning:** This is storing the backup in a different geographical area than where the original server is located.
   * **Benefit:**
     * **Disaster protection:** Minimize the risk of data loss due to natural disasters, infrastructure failures in an area.
     * **Increased availability:** Even if one region fails, data is still securely protected in other regions.
     * **Regulatory Compliance:** Meet data storage requirements across multiple regions for certain industries.
2. **Soft Delete:**
   * **Meaning:** When a backup is deleted, it is not permanently deleted immediately but moved to the virtual recycle bin.
   * **Benefit:**
     * **Recover Deleted Data:** Users can restore deleted backups within a certain period of time.
     * **Avoid losing important data:** Prevent data loss due to accidental deletion.
3. **Location Lock:**
   * **Meaning:** Set retention rules and configuration changes for backups at a specific location.
   * **Benefit:**
     * **Protect important data:** Prevent unauthorized deletion or modification of backups.
     * **Regulatory Compliance:** Ensure compliance with regulatory data retention requirements.

## Create Multiple Backup Locations: Benefits and How to Manage Them <a href="#tao-nhieu-backup-location-loi-ich-va-cach-quan-ly" id="tao-nhieu-backup-location-loi-ich-va-cach-quan-ly"></a>

* **Benefit:**
  * **Data Classification:** Organize backups by server group, project, or department.
  * **Efficient Management:** Easily track and manage storage capacity of each location.
  * **Cost Optimization:** Use different types of storage (e.g. cloud storage, local storage) to optimize costs.
  * **Enhanced Security:** Decentralize access to different storage locations to ensure data security.
* **How to manage:**
  * **Create New:** Create new Backup Locations with different configurations (region, capacity, deletion policy).
  * **Configuration:** Configure features like Soft Delete, Location Lock for each location.
  * **Assign:** Assign Backup Servers to appropriate Backup Locations.
  * **Monitoring:** Monitor usage and status of backups at each location.

## **Summary**

Using Backup Location flexibly helps users build a comprehensive data backup strategy, protect data from risks and ensure system availability. By taking advantage of features such as Cross-region Backup, Soft Delete, Location Lock and the ability to create multiple Backup Locations, users can manage their data efficiently and securely.
