# Access control to specific resources

When you need to assign specific permissions on each resource, you need to create a Policy and specify the Resource correctly. In this tutorial, we will guide you to assign permissions on each server of vServer, for example when you have 2 servers: web1-server, db-server, **and you want User: System1 to have full rights on all Resources of vServer. , but only full rights on Resource:server are web1-server, not allowing operations on the important server db-server** . The model will look like below:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fb6DTqNdnWe2LUfCCnJZY%252Fiam-specific-resource.drawio.png%3Falt%3Dmedia%26token%3D85fbe7d0-e189-4f25-a6b1-927aea64d9c9&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e2e3c514&#x26;sv=1" alt=""><figcaption></figcaption></figure>

To set up IAM according to the above model, we will have the following steps:

**Step 1** : Create User: System1 if you do not have a User Account (note that if you already have User: System1, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)

**Step 2** : Get the ID information of the server web1-server

**Step 3** : Create a Policy with the name vServerFullAccessWebServers that allows access to all resources of vServer, but only full rights on web1-server

**Step 4** : Attach Policy: vServerFullAccessWebServers to User: System1

**Step 5** : Log in and check the rights of User: System1

Detailed steps are as follows

**Step 1: Create User: System1 if you do not have a User Account (note that if you already have User: System1, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)**

