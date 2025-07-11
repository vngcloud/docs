# Audit Logs Management

Cloud Audit Logs is a feature that records all administrative and access activities on your VNG Cloud resources. Audit Logs helps you answer the questions: "**Who did what, where, and when?**" on VNG Cloud resources with the same level of transparency as your on-premise environment. Enabling Audit Logs allows you to monitor, review, and ensure the security of your VNG Cloud resources.

#### **1. Type of Audit Logs** <a href="#auditlogs-1.cacloaiauditlogs" id="auditlogs-1.cacloaiauditlogs"></a>

Cloud Audit Logs provide the following types of Audit Logs below; depending on the product or service, the supported audit log type may vary:

* **Admin Activity Audit Logs**: contains all logs for actions that change resources (Create, Update, Delete) on VNG Cloud. For example: logs when users create vServer or delete security group. Abbreviated as ADMIN\_WRITE&#x20;
*   **Data Access Audit Logs** (coming soon): contains all logs for actions that read resource configuration information, as well as actions that create, delete, edit and read resource data. Resource data is data that users upload to VNG Cloud, such as vStorage objects. Specifically divided into 3 types as below:

    * **ADMIN\_READ**: action to read resource configuration information. For example: list vServer or view details of a vServer&#x20;
    * **DATA\_WRITE:** action to create, delete, edit resource data. For example: uploading objects to vStorage or deleting objects on vStorage&#x20;
    * **DATA\_READ**: action to read data of resources. For example: listing objects of vStorage&#x20;

    **System Event Audit Logs**: contains all logs for actions that change resources on VNG Cloud; however, these are actions that are created by VNG Cloud systems, not directly performed by users. For example, logs when VNG Cloud systems automatically expand (autoscale) node groups of vContainer, or actions that automatically create daily backups for vDB. Abbreviated as SYSTEM\_EVENT&#x20;
* **Policy Denied Audit Logs** (coming soon): contains all logs when VNG Cloud products/services deny access to IAM user accounts or service accounts because of violating the Policy. Abbreviated as POLICY\_DENIED

**2. List of Products/Services Supporting Various Types of Audit Logs**

<table data-header-hidden><thead><tr><th width="154"></th><th width="127"></th><th width="137"></th><th width="134"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Products/Service Name</td><td>Admin Activity Audit Logs</td><td>Data Access Audit Logs<br><br></td><td>System Event Audit Logs</td><td>Policy Denied Audit Logs</td><td></td><td></td></tr><tr><td>ADMIN_WRITE</td><td>ADMIN_READ</td><td>DATA_WRITE</td><td>DATA_READ</td><td>SYSTEM_EVENT</td><td>POLICY_DENIED</td><td></td></tr><tr><td>vServer</td><td>YES</td><td><strong>COMING SOON</strong></td><td>N/A</td><td>N/A</td><td>N/A</td><td>COMING SOON</td></tr><tr><td>vLB</td><td>YES</td><td>COMING SOON</td><td>N/A</td><td>N/A</td><td>N/A</td><td>COMING SOON</td></tr><tr><td>vDB</td><td>COMING SOON</td><td>COMING SOON</td><td>N/A</td><td>N/A</td><td>COMING SOON</td><td>COMING SOON</td></tr><tr><td>vContainer</td><td>YES</td><td>COMING SOON</td><td>N/A</td><td>N/A</td><td>YES</td><td>COMING SOON</td></tr><tr><td>vMonitor</td><td>YES</td><td>COMING SOON</td><td>N/A</td><td>N/A</td><td>N/A</td><td>COMING SOON</td></tr><tr><td>vStorage</td><td>YES</td><td>YES</td><td>YES</td><td>YES</td><td>N/A</td><td>COMING SOON</td></tr></tbody></table>

* Status meanings

N/A: does not support this type of audit logs\
COMING SOON: supports this type of audit logs and will be available soon\
PARTIAL YES: partially supports this type of audit logs\
YES: fully supports this type of audit logs

#### **3. Activate Audit Logs** <a href="#auditlogs-3.kichhoatauditlogs" id="auditlogs-3.kichhoatauditlogs"></a>

By default, VNG Cloud does not enable the Audit Logs feature, customers need to follow the steps below to activate it:

1. Access the Audit Logs page of the IAM Portal: https://iam.console.vngcloud.vn/audit-logs
2. Select Set default configuration, a setup popup will appear allowing you to choose to enable ADMIN\_WRITE or SYSTEM\_EVENT
3. Select to activate the type of audit logs ADMIN\_WRITE or SYSTEM\_EVENT that you desire
4. Press the Save button to activate

For example, if you choose both types of supported Audit Logs, you will see a screen like below, for both types ADMIN\_WRITE and SYSTEM\_EVENT when activated will apply to all products/services that are supported as shown in the table above\
Once Audit Logs are activated, the system will start saving Audit Logs from the moment of activation (no historical data), and will automatically create a Log Project: required on the vMonitor Logs side for storage, the Log Project: required will be completely free and will store the Audit Logs for 90 days. At the same time, once both types of Audit Logs: ADMIN\_WRITE AND SYSTEM\_EVENT are activated, you will not be able to disable this feature, the system will always store all actions belonging to these two types of Audit Logs.

