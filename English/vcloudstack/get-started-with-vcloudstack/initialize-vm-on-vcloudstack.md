# Initialize VM on vCloudStack

### Overview <a href="#tong-quan" id="tong-quan"></a>

After successfully configuring the infrastructure device and connecting to the VNG Cloud cloud system, users can initialize a virtual server at the User Site interface on the internal infrastructure. In addition, users need to Create Network first to be ready to initialize a virtual server.

***

### Steps to follow: <a href="#cac-buoc-thuc-hien" id="cac-buoc-thuc-hien"></a>

**Step 1** : User accesses and logs in to User Site;

If the user accesses the vServer section of VNG Cloud, they can access the registered vCloudstack by clicking on the Region section and **selecting the Region of vCloudStack.**

**Step 2:** At the User Site interface, on the Navigation bar, select Server/Servers;

**Step 3:** On the Servers screen, select Create a new Server;

**Step 4:** At the Create Server screen, allow users to fill in the information to initialize as follows:

* **Server name** : enter the server name to identify the server after creation;
* **Tag:** Tag the server;
* **Your Image:**
  * OS: Select operating system for Server
  * My Images: Or select Image created for Server
  * My Backup: Or choose to restore Server with the created Backup file
  * My Snapshot: Or choose to restore the server with the created Snapshot file.
* **Instance type** : Choose the Server configuration that suits your needs.
* **Volume settings:** Configure the volume type by selecting the volume type, capacity, and IOPS.

vCloudStack provides an option to enable **Volume Encryption** , a function that allows all data stored on this Volume to be encrypted, preventing data loss but hackers still cannot use or view it.

* **Network settings:**
  * Select Network for the Server created in advance on the Admin Site page. (You can enter IP or the system will automatically select IP)
  * Select Security Group - Security Group
  * Choose 1 of 2 login information options:
    * Option 1: Basic Information - Base Data: Select the generated SSH key and enter the Username/Password information;
    * Option 2: User Data: Upload file or enter user information directly

**Note:** If the user information is encrypted, check the box “ **User information is base 64 encoded** ”.

* Other settings:
  * Backup Settings: select the “Enable Backup” option to have the system rely on the default backup policy to create the Server Backup file;
  * Select Placement Group to group servers together;

**Note:** Grouping servers into a group involves allowing servers to be allocated on a physical host or not to ensure performance and availability of the servers. ( _See more in the Server Group section_ )

**Step 5:** Review all the virtual server initialization information on the left side of the interface screen. Then select the **Initialize Server** button .

**Step 6:** The system initializes successfully, users can access the server to use and operate.
