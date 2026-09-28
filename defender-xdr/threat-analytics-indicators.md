---
layout: Conceptual
title: Access indicators in threat analytics in Microsoft Defender (preview) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/threat-analytics-indicators
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Learn about the indicators section of each threat analytics report and how to get access to it
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ta
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fd2d5242-a83f-b249-1cfa-6c6f7dd0993e
document_version_independent_id: fd2d5242-a83f-b249-1cfa-6c6f7dd0993e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/threat-analytics-indicators.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-analytics-indicators
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/threat-analytics-indicators.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4fc30ab9-b1bb-3e02-753d-f4dc5c704531
---

# Access indicators in threat analytics in Microsoft Defender (preview) - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Each [threat analytics report](threat-analytics) includes an *indicators* section that lists all indicators of compromise (IOCs) associated with the threat. Microsoft researchers update these IOCs in real time as they find new evidence related to the threat. These IOCs and their real-time updates help your security operations center (SOC) and threat intelligence analysts with remediation and proactive hunting. The list also retains expired IOCs, so you can investigate past threats and understand their impact in your environment.

Because IOCs are valuable information in the context of prevalent threats and threat campaigns, only verified Microsoft Defender customers can access them. This article explains how you can check if you have access to the indicators section and how you unlock it if you don't.

## View IOCs in threat analytics

To access the indicators section, go to the **Threat analytics** page, open the report about the tracked threat, and select the **Indicators** tab.

If you're a verified customer, you can immediately see the list of IOCs displayed in the **Indicators** tab.

[![Screenshot of the Indicators tab in a threat analytics report.](/en-us/defender-xdr/media/ta-indicators/indicators-full.png)](/en-us/defender-xdr/media/ta-indicators/indicators-full.png#lightbox)

If you're not a verified customer, the **Indicators** tab displays a message that access to indicators is restricted.

[![Screenshot of a restricted Indicators tab in a threat analytics report.](media/threat-analytics-indicators/indicators-restricted.png)](media/threat-analytics-indicators/indicators-restricted.png#lightbox)

## Unlock access to indicators

To unlock the **Indicators** tab, complete these steps:

1. On the **Indicators** page, select **Complete Verification**.
2. Provide the required information and any supporting documents.
3. Select **Submit verification request**.

Verification can take an hour or more. After it completes, refresh the **Indicators** tab. If your tenant is validated, the list of IOCs appears.

Note

In some cases, we might require additional information during the verification process. We communicate these requirements through email.

If you still don't have access to the **Indicators** section after going through the verification process, contact the email address displayed on the **Indicators** page.

[![Screenshot of a restricted Indicators tab in a threat analytics report showing the email address to contact.](media/threat-analytics-indicators/indicators-contact.png)](media/threat-analytics-indicators/indicators-contact.png#lightbox)