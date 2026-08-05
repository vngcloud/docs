# Manage AgentBase with the GreenNode CLI

### Introduction

The **GreenNode CLI** (the `grn` command) is a command-line tool for managing GreenNode resources directly from your terminal. For **GreenNode AgentBase**, the `grn agentbase` command group lets you create and operate the full lifecycle of an agent — Identity, Runtime, Memory, MCP Gateway, Policy and Container Registry — instead of using the Portal.

The `agentbase` command group ships in the default `grn` binary — no special build is required:

```bash
grn agentbase --help
```

Full command reference: [https://greennodehub.github.io/greennode-cli/](https://greennodehub.github.io/greennode-cli/).

The CLI is one of several ways to work with AgentBase, alongside the [Portal](README.md) and [MCP](manage-agentbase-with-the-greennode-mcp.md). Choose the CLI when you need fast, repeatable operations, or when you want to move agent deployment into automation scripts and CI/CD.

{% hint style="info" %}
The `agentbase` command group is still being added to the public reference site. In the meantime, run `grn agentbase --help` or `grn agentbase <group> --help` to see the commands and parameters available in the version you have installed.
{% endhint %}

---

### 1. Installation

`grn` is a single binary with zero external dependencies. Download the latest build for your platform from [GitHub Releases](https://github.com/GreenNodeHub/greennode-cli/releases).

**macOS**

```bash
# Apple Silicon (M1/M2/M3)
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-darwin-arm64
# Intel
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-darwin-amd64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Linux**

```bash
# x86_64
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-linux-amd64
# ARM64
curl -L -o grn https://github.com/GreenNodeHub/greennode-cli/releases/latest/download/grn-linux-arm64
chmod +x grn && sudo mv grn /usr/local/bin/
```

**Windows:** download `grn-windows-amd64.exe` from GitHub Releases and add it to your `PATH`.

**Build from source** (requires [Go 1.22+](https://go.dev/dl/)):

```bash
git clone https://github.com/GreenNodeHub/greennode-cli.git
cd greennode-cli/go
go build -o grn . && sudo mv grn /usr/local/bin/
```

Verify: `grn --version`

---

### 2. Configuration and authentication

The `agentbase` command group **shares the `~/.greennode` profile** with the rest of `grn` (`vks`, `vserver`) — there is no separate config file. Two authentication modes are available.

**Machine mode (M2M)** — recommended for CI/CD and scripts:

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

**Client ID** and **Client Secret** come from the **GreenNode IAM Portal → Service Accounts** ([hcm-3.console.vngcloud.vn/iam](https://hcm-3.console.vngcloud.vn/iam/)). Leave **Project ID** blank and the wizard auto-detects it.

**User mode (PKCE)** — recommended for interactive use on your own machine:

```bash
grn login      # browser-based login
grn logout     # clear the stored login
```

The active mode is determined by `auth_mode` in the profile (`user` or `machine`). `grn login` persists only the **refresh token** to disk (`0600`); the access token is held in process memory and refreshed automatically before it expires.

#### Config files and environment variables

Configuration is stored in `~/.greennode/credentials` (permissions `0600`) and `~/.greennode/config`. You can override it with environment variables — environment variables always take priority over the files:

| Environment variable | Purpose |
|---|---|
| `GRN_ACCESS_KEY_ID` | Client ID |
| `GRN_SECRET_ACCESS_KEY` | Client Secret |
| `GRN_DEFAULT_REGION` | Default region |
| `GRN_DEFAULT_PROJECT_ID` | Project ID |
| `GRN_PROFILE` | Profile to use (default `default`) |
| `GRN_DEFAULT_OUTPUT` | Default output format |

For multiple environments, use profiles: `grn configure --profile staging`, then `grn --profile staging agentbase runtime list`.

#### Choosing the dev / prod environment

The environment is selected via `iam_env` in the profile (default `prod`). AgentBase calls `agentbase.api.vngcloud.vn` in prod and `agentbase.api-dev.vngcloud.tech` in dev.

```bash
grn configure set iam_env <dev|prod>   # machine mode
grn login --iam-env <dev|prod>         # user mode
grn agentbase context current          # show the active environment + endpoints
```

{% hint style="info" %}
In **user mode**, `iam_env` is bound to the login token — to switch environments you must run `grn login --iam-env <env>` again. In **machine mode**, you can switch `iam_env` freely.
{% endhint %}

---

### 3. AgentBase command groups

Command structure: `grn agentbase <group> <command> [options]`. Each group maps to one AgentBase service:

| Command group | Manages | Related page |
|---|---|---|
| `context` | The active environment, endpoints, headers and decorators | — |
| `identity` | Workload Identity and Outbound Auth (OAuth2, static API key, delegated), api-key delegate | [Access Control](access-control/README.md) |
| `gateway` | Create and manage MCP Gateways, access logs, Inbound Auth JWT, private network routes | [MCP Gateway](mcp-governance/mcp-gateway/README.md) |
| `runtime` | Deploy the container that runs the agent code (image, command, args, env, autoscaling), endpoints, logs, metrics, traces | [Agent Runtime](agent-runtime/README.md) |
| `memory` | Memory containers, strategies, sessions, events and records | [Memory](memory/README.md) |
| `catalog` | Runtime flavors, OpenClaw versions and workspaces | [OpenClaw](agent-runtime/openclaw/README.md) |
| `policy` | Policy Groups, policies, condition operators and decisions | [Policy Groups](mcp-governance/policy-groups/README.md) |
| `cr` | Repositories, images, artifacts and registry credentials on vCR | [Container Registry](container-registry/README.md) |
| `deploy` | Orchestrator that composes `identity` + `memory` + `runtime` (+ `cr`) into a single lifecycle | — |

Get help any time with `grn agentbase <group> --help`.

Every command accepts `-o` (`--output`) to pick the result format, and `--interactive` to have the CLI prompt for any missing required parameters:

| `-o` value | Meaning |
|---|---|
| `table` (default) | Human-readable table; secrets masked |
| `json` | Raw JSON; secrets revealed (e.g. to pipe into `docker login`) |
| `id` | Print only the ID — handy for scripting |

{% hint style="warning" %}
`-o json` prints secrets in cleartext (Client Secret, robot account password). Do not use `-o json` in public CI logs or while sharing your screen.
{% endhint %}

---

### 4. Deploy an agent with `deploy`

In AgentBase, an **agent** is the set of resources that share a **name** as the join key: an Identity (always present), a Memory container (optional — omit it for a stateless agent), and a Runtime that runs the agent code. The `deploy` command group is a client-side orchestrator that composes these services into one lifecycle:

| Command | Effect |
|---|---|
| `deploy generate` | Print an agent manifest template (YAML or JSON) |
| `deploy up` | Apply the manifest — create resources if absent, then wait for the Runtime to reach `ACTIVE` |
| `deploy status` | Show the agent's state across all services |
| `deploy destroy` | Delete the agent's Runtime and Memory (add `--purge` to delete the Identity too) |

Generate a template, then fill it in:

```bash
grn agentbase deploy generate > agent.yaml
```

```yaml
# name is the shared join key across identity + memory + runtime
# (3-50 chars, ^[a-zA-Z0-9_-]+$). identity is always created.
name: my-agent
description: "A customer-support agent"

identity:
  allowedReturnUrls:
    - https://app.example.com/callback

# memory: OPTIONAL. Omit the whole block for a stateless agent.
# When present, at least one strategy (name/type/namespaceTemplate) is required.
memory:
  eventExpiryDuration: 3600
  strategies:
    - name: prefs
      type: USER_PREFERENCE
      namespaceTemplate: "/strategies/USER_PREFERENCE/actors/{actorId}"

runtime:
  image: registry.vngcloud.vn/<your-repo>/my-agent:v1
  imageAuth: auto          # "auto" resolves pull credentials from your vCR robot account
  command: [./agent]
  args: [--port, "8080"]
  env: {LOG_LEVEL: info}
  flavorId: agent.small
  autoscaling: {minReplicas: 1, maxReplicas: 3, cpuUtilization: 70, memoryUtilization: 80}
```

Apply the manifest, track it, then clean up when you no longer need it:

```bash
grn agentbase deploy up --file agent.yaml
grn agentbase deploy status my-agent
grn agentbase deploy destroy my-agent            # deletes runtime + memory
grn agentbase deploy destroy my-agent --purge    # also deletes the identity
```

`deploy up` is **idempotent** — running it repeatedly does not create duplicate resources. `up`, `status` and `destroy` all look resources up by name, so no state file is needed.

{% hint style="warning" %}
If `deploy up` fails partway through, the CLI does **not** roll back the resources it already created. Re-run `deploy up` (it is idempotent) to continue, or run `deploy destroy` to clean up and start over. `deploy destroy --purge` also deletes the Identity and **cannot be undone**.
{% endhint %}

---

### 5. Troubleshooting

| Symptom | What to do |
|---|---|
| `authentication failed: ...` | Run `grn configure` (machine) or `grn login` (user). Check the environment and profile with `grn agentbase context current` |
| 404 on a resource lookup | `deploy` and `status` look up by name — a wrong name, or a resource in a different environment, both report as absent |
| Runtime stuck in `CREATING` | Runtimes converge asynchronously — use `grn agentbase runtime wait <id>` or `deploy status <name>` to wait |
| Switching dev ↔ prod has no effect | Machine mode: `grn configure set iam_env <env>`. User mode: you must run `grn login --iam-env <env>` again, since the token is bound to the environment |

---

If you run into problems, contact GreenNode by email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Help center: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
