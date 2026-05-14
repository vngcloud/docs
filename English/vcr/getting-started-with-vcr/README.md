# Getting Started with vCR

In this section, we will learn how to use and manage images within a Repository in the most basic way, providing a better overview of how to use the Container Registry (vCR) service.

### Before You Begin

Before using Container Registry, you should first familiarize yourself with the following guides/concepts:

* If you do not already have a GreenNode account, you need to register for one in order to use the service. Refer to the [**Account Registration**](../../getting-start-with-vng-cloud-account/) guide.
* Learn how to access the GreenNode Portal using either a Root User Account or an IAM User Account. Refer to the [**How to Login into GreenNode**](../../identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/) guide.
* Download and install Docker/Podman or any tool on your local/on-cloud machine that will be used to interact with the Container Registry.

### 1. Access the vCR Console

The vCR Console is a web-based user interface that allows you to manage Repositories, Images, and Repository Users within your cloud environment. It provides an intuitive interface for easier control and management of container images.

#### How to Access the vCR Console

* Directly access the vCR Console via:\
  [https://vcr.console.vngcloud.vn/](https://vcr.console.vngcloud.vn/)
*   Access from the vServer homepage:\
    [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)

    On the vServer homepage, navigate to the vCR portal by selecting “Container Registry” from the left-side menu.
*   Access from the vConsole homepage:\
    [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/)

    Under the “GreenNode Service” section, select “vServer”, then choose “Container Registry” from the corresponding product/service list on the right.

### 2. Create a Repository

#### How to Create a Repository

On the Container Registry homepage, click the “Repository” menu on the left side to access the Repository list, then click the “Create a repository” button to start creating a new Repository.

A “Create Repository” popup will appear, allowing you to enter the following information:

#### Repository Name (optional)

The name of the Repository. If left blank, the system will automatically generate a name.\
Note: The generated/provided name will automatically be prefixed with `{AccountID}` corresponding to the currently logged-in GreenNode account.

#### Access Level

Determines the accessibility of the Repository (Public / Private).

* **Public:** Users can freely Pull/Push without using a Repository User.
* **Private:** Users must provide credentials (username/password) to access Images managed in this Repository.

#### Quota Limit

The maximum storage capacity allowed for the Repository.

For example, if you set 20GB, the Repository can only store up to 20GB of data. However, you can change this limit later depending on your actual needs.

Click “Create” to complete the creation process.

Verify the newly created Repository information in the Repository list.

### 3. Create a Repository User

#### How to Create a Repository User

On the Container Registry homepage, click the “Repository User” menu on the left side to access the Repository User list, then click the “Create Repository User” button to create a new Repository User.

A “Create Repository” popup will appear, allowing you to enter the following information:

#### User Name (optional)

The name of the Repository User. If left blank, the system will automatically generate a name.

Note: The generated/provided name will automatically be prefixed with `{AccountID}` corresponding to the currently logged-in GreenNode account.

#### Expiration Date

The expiration date of the user. There are 3 modes:

* **Leave blank:** The user will not expire.
* **Specify a date:** The user will expire at the selected time. Once expired, all related features for this Repository User will be temporarily disabled until the expiration time is extended.

#### Description (optional)

Additional information about the Repository User.

#### Repositories (required)

Attach Repositories and configure corresponding permissions.

* Search for the Repository to attach using the repository name.
* Click the “Add” button.
* In the attached Repository list below, configure permissions as:
  * Push & Pull
  * Pull Only

Click the “Create” button to complete the process.

Verify the newly created Repository User information in the list.

### 4. Push Images for Storage and Management

#### How to Push Images to a Repository

Open Docker/Podman and log in using the newly created Repository User credentials:

* **Username:** Repository Name
* **Password:** Repository User Secret Key

Access the vCR Console and select the Repository where you want to upload the image.

In the “Image” tab, click “Push Command” to quickly view the required commands.

* Copy the “Tag an image for this project” command to tag the image before pushing.
* Copy the “Push an image to this project” command to push the image to the Repository.

Verify whether the image has been successfully pushed by checking the “Image” tab on the Repository detail page.
