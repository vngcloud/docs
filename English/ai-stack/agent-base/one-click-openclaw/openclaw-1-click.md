# OpenClaw 1-Click

## Overview

**OpenClaw 1-Click** lets you deploy a personal AI Agent powered by OpenClaw directly from the **Agent Marketplace** on GreenNode AgentBase — no technical knowledge required, no manual setup, ready in just **40–60 seconds**.

### What is OpenClaw?

[OpenClaw](https://open.claw.cloud/) is an open-source AI agent capable of autonomously completing tasks: browsing the web, managing files, running commands, writing code, and integrating with messaging platforms (Telegram, Zalo). Instead of installing OpenClaw on your local machine, GreenNode AgentBase lets you run OpenClaw on the cloud with full compute resources and a built-in connection to GreenNode MaaS (Model-as-a-Service).

To get started deploying and managing an OpenClaw instance, see [Deploy & Manage OpenClaw](deploy-and-manage-openclaw.md).

### Self-install vs. 1-Click Deploy

| Criteria | Self-install OpenClaw (Local) | OpenClaw 1-Click (AgentBase) |
| --- | --- | --- |
| **Setup time** | 30–60 minutes | 40–60 seconds |
| **Technical requirement** | DevOps knowledge required | None |
| **API key configuration** | Manual | Auto-connected to GreenNode MaaS |
| **Infrastructure** | Local machine | Cloud (GreenNode AgentBase) |
| **Messaging integration** | Manual setup | Telegram, Zalo — configurable at deploy time |
| **Instance management** | Self-managed | Via My Agents Dashboard |

### When should you use OpenClaw 1-Click?

* **General users**: Want to use an AI Agent immediately without any installation or technical configuration.
* **Developers**: Want OpenClaw running on the cloud, pre-connected to an LLM, without managing infra.
* **Non-GreenNode users**: Want to use a model from an external provider (OpenAI, Anthropic, Gemini) — BYOK is supported.

***

## How OpenClaw 1-Click Works

When you click Deploy, AgentBase automatically runs 4 provisioning tasks:

| Step | Task | Description |
| --- | --- | --- |
| 1 | **OpenClaw Token** | Creates an Identity and authentication token for the instance |
| 2 | **AI Service Account** | Creates an IAM Service Account connected to GreenNode MaaS |
| 3 | **AI Service Token** | Retrieves an access token for the selected AI model |
| 4 | **Cloud Computer** | Starts the OpenClaw container on AgentBase Runtime |

Once complete, you receive an **OpenClaw Gateway URL** to access your chat portal immediately.

***

## AI Sources

### GreenNode MaaS (Default)

For users with a GreenNode account. The system automatically creates an API key and connects to GreenNode Model-as-a-Service — no copy/pasting of keys required.

### BYOK — Bring Your Own Key

For users who want to use a model from an external provider. You supply your own API key during configuration.

| Supported Provider | Example Models |
| --- | --- |
| OpenAI | gpt-4o, gpt-4.1 |
| Anthropic | claude-sonnet-4, claude-opus-4 |
| Gemini | gemini-2.0-flash |
| Custom | Custom endpoint |

***

## Channel Integrations

OpenClaw supports connecting to messaging platforms so you can chat with your AI Agent directly from your preferred app:

| Channel | Description |
| --- | --- |
| **Telegram** | Connect via Telegram Bot Token. Supports Pairing and Allow List modes |
| **Zalo** | Connect via Zalo |

Channels can be configured during the deploy step or later at **Settings → Config** in the OpenClaw Gateway.

***

## FAQ

### 1. I don't have a GreenNode account — can I still use this?

**Yes.** Select **BYOK** during configuration and enter an API key from an external provider (OpenAI, Anthropic, Gemini...).

### 2. Can I deploy multiple OpenClaw instances?

**Yes.** A single user can deploy multiple instances. Manage all of them from the **My Agents Dashboard**.

### 3. My instance shut down automatically — did I lose my data?

Instance data is preserved after an auto-shutdown. Simply Restart from My Agents Dashboard to continue.

### 4. Can I integrate Telegram or Zalo?

**Yes.** You can configure the integration during the deploy step or later at **Settings → Config** in the OpenClaw Gateway. Both Telegram and Zalo are supported.

For current limitations and important technical notes, see [Limitations & Notes](limitations-and-notes.md).
