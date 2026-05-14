# Pull và Push image with Docker

### Prerequisites

Your computer must have Docker Engine or Docker Desktop installed.

### Create a Repository

A Repository (or “repo”) is a storage location for Docker images. A repo is similar to a folder containing multiple versions of an application in the form of Docker images. Each version is usually identified by a tag such as `:latest`, `:v1.0`, `:2025-04-15`, etc.

Follow these steps to create a Repository:

#### Step 1: Access the vContainer Registry Portal

* For HCM Region:\
  [https://vcr.console.vngcloud.vn/repository/list](https://vcr.console.vngcloud.vn/repository/list)
* For HAN Region:\
  [https://han-1.console.vngcloud.vn/vcr/repository/list](https://han-1.console.vngcloud.vn/vcr/repository/list)

#### Step 2:

Select the **Repository** menu, then click the **“Create Repository”** button.

#### Step 3:

Enter the **Repository name**, **Access level**, and **Quota Limit** according to your requirements.

#### Step 4:

Click **“Create”** to complete the creation process.

***

### Create a Repository User

A Repository User is a dedicated user account used specifically for pushing and pulling Docker Images. Repository Users can be assigned specific access permissions to individual Repositories, helping ensure effective security and access control.

Follow these steps to create a Repository User:

#### Step 1: Access the vContainer Registry Portal

* For HCM Region:\
  [https://vcr.console.vngcloud.vn/repository/list](https://vcr.console.vngcloud.vn/repository/list)
* For HAN Region:\
  [https://han-1.console.vngcloud.vn/vcr/repository/list](https://han-1.console.vngcloud.vn/vcr/repository/list)

#### Step 2:

Select the **Repository** menu, choose the Repository where you want to create a Repository User, then select the **Repository User** section.

Next, click **“Create a user”**.

#### Step 3:

Enter the **User name**, select the **Expiration Date**, optionally enter a **Description**, then choose the desired **Permission** according to your needs.

#### Step 4:

Click **“Create”** to complete the creation process.

After the user is created, make sure to save the **Secret key** information for future use.

Example:

***

### Perform PULL / PUSH Image Operations

After creating the Repository and Repository User, you can start pushing Docker images to the vContainer Registry system.

Before proceeding, ensure that:

* Docker is installed and running.
* The Repository and Repository User with Pull/Push permissions have been created.
* You have obtained the Username and Secret key of the newly created Repository User.

Below is an example of pulling/pushing the `nginx` image on vCR:

#### Step 1:

Pull the `nginx` image to your local machine using the following command:

```
docker pull nginx:latest
```

#### Step 2:

Log in to vCR using the following command:

**For HCM Region:**

```
docker login vcr.vngcloud.vn -u <repository_user>
```

**For HAN Region:**

```
docker login vcr-han.vngcloud.vn -u <repository_user>
```

Example command used to log in to the demo repository:

```
docker login vcr-han.vngcloud.vn -u 53461-user_demo
```

#### Step 3:

Tag the `nginx` image.

**For HCM Region:**

```
docker tag SOURCE_IMAGE[:TAG] vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

**For HAN Region:**

```
docker tag SOURCE_IMAGE[:TAG] vcr-han.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

Example command used to tag the `nginx` image:

```
docker tag nginx:latest vcr-han.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```

#### Step 4:

Push the image to the repository using the following command:

**For HCM Region:**

```
docker push vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

**For HAN Region:**

```
docker push vcr-han.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

Example command used to push the image to `demo_repo`:

```
docker push vcr-han.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```
