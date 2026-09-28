---
layout: Conceptual
title: Use a Microsoft Sentinel MCP Tool in Microsoft Security Copilot - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-use-tool-security-copilot
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
description: Learn how to add Microsoft Sentinel's Model Context Protocol (MCP) collection of security tools or your own custom tool in Microsoft Security Copilot
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e41080ac-c0f1-df25-87a5-d0fad76d59c4
document_version_independent_id: 9cb98bc2-afac-1394-b0a1-5714d8d9e304
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-use-tool-security-copilot.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-use-tool-security-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-use-tool-security-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: ba11bbe9-bd78-dbfe-430c-2561a183db70
---

# Use a Microsoft Sentinel MCP Tool in Microsoft Security Copilot - Microsoft Security | Microsoft Learn

This article shows you how to add Microsoft Sentinel's Model Context Protocol (MCP) [collection of security tools](sentinel-mcp-tools-overview#available-collections) or your own custom tools to your AI agents in [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot).

For information about how to get started with MCP tools, see the following articles:

- [Get started with Microsoft Sentinel MCP server](sentinel-mcp-get-started)
- [Create and use custom Microsoft Sentinel MCP tools](sentinel-mcp-create-custom-tool)

## Add a Microsoft Sentinel tool collection

Important

You need to build your own custom Security Copilot agent before you can add Sentinel's collection of MCP tools. For more information, see [Build an agent from scratch using the lite experience](/en-us/copilot/security/developer/create-agent-dev#steps-to-create-your-custom-agent).

To add a Microsoft Sentinel tool collection during custom agent building, follow these steps:

1. Select **Add tool** to open the Tools catalog modal.
2. In the **Add a tool** modal, search for and select the tools you want to add from Microsoft Sentinel's collection of MCP tools. For example, search for "entity analyzer" to find the entity analyzer tools.
3. Select **Add selected** to add the tools to your agent.

Your agent is now connected with Sentinel's available collection of tools. You can start prompting your agent and use the tools to deliver outcomes.

## Add a custom tool collection

Custom MCP tools let you build deterministic workflows by prescribing exactly what data agents can reason over. To add your custom tool collection in Security Copilot, follow these steps:

### Step 1: Create a YAML file for your tool collection

Use the following YAML file template to create and save your plugin. This YAML defines the collection descriptor for your custom plugin, including its metadata and connection settings. Replace each placeholder value (enclosed in angle brackets) with your collection-specific information, such as the collection name, endpoint URL, and the tools you want to add.

The following YAML is the plugin descriptor template. Customize it with your collection details before uploading it to Security Copilot as a custom plugin.

```yaml
Descriptor:
  Name: <Name of the collection>
  DisplayName: <Friendly name for the collection>
  Description: <Friendly description for the collection>
  DescriptionForModel: <Detailed description of the collection to help with AI selection>
SkillGroups:
- Format: MCP
  Settings:
    Endpoint: <Enter custom tool URL>
    TokenScope: 4500ebfb-89b6-4b14-a480-7f749797bfcd/.default
    UseStreamableHttp: true
    UsePluginAuth: false
    AllowedTools: <Comma-separated list of tool names to add>
    TimeoutInSeconds: 300
```

For more information about all the parameters you can add and configure in your YAML file, see [Model Context Protocol (MCP) plugins in Microsoft Security Copilot](/en-us/copilot/security/plugin-mcp).

### Step 2: Add the YAML file as a custom plugin

1. Go to the [Security Copilot portal](https://securitycopilot.microsoft.com/) and select the **Sources** icon in the prompt bar.

    ![Screenshot of the prompt bar in Security Copilot with the Sources icon highlighted.](media/sentinel-mcp/custom-copilot-source.png)
2. In the **Manage sources** pop-up window that appears, under **Plugins**, scroll down to the **Custom** section and select **Add plugin**.

    [![Screenshot of the Manage sources window in Security Copilot with the Add plugin option highlighted.](media/sentinel-mcp/custom-copilot-manage-sources.png)](media/sentinel-mcp/custom-copilot-manage-sources.png#lightbox)
3. From the drop-down options, specify if you want to make the plugin available to just yourself or anyone in the organization.
4. Select **Security Copilot plugin**, choose the YAML plugin file you created from the template in step 1 of this section, then select **Add**.

    [![Screenshot of Add plugin pop-up window in Security Copilot with Security Copilot plugin and Add options highlighted.](media/sentinel-mcp/custom-copilot-add-plugin.png)](media/sentinel-mcp/custom-copilot-add-plugin.png#lightbox)
5. Finish the setup. Once your plugin is visible in the **Custom** section, you can turn the toggle on or off.

    [![Screenshot of Custom plugin option in Security Copilot with the added plugin visible.](media/sentinel-mcp/custom-copilot-toggle-plugin.png)](media/sentinel-mcp/custom-copilot-toggle-plugin.png#lightbox)

### Step 3: Build an agent using the saved plugin

1. In the Security Copilot portal, go to **Build** and select **Start from Scratch** or open an existing custom agent.
2. In your agent skill, select **Add a tool** and find the custom plugin you added earlier in the **Custom** section of **Manage sources**.

    [![Screenshot of Add a tool option in Security Copilot.](media/sentinel-mcp/custom-copilot-add-tool.png)](media/sentinel-mcp/custom-copilot-add-tool.png#lightbox)

    [![Screenshot of Add a tool option in Security Copilot with the added plugin visible.](media/sentinel-mcp/custom-copilot-search-tool.png)](media/sentinel-mcp/custom-copilot-search-tool.png#lightbox)
3. Add the plugin to your agent.