---
layout: Conceptual
title: Use a Microsoft Sentinel MCP tool in Visual Studio Code - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-use-tool-visual-studio-code
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
description: Learn how to use Microsoft Sentinel's Model Context Protocol (MCP) collection of security tools or your own custom tool in Visual Studio Code
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f8075a35-a43d-7492-bb0c-0a4db018917f
document_version_independent_id: 69cbe6e0-e520-dede-5137-a9c2a271ce2f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-use-tool-visual-studio-code.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-use-tool-visual-studio-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-use-tool-visual-studio-code.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
platformId: f9fb4f42-e1fb-d753-fb4b-5fb00b8ce7fc
---

# Use a Microsoft Sentinel MCP tool in Visual Studio Code - Microsoft Security | Microsoft Learn

This article shows you how to add Microsoft Sentinel's Model Context Protocol (MCP) [collection of security tools](sentinel-mcp-tools-overview#available-collections) or your own custom tools to your AI agents in Visual Studio Code.

For information about how to get started with MCP tools, see the following articles:

- [Get started with Microsoft Sentinel MCP server](sentinel-mcp-get-started)
- [Create and use custom Microsoft Sentinel MCP tools](sentinel-mcp-create-custom-tool)

## Add a Microsoft Sentinel or custom tool collection

To add a Microsoft Sentinel tool collection or your own custom tools in Visual Studio Code, follow these steps:

1. **Add MCP server:**

    1. Press **Ctrl** + **Shift** + **P** then type or choose `MCP: Add Server`.

        [![Screenshot of Visual Studio Code with Add server highlighted.](media/sentinel-mcp/mcp-get-started-add-server.png)](media/sentinel-mcp/mcp-get-started-add-server.png#lightbox)
    2. Choose **HTTP (HTTP or Server-Sent Events)**.

        [![Screenshot of Visual Studio Code with HTTP or Server-Sent Events highlighted.](media/sentinel-mcp/mcp-get-started-http.png)](media/sentinel-mcp/mcp-get-started-http.png#lightbox)
    3. Enter the URL of the MCP server of the tool collection you want to access, which can be from one of the [available Microsoft Sentinel tool collections](sentinel-mcp-tools-overview#available-collections) or your own custom collection, then press **Enter**.
    4. Assign a friendly **Server ID** (for example, `Microsoft Sentinel MCP server`)
    5. Choose whether to make the server available in all Visual Studio Code workspaces or just the current one.
2. **Allow authentication.** When prompted, select **Allow** to authenticate using an account with at least a Security reader role.

    [![Screenshot of a Visual Studio Code dialog box prompting the user to authenticate.](media/sentinel-mcp/mcp-get-started-authenticate.png)](media/sentinel-mcp/mcp-get-started-authenticate.png#lightbox)
3. **Open Visual Studio Code's chat.** Select **View** &gt; **Chat**, select the **Toggle Chat** icon ![](media/sentinel-mcp/mcp-chat-icon.png) beside the search bar, or press **Ctrl** + **Alt** + **I**.
4. **Verify connection.** Set the chat to Agent mode then confirm by selecting the **Configure Tools** icon ![](media/sentinel-mcp/mcp-tools-icon.png) that you see added under the MCP server you added.

    [![Screenshot of a Visual Studio Code Agent menu with the Agent mode and tool icon highlighted.](media/sentinel-mcp/mcp-get-started-04.png)](media/sentinel-mcp/mcp-get-started-04.png#lightbox)