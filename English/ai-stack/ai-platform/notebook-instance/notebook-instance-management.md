---
description: >-
  After creating a notebook instance, you can perform the following actions to
  manage it:
---

# Notebook Instance Management

**Access Notebook Instance**

* Log in to [GreenNode AI Platform](https://aiplatform.console.vngcloud.vn/overview).
* Select “Notebook instance” from the left-hand menu.

**Connect to Running Instances**\
When the status changes to Active, you can click “Connect” to open the Jupyter Notebook interface, where you can start working on your projects.

* Method 1: Access via the instance name link

<figure><img src="../../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

* Method 2: Connect via the Action column

<figure><img src="../../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

2. **Start and Stop Instance**\
   **Start Instance**\
   After a notebook instance is created, it will automatically start. If a notebook is currently stopped, locate your instance in the table and click the "Start" button.

* Method 1: Access via the instance name link

<figure><img src="../../../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure>

* Method 2: Start via the Action column

<figure><img src="../../../.gitbook/assets/image (269).png" alt=""><figcaption></figcaption></figure>

**Stop Instance**\
If you need to pause your work or save resources, you can stop your notebook instance. Simply select the instance you want to stop and click the "Stop" button. This action will pause the instance until you start it again.

* Method 1: Access via the instance name link

<figure><img src="../../../.gitbook/assets/image (286).png" alt=""><figcaption></figcaption></figure>

* Method 2: Stop via the Action column

<figure><img src="../../../.gitbook/assets/image (317).png" alt=""><figcaption></figcaption></figure>

3. **Delete Instance**\
   When a notebook instance is no longer needed, you can delete it to free up resources and manage costs. Please note that once a notebook instance is deleted, it cannot be recovered.

* Method 1: Access via the instance name link

<figure><img src="../../../.gitbook/assets/image (320).png" alt=""><figcaption></figcaption></figure>

* Method 2: Delete via the Action column

<figure><img src="../../../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

A confirmation dialog will appear to ensure you do not accidentally delete the instance.

<figure><img src="../../../.gitbook/assets/image (322).png" alt=""><figcaption></figcaption></figure>

4. **Resize Block Storage**\
   Select "Resize" when you want to increase block storage capacity to store more data.

The new size must be greater than or equal to the current storage size.

* Access via the instance name link

<figure><img src="../../../.gitbook/assets/image (323).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>

**Important Notes:**\
**Pricing:** Notebook instances incur charges while they are running. Make sure to stop instances when not in use to avoid unnecessary costs.

**Data persistence:** Data stored on the instance’s local storage will be lost when the instance is stopped. Therefore, ensure you back up your data to another location (e.g., S3 bucket) before stopping the instance.
