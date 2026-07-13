# Manage VKS with the GreenNode CLI

### Introduction

The **GreenNode CLI** (the `grn` command) is a command-line tool for managing GreenNode resources directly from your terminal. For VKS, you can create and manage the full lifecycle of **Clusters** and **Node Groups** instead of using the web console.

Full command reference: [https://vngcloud.github.io/greennode-cli/](https://vngcloud.github.io/greennode-cli/).

The CLI is one of several ways to work with VKS, alongside the [Console](README.md), [API](create-a-cluster-via-api.md) and [Terraform](su-dung-terraform-de-khoi-tao-cluster-va-node-group.md). Choose the CLI when you need fast, repeatable operations or lightweight automation scripts.

***

### 1. Installation

Source: [Installation](https://vngcloud.github.io/greennode-cli/installation/).

Download the latest binary for your platform from [GitHub Releases](https://github.com/vngcloud/greennode-cli/releases).

**macOS**

```bash
# Apple Silicon (M1/M2/M3)
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-darwin-arm64
# Intel
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-darwin-amd64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Linux**

```bash
# x86_64
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-linux-amd64
# ARM64
curl -L -o grn https://github.com/vngcloud/greennode-cli/releases/latest/download/grn-linux-arm64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Windows:** download `grn-windows-amd64.exe` from GitHub Releases and add it to your `PATH`.

**Build from source** (requires [Go 1.22+](https://go.dev/dl/)): `git clone`, `cd greennode-cli/go`, `go build -o grn .`

Verify: `grn --version`

***

### 2. Configuration

Source: [Configuration](https://vngcloud.github.io/greennode-cli/configuration/).

Run the wizard and provide your details:

```bash
grn configure
```

```
GRN Client ID [None]: <your-client-id>
GRN Client Secret [None]: <your-client-secret>
Default region name [HCM-3]:
Default output format [json]:
Project ID (leave blank to auto-detect) [None]:
```

Credentials (Client ID / Secret) come from the **GreenNode IAM Portal → Service Accounts** ([hcm-3.console.vngcloud.vn/iam](https://hcm-3.console.vngcloud.vn/iam/)). Leave **Project ID** blank and the wizard auto-detects it.

**Available regions:**

| Region | VKS Endpoint |
| --- | --- |
| `HCM-3` | `https://vks.api.vngcloud.vn` |
| `HAN` | `https://vks-han-1.api.vngcloud.vn` |

Configuration is stored in `~/.greenode/credentials` (permissions `0600`) and `~/.greenode/config`. You can override it with environment variables (`GRN_ACCESS_KEY_ID`, `GRN_SECRET_ACCESS_KEY`, `GRN_DEFAULT_REGION`, `GRN_DEFAULT_PROJECT_ID`, `GRN_PROFILE`, `GRN_DEFAULT_OUTPUT`) — environment variables take priority over the config file.

For multiple environments, use profiles: `grn configure --profile staging`, then `grn --profile staging vks ...`.

***

### 3. VKS commands

Source: [VKS Commands Overview](https://vngcloud.github.io/greennode-cli/commands/vks/).

Structure: `grn [global-options] vks <command> [command-options]`. Get help any time with `grn vks` or `grn vks <command> --help`.

| Group | Commands |
| --- | --- |
| **Cluster** | [list-clusters](https://vngcloud.github.io/greennode-cli/commands/vks/list-clusters/), [get-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/get-cluster/), [create-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/create-cluster/), [update-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/update-cluster/), [delete-cluster](https://vngcloud.github.io/greennode-cli/commands/vks/delete-cluster/) |
| **Node Group** | [list-nodegroups](https://vngcloud.github.io/greennode-cli/commands/vks/list-nodegroups/), [get-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/get-nodegroup/), [create-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/create-nodegroup/), [update-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/update-nodegroup/), [update-nodegroup-metadata](https://vngcloud.github.io/greennode-cli/commands/vks/update-nodegroup-metadata/), [upgrade-nodegroup-version](https://vngcloud.github.io/greennode-cli/commands/vks/upgrade-nodegroup-version/), [list-nodes](https://vngcloud.github.io/greennode-cli/commands/vks/list-nodes/), [delete-nodegroup](https://vngcloud.github.io/greennode-cli/commands/vks/delete-nodegroup/) |
| **Versions** | [list-cluster-versions](https://vngcloud.github.io/greennode-cli/commands/vks/list-cluster-versions/) |
| **Auto-Upgrade** | [config-auto-upgrade](https://vngcloud.github.io/greennode-cli/commands/vks/config-auto-upgrade/), [delete-auto-upgrade-config](https://vngcloud.github.io/greennode-cli/commands/vks/delete-auto-upgrade-config/) |
| **Auto-Healing** | [config-auto-healing](https://vngcloud.github.io/greennode-cli/commands/vks/config-auto-healing/) |
| **Events** | [get-cluster-events](https://vngcloud.github.io/greennode-cli/commands/vks/get-cluster-events/) |
| **Kubeconfig** | [generate-kubeconfig](https://vngcloud.github.io/greennode-cli/commands/vks/generate-kubeconfig/), [update-kubeconfig](https://vngcloud.github.io/greennode-cli/commands/vks/update-kubeconfig/) |
| **Quota** | [get-quota](https://vngcloud.github.io/greennode-cli/commands/vks/get-quota/) |
| **Waiter** | [wait](https://vngcloud.github.io/greennode-cli/commands/vks/wait/) |

Global options (`--profile`, `--region`, `--output`, `--query`, `--endpoint-url`, `--debug`) and other topics (Output, Pagination, Dry-run, Shell Completion) are documented in the [CLI docs](https://vngcloud.github.io/greennode-cli/).

***

### Quick example: from zero to a working kubectl

{% hint style="warning" %}
`create-cluster` provisions the **control plane only**. The cluster has no worker nodes until you create a **Node Group**.
{% endhint %}

```bash
# 1. Create the control plane
grn vks create-cluster --name my-cluster \
  --k8s-version v1.30.10-vks.1746550800 \
  --network-type CILIUM_OVERLAY --cidr 192.168.0.0/16 \
  --vpc-id <net-...> --subnet-id <sub-...>
grn vks wait cluster-active --cluster-id <cls-...>

# 2. Add a node group
grn vks create-nodegroup --cluster-id <cls-...> --name default \
  --flavor-id <flv-...> --disk-type SSD --ssh-key-id <ssh-...> --num-nodes 2
grn vks wait nodegroup-active --cluster-id <cls-...> --nodegroup-id <ng-...>

# 3. Fetch the kubeconfig, then verify
grn vks generate-kubeconfig --cluster-id <cls-...>
grn vks update-kubeconfig --cluster-id <cls-...>   # after the kubeconfig is ACTIVE
kubectl get nodes
```

Use `grn vks list-cluster-versions` to get `--k8s-version`; the remaining IDs (VPC, subnet, flavor, SSH key) come from the Console.

***

If you run into problems, contact GreenNode by email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Help center: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
