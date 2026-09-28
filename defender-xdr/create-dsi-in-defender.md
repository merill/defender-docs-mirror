---
layout: Conceptual
title: Create investigations in Data Security Investigations (preview) from the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/create-dsi-in-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create investigations in the Microsoft Defender portal with the Microsoft Purview Data Security Investigations (preview) integration.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 8fb101ac-5170-2846-340f-65d76a8ca4af
document_version_independent_id: 8fb101ac-5170-2846-340f-65d76a8ca4af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/create-dsi-in-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-dsi-in-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/create-dsi-in-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 74070ccb-44ce-64cf-edef-4a3561f2b487
---

# Create investigations in Data Security Investigations (preview) from the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

You can now start an investigation on data security incidents from the Microsoft Defender portal with the integration of [Microsoft Purview Data Security Investigations (preview)](/en-us/purview/data-security-investigations) and Microsoft Defender XDR.

Security operations center (SOC) teams can take advantage of the integration between Microsoft Purview Data Security Investigations (preview) and Microsoft Defender XDR to enhance their investigation and response to potential data security incidents like data breaches or data leaks. Data Security Investigations (preview) uses generative AI to analyze impacted data, draws connections to identify risks, and provide actionable insights to protect your organization.

SOC teams can start an investigation in Data Security Investigations (preview) from an incident page where a potentially affected data set is in the Microsoft Defender portal.

## Prerequisites

To create investigations in Data Security Investigations (preview) in the Microsoft Defender portal, you must have the following permissions:

- Security Administrator
- Security Operator

To view and access the investigation in Data Security Investigations (preview) in the Microsoft Purview portal, the *Data Security Investigations Administrator*[Data Security Investigations permissions](/en-us/purview/data-security-investigations-permissions) role is required.

## Create a data security investigation

Microsoft Defender XDR identifies possibly impacted sensitive data in incidents. You can start creating an investigation in Data Security Investigations (preview) from the incident page in the Microsoft Defender portal. Investigations support mailboxes, files, and mail messages as the scope of the investigation.

To create an investigation in Data Security Investigations (preview) in the Microsoft Defender portal, follow these steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. In the navigation pane, select **Investigation & response** &gt; **Incidents & alerts** &gt; **Incidents** to open the incident queue. Select an incident from the queue to open the incident page.
3. When the selected incident contains potentially impacted data, the option to create a Data Security investigation appears on the incident page message banner. Choose **Investigate this incident**. [![Screenshot of the incident page highlighting the create investigation message banner](media/create-dsi-in-defender/xdr-dsi-banner-small.png)](media/create-dsi-in-defender/xdr-dsi-banner.png#lightbox)
4. In the pop-up window, provide a name and description for the investigation. Investigation names must be unique. [![Screenshot of the Data Security investigations pop-up window](media/create-dsi-in-defender/xdr-dsi-popup-small.png)](media/create-dsi-in-defender/xdr-dsi-popup.png#lightbox)
5. In the Investigation scope, attach mailboxes or files and mail messages to the investigation. 
    Note

    You can attach either mailboxes or files and mail messages in an investigation, but not both at the same time. If an incident involves both mailboxes and files or mail messages, you need to create separate investigations. For example, create one investigation for all mailboxes and another for all files and mail messages. Files and mail messages can be attached in one investigation.
6. Select **Create investigation** to finish creating the data security investigation.

Once the investigation in Data Security Investigations (preview) is created, a link to the Microsoft Purview portal appears on the message banner in the incident page. Here’s an example.

[![Screenshot highlighting the link to Microsoft Purview portal after successful creation](media/create-dsi-in-defender/xdr-dsi-success-link-small.png)](media/create-dsi-in-defender/xdr-dsi-success-link.png#lightbox)

You can also create an investigation in Data Security Investigations (preview) from the incident page in the following ways:

- From the **Incidents** page, select the **More actions** ellipsis to see the options, then choose **Investigate data security with AI**.

    [![Screenshot highlighting the Create Data Security investigation option from the more actions ellipsis](media/create-dsi-in-defender/xdr-dsi-create-action-small.png)](media/create-dsi-in-defender/xdr-dsi-create-action.png#lightbox)
- When you select an entity like an email in the incident graph, choose **Investigate data security with AI** from the entity context menu.

    [![Screenshot highlighting the Create Data Security investigation option from an entity in the incident graph](media/create-dsi-in-defender/xdr-dsi-create-entity-small.png)](media/create-dsi-in-defender/xdr-dsi-create-entity.png#lightbox)

Each investigation in Data Security Investigations (preview) created is recorded in the Microsoft Defender portal activity log. The activity log entry also includes the relevant link to the investigation created in the Microsoft Purview portal.

[![Screenshot highlighting the link to Microsoft Purview portal in the activity log](media/create-dsi-in-defender/xdr-dsi-activity-log-small.png)](media/create-dsi-in-defender/xdr-dsi-activity-log.png#lightbox)