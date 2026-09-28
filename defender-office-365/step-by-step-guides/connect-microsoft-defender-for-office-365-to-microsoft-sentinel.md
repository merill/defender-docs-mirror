---
layout: Conceptual
title: Connect Microsoft Defender for Office 365 to Microsoft Sentinel - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/connect-microsoft-defender-for-office-365-to-microsoft-sentinel
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to connect Microsoft Defender for Office 365 data to Microsoft Sentinel. Ingest incidents, alerts, and other Defender XDR data for unified investigation and advanced hunting.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: ed2863c2-5a3f-25ad-529c-eac2e48ac2c4
document_version_independent_id: ed2863c2-5a3f-25ad-529c-eac2e48ac2c4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/connect-microsoft-defender-for-office-365-to-microsoft-sentinel.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/connect-microsoft-defender-for-office-365-to-microsoft-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/connect-microsoft-defender-for-office-365-to-microsoft-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 753408e0-8fa1-7966-81c5-f9504daeea2c
---

# Connect Microsoft Defender for Office 365 to Microsoft Sentinel - Microsoft Defender for Office 365 | Microsoft Learn

This article walks you through connecting Microsoft Defender for Office 365 to Microsoft Sentinel by using the Microsoft Defender XDR data connector. This includes incidents and data from the rest of the Microsoft Defender suite.

This integration provides security information and event management (SIEM) features with data from other Microsoft 365 sources. You can also sync incidents and alerts, and run advanced hunting queries.

## Prerequisites

Before you begin, make sure you have the following items:

- Microsoft Defender for Office 365 Plan 2 or higher. (Included in E5 plans)
- Microsoft Sentinel [Quickstart guide](/en-us/azure/sentinel/quickstart-onboard).
- Sufficient permissions (Security Administrator in Microsoft 365 & Read / Write permissions in Sentinel).

## Add the Microsoft Defender XDR Connector

Microsoft Defender for Office 365 data is onboarded to Microsoft Sentinel through the Microsoft Defender XDR connector. Follow these steps to add and configure the connector:

1. [Sign in to the Azure portal](https://portal.azure.com) and go to **Microsoft Sentinel**. Pick the workspace to use with Microsoft Defender XDR.
2. Under **Configuration**, select **Data connectors**.
3. Search for **Microsoft Defender XDR** and select the connector.
4. Select **Open Connector Page**.
5. Under **Configuration**, select **Connect incidents & alerts**. Keep **Turn off all Microsoft incident creation rules for these products** selected.
6. In the **Connect events** section, under **Microsoft Defender for Office 365**, select **EmailEvents**, **EmailUrlInfo**, **EmailAttachmentInfo**, and **EmailPostDeliveryEvents**, then select **Apply Changes**. You can also choose tables from other Defender products during this step.