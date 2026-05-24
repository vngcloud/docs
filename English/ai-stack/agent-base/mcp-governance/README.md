# MCP Governance

MCP Governance gives you centralized control over all traffic from AI agents to external services — authentication, authorization, and audit logging — without changing agent code.

---

## Overview

When agents call **MCP Tool Servers** (web search, database, file system, etc.) directly with no intermediary control layer, you have no way to know which agent is calling which tool, you cannot restrict access, and there is no audit trail when incidents occur.

MCP Governance provides a **centralized control plane** between agents and external services, consisting of two main components:

| Component | Function |
|---|---|
| **MCP Gateway** | Centralized proxy for all MCP tool calls — authenticates inbound requests from agents, authenticates outbound requests to MCP servers, and enforces attached Policy Groups |
| **Policy Group** | A set of operator-first rules defining which agents can call which tools under which conditions — attach to an MCP Gateway for automatic enforcement |

---

## Scope

- MCP Gateway CRUD (create / view / edit / delete)
- Attach Policy Group to MCP Gateway

---

## Get Started with MCP Governance

| I want to... | Go to |
|---|---|
| Understand how MCP Gateway works | [MCP Gateway](mcp-gateway/README.md) |
| Create my first MCP Gateway | [Manage MCP Gateway](mcp-gateway/manage-mcp-gateway.md) |
