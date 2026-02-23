# Create a Cluster and Node Group via API

### Introduction

The VKS API allows users to automate the creation of **Clusters** and **Node Groups** instead of manual operations on the portal.\
Detailed documentation: [https://docs.api.vngcloud.vn/service-docs/vks-api.html](https://docs.api.vngcloud.vn/service-docs/vks-api.html?utm_source=chatgpt.com)

***

### Prerequisites

| Component                    | Description                        |
| ---------------------------- | ---------------------------------- |
| **Token**                    | Valid Bearer token                 |
| **VPC / Subnet**             | Already created                    |
| **Image / Flavor**           | Check valid list                   |
| **SSH Key / Security Group** | Used for access & node security    |

***

### Create Cluster + Node Group via API

**Endpoint:**

```
POST /v1/clusters
```

**Example Body:**

```json
{
  "name": "cluster-demo-01",
  "version": "v1.29.13-vks.1740045600",
  "description": "Cluster demo created via API",
  "isBuyMorePoc": false,
  "isPoc": false,
  "isEnableAutoRenew": false
  "enablePrivateCluster": false,
  "networkType": "CILIUM_OVERLAY",
  "ipipEncapsulationMode": "ALWAYS",
  "cidr": "192.168.0.0/16",
  "vpcId": "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subnetId": "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "whitelistIp": "0.0.0.0/0",
  "nodeGroups": [
    {
      "name": "nodegroup-demo",
      "numNodes": 3,
      "enableAutoHealing": true,
      "autoScaleConfig": null,
      "upgradeConfig": {
        "maxSurge": 1,
        "maxUnavailable": 0,
        "strategy": "SURGE"
      },
      "enablePrivateNodes": false,
      "imageId": "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "flavorId": "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "diskSize": 100,
      "diskType": "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "securityGroups": ["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"],
      "sshKeyId": "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "labels": {},
      "taints": [],
      "subnetId": "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "enabledEncryptionVolume": false
    }
  ],
  "enabledBlockStoreCsiPlugin": true,
  "enabledLoadBalancerPlugin": true,
  "enabledServiceEndpoint": false,
  "autoUpgradeConfig": null,
  "releaseChannel": "STABLE",
  "fleetConfig": null
}
```

***

### Create a standalone Node Group via API

**Endpoint:**

```
POST /v1/clusters/{clusterId}/node-groups
```

The body is similar to the `nodeGroups` section above.

***

### Other APIs

| Purpose              | API                                |
| -------------------- | ---------------------------------- |
| List Clusters        | `GET /v1/clusters`                 |
| Delete Cluster       | `DELETE /v1/clusters/{id}`         |
| Get kubeconfig       | `GET /v1/clusters/{id}/kubeconfig` |
