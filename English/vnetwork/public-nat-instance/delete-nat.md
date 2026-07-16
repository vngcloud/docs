# Delete NAT

1. Log in to https://hcm-3-vnetwork.console.greennode.ai/nat/list with region set to HCM.
2. In the "Public NAT" menu, find and select the NAT you want to delete.
3. Right-click and select "Delete".
4. A warning screen appears: "Deleting NAT may have some consequences for the user." Click "Delete" to confirm.

{% hint style="info" %}
When a V2 NAT is deleted, the default route to the internet that was added automatically to your VPC route table when the NAT was created is also removed. After deletion, instances in the VPC will no longer reach the internet through this NAT.
{% endhint %}

