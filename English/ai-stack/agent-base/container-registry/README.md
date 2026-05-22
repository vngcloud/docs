# Container Registry

GreenNode automatically provisions a private repository in Container Registry for your organization — store container images securely and use them directly when deploying Agent Runtime, with no external registry setup required.

---

## Overview

Container Registry in AgentBase is built on [VNG Cloud Container Registry (vCR)](../../../../vcontainer-registry/README.md). When your organization is onboarded to AgentBase, a private repository is already created for you — no manual setup needed.

View your organization's image list at: [https://aiplatform.console.vngcloud.vn/container-registry/repository](https://aiplatform.console.vngcloud.vn/container-registry/repository)

![Container Registry — image list](../../../.gitbook/assets/Agentbase-image/Container-registry.png)

**Benefits:**
- Images are not publicly accessible
- Combine with Private VPC for a fully internal deploy pipeline
- Natively integrated when creating a Custom Agent Runtime — no extra configuration needed

---

## Push an Image to the Registry

### Using AgentBase Skills (recommended)

If you have [AgentBase Skills](https://github.com/vngcloud/greennode-agentbase-skills) installed, use the built-in scripts — credentials are handled in-memory and never exposed to the terminal or disk:

**Step 1:** Get your organization's repository info

```bash
bash .claude/skills/agentbase/scripts/cr.sh repo get
```

Returns `registryUrl` (`vcr.vngcloud.vn`) and `name` (your organization's repo name).

**Step 2:** Log in to Docker securely

```bash
bash .claude/skills/agentbase/scripts/cr.sh credentials docker-login
```

**Step 3:** Tag and push your image

```bash
docker tag my-agent:latest vcr.vngcloud.vn/<repoName>/my-agent:v1.0
docker push vcr.vngcloud.vn/<repoName>/my-agent:v1.0
```

### Using Docker CLI manually

**Step 1:** Log in (using credentials from the Portal)

```bash
docker login vcr.vngcloud.vn
```

**Step 2:** Tag your image

```bash
docker tag my-agent:latest vcr.vngcloud.vn/<repoName>/my-agent:v1.0
```

**Step 3:** Push the image

```bash
docker push vcr.vngcloud.vn/<repoName>/my-agent:v1.0
```

---

## Use the Image When Creating a Runtime

**Using AgentBase Skills** — pass the `--from-cr` flag, credentials are fetched automatically:

```bash
bash .claude/skills/agentbase/scripts/runtime.sh create \
  --image "vcr.vngcloud.vn/<repoName>/my-agent:v1.0" \
  --from-cr
```

**Using the Portal** — when creating a Custom Agent Runtime, enter:
- **Image URL:** `vcr.vngcloud.vn/<repoName>/my-agent:v1.0`
- **Registry Auth:** enable → enter robot account username and password

See the full guide at [Create Runtime](../agent-runtime/create-runtime.md).

---

## Advanced Management

The Container Registry page in AgentBase is sufficient for pushing and using images with Runtime. For full management (additional repositories, access control policies, image lifecycle rules...) → see [VNG Cloud Container Registry](../../../../vcontainer-registry/README.md).

---

## Getting Started

| I want to... | Go to |
|---|---|
| Create a Runtime from an image in this registry | [Create Runtime](../agent-runtime/create-runtime.md) |
| Manage Container Registry in full | [VNG Cloud Container Registry](../../../../vcontainer-registry/README.md) |