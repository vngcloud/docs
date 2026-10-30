# Use Browser

> Connect your agent to **Browser** — drive a real Chrome inside a microVM dedicated to each session: automation over CDP, live screen view, and session recordings, integrated over MCP.

---

## Prerequisites

- A GreenNode account, and having completed [Getting Started with AgentBase](../getting-started.md)
- An account enabled in the Built-in Tools whitelist — see [Built-in Tools](README.md) if not yet enabled
- An agent with MCP client support (Claude Code, Cursor, or an MCP SDK)
- If your agent does its own automation: a **Chrome DevTools Protocol (CDP)** client — Playwright, Puppeteer, or any CDP client

---

## Connecting over MCP

**Step 1:** Get the Browser MCP endpoint:

```
https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser
```

**Step 2:** Add it to your MCP client configuration, with a header pointing to the Browser to use. Example for Claude Code:

```bash
claude mcp add --transport http --scope user browser \
  "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser" \
  --header "x-browser-id: <YOUR_BROWSER_ID>"
```

Or for Cursor / VS Code — add the header to the config:

```json
{
  "mcpServers": {
    "browser": {
      "url": "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser",
      "headers": {
        "x-browser-id": "<YOUR_BROWSER_ID>"
      }
    }
  }
}
```

Replace `<YOUR_BROWSER_ID>` with the `id` of the Browser you created — every call over this MCP connection goes into that exact Browser.

**Step 3:** Sign in the first time — your client runs the login flow itself (**Dynamic Client Registration**) and opens the GreenNode Portal login URL in the browser; the access token is kept and **refreshed automatically** afterwards. Tokens from a **Root user, IAM user, or Service Account** all work.

---

## How it works

Each **session** is a real Chrome browser running inside its own microVM. There are three separate streams:

```
Agent ──── automation stream (CDP, port 9222) ─────┐
Viewer ─── live view (noVNC, port 6080) ───────────┤── Chrome inside the microVM
Recording ─ saved when the session is deleted ─────┘
```

- **Automation stream** — your agent drives Chrome: the service relays your CDP connection to Chrome's debug port inside the VM. Playwright / Puppeteer work as if on localhost.
- **Live view** — a human watches Chrome's screen live over noVNC, embedded in the portal via an iframe.
- **Recording** — a session recording is preserved when the session ends.

Browser follows the same pattern as [Code Interpreter](use-code-interpreter.md): create the resource, wait for `ACTIVE`, create sessions (one VM per session), delete when done.

---

## Driving Chrome with the automation stream

**Step 1:** Create a Browser with the `POST /v1/browsers` API, wait for the `ACTIVE` status, then create a session — same as Code Interpreter. The `id` returned on creation is the value for the `x-browser-id` header when connecting over MCP.

**Step 2:** Enable the automation stream for the session (tool / API `PUT .../sessions/{sessionId}/streams`). The stream can be toggled per session.

**Step 3:** Point your CDP client (Playwright, Puppeteer) at the session's automation stream address. The service relays your connection to Chrome inside the VM and rewrites the debugger address to point back at itself.

---

## Watching live (live view)

Chrome's screen is served over noVNC and embedded in the portal via an iframe. Because iframes and WebSockets cannot carry authentication headers, live view uses a **signed URL** (like a presigned URL):

1. The portal requests a signed live-view URL for the session (ticket valid for **5 minutes**).
2. The URL is placed in the `iframe src` — the ticket travels in the WebSocket path and is stripped before reaching the VM.
3. An established connection is not re-authenticated; each connection lives at most **1 hour**. On expiry, the portal signs a new URL and reloads the iframe.

---

## Recordings

The recording file lives inside the VM and would be lost when the VM is destroyed. Therefore, **when you delete a session**, the service reads the recording file just before the VM is destroyed and stores it on object storage. You can then fetch it with `GET .../sessions/{sessionId}/recording`.

{% hint style="warning" %}
Recording is **best effort**: if the file cannot be read or stored, the session deletion still proceeds and no recording is kept. Recordings larger than 64 MiB (default configuration) are not stored.
{% endhint %}

---

## Main API

| Path under `/v1/browsers` | Purpose |
|---|---|
| `POST`, `GET`, `GET /{id}`, `DELETE /{id}` | Create, list, view, delete a Browser |
| `POST/GET/DELETE /{id}/sessions[/{sessionId}]` | Manage sessions — each session is one Chrome in one VM |
| `PUT /{id}/sessions/{sessionId}/streams` | Enable/disable the automation stream |
| `/{id}/sessions/{sessionId}/automation-stream[/*]` | CDP relay, all methods |
| `POST .../live-view-stream-sign` and `GET .../live-view-stream[/*]` | Sign a live-view URL, and the view stream |
| `GET .../recording` | Fetch the stored recording |

---

## Deleting

1. Delete the session — the service saves the recording (if enabled), then destroys the VM and all state.
2. Delete the Browser when no longer needed — this returns the quota.

---

## Result

Your agent can drive a real Chrome (CDP), you can watch the screen live in the portal, and you can download the session recording after it ends.

| I want to... | Go to |
|---|---|
| Let my agent run Python / shell | [Use Code Interpreter](use-code-interpreter.md) |
| See all limits and the security model | [Sandbox: security and limits](sandbox-security-and-limits.md) |
