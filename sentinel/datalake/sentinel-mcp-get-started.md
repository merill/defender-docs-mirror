---
layout: Conceptual
title: Get started with Microsoft Sentinel MCP server - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-get-started
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how to set up and use Microsoft Sentinel's Model Context Protocol (MCP) collection of security tools to enable natural language queries and AI-powered security investigations
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: get-started
ms.date: 2026-05-07T00:00:00.0000000Z
locale: en-us
document_id: cb057f2c-039c-9050-cdce-5baabfa6b88a
document_version_independent_id: 7fba0de6-854c-0a72-cb92-6234474d2c98
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-get-started.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 692b37a0-6218-3837-566d-6543fe5bdf8b
---

# Get started with Microsoft Sentinel MCP server - Microsoft Security | Microsoft Learn

This article shows you how to set up and use Microsoft Sentinel's Model Context Protocol (MCP) collection of security tools to enable natural language queries against your security data. Sentinel's support for MCP enables security teams to bring AI into their security operations by allowing AI models to access security data in a standard way. For more information on how AI is used within Microsoft Sentinel's unified MCP server, see [Application card: Microsoft Sentinel MCP server](sentinel-mcp-application-card).

Sentinel's [collection](sentinel-mcp-tools-overview) of security tools works with multiple clients and automation platforms. You can use these tools to search for relevant tables and retrieve data, analyze entities, triage incidents, hunt for threats, and other tasks.

## Prerequisites

Most of the tools in the Microsoft Sentinel MCP server require you to be onboarded to the [Microsoft Sentinel data lake](sentinel-lake-onboarding) to use them.

Other tools might also need you to be onboarded to at least one of the following products:

- [Microsoft Sentinel in Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard)
- [Microsoft Defender XDR or Microsoft Defender for Endpoint](/en-us/defender-xdr/isoc-overview)
- [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot)

For more information about a tool collection's specific product prerequisites, see their respective articles.

You also need the **Security reader** role to list and invoke Sentinel's collection of MCP tools. The [triage tool collection](sentinel-mcp-triage-tool) lets you use any tool your existing permissions grant you.

## Add Microsoft Sentinel's collection of MCP tools

For more information on how to add Microsoft Sentinel's collection of MCP tools, see the articles for the following AI-powered code editors and agent-building platforms:

- [Microsoft Security Copilot](sentinel-mcp-use-tool-security-copilot#add-a-microsoft-sentinel-tool-collection)
- [Microsoft Copilot Studio](sentinel-mcp-use-tool-copilot-studio#add-a-microsoft-sentinel-tool-collection)
- [Microsoft Foundry](sentinel-mcp-use-tool-azure-ai-foundry#add-a-microsoft-sentinel-tool-collection)
- [Visual Studio Code](sentinel-mcp-use-tool-visual-studio-code)

## Test your added tools with sample prompts

After adding Microsoft Sentinel's collection of tools, use the following sample prompts to interact with data in your Microsoft Sentinel data lake.

- Find the top three users that are at risk and explain why they're at risk.
- Find sign-in failures in the last 24 hours and give me a brief summary of key findings.
- Identify devices that showed an outstanding number of outgoing network connections.
- Help me understand if the user &lt;user object ID&gt; is compromised.
- Investigate users with a password spray alert in the last seven days and tell me if any of them are compromised.
- Find all the URL IOCs from &lt;threat analytics report&gt; and analyze them to tell me everything Microsoft knows about them.

To understand how agents invoke these tools to answer these prompts, see [How Microsoft Sentinel MCP tools work alongside your agent](sentinel-mcp-data-exploration-tool#how-microsoft-sentinel-mcp-tools-work-alongside-your-agent).

## Turn off Microsoft Sentinel MCP tool access

To turn off your access to Microsoft Sentinel's collection of MCP tools, contact customer support.