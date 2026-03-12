# Manage Kafka User

## What is a Kafka User?

A Kafka user is an important component in securing and controlling access to a Kafka cluster. Each user represents an application or service connecting to Kafka to produce or consume data. Managing Kafka users allows you to define each user's access rights to specific topics, ensuring that data is only accessed by authorized applications.

**Kafka User Functions and Operations**

* **Authentication:** Kafka users provide an authentication mechanism to verify the identity of applications or services connecting to the Kafka cluster. The authentication process typically uses methods such as mTLS (Mutual TLS) or SASL (Simple Authentication and Security Layer).
* **Authorization:** After successful authentication, Kafka users are granted access to specific topics based on the permissions assigned to that user. Common access permissions include:
  * **Produce:** Permission to write data to a topic.
  * **Consume:** Permission to read data from a topic.
  * **Manage topic**: Permission to manage topics

## Manage Kafka User

vDB Kafka Cluster provides comprehensive Kafka user management features, making it easy to create, update permissions, delete and manage certificates for users.

**1. Select Kafka Cluster**

* Log in to the vDB Kafka Cluster interface here: [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster)
* From the list of Kafka clusters, select the cluster where you want to manage users.

**2. Access the "Users" Section**

* After selecting the Kafka cluster, find and navigate to the "Users" section in the management interface.

**3. Create User**

1. Click the "Create User" button.
2. Fill in the following information:
   * **Username:** Name the new Kafka user. This name should be unique and clearly describe the application or service the user represents.
   * **Topic permissions:** Select the topics this user has access to and grant corresponding permissions (Produce, Consume).
   * **Kafka cluster access method:** Select the authentication method (mTLS or SASL) that matches the security configuration of the Kafka cluster.
3. Click the "Create" button to create the user. The system will automatically generate corresponding certificates for the user to use when connecting to the Kafka cluster.
4. Access the user detail section to download the certificates.

**4. Update Permission**

1. In the user list, find the user whose permissions you want to update.
2. Click the "Update Permission" icon or link corresponding to that user.
3. Add, remove or change access permissions to topics for the user.
4. Click the "Save" button to apply the changes.

**5. Delete User**

1. In the user list, find the user you want to delete.
2. Click the "Delete" icon or link corresponding to that user.
3. Confirm the delete operation. Note that deleting a user will revoke all access rights of that user to the Kafka cluster.

**6. Re-Generate Certificate**

1. In the user list, find the user whose certificate you want to regenerate.
2. Click the "Re-Generate Certificate" icon or link corresponding to that user.
3. Confirm the operation and download the new certificate. Note that the old certificate will no longer be valid after regenerating a new certificate.

**Conclusion**

Managing Kafka users is an important part of securing and controlling access to your Kafka cluster. By using the user management features in vDB Kafka Cluster, you can easily create, update permissions, delete and manage certificates for users, ensuring that your data is protected and only accessed by authorized applications.
