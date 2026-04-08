---
title: "DRAFT - MCP Security Review Checklist"
date: 2026-03-05
draft: false
tags: ["mcp", "AI", "security", "checklist"]
categories: ["MCP", "AI"]
description: "A structured guide for reviewing the MCP implementation within your environment."
---
The Model Context Protocol (MCP) is an open standard developed by Anthropic that enables AI models like Claude, Copilot, etc to connect with external tools (e.g., image generation, web browsers), data sources (e.g., Confluence, Google Drive, GitHub repos), and services (e.g., Outlook, Slack messaging, Jira tickets) in a structured way. This would be like a universal plug for AI integrations. 

While MCP unlocks powerful capabilities like file access, web browsing, database queries - it also introduces a new attack surface that developers and security teams need to consider seriously. Since MCP servers can execute actions on behalf of an AI model, a misconfigured or compromised server could lead to risks like data leaks, unauthorized access or prompt injection attacks.

This article breaks down the checklist into five layers:
___

1: Protocol - How the server implements MCP itself

___

2: Auth - Authentication and authorization

___

3: Data Flow - What moves where, prompt injection

___

4: Runtime - System privileges, logging, transit

___

5: Dynamic Testing - Actually breaking it

___

### Layer 1 - Protocol

### Layer 2 - Authentication and Authorization

Authentication is, *who are you?* - proving identity. Authorization is, *are you allowed to do this?* - checking the permissions.

In a normal web application, both is checked at the same place - the web application. In MCP scenario, there are multiple parties involved and this question gets asked at many point. For example, consider a Jira MCP. In that case, this would follow like:

    User -> AI host like Claude -> MCP Client -> MCP Server -> Jira API -> Atlassian servers

Each arrow above shows trust boundary, as they are separate assets. Each boundary needs its own authentication and authorization. Most security issues come from a boundary where one of these was skipped, assumed or inherited incorrectly.

#### OAuth 2.1

**Explaining with a simple example**: OAuth can be like a hotel key-card system. When you check-in, the hotel gives you a key-card (access token) that opens your room and maybe the gym and terrace pool. It would not open any other places in the building (scope) like other guests' rooms, manager's cabin, staff area. The key-card has an expiry time, normally the check-out time. Also, this key-card is made specifically for you to be used at only that hotel building - not any other hotel or room.

MCP's auth spec uses OAuth 2.1, the stricter successor to OAuth 2.0.

- **Server uses Authorization Code + PKCE flow for user delegated access.** PKCE prevents someone from intercepting the authorization code in transit and exchanging it for a token. It would be like the key-card is handed to you in a sealed envelope.

If the MCP server is using Client Credentials flow (service account) for all users, that's not correct. This can be risky because all actions happen under one shared identity, so the system cannot clearly tell which user actually performed an action. If that single credential is leaked or misused, it may grant broad access to many users’ data instead of just one person’s data.

#### Token Audience Binding

This is like 'this key-card only works for that specific hotel building'. An access token issued for one Jira MCP server should only work for that Jira MCP server, not at the direct Jira API and not at any other MCP server within your environment.

- **Server validates the `aud` (audience) claim on every token.** If the `aud` validation is not happening, that means a token issued for any service in the environment could be replayed against the MCP server.
- **Token passthrough to the downstream APIs is absent.** The server must not take whatever token the MCP client sends and directly forward it to the Jira or Confluence API. It should use its own service credentials tor exchange the token properly. Token passthrough should not happen.
