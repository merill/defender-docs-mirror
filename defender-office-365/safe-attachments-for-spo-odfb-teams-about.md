---
layout: Conceptual
title: Safe Attachments for SharePoint, OneDrive, and Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/safe-attachments-for-spo-odfb-teams-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: concept-article
ms.localizationpriority: medium
ms.assetid: 26261670-db33-4c53-b125-af0662c34607
ms.collection:
- m365-security
- SPO_Content
- tier2
ms.custom:
- seo-marvel-apr2020
- seo-marvel-jun2020
- sfi-image-nochange
description: Learn about Microsoft Defender for Office 365 for files in SharePoint, OneDrive, and Microsoft Teams.
ms.service: defender-office-365
ms.date: 2026-04-09T00:00:00.0000000Z
locale: en-us
document_id: c579009a-63b5-510c-dd63-b57763e219c0
document_version_independent_id: c579009a-63b5-510c-dd63-b57763e219c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/safe-attachments-for-spo-odfb-teams-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: safe-attachments-for-spo-odfb-teams-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/safe-attachments-for-spo-odfb-teams-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
platformId: 27ba4dda-1770-a409-a52e-70d5d4e02bce
---

# Safe Attachments for SharePoint, OneDrive, and Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft Defender for Office 365, Safe Attachments for SharePoint, OneDrive, and Microsoft Teams provides an extra layer of protection against harmful files. After the [common virus detection engine in Microsoft 365](anti-malware-protection-for-spo-odfb-teams-about) scans the files, Safe Attachments opens files in a virtual environment to see what happens (a process known as *detonation*). As part of detonation, any password protected files are checked against a list of known passwords or patterns that are typically used by malicious actors. Safe Attachments for SharePoint, OneDrive, and Microsoft Teams also helps detect and block existing files that are identified as malicious in team sites and document libraries.

Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is enabled by default. To turn it on or off, see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure).

## How Safe Attachments for SharePoint, OneDrive, and Microsoft Teams works

When Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is enabled and identifies a file as malicious, the file is locked using direct integration with the file stores. The following image shows an example of a malicious file detected in a library.

[![Screenshot of files in OneDrive with one file detected as malicious.](media/2bba71cc-7ad1-4799-8b9d-d56f923db3a7.png)](media/2bba71cc-7ad1-4799-8b9d-d56f923db3a7.png#lightbox)

Note

The visual indicator is shown where the file is stored. For example, if the file is shared in Microsoft Teams, the blocked file indicator is shown in the corresponding SharePoint document library or OneDrive location.

Although the blocked file is still listed in the document library and in web, mobile, or desktop applications, people can't open, copy, move, or share the file. But, they can delete the blocked file.

Here's an example of what a blocked file looks like on a mobile device:

[![Screenshot of the option to delete a blocked file from OneDrive in the OneDrive mobile app.](media/cb1c1705-fd0a-45b8-9a26-c22503011d54.png)](media/cb1c1705-fd0a-45b8-9a26-c22503011d54.png#lightbox)

By default, people can download a blocked file. Here's what downloading a blocked file looks like on a mobile device:

[![Screenshot of the option to download a blocked file in OneDrive.](media/be288a82-bdd8-4371-93d8-1783db3b61bc.png)](media/be288a82-bdd8-4371-93d8-1783db3b61bc.png#lightbox)

SharePoint admins can prevent people from downloading malicious files. For instructions, see [Use SharePoint Online PowerShell to prevent users from downloading malicious files](safe-attachments-for-spo-odfb-teams-configure#step-2-recommended-use-sharepoint-online-powershell-to-prevent-users-from-downloading-malicious-files).

To learn more about the user experience when a file is identified as malicious, see [What to do when a malicious file is found in SharePoint, OneDrive, or Microsoft Teams](https://support.microsoft.com/office/01e902ad-a903-4e0f-b093-1e1ac0c37ad2).

## View information about malicious files detected by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams

Files identified as malicious by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams appear in [reports for Microsoft Defender for Office 365](reports-defender-for-office-365) and in [Explorer (and real-time detections)](threat-explorer-real-time-detections-about).

When a file is identified as malicious by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams, the file is also available in quarantine, but only to admins. For more information, see [Manage quarantined files in Defender for Office 365](quarantine-admin-manage-messages-files#use-the-microsoft-defender-portal-to-manage-quarantined-files-in-defender-for-office-365).

## Keep these points in mind

- Defender for Office 365 doesn't scan every single file in SharePoint, OneDrive, or Microsoft Teams. This behavior is by design. Files are scanned asynchronously. The process uses sharing and guest activity events along with smart heuristics and threat signals to identify malicious files.
- Make sure your SharePoint sites are configured to use the [Modern experience](/en-us/sharepoint/guide-to-sharepoint-modern-experience). Visual indicators that a file is blocked are available only in the Modern experience.
- Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is part of your organization's overall threat protection strategy. Other features include the default anti-spam and anti-malware protections in all organizations with cloud mailboxes, and Safe Links and Safe Attachments protection in Microsoft Defender for Office 365.