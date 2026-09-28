---
layout: Conceptual
title: Use a Microsoft Sentinel MCP Tool in Microsoft Foundry - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-use-tool-azure-ai-foundry
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
description: Add Microsoft Sentinel MCP security tool collections or your own custom MCP tools to AI agents in Microsoft Foundry. Includes steps for app registration, authentication, and connecting tools.
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9c02d368-a3bf-7dac-cfd4-65834fbe44d5
document_version_independent_id: 7a5ef275-51c0-4943-cc27-4a5ff82d5777
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-use-tool-azure-ai-foundry.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-use-tool-azure-ai-foundry
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-use-tool-azure-ai-foundry.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/de19c5b8-e208-412e-9238-db3f631dea5b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ea7bf5d6-7154-4ba9-8ebc-59117ccacd49
platformId: 63eb3e3a-7853-d517-fd2b-706c1b04f468
---

# Use a Microsoft Sentinel MCP Tool in Microsoft Foundry - Microsoft Security | Microsoft Learn

Important

This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

This article shows you how to add Microsoft Sentinel's Model Context Protocol (MCP) [collection of security tools](sentinel-mcp-tools-overview#available-collections) or your own custom tools to your AI agents in [Microsoft Foundry](/en-us/azure/ai-foundry/what-is-azure-ai-foundry).

For information about how to get started with MCP tools, see the following articles:

- [Get started with Microsoft Sentinel MCP server](sentinel-mcp-get-started)
- [Create and use custom Microsoft Sentinel MCP tools](sentinel-mcp-create-custom-tool)

## Add a Microsoft Sentinel tool collection

To add a Microsoft Sentinel tool collection in Microsoft Foundry, follow these steps:

1. Go to [Microsoft Foundry's agent builder](https://go.microsoft.com/fwlink/?linkid=2340185) then select **Build** &gt; **Agent**.

    [![Screenshot of Microsoft Foundry agent builder page with the build agent option highlighted.](media/sentinel-mcp/get-started-foundry-build-agent.png)](media/sentinel-mcp/get-started-foundry-build-agent.png#lightbox)
2. Enter a name for your agent.

    [![Screenshot of the Create new agent pop-up window in Microsoft Foundry agent builder page.](media/sentinel-mcp/get-started-foundry-create-agent.png)](media/sentinel-mcp/get-started-foundry-create-agent.png#lightbox)
3. On the **Tools** panel, select **Add a new tool** to ground your agent instructions with relevant security data from Microsoft Sentinel.

    [![Screenshot of an agent's page in Microsoft Foundry with add tool option highlighted.](media/sentinel-mcp/get-started-foundry-add-tool.png)](media/sentinel-mcp/get-started-foundry-add-tool.png#lightbox)
4. On the **Select a tool** pop-up window, search for `Sentinel` and choose any [available Microsoft Sentinel tool collection](sentinel-mcp-tools-overview) (for example, `Microsoft Sentinel – Data exploration`).

    [![Screenshot of the Select a tool pop-up window in Microsoft Foundry agent builder page with a Sentinel tool collection highlighted.](media/sentinel-mcp/get-started-foundry-select-tool.png)](media/sentinel-mcp/get-started-foundry-select-tool.png#lightbox)
5. Select **Connect**.

Your agent is now connected with Sentinel's available collection of tools. You can start prompting your agent and use the tools to deliver outcomes.

## Add a custom tool collection

Custom tools let you build deterministic workflows by prescribing exactly what data agents can reason over. To add your custom tool collection in Microsoft Foundry, follow these steps:

### Step 1: Register an app in Azure portal

1. Open your tenant's [Azure portal](https://portal.azure.com) then go to **App registrations** &gt; **New registration**.

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

    Once the client secret is added, copy and save its **Value**, which you use in the next steps.
8. Go back to the Azure portal's **Overview** page and copy and save the following values for the next steps:

    - Application (client) ID
    - Directory (tenant) ID

    [![Screenshot of the Overview page in Azure portal.](media/sentinel-mcp/custom-azure-ids.png)](media/sentinel-mcp/custom-azure-ids.png#lightbox)

### Step 2: Add your custom MCP tool

Add the custom MCP tool to your agent in Microsoft Foundry by following these steps:

1. Go to Microsoft Foundry and select an existing agent or a newly created agent.
2. On the agent's page, go to the **Tools** section then select **Add** &gt; **+ Add a new tool**.

    [![Screenshot of an agent's page in Microsoft Foundry with Add a new tool highlighted.](media/sentinel-mcp/custom-foundry-add-tool.png)](media/sentinel-mcp/custom-foundry-add-tool.png#lightbox)
3. In the **Add a new tool** pop-up window, select **Custom** &gt; **Model Context Protocol (MCP)**, and then select **Create**.

    [![Screenshot of the add tool setup in Microsoft Foundry.](media/sentinel-mcp/custom-foundry-mcp.png)](media/sentinel-mcp/custom-foundry-mcp.png#lightbox)
4. Add the following values:

    - **Name:** Enter a friendly name for your tool
    - **Remote MCP server endpoint:** Paste the endpoint you copied from your custom tool collection; it should have the following format:

        ```
        https://sentinel.microsoft.com/mcp/custom/<name of your custom collection>
        ```
    - **Authentication:** OAuth Identity Passthrough
    - **Client ID:** Use the **Application (client) ID** value you saved previously
    - **Client secret:** Use the secret value you saved previously
    - **Token URL** and **Refresh URL:** Use the following format and replace `<tenant ID>` with the **Directory (tenant) ID** value you saved previously:

        ```
        https://login.microsoftonline.com/<tenant ID>/oauth2/v2.0/token
        ```
    - **Authorization URL:** Use the following format and replace `<tenant ID>` with the **Directory (tenant) ID** value you saved previously:

        ```
        https://login.microsoftonline.com/<tenant ID>/oauth2/v2.0/authorize
        ```
    - **Scope:** Use the following:

        ```
        4500ebfb-89b6-4b14-a480-7f749797bfcd/.default,offline_access
        ```

    [![Screenshot of the MCP details in add tool setup in Microsoft Foundry.](media/sentinel-mcp/custom-foundry-mcp-details.png)](media/sentinel-mcp/custom-foundry-mcp-details.png#lightbox)
5. Select **Connect**. Your tool is created successfully and a redirect URL is generated. Copy and save the redirect URL.

    [![Screenshot of the credential provider or redirect URL details in add tool setup in Microsoft Foundry.](media/sentinel-mcp/custom-foundry-redirect.png)](media/sentinel-mcp/custom-foundry-redirect.png#lightbox)

### Step 3: Authenticate Microsoft Foundry to use your custom tool

To authenticate Microsoft Foundry with the custom tool, complete the following steps:

1. Go back to your tenant's Azure portal and into the app you just added then select **Add a redirect URI**.
2. Select **+ Add a platform** &gt; **Web**.

    [![Screenshot of the Authentication page in Azure portal.](media/sentinel-mcp/custom-azure-add-platform.png)](media/sentinel-mcp/custom-azure-add-platform.png#lightbox)
3. In the **Redirect URIs** text box, add the redirect URL you copied then select **Configure**.
4. Go back to Microsoft Foundry and use a prompt that matches the tool you created. On your first attempt, select **Open consent** to give consent to your signed in user account.

    [![Screenshot of chat details in Microsoft Foundry with Open consent window highlighted.](media/sentinel-mcp/custom-foundry-open-consent.png)](media/sentinel-mcp/custom-foundry-open-consent.png#lightbox)
5. In the consent pop-up window, select **Allow access**.

Once you give consent, your agent can reason over data returned by your custom MCP tool.

[![Screenshot of chat details in Microsoft Foundry that uses a custom tool.](media/sentinel-mcp/custom-foundry-prompt-result.png)](media/sentinel-mcp/custom-foundry-prompt-result.png#lightbox)