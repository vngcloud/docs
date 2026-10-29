# Sandbox — Security and Limits

## Isolation model

| Boundary | What it provides |
|---|---|
| microVM per session | Dedicated kernel, processes, filesystem, and memory. State from one session is never visible to another and is destroyed when the session is deleted. Uses Kata Containers + Cloud Hypervisor |
| Namespace per user | All VMs of one user live in a dedicated namespace (`agent-core-<userId>`), attached by the platform — callers cannot set or override it |
| Authentication at the gateway | Only valid tokens of the resource owner pass the gateway; downstream hops trust the tenant information attached by the gateway |
| Credential stripping | `Authorization`, `Cookie`, and identity headers are removed before a request reaches the VM; no service-account token is ever mounted into a sandbox pod |
| Dedicated vKS node group | Sandbox workloads run on a dedicated node group with nested virtualization enabled and the `nested-virt=true:NoSchedule` taint; sandbox pods run through RuntimeClass `kata-clh` |

## Credentials inside the sandbox

| Topic | Behavior |
|---|---|
| Caller's token | Never reaches the VM — stripped at the gateway/runtime before relay |
| Platform's internal tokens | Not mounted into sandbox pods; the tool service signs its own short-lived JWTs when calling into the runtime |
| Credentials for your agent | If the agent inside the sandbox needs credentials, pass them through your own channel — not via default headers |
| Vault credential | Roadmap: OpenSandbox's credential vault feature is not integrated in the current release |

## Network

| Flow | Allowed? |
|---|---|
| Inbound: from the gateway and sandbox management | Yes |
| Outbound: DNS, telemetry collector | Yes |
| Outbound: public internet | Yes |
| Outbound: private IP ranges (RFC 1918), metadata service, Kubernetes API server | No — blocked by a deny network policy |

## Limits and quotas

| Limit | Value | Notes |
|---|---|---|
| Code Interpreters per user | 5 (default) | Recorded into the quota row on first use |
| Browsers per user | 5 (default) | Counted per tool type |
| Total sessions per user | 10 (default) | Summed across all tools — sessions are what actually bounds resources |
| Session creation time (warm VM) | ~3 seconds | |
| Session creation time (cold VM boot) | ~17 seconds | Burst beyond the warm pool |
| First tool creation time | a few minutes | The VM pool must be provisioned and the first VM booted |
| One proxy call (including streaming) | 10 minutes | Exceeding returns `504` |
| Synchronous shell command | 30 seconds | Use `startCommandExecution` for longer work |
| Background command | 15 minutes | Fetch the result via `getTask` |
| File size per read/write | 10 MiB | Exceeding returns `413`; one file per call |
| Recording size | 64 MiB | Larger recordings are not stored |
| Sessions per endpoint | under 100 | Including warm VMs in the pool |
| Concurrent HTTP proxy calls service-wide | 25 | Shared across all callers; exceeding returns `503` |
| Concurrent WebSocket proxies service-wide | 25 | Exceeding closes with code `1013` |
| WebSocket idle / message size | 5 minutes / 1 MiB | |
| Session TTL / idle timeout | None | A session only ends when deleted |

{% hint style="warning" %}
There is no automatic session cleanup: a forgotten session keeps its VM and holds a quota slot until it is deleted or the tool is deleted. Always delete sessions when done.
{% endhint %}

## Resource statuses

| Status | Description |
|---|---|
| `CREATING` | Provisioning the VM pool and booting the first VM |
| `ACTIVE` | Ready to create sessions and invoke tools |
| `FAILED` | Timed out during creation — terminal status |
| `DELETED` | Deleted, quota returned |

## Common error codes

| Code | Meaning |
|---|---|
| `401` | Not signed in or token expired — re-run your MCP client's login flow |
| `404` | Resource does not exist — or belongs to another user (existence is not revealed) |
| `409` | Resource not yet `ACTIVE` when calling session/invoke |
| `413` | File exceeds the size limit |
| `429` / `503` | Platform busy or over the concurrent-call limit — retry later |
| `502` / `504` | Sandbox infrastructure error/timeout; call exceeded the 10-minute limit |

## Roadmap

| Topic | Status |
|---|---|
| Vault credential for sandbox | Not integrated yet (upstream OpenSandbox feature) |
| Custom sandbox runtime (own image, direct session API) | Internal only, not publicly available yet — pending the billing model |
| Session TTL / auto-cleanup | Under consideration (TTL or a reaper job) |
| Languages other than Python for `executeCode` | Roadmap |