**4.View the Activated Audit Logs**\
To view the activated Audit Logs, you need to follow these instructions:

1. Access the Log Search section of vMonitor Logs: https://hcm-3.console.vngcloud.vn/vmonitor/log/search
2. Select Log Project: required to view the stored Audit Logs.&#x20;

For example, the image below shows an action where 1 root user account created a Security Group belonging to vServer at the time 19/06/2023 17:51:57 was recorded.

**3 Structure and format of Audit Logs**\
Each line of Audit Logs may contain the fields as below

* timestamp time when the log is generated
* logId UUID to distinguish each log line
* source the origin of the log line and specifies what type of logs it is for example if the log line is generated from audit logs and the type is ADMIN\_WRITE then the content will be source cloud\_audit/admin\_write
* serviceName information about the product/service being monitored for example if this Audit Log line is for vServer then the content will be serviceName vserver
* resource detailed information about which resource is being monitored consisting of 2 subfields type and labels
* type information about which resource of the product for example if it is a log line related to server it will be type vserver\_server
* labels name and ID of the resource or other information about the resource
* The example below is the resource server of vServer with serverID ins-b019f5d0-1234-41ba-1234-851f9ef39003

| <p><code>"resource":{</code><br><code>"labels":{</code><br><code>"serverVRN":"vserver::12345:server/ins-b019f5d0-1234-41ba-1234-851f9ef39003",</code><br><code>"serverId":"ins-b019f5d0-1234-41ba-1234-851f9ef39003"</code><br><code>},</code><br><code>"type":"vserver:server"</code><br><code>},</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* JsonPayload: contains specific information about what the action is, who initiated this action (root user account, IAM user account or service account), request metadata and request/response body if any. For example below you can see userType: root-user is the root user account with ID: 12345 performing the DeleteServer action with the server with ID: ins-b019f5d0-1234-41ba-1234-851f9ef39003

| <p><code>"jsonPayload":{</code><br><code>"authenticationInfo":{</code><br><code>"rootUserAccountId":12345,</code><br><code>"userType":"root-user"</code><br><code>},</code><br><code>"serviceName":"vserver"</code><br><code>"action":"vserver:DeleteServer",</code><br><code>"resource":"vserver::12345:server/ins-b019f5d0-1234-41ba-1234-851f9ef39003",</code><br><code>"request":{},</code><br><code>"requestMetadata":{},</code><br><code>"response":{}</code><br><code>},</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

* With the example below, you can see userType: iam-user is IAM user account with ID: e6d39955-e4c3-1234-1234-84d82ea554bf belonging to root user account with ID: 12345 performing SearchLogs action with Log Project with ID: bbb5f6ef-1234-49a1-1234-b41332376fef. Similarly with serviceAccount you will also see userType: user-sa.

| <p><code>"jsonPayload":{</code><br><code>"authenticationInfo":{</code><br><code>"userType":"iam-user",</code><br><code>"rootUserAccountId":12345,</code><br><code>"userAccount":"e6d39955-e4c3-1234-1234-84d82ea554bf"</code><br><code>},</code><br><code>"serviceName":"vmonitor",</code><br><code>"action":"vmonitor:SearchLogs",</code><br><code>"resource":"vmonitor::12345:log-project/bbb5f6ef-1234-49a1-1234-b41332376fef",</code><br><code>"request":{},</code><br><code>"requestMetadata":{},</code><br><code>"response":{}</code><br><code>},</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

* You can also see additional information about requestMetadata, request and response of this action (depending on the type of action, there will be or not)

| <p><code>"jsonPayload":{</code><br><code>"authenticationInfo":{</code><br><code>"userType":"iam-user",</code><br><code>"rootUserAccountId":12345,</code><br><code>"userAccount":"e6d39955-e4c3-1234-1234-84d82ea554bf"</code><br><code>},</code><br><code>"serviceName":"vmonitor",</code><br><code>"action":"vmonitor:SearchLogs",</code><br><code>"resource":"vmonitor::12345:log-project/bbb5f6ef-1234-49a1-1234-b41332376fef",</code><br><code>"request":{</code><br><code>"method":"POST",</code><br><code>"path":"/v1/projects/bbb5f6ef-1234-49a1-1234-b41332376fef/search-logs",</code><br><code>"httpVersion":"HTTP/1.1"</code><br><code>},</code><br><code>"requestMetadata":{</code><br><code>"callerIp":"103.1.208.50",</code><br><code>"userAgent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36"</code><br><code>},</code><br><code>"response":{</code><br><code>"duration":272,</code><br><code>"status":200</code><br><code>}</code><br><code>},</code></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
