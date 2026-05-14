# How to Create a Repository

Refer to the following instructions to create your Repository.

#### Steps to Create a Repository

On the Container Registry homepage, click the **"Repository"** menu on the right-hand side to access the Repository list page. Then click the **"Create a repository"** button to start creating a new Repository.

A **"Create Repository"** popup will appear, allowing you to enter the following information:

* **Repository name (optional):**\
  The name of the Repository. If no name is provided, the system will automatically generate one.\
  Note: After entering or auto-generating the name, the system will automatically prepend the prefix `{AccountID}` corresponding to the currently logged-in GreenNode account.
* **Access level:**\
  Defines the accessibility of the Repository (**Public / Private**).
  * **Public:**\
    Repositories where users can freely pull/push images without using a Repository User.
  * **Private:**\
    Repositories where users must provide credentials (username/password) to access the Images managed within the Repository.
* **Quota Limit:**\
  The maximum storage capacity that the Repository can use.\
  For example, if you set the quota to **20GB**, the Repository can store up to **20GB** of data. However, you can change this value later based on your actual usage requirements after the Repository has been created.

Click **"Create"** to complete the creation process.

After creation, verify the newly created Repository information in the Repository list.

> **Note:** For POC accounts, you can create a maximum of only **1 Repository**.
