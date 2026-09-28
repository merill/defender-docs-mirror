---
layout: Conceptual
title: Add Microsoft Sentinel MCP tools to AI agents in Microsoft Copilot Studio - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-use-tool-copilot-studio
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
description: Add Microsoft Sentinel MCP security tools or custom tools to AI agents in Microsoft Copilot Studio. Includes steps for authentication, app registration, and connecting tool collections.
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 27b91965-4e49-6330-862a-0607f1881575
document_version_independent_id: bd8c1e4d-31c6-f3a0-d540-f04e917dd747
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-use-tool-copilot-studio.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-use-tool-copilot-studio
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-use-tool-copilot-studio.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 93dc67e8-a9c8-f7ec-980e-ee9d608e2de0
---

# Add Microsoft Sentinel MCP tools to AI agents in Microsoft Copilot Studio - Microsoft Security | Microsoft Learn

Important

This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

This article shows you how to add Microsoft Sentinel's Model Context Protocol (MCP) [collection of security tools](sentinel-mcp-tools-overview#available-collections) or your own custom tools to your AI agents in [Microsoft Copilot Studio](/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio) .

For information about how to get started with MCP tools, see [Get started with Microsoft Sentinel MCP server](sentinel-mcp-get-started) and [Create and use custom Microsoft Sentinel MCP tools](sentinel-mcp-create-custom-tool).

Tip

For the best performance with MCP tools, use GPT-5 or a later version with a higher context window.

## Add a Microsoft Sentinel tool collection

To add a Microsoft Sentinel tool collection in Copilot Studio, follow these steps:

