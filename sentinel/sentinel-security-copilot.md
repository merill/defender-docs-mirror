---
layout: Conceptual
title: Security Copilot with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-security-copilot
breadcrumb_path: breadcrumb/toc.json
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
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn about Microsoft Sentinel capabilities in Security Copilot. Understand the best prompts to use and how to get timely, accurate results for natural language to KQL.
keywords: security copilot, Microsoft Defender XDR, embedded experience, incident summary, query assistant, incident report, incident response automated, automatic incident response, summarize incidents, summarize incident report, plugins, Microsoft plugins, preinstalled plugins, Microsoft Security Copilot, Security Copilot, Microsoft Defender, Copilot in Sentinel, NL2KQL, natural language to KQL, generate queries
ms.collection: usx-security
ms.pagetype: security
ms.author: macapara
author: mjcaparas
ms.reviewer: corinaf
ms.localizationpriority: medium
ms.topic: concept-article
ms.date: 2026-08-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: f8750937-9f99-6819-f360-5281631400d3
document_version_independent_id: 983f0096-37a3-b088-8a0a-813beb877f57
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-security-copilot.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-security-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-security-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 01470660-8365-454d-a2a2-f13ddf11d9c9
---

# Security Copilot with Microsoft Sentinel | Microsoft Learn

Microsoft Security Copilot is a platform that helps you defend your organization at machine speed and scale. Microsoft Sentinel's vast security data provides an excellent source for Copilot to help analyze incidents and generate hunting queries.

Together with other Security Copilot sources you enable, your Microsoft Sentinel incidents and data provide wider visibility into threats and their context for your organization.

## Know before you begin

If you're new to Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Microsoft Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Microsoft Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Microsoft Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Microsoft Security Copilot](/en-us/security-copilot/prompting-security-copilot)

## Security Copilot integration with Microsoft Sentinel

