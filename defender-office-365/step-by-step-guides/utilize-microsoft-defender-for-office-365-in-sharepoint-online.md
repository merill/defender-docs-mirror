---
layout: Conceptual
title: Use Microsoft Defender for Office 365 in SharePoint and OneDrive - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/utilize-microsoft-defender-for-office-365-in-sharepoint-online
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The steps to ensure that you can use, and get the value from, Microsoft Defender for Office 365 in SharePoint and OneDrive.
ms.service: defender-office-365
author: MSFTBen
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
document_id: f94a097b-529f-0831-f832-034f2b5e802c
document_version_independent_id: f94a097b-529f-0831-f832-034f2b5e802c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/utilize-microsoft-defender-for-office-365-in-sharepoint-online.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/utilize-microsoft-defender-for-office-365-in-sharepoint-online
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/utilize-microsoft-defender-for-office-365-in-sharepoint-online.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
platformId: 46fccbd7-0937-bb96-b2d3-093b17e8bd0b
---

# Use Microsoft Defender for Office 365 in SharePoint and OneDrive - Microsoft Defender for Office 365 | Microsoft Learn

SharePoint in Microsoft 365 is a widely used user collaboration and file storage tool. The following steps help reduce the attack surface area in SharePoint and that help keep this collaboration tool in your organization secure. However, it's important to note there's a balance to strike between security and productivity, and not all these steps might be relevant for your organizational risk profile. Take a look, test, and maintain that balance.

## Prerequisites

- Microsoft Defender for Office 365 Plan 1
- Sufficient permissions (SharePoint administrator/security administrator)
- Microsoft SharePoint (part of Microsoft 365)
- [SharePoint Online Management Shell](/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online) installed and configured
- Five to 10 minutes to perform these steps

## Turn on Microsoft Defender for Office 365 in SharePoint

If you're licensed for Microsoft Defender for Office 365 **(free 90-day evaluation available at aka.ms/trymdo)**, you can ensure seamless protection from zero day malware and time of click protection within Microsoft Teams.

To learn more, read [Step 1: Use the Microsoft Defender portal to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](../safe-attachments-for-spo-odfb-teams-configure#step-1-use-the-microsoft-defender-portal-to-turn-on-safe-attachments-for-sharepoint-onedrive-and-microsoft-teams).

1. Sign in to the [security center's safe attachments configuration page](https://security.microsoft.com/safeattachmentv2).
2. Select **Global settings**.
3. Ensure that **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** is set to **on**.
4. Select **Save**.

## Stop infected file downloads from SharePoint

By default, users can't open, move, copy, or share malicious files that are detected by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams. However, the *Download* option is still available and should be *disabled*.

To learn more, read [Step 2: (*Recommended*) Use SharePoint Online PowerShell to prevent users from downloading malicious files](../safe-attachments-for-spo-odfb-teams-configure#step-2-recommended-use-sharepoint-online-powershell-to-prevent-users-from-downloading-malicious-files).

1. Open and connect to [SharePoint Online PowerShell](/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online).
2. Run the following command: **Set-SPOTenant -DisallowInfectedFileDownload $true**.