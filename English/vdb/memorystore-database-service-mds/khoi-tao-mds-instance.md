# Create MDS Instance

**Step 1: Basic Configuration**

* Choose the desired Database Name and Database Engine.

**Step 2: Technical Specifications**

* **Engine License:** Select the license type, either community or enterprise (depending on the database type).
* **Engine Version:** Choose the database version.
* **Flavor:** Configure the MDS Instance, including the number of cores, RAM, and included Free Backup capacity. Note: If the total capacity of all your backups exceeds this quota, you will be charged additional fees for the excess backup capacity.

**Step 3: DB Version Installation**

* **Password Requirement:** Enable password requirement to manage this database instance if desired.
* **Password:** If the password requirement is enabled, enter your password. VNG Cloud recommends setting a strong password and storing it in a secure location. To ensure information security, the password must meet all minimum requirements for length, allowed characters, special characters, etc.

**Step 4: Network and Security**

* **Cloud Network (VPC & Subnet):** Select the Cloud Network (VPC & Subnet) to be used for this MDS Instance. All RDS Instances must be connected to a Cloud Network. If you don't have a Cloud Network yet, you can create a new one by following the instructions here.
* **Public Access:** If you want the MDS Instance to have a Public IP and be accessible from the Internet, you need to enable Public Accessibility. If you want the MDS Instance to have only a Private IP and be accessible only by Cloud Servers, you need to disable Public Accessibility.

Note: To enhance security, VNG Cloud allows you to restrict trusted IP addresses that are allowed to access each MDS Instance through Security Group Rules.

**Step 5: DB Options**

* **DB Configuration Group (optional):** Select the Configuration Group to be applied to this MDS Instance. If you don't need to customize the configuration, you can skip this field.

**Step 6: Backup Settings**

* **Automatic Daily Backup:** Enable/disable automatic daily backups at a pre-selected time.
* **Backup Retention Period:** The period for storing automatic backups. Automatic backups stored beyond this period will be automatically deleted from the system. This parameter does not affect the lifecycle of backups created manually.
* **Backup Time:** The time to perform automatic backups. VNG Cloud recommends configuring this time during the period of lowest system traffic, usually from 12 AM to 5 AM.

After completing the configuration, review the information in the Summary section on the right. When all information is correct, click Create Database to complete the process. During the initialization process, the MDS Instance will have the status Building or Build. If the initialization is successful, the MDS Instance will have the status Active.

Congratulations on successfully creating a DB Instance on the VNG Cloud system. Please refer to the instructions on connecting to the MDS Instance to start using the database.