Use Microsoft Sentinel data with Security Copilot in both the standalone [Security Copilot portal](https://securitycopilot.microsoft.com) and the embedded experience in the Microsoft Defender portal after you onboard Microsoft Sentinel. For more information, see [Microsoft Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot#standalone-and-embedded-experiences).

## Key features

Microsoft Sentinel data integrates with Security Copilot in the Defender portal as follows:

- When you also have Microsoft Defender XDR, Copilot in Microsoft Defender XDR benefits from unified incidents integrated with Microsoft Sentinel.
- In the standalone experience, Microsoft Sentinel provides the following plugins to integrate with Security Copilot: **Microsoft Sentinel (Preview)** **Natural language to KQL for Microsoft Sentinel (Preview)**.

## Enable Security Copilot integration with Microsoft Sentinel

To maximize your Security Copilot integration with Microsoft Sentinel do the following:

- configure a default Microsoft Sentinel workspace for Security Copilot
- connect your Microsoft Sentinel workspace to Microsoft Defender XDR

### Configure a default Microsoft Sentinel workspace

Increase your prompt accuracy by configuring a Microsoft Sentinel workspace as the default.

1. Navigate to Security Copilot at https://securitycopilot.microsoft.com/.
2. Open **Sources**![](media/sentinel-security-copilot/sources.png) in the prompt bar.
3. On the **Manage plugins** page, set the toggle to **On**
4. Select the gear icon on the Microsoft Sentinel (Preview) plugin.

    ![Screenshot of the personalization selection gear icon for the Microsoft Sentinel plugin.](media/sentinel-security-copilot/sentinel-plugins.png)
5. Configure the default workspace name.

    ![Screenshot of the plugin personalization options for the Microsoft Sentinel plugin.](media/sentinel-security-copilot/configure-default-sentinel-workspace.png)

Tip

Specify the workspace in your prompt when it doesn't match the configured default.

Example: `What are the top 5 high priority Sentinel incidents in workspace "soc-sentinel-workspace"?`

### Integrate Microsoft Sentinel with Copilot in Defender

Use the Microsoft Defender portal with your Microsoft Sentinel data for an embedded Security Copilot experience. Microsoft Sentinel's unique data sources flowing into Microsoft Defender XDR unified incidents allow Copilot in Defender to maximize its capabilities.

For example:

- The SAP (Preview) solution is installed in your workspace for Microsoft Sentinel.
- The near real-time rule [**SAP - (Preview) File Downloaded From a Malicious IP Address**](sap/sap-solution-security-content#data-exfiltration) triggers an alert, creating a Microsoft Sentinel incident.
- [Microsoft Sentinel was onboarded to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).
- Microsoft Sentinel incidents are now unified with Defender XDR incidents.
- Use Copilot in Microsoft Defender for incident summary, guided responses and incident reports.

[![Screenshot of Microsoft Sentinel incident from Defender portal with Copilot embedded experience.](media/sentinel-security-copilot/sentinel-incident-copilot-in-defender-example.png)](media/sentinel-security-copilot/sentinel-incident-copilot-in-defender-example.png#lightbox)

For more information, see the following resources:

- [Integrate Microsoft Defender XDR](microsoft-365-defender-sentinel-integration)
- [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal#feature-comparison-sentinel-in-azure-vs-sentinel-in-the-defender-portal)
- [Copilot in Microsoft Defender](/en-us/defender-xdr/security-copilot-in-microsoft-365-defender)

### Integrate Microsoft Sentinel with Security Copilot in advanced hunting

The Natural language to KQL for Microsoft Sentinel (Preview) plugin generates and runs KQL hunting queries using Microsoft Sentinel data. This capability is available in the standalone experience and the advanced hunting section of the Microsoft Defender portal.

Note

In the unified Microsoft Defender portal, you can prompt Security Copilot to generate advanced hunting queries for both Defender XDR and Microsoft Sentinel tables. Not all Microsoft Sentinel tables are currently supported.

For more information, see [Security Copilot in advanced hunting](/en-us/defender-xdr/advanced-hunting-security-copilot).

## Sample Microsoft Sentinel prompts

Consider the **Microsoft Sentinel incident investigation** promptbook as a starting point for creating effective prompts. This promptbook delivers a report about a specific incident, along with related alerts, reputation scores, users, and devices.

| Guidance | Prompt |
| --- | --- |
| Nudge Copilot to provide human readable information instead of responding with object IDs. | `Show me Sentinel incidents that were closed as a false positive. Supply the Incident number, Incident Title, and the time they were created.` |
| Copilot knows who you are. Use the "me" pronoun to find incidents related to you. The following prompt targets incidents assigned to you. | `What Sentinel incidents created in the last 24 hours are assigned to me? List them with highest priority incidents at the top.` |
| When you narrow a prompt response down to a single incident, Copilot knows the context. | `Tell me about the entities associated with that incident.` |
| Copilot is good at summarizing. Describe a specific audience you want the prompts and responses summarized for. | `Write an executive report summarizing this investigation. It should be suited for a nontechnical audience.` |

For more prompt guidance and samples, see the following resources:

- [Using promptbooks](/en-us/copilot/security/using-promptbooks)
- [Prompting in Microsoft Security Copilot](/en-us/copilot/security/prompting-security-copilot)
- [Rod Trent's Security Copilot Prompt Library](https://github.com/rod-trent/Copilot-for-Security/tree/main/Prompts)

## Provide feedback

Your feedback is vital to guide the current and planned development of the product. The best way to provide this feedback is directly in the product. Select **How’s this response?** at the bottom of each completed prompt and choose any of the following options:

- **Looks right** - Select if the results are accurate, based on your assessment.
- **Needs improvement** - Select if any detail in the results is incorrect or incomplete, based on your assessment.
- **Inappropriate** - Select if the results contain questionable, ambiguous, or potentially harmful information.

For each feedback option, you can provide more information in the next dialog box that appears. Whenever possible, and especially when the result is **Needs improvement**, write a few words explaining what can be done to improve the outcome. If you entered prompts specific to Azure Firewall and the results aren't related, then include that information.

## Privacy and data security in Security Copilot

To understand how Security Copilot handles your prompts and the data that's retrieved from the service (prompt output), see [Privacy and data security in Microsoft Security Copilot](/en-us/security-copilot/privacy-data-security).