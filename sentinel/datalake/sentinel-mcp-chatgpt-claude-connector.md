---
layout: Conceptual
title: Use the Microsoft Sentinel MCP connector in ChatGPT or Claude - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-chatgpt-claude-connector
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
description: Learn how to turn on and use a custom Microsoft Sentinel's Model Context Protocol (MCP) connector in ChatGPT or Claude
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-nochange
ai-usage: ai-assisted
locale: en-us
document_id: a8d04fed-3c64-9074-e176-1e3ad13a087d
document_version_independent_id: f7c5c111-57c3-1b87-259a-1b8174dde0bc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-chatgpt-claude-connector.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-chatgpt-claude-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-chatgpt-claude-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 90552746-ea15-5ca0-1c36-ee6b6c6e01f2
---

# Use the Microsoft Sentinel MCP connector in ChatGPT or Claude - Microsoft Security | Microsoft Learn

Important

This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

This article shows you how to enable and use a custom Microsoft Sentinel Model Context Protocol (MCP) connector in ChatGPT by OpenAI or Claude by Anthropic. By using a custom Microsoft Sentinel MCP connector in ChatGPT or Claude, Security Operations Center (SOC) analysts can run security tasks by using Microsoft Sentinel MCP. Before you begin, make sure you meet the prerequisites, including a supported subscription and a registered Microsoft Entra application.

## Prerequisites

Before configuring a Microsoft Sentinel MCP connector in ChatGPT or Claude, you must have the following prerequisites:

- A ChatGPT Pro or a Claude Pro, Max, Team, or Enterprise plan subscription.
- A Microsoft Entra application, which represents ChatGPT or Claude as a client; for more information, see Add a Microsoft Entra application.
- [Microsoft Sentinel data lake](sentinel-lake-onboarding).
- Tenant-level administrative privileges.

Important

Use roles with the fewest permissions to help improve security for your organization. Global Administrator is a highly privileged role. Limit its use to emergency scenarios when you can't use an existing role.

### Add a Microsoft Entra application

To add a Microsoft Entra application, follow these steps:

1. Open your tenant's [Microsoft Entra admin center](https://entra.microsoft.com/), go to **App registrations**, and then select **New registration**.
2. On **Register an application**, enter a friendly user-facing **Name** for the app.
3. Under **Redirect URIs**, select **Select a platform** and then choose **Web**.
4. Add any of the following URLs:

    - **For ChatGPT**

        ```
        https://chatgpt.com/connector_platform_oauth_redirect
        ```
    - **For Claude**

        ```
        https://claude.ai/api/mcp/auth_callback
        ```
5. Select **Register**.
6. On your newly registered app's page, go to **Manage** &gt; **API permissions**, and then select **Add a permission**.
7. On the **APIs my organization uses** tab, search for `Sentinel Platform Services`.
8. Choose **SentinelPlatform.DelegatedAccess**, and then select **Add permissions**.
9. Select **Manage** &gt; **Certificates & secrets** and select **New client secret**.
10. Add a **Description** for your client secret and set an expiration date.

    Important

    The client secret value is shown only once and disappears after you leave the page. Be ready to copy and save it in a secure location before you continue.
11. Select **Add**, and then immediately copy the **Value** and save it in a secure location.
12. Go back to your app's **Overview** page and copy its **Application (client) ID**.

## Create and use a custom Microsoft Sentinel MCP connector

To create and use a custom Microsoft Sentinel MCP connector, follow the instructions for your platform. For ChatGPT, see the ChatGPT section. For Claude, see the Claude section.

# [ChatGPT](#tab/chatgpt)
Use the following steps to create and use the Microsoft Sentinel MCP connector in ChatGPT.

Note

- If you're using the ChatGPT desktop application, you must first complete the ChatGPT custom connector setup in the ChatGPT web version.
- For ChatGPT Enterprise, an administrator can roll out a connector to all users in that ChatGPT organization.

**To create a custom connector:**

1. Turn on the ChatGPT developer mode. In ChatGPT, select your account icon, go to **Apps & connectors** &gt; **Advanced Settings**, and toggle **Developer mode**.
2. Go back to **Apps & connectors** and select **Create Connector**.
3. Provide the following required details:
    - **Connector name:** For example, `Microsoft  MCP`
    - **MCP Server URL:**`https://sentinel.microsoft.com/mcp/data-exploration`
    - **Client ID:** The **Application (client) ID** of the Microsoft Entra application you created previously.
4. When prompted, complete the OAuth consent flow. Once the MCP connector authenticates successfully, it appears in your ChatGPT connector list.

**To attach and use the connector:**

1. Start a new chat in ChatGPT.
2. Select the **(+)** icon next to the message box.
3. Select **More** &gt; **Microsoft MCP Connector**. The Microsoft Sentinel MCP connector's tools become available automatically, and ChatGPT can begin calling Microsoft Sentinel operations on your behalf.

# [Claude](#tab/claude)
To create and use a custom Microsoft Sentinel MCP connector in Claude, complete the following steps.

**To create a custom connector:**

1. Go to https://claude.ai/customize/connectors, to create a new custom connector. Select the **+** icon and choose **Add a custom connector**.
2. Provide the following required details:
    - **Connector name:** For example, `Microsoft Sentinel MCP`
    - **MCP Server URL:**`https://sentinel.microsoft.com/mcp/data-exploration`
    - **Client ID:** The **Application (client) ID** of the Microsoft Entra application you created previously.
    - **OAuth Client Secret:** The client secret of the Microsoft Entra application you created previously.
3. When prompted, complete the OAuth consent flow. Once the MCP connector authenticates successfully by using the Microsoft Entra credentials, it appears in your Claude connector list.
4. Select the MCP connector and choose **Connect**.
5. Select **Configure** to determine which tools to allow for your environment.

**To attach and use the connector:**

Start a new chat in Claude. The Microsoft Sentinel MCP connector tools become available automatically, and Claude can begin calling Microsoft Sentinel operations on your behalf.

Note

You can only use the [data exploration tool collection](sentinel-mcp-data-exploration-tool).

---