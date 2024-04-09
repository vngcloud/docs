# Step 2: Create a container

Before you can store data in vStorage, you need to create a container. A container is an object that holds data (Objects). In vStorage, you can think of this object as equivalent to a directory in the operating system. You can manage files and directories using the provided tools and APIs.

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/). Choose the **project** in which you want to create a **container**.
2. Select **Create a Container**.
3. Enter the **container name** as per our guidelines.
4. Choose **Create**.

When creating a container successfully, container segments are initialized along with the root container. Large objects, when uploaded, are segmented for uploading. These segments are stored in one of the segment containers depending on the tool used to upload large objects. Meanwhile, the root container contains a manifest file linked to the content of the segments. The names of object segments are either preserved or base64 encoded depending on the user's tool behavior for uploading. vStorage supports 2 types of segment containers with suffixes: \_segments, +segments. Each user tool will interact with each type of segment container based on the specific characteristics of each tool.
