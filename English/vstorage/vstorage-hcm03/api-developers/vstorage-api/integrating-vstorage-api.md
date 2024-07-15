# Integrating vStorage API

To view the vStorage API integration guide, you can follow these steps on the vStorage Portal:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the **Integration** menu.
3. Choose the **vStorage API** icon.
4. In the **Authorization** section, you need to provide the necessary information to configure your vStorage API, including:
   1. Enter the **Client ID**: A unique character string used by the Service API to identify the application, also used to build the authorization URL displayed to users. You can create and manage the **Client ID** through the vIAM system. The **Client ID** will be automatically generated when you create a new Service Account. Refer to the details at \[Initialize a Service Account]\(Link to the relevant documentation).
   2. Enter the corresponding **Client Secret** for the entered **Client ID**. The Client ID and Client Secret pair are created and managed through the vIAM system. You can click Click here to manage your Client ID to navigate to the vIAM system and access the Service Account management screens. Refer to the details at \[Initialize a Service Account]\(Link to the relevant documentation).
5. After completing the authorization configuration, select **Authentication** to go to the **Configuration screen**. You can always return here to change your permission information, then select Authentication again to update the S3 Rest API list with your new settings.

***

#### Experience vStorage API directly on the vStorage Portal: <a href="#integratingvstorageapi-experiencevstorageapidirectlyonthevstorageportal" id="integratingvstorageapi-experiencevstorageapidirectlyonthevstorageportal"></a>

To experience using the vStorage API, you need at least one Client ID and Client Secret (this information is obtained from the Service Account). To create a Service Account, refer to \[Initialize a Service Account]\(Link to the relevant documentation). You can use this Service Account to create (or delete) multiple containers. A container acts as a storage unit (similar to a directory), and within each container, customers can upload, get, and delete multiple corresponding objects (objects here can be understood as a file or a subfolder in the container).

Basic procedure: Authenticate -> Create Project -> Create Container -> Upload Object

We provide you with a quick operation interface with the vStorage API. After integrating as instructed in \[Integrate vStorage API]\(Link to the relevant documentation), continue following these steps:

1. Select **Try it out**.
2. Enter the **input** for each API.
3. Select **Execute**.
4. Check the **returned result**.

Below is an example of the four basic vStorage APIs that you can experience:

**1. Create a project**

Prerequisite:

* Postpaid user

Result:

* The project is initialized with properties:
  * Project type: Gold class.
  * Region: HCM01.

![](https://docs.vngcloud.vn/download/attachments/69468565/image2023-7-17\_11-26-39.png?version=1\&modificationDate=1703571651000\&api=v2)

**2. Create a container**

The following API is used to initialize a container within a project.

![](https://docs.vngcloud.vn/download/attachments/69468565/image2023-7-17\_11-27-51.png?version=1\&modificationDate=1703571651000\&api=v2)

**3. Delete a container**

The following API is used to delete a container within a project.

![](https://docs.vngcloud.vn/download/attachments/69468565/image2023-7-17\_11-32-37.png?version=1\&modificationDate=1703571651000\&api=v2)

**4. Delete an object**

The following API is used to delete an object within a container.

![](https://docs.vngcloud.vn/download/attachments/69468565/image2023-7-17\_11-33-32.png?version=1\&modificationDate=1703571651000\&api=v2)

In addition to the quick usage on the vStorage Portal, you can use the vStorage API on personal devices following the instructions in \[Use vStorage API]\(Link to the relevant documentation).

\
