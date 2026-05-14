# Getting Started

This section will guide you through the basic usage and management of images in a Repository, providing a comprehensive overview of the Container Registry (vCR) service.

## Before You Begin

To start using Container Registry, you need to understand the following instructions/concepts:

* If you don't have a GreenNode account, you need to register for an account to use the service. Refer to the instructions for Account Registration.
* Learn how to access the GreenNode Portal with a Root User Account or IAM User Account. Refer to the instructions on How to log in to GreenNode.
* Download and install Docker/Podman or any tool on your local/cloud machine to interact with Container Registry.

## 1. Accessing the vCR Console

The vCR Console is a web-based user interface that allows you to manage Repositories, Images, and Repository Users in your cloud computing environment. It provides an intuitive interface for easier control and management of container images.

**How to access the vCR Console:**

* Access the vCR Console directly through the link: [https://vcr.console.vngcloud.vn/list](https://vcr.console.vngcloud.vn/list)
* Access from the vServer homepage: [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)
  * On the vServer homepage, navigate to the vCR portal by clicking on "Container Registry" in the "Container Registry" section of the left menu.
* Access from the vConsole homepage: [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/)
  * In the "GreenNode Service" section on the interface, click on "vServer", then click on "Container Registry" from the list of corresponding products/services on the right.

## 2. Creating a Repository

1. On the Container Registry homepage, click on the "Repository" menu on the right side to access the list of Repositories. Click the "Create a repository" button to start creating a new Repository.
2. A "Create Repository" popup will appear, allowing you to fill in the following information:

* **Repository name (optional):** The name of the Repository. If no name is entered, the system will automatically generate a corresponding name. Note that the name, after being entered or automatically generated, will be added with the prefix `{AccountID}` corresponding to the currently logged-in GreenNode account.
* **Access level:** Accessibility to the Repository (Public / Private).
  * **Public:** Repositories where users can freely Pull/Push without going through a Repository User.
  * **Private:** Repositories where users must provide credentials (username/password) to access the Images managed in this Repository.
* **Quota Limit:** The maximum storage capacity that the Repository can store. For example, if you enter 20GB, your Repository can only store up to 20GB of capacity. However, you can change this number later according to your needs after initialization.

3. Click "Create" to complete the initialization process.
4. Check the information of the newly created Repository in the list.

## 3. Creating a Repository User

1. On the Container Registry homepage, click on the "Repository User" menu on the right side to access the list of Repository Users. Click the "Create Repository User" button to start creating a new Repository User.
2. A "Create Repository User" popup will appear, allowing you to fill in the following information:

* **User Name (optional):** The name of the Repository User. If no name is entered, the system will automatically generate a corresponding name. Note that the name, after being entered or automatically generated, will be added with the prefix `{AccountID}` corresponding to the currently logged-in GreenNode account.
* **Expiration Date:** The expiration date of the User. There are 3 modes:
  * **Leave blank:** This means the user has no expiration time.
  * **Enter a specific date:** This user will expire at the selected time. For expired users, the system will temporarily lock all related features for this Repository User until the user is granted an extension.
* **Description (optional):** Additional information about the Repository User.
* **Repositories (required):** Attach Repositories and set corresponding Permissions.
  * Find the Repository you want to attach by repository name.
  * Click the "Add" button.
  * In the list of Repositories added below, set the corresponding permission Push\&Pull/Pull Only.

3. Click the "Create" button to complete the creation.
4. Check the information of the newly created Repository User in the list.

## 4. Pushing (Uploading) Images for Management

1. Open docker/podman and log in with the newly created Repository User:

* **User name:** Repository Name
* **Password:** Repository User Secret Key

2. Access the vCR Console, click on the Repository you want to upload the image to, in the "Image" tab, click on "Push Command" to quickly view the commands you need to perform.
3. Copy the command "Tag an image for this project" to tag the image you want to push.
4. Copy the command "Push an image to this project" to push the image to the Repository.
5. Check if the image has been successfully pushed in the "Image" tab on the Repository details page.