1. Go to [Copilot Studio](https://copilotstudio.microsoft.com/) and create a new agent or select an existing agent.
2. After provisioning your agent, on your agent's **Overview** page, go to **Tools** and select **Add tool**.

    [![Screenshot of an agent's Overview page in Copilot Studio with Add tool button highlighted.](media/sentinel-mcp/get-started-studio-add-tool.png)](media/sentinel-mcp/get-started-studio-add-tool.png#lightbox)
3. On the **Add tool** pop-up window, search for `Sentinel` then choose one of the [available Sentinel MCP tool collection](sentinel-mcp-tools-overview#available-collections) that suits your needs.

    [![Screenshot of the Add tool pop-up window in Copilot Studio with a Microsoft Sentinel tool collection highlighted.](media/sentinel-mcp/get-started-studio-select-tool.png)](media/sentinel-mcp/get-started-studio-select-tool.png#lightbox)
4. Make sure that the **Authentication type** is set to **Microsoft Entra ID Integrated**, then select **Create**.

    [![Screenshot of the Add tool pop-up window in Copilot Studio showing the authentication type step.](media/sentinel-mcp/get-started-studio-authenticate.png)](media/sentinel-mcp/get-started-studio-authenticate.png#lightbox)
5. Select **Add and configure**.

    [![Screenshot of the Add tool pop-up window in Copilot Studio showing with Add and configure button highlighted.](media/sentinel-mcp/get-started-studio-add-connection.png)](media/sentinel-mcp/get-started-studio-add-connection.png#lightbox)

Your agent is now connected with Sentinel's available collection of tools. You can start prompting your agent and use the tools to deliver outcomes.

## Add a custom tool collection

Custom MCP tools let you build deterministic workflows by prescribing exactly what data agents can reason over. To add your custom tool collection in Copilot Studio, follow these steps:

Tip

Open two browser tabs or windows because you'll switch between your tenant's [Azure portal](https://portal.azure.com) and your Copilot Studio page.

### Step 1: Register an app in Azure portal

Register a Microsoft Entra application that Copilot Studio uses to authenticate with your custom MCP tool.

1. Open your tenant's Azure portal, then go to **App registrations** &gt; **New registration**.

    [![Screenshot of Azure portal with New registration option highlighted.](media/sentinel-mcp/custom-azure-new-reg.png)](media/sentinel-mcp/custom-azure-new-reg.png#lightbox)
2. On the **Register an application** page, enter a friendly user-facing **Name** for the app, then select **Register**.

    [![Screenshot of the new application registration page in Azure portal.](media/sentinel-mcp/custom-azure-register.png)](media/sentinel-mcp/custom-azure-register.png#lightbox)
3. On your newly registered app's page, go to **Manage** &gt; **API permissions**, then select **Add a permission**.

    [![Screenshot of the API permissions page and flyout panel in Azure portal.](media/sentinel-mcp/custom-azure-permissions.png)](media/sentinel-mcp/custom-azure-permissions.png#lightbox)
4. On the flyout panel that appears, go to the **APIs my organization uses** tab and search for `Sentinel Platform Services`.

    [![Screenshot of the APIs my organization uses tab in the Request API permissions panel in Azure portal.](media/sentinel-mcp/custom-azure-api-reg.png)](media/sentinel-mcp/custom-azure-api-reg.png#lightbox)
5. Choose **SentinelPlatform.DelegatedAccess**, then select **Add permissions**.

    [![Screenshot of the Request API permissions panel in Azure portal with permissions selected.](media/sentinel-mcp/custom-azure-api-delegate.png)](media/sentinel-mcp/custom-azure-api-delegate.png#lightbox)
6. Back on your app's page, go to **Manage** &gt; **Certificates & secrets**, then select the **Client secrets** tab.
7. Select **New client secret**. On the flyout panel that appears, add a **Description**, then select **Add**.

    [![Screenshot of the Certificates and secrets page in Azure portal.](media/sentinel-mcp/custom-azure-secret.png)](media/sentinel-mcp/custom-azure-secret.png#lightbox)

    Tip

    Create a single app for all Sentinel custom tools, but create separate client secrets for each custom collection you want to add to your agent.

    Important

    Once the client secret is added, copy and save its **Value**. You use it as the **Client secret** when you add the tool in Copilot Studio.
8. Go back to the Azure portal's **Overview** page and copy and save the following values to use in the Copilot Studio OAuth settings:

    - Application (client) ID
    - Directory (tenant) ID

    [![Screenshot of the Overview page in Azure portal.](media/sentinel-mcp/custom-azure-ids.png)](media/sentinel-mcp/custom-azure-ids.png#lightbox)

### Step 2: Add your custom MCP tool to an agent

In Copilot Studio, create a new MCP tool entry for the custom tool you registered in Azure.

1. Open Copilot Studio and select the agent where you want to add your custom tool. From the agent's **Overview** page, go to the **Tools** section and select **+ Add tool**.
2. On the pop-up window that appears, select **+ New tool**.

    [![Screenshot of Copilot Studio with the Add tool modal open.](media/sentinel-mcp/custom-studio-add-tool.png)](media/sentinel-mcp/custom-studio-add-tool.png#lightbox)
3. Select **Model Context Protocol** and add your custom tool collection’s details. Make sure that you add the following OAuth settings properly:

    - **Type:** Manual
    - **Client ID:** Use the **Application (client) ID** value you saved previously
    - **Client secret:** Use the secret value you saved previously
    - **Authorization URL:** Use the following format and replace `<tenant ID>` with the **Directory (tenant) ID** value you saved previously: 

        ```
        https://login.microsoftonline.com/<tenant ID>/oauth2/v2.0/authorize
        ```
    - **Token URL template** and **Refresh URL:** Use the following format and replace `<tenant ID>` with the **Directory (tenant) ID** value you saved previously: 

        ```
        https://login.microsoftonline.com/<tenant ID>/oauth2/v2.0/token
        ```
    - **Scope:** Use the following: 

        ```
        4500ebfb-89b6-4b14-a480-7f749797bfcd/.default
        ```

    [![Screenshot of the MCP details in Copilot Studio Add tool setup.](media/sentinel-mcp/custom-studio-mcp-details.png)](media/sentinel-mcp/custom-studio-mcp-details.png#lightbox)
4. Select **Create**. Your tool is created successfully and a redirect URL is generated. Copy and save this URL and leave the pop-up window open for now.

    [![Screenshot of the URL redirect details in Copilot Studio Add tool setup.](media/sentinel-mcp/custom-studio-redirect.png)](media/sentinel-mcp/custom-studio-redirect.png#lightbox)

### Step 3: Configure a redirect URI to authenticate Copilot Studio

Configure a redirect URI so that Copilot Studio can authenticate with your custom MCP tool.

1. Go back to your tenant's Azure portal and into the app you just added then select **Add a redirect URI**.
2. Select **+ Add a platform** &gt; **Web**.

    [![Screenshot of the Authentication page in Azure portal.](media/sentinel-mcp/custom-azure-add-platform.png)](media/sentinel-mcp/custom-azure-add-platform.png#lightbox)
3. In the **Redirect URIs** text box, add the redirect URL you copied then select **Configure**.
4. Return to the **Add tool** dialog in Copilot Studio, where the redirect URL was generated, and select **Next**.
5. Select **Create new connection**. If the tool connects successfully, a green check mark appears beside the connection.

    [![Screenshot of the connection details in Copilot Studio Add tool setup.](media/sentinel-mcp/custom-studio-new-connection.png)](media/sentinel-mcp/custom-studio-new-connection.png#lightbox)
6. Select **Add and configure**.