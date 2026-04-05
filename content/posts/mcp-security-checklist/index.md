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
