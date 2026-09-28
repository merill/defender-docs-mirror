---
layout: Conceptual
title: Create and use custom Microsoft Sentinel MCP tools - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-create-custom-tool
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
description: Learn how to set up and use custom Microsoft Sentinel Model Context Protocol (MCP) tools using saved KQL queries in advanced hunting
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: get-started
ms.date: 2025-11-24T00:00:00.0000000Z
locale: en-us
document_id: 9858abbd-fbf8-605f-6ee9-0964ee6db82f
document_version_independent_id: 7dc13917-b170-2d15-6496-c1fa3f728e91
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-create-custom-tool.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-create-custom-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-create-custom-tool.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ac699f7a-e561-1651-b8ba-cb0e2d00c1b5
---

# Create and use custom Microsoft Sentinel MCP tools - Microsoft Security | Microsoft Learn

Important

This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Security agents built with Microsoft Sentinel's collection of Model Context Protocol (MCP) tools can effectively reason over data in Microsoft Sentinel. You can create custom Sentinel MCP tools to have granular control over the data accessible to your security agents and create deterministic agentic workflows.

This article shows how you can enable agents to retrieve and reason over knowledge from your library of saved Kusto Query Language (KQL) queries in [advanced hunting](/en-us/defender-xdr/advanced-hunting-microsoft-defender?toc=%2Fazure%2Fsentinel%2FTOC.json&amp;bc=%2Fazure%2Fsentinel%2Fbreadcrumb%2Ftoc.json) and Sentinel data lake by creating custom MCP tools.

## Prerequisites

To create custom Microsoft Sentinel MCP tools, you need the following prerequisites:

- Microsoft Sentinel data lake and Microsoft Defender licenses
- **Security Operator**, **Security Admin**, or **Global Admin** role to create, update, or delete custom tools
- **Security reader** or **Global reader** role to list and invoke custom tools

## Create custom tools with KQL queries

Use advanced hunting queries in Microsoft Defender portal and KQL queries in Microsoft Sentinel data lake to find and discover security data that you can use in agentic workflows. This approach lets you control the type and amount of information your agents can reason over. When you verify that a query retrieves the data you want your agent to reason with, save it as a custom MCP tool.

To save a KQL query as an MCP tool, follow these steps:

1. In the **Advanced hunting** page in Microsoft Defender, find and discover from your manually authored KQL queries or from your library of saved queries the security data you want to use in your agentic flows, then open it in the query window.
2. Select **Save as tool** from any of the following Defender portal experiences:

    - Context menu of a query

        [![Screenshot of the Save as tool option in the context menu of a KQL query.](media/sentinel-mcp/custom-tool-save-context-menu.png)](media/sentinel-mcp/custom-tool-save-context-menu.png#lightbox)
    - KQL query box menu of a query

        [![Screenshot of the Save as tool option in a KQL query box.](media/sentinel-mcp/custom-tool-save-kql-box.png)](media/sentinel-mcp/custom-tool-save-kql-box.png#lightbox)
3. In the **Save tool** flyout panel that appears, enter the following details:

    - **Name:** A discoverable name for your tool that helps AI models correctly identify and select the tool for specific tasks.
    - **Description:** The description of the tool. For more information, see Best practices for creating tool descriptions.
    - **Collection:** Choose whether you want to add the tool an existing tool collection or create a new one by selecting **Create new collection**.
    - **Default workspace:** The default workspace you want your agent to use as a hint whenever a prompt doesn't specify any workspaces.
    - **Parameters (optional):** The customizable inputs the tool supports. You can convert some of the values in your KQL query into parameters following the `{ParamaterName}` format, then add their **Parameter name** and **Description** so that the agent has a good understanding on how to populate them based on available conversation context.

    [![Screenshot of the MCP custom tool flyout panel in advanced hunting.](media/sentinel-mcp/custom-tool-save-panel.png)](media/sentinel-mcp/custom-tool-save-panel.png#lightbox)

    [![Screenshot of a KQL query with certain values converted into parameters.](media/sentinel-mcp/custom-tool-parameters.png)](media/sentinel-mcp/custom-tool-parameters.png#lightbox)
4. Select **Save**.

### View saved custom MCP tools

To view the custom MCP tools you saved from advanced hunting queries, go to the **Tools** tab in the **Advanced hunting** page.

### Best practices for creating tool descriptions

When saving your custom tool, its name and, more importantly, its description are crucial for identifying and selecting it for specific tasks. The following best practices and considerations can help when describing your tool:

- **Keep it short and action-oriented.** Use one to two sentences that start with a clear verb and resource (for example, "Retrieves audit log data for a specific user"). Avoid jargon or overly technical phrasing.
- **Focus on purpose, not parameters.** Describe what the tool does and its primary use case. Leave parameter details to the schema, not the description.
- **Include workflow hints only if critical.** If a tool requires a prerequisite step (for example, "Call `risky_users_tool` first"), mention it briefly to prevent misuse.
- **Optimize for discoverability and clarity.** Use consistent naming, avoid ambiguous terms, and ensure descriptions help AI models and users quickly select the right tool.

## Use custom tools in custom agents and coding platforms

For more information on how to use your custom tool collection in your security agents, see the articles for the following AI-powered code editors and agent-building platforms:

- [Microsoft Security Copilot](sentinel-mcp-use-tool-security-copilot#add-a-custom-tool-collection)
- [Microsoft Copilot Studio](sentinel-mcp-use-tool-copilot-studio#add-a-custom-tool-collection)
- [Microsoft Foundry](sentinel-mcp-use-tool-azure-ai-foundry#add-a-custom-tool-collection)
- [Visual Studio Code](sentinel-mcp-use-tool-visual-studio-code)