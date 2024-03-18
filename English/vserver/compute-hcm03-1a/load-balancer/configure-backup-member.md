# Configure Backup Member

One of the strengths of the Load Balancer(LB) is that it is flexible and allows traffic to be redirected to a health member, when one or more members in the same pool experience downtime based on the healthcheck feature. So in the worst case, all members have downtime or some reason cannot serve the client, what do we do now? In this article I want to mention the  Backup Member  feature to solve such bad cases. That is, when a member has downtime, LB will immediately turn on another member in the backup state, to replace the member with downtime.

**Configure Backup Member**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802727/Backup_LB.jpg?version=1&#x26;modificationDate=1685081626000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

In the **ATTACH** member section we choose to add the Backup role  box as shown, now the member named "nginx02" will be in the backup state.

\
