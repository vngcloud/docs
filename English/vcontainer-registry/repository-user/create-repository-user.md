# Create repository user

Refer to the following instructions to create your Repository User.

#### How to Create a Repository User

1. On the Container Registry homepage, click on the "Repository User" menu on the right side to access the list of Repository Users. Click the "Create Repository User" button to start creating a new Repository User.
2. A "Create Repository User" popup will appear, allowing you to fill in the following information:

* **User Name (optional):** The name of the Repository User. If you don't enter a name, the system will automatically generate one. Note that the name, whether entered or automatically generated, will be prefixed with your `{AccountID}`, corresponding to your VNG Cloud account.
* **Expiration Date:** The expiration date of the User. There are 3 options:
  * **Leave blank:** This means the user has no expiration date.
  * **Enter a specific date:** This user will expire at the selected time. For expired users, the system will temporarily lock all related features for this Repository User until the user is granted an extension.
* **Description (optional):** Additional information about the Repository User.
* **Repositories (required):** Attach Repositories and set corresponding permissions.
  * Find the Repository you want to attach by its name.
  * Click the "Add" button.
  * In the list of Repositories added below, set the corresponding permission: Push & Pull or Pull Only.

3. Click the "Create" button to complete the creation.
4. Check the information of the newly created Repository User in the list.