Create a User Account by accessing the User Account tab on the IAM management page here [,](https://iam.console.vngcloud.vn/user-accounts) clicking **Create a User Account,** filling in Username and Password information, then clicking **Create User Account**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fh99DI1M7zd14TH4fddYZ%252Fimage2023-7-12_15-18-33.png%3Falt%3Dmedia%26token%3Ddd0d78fd-d46d-4dab-bca3-504a1399e838&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8d4f9bb2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After successfully creating a User Account, it will be listed on the User Account page as below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FtT7hVLY2ITRVPFTHooqq%252Fimage2023-7-12_15-19-37.png%3Falt%3Dmedia%26token%3D864c508a-f984-4114-8c9b-27bf6b0f5164&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=faf9ba40&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2: Get the ID information of the server web1-server**

Visit the server management page here [to](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) get server ID information, click **Copy ID** at server web1-server to get the ID, save it for use in the next steps.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FsrOvIubGZoxv2aqpbCil%252Fimage2023-7-12_16-25-13.png%3Falt%3Dmedia%26token%3Db3097754-146d-4f28-82b7-e152f05cfde3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1dfdf3d8&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3: Create a Policy with the name vServerFullAccessWebServers that allows access to all resources of vServer, but only full rights on web1-server**

To create a Policy, go to the Policy tab on the IAM page here [,](https://iam.console.vngcloud.vn/policies) click **Create a Policy** , **name** the Policy: vServerFullAccessWebServers and click **Next step**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FmPCGK6iLohYVYnSXodMK%252Fimage2023-7-12_15-22-45.png%3Falt%3Dmedia%26token%3Dfd3f5c6d-7d56-4e49-9883-57f5df69b232&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ef5e8a05&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Select **Product** : **vserver** and **Actions** : **All vserver actions** to select all vServer actions

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fo00qtZOf2HaqczBNhVgo%252Fimage2023-7-12_15-24-23.png%3Falt%3Dmedia%26token%3Def775eee-f5e9-4100-8e03-596d9a682fa6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1f6391c1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Then in the **Resource section,** click on **the Resource arrow** to select Resource information, select **Any** for other Resource types, and **Resource: server** , click **Add a server** to add specific servers that are allowed to operate.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0lmSdWdFm6dfuL87tpQz%252Fimage2023-7-12_15-36-37.png%3Falt%3Dmedia%26token%3D84f6f34c-ac9f-43e9-8e38-b0dee11dd998&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=31ff0f14&#x26;sv=1" alt=""><figcaption></figcaption></figure>

The popup displays you **fill in the server ID information of web1-server** , click **Add** to add.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FIKKKPIlUDn3PUKsuzbpU%252Fimage2023-7-12_15-37-46.png%3Falt%3Dmedia%26token%3Dae9aef31-d4e6-4d37-bf6d-db60a7d9b7a6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a04ff287&#x26;sv=1" alt=""><figcaption></figcaption></figure>

At this point you will see Resouce information: the server already has the server ID of web1-server. If you want to add more server IDs, continue clicking Add a server to add. Then click **Create Policy** to create the Policy

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FuCLHmPqziHkmd3NP7ZxX%252Fimage2023-7-12_15-39-6.png%3Falt%3Dmedia%26token%3Dd687b8fb-a1af-4051-b019-c85e2963bcf1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=adad6ec2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 4: Attach Policy: vServerFullAccessWebServers to User: System1**

After successfully creating Policy: vServerFullAccessWebServers, you proceed to attach this Policy to User: System1, you can do it in User Account or Policy, here we will guide in Policy, **click on the name of the Policy** to go to the details page. Policy details:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F18cygYbXDvuCdNh8g1M1%252Fimage2023-7-12_15-46-16.png%3Falt%3Dmedia%26token%3D1c58ca61-1496-46d2-8aad-13dc74ac5c8f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ad7a0b0&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Select the Policy usage tab** and **click Attach** to add User: System1

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FqAroznTiJBumVoGF9N3G%252Fimage2023-7-12_15-46-46.png%3Falt%3Dmedia%26token%3D4e103960-2600-4cf0-9ab6-75b604bbd3f3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8c930536&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Select User: System1** and **click Add**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FaNUhrPxOO3bkWKRbNUXe%252Fimage2023-7-12_15-48-3.png%3Falt%3Dmedia%26token%3D67f20fee-8b52-43f5-9d75-255abd286b5a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9f42b123&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After adding User: System1 to Policy: vServerFullAccessWebServer, you will see information like below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FdcmNQSWExCFNaul2PVAP%252Fimage2023-7-12_15-49-17.png%3Falt%3Dmedia%26token%3D5a205a08-7ccd-4418-ba85-7a5d3a9af776&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c0d0690c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5** : Log in and check the rights of User: System1

Now you can log in to User: System1 to check permissions

Access vServer here [,](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) without logging into any account you will be redirected to the sign-in page, select " **Sign-in With IAM User Account** "

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FRQCKLmbVTKw01hNW2oBa%252Fimage2023-7-12_13-48-49.png%3Falt%3Dmedia%26token%3Db0388752-d3c2-4dab-ada2-3aec720d8387&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bd5f0942&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Fill in the root user email account information that User: System1 was previously created, IAM username and password information of User: System1, click **Sign-in with IAM User Account**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0VMJCy7OahicDX416x61%252Fimage2023-7-12_15-56-13.png%3Falt%3Dmedia%26token%3D8463d9d7-bd9d-4f62-bb9a-789cc25743dc&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7b5bb285&#x26;sv=1" alt=""><figcaption></figcaption></figure>

You will now see that User: System1 will have full rights on server web1-server and other resources of vServer.

Accessed web1-server's detail page successfully

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FtFNBw1Uk4Bps2nCjOBFc%252Fimage2023-7-12_15-58-35.png%3Falt%3Dmedia%26token%3D176f890b-966c-4a41-9e25-13bfd90a77e3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a0b411f3&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Successfully shutdown web1-server:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F9fUwUF8dFhy9C2k7nsN0%252Fimage2023-7-12_15-59-35.png%3Falt%3Dmedia%26token%3Da4f059e8-4749-4ce8-b1e3-38ff6cca6bd5&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b8dd75e2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Accessing db-server details page failed:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FfMHITsnvvieahQ9KJaS9%252Fimage2023-7-12_16-0-35.png%3Falt%3Dmedia%26token%3D90b05e21-a598-445e-9520-9485d4c161eb&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cafeb74e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Failed to shutdown db-server:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FCA6GDOgdQgMrKjXE6R2T%252Fimage2023-7-12_16-1-28.png%3Falt%3Dmedia%26token%3D50d2e6b9-119f-4c79-8afa-cb011174d72b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=285dde6d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

So you have completed decentralizing User: System1 with full rights on all Resources of vServer, but only granting full rights on Resource: server: web1-server, not allowing operations on the important server, db. -server
