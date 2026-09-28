---
layout: Conceptual
title: Threat trackers in Microsoft Defender for Office 365 Plan 2 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/threat-trackers
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.assetid: a097f5ca-eac0-44a4-bbce-365f35b79ed1
ms.collection:
- m365-security
- tier2
ms.custom:
- sfi-ga-nochange
description: Learn about Threat Trackers, including new Noteworthy Trackers, to help your organization stay on top of security concerns.
ms.service: defender-office-365
ms.date: 2024-03-19T00:00:00.0000000Z
locale: en-us
document_id: e53d72ea-a30d-fc3f-93e0-aaba485ad9db
document_version_independent_id: e53d72ea-a30d-fc3f-93e0-aaba485ad9db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/threat-trackers.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-trackers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/threat-trackers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9c3175cd-c86b-75a1-e0ba-620141287fc0
---

# Threat trackers in Microsoft Defender for Office 365 Plan 2 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Microsoft 365 organizations that have [Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) included in their subscription or purchased as an add-on have *Threat trackers*. Threat trackers are queries that you create and save in [Threat Explorer (also known as Explorer)](threat-explorer-real-time-detections-about). You use these queries to automatically or manually discover cybersecurity threats in your organization.

For information about creating and saving queries in Threat Explorer, see [Saved queries in Threat Explorer](threat-explorer-real-time-detections-about#saved-queries-in-threat-explorer).

## Permissions and licensing for Threat trackers

To use Threat trackers, you need to be assigned permissions. You have the following options:

- [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):
    - *Create, save, and modify Threat Explorer queries*: Membership in the **Organization Management** or **Security Administrator** role groups.
    - *Read-only access to Threat Explorer queries on the Threat tracker page*: Membership in the **Security Reader** or **Global Reader** role groups.
- [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in these roles gives users the required permissions *and*permissions for other features in Microsoft 365:
    - *Create, save, and modify Threat Explorer queries*: Membership in the **Global Administrator**^\*^ or **Security Administrator** roles.
    - *Read-only access to Threat Explorer queries on the Threat tracker page*: Membership in the **Security Reader** or **Global Reader** roles.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

To remediate messages in Threat Explorer, you need additional permissions. For more information, see [Permissions and licensing for Threat Explorer and Real-time detections](threat-explorer-real-time-detections-about#permissions-and-licensing-for-threat-explorer-and-real-time-detections).

To use Threat Explorer or Threat trackers, you need to be assigned a license for Defender for Office 365 (included in your subscription or an add-on license).

Threat Explorer and Threat trackers contain data for users with Defender for Office 365 licenses assigned to them.

## Threat trackers

The **Threat tracker** page is available in the Microsoft Defender portal at https://security.microsoft.com at **Email & collaboration** &gt; **Threat tracker**. Or, to go directly to the **Threat tracker** page, use https://security.microsoft.com/threattrackerv2.

The **Threat tracker** page contains three tabs:

- **Saved queries**: Contains all queries that you saved in Threat Explorer.
- **Tracked queries**: Contains the results of queries that you saved in Threat Explorer where you selected **Track query**. The query automatically runs periodically, and the results are shown on this tab.
- **Trending campaigns**: We populate the information on this tab to highlight new threats received in your organization.

These tabs are described in the following subsections.

### Saved queries tab

The **Save queries** tab on the **Threat tracker** page at https://security.microsoft.com/threattrackerv2 contains all of your saved queries from Threat Explorer. You can use these queries without having to re-create the search filters.

The following information is shown on the **Save queries** tab. You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Date created**
- **Name**
- **Type**
- **Author**
- **Last executed**
- **Tracked query**: This value is controlled by whether you selected **Track this query**when you created the query in Threat Explorer:
    - **No**: You need to run the query manually.
    - **Yes**: The query automatically runs periodically. The query and the results are also available on the **Tracked queries** page.
- **Actions**: Select **Explore** to open and run the query in Threat Explorer, or to update or save a modified or unmodified copy of the query in Threat Explorer.

If you select a query, the ![](media/defender-portal-icon-edit.png)**Edit** and ![](media/defender-portal-icon-delete.png)**Delete** actions that appear.

If you select ![](media/defender-portal-icon-edit.png)**Edit**, you can update the date and **Track query** settings of the existing query in the details flyout that opens.

### Tracked queries

The **Tracked queries** tab on the **Threat tracker** page at https://security.microsoft.com/threattrackerv2 contains the results of queries that you created in Threat Explorer where you selected **Track this query**. Tracked queries run automatically, giving you up-to-date information without having to remember to run the queries.

The following information is shown on the **Tracked queries** tab. You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Date created**
- **Name**
- **Today's message count**
- **Prior day message count**
- **Trend: today vs. prior week**
- **Actions**: Select **Explore** to open and run the query in Threat Explorer.

If you select a query, the ![](media/defender-portal-icon-edit.png)**Edit** action appears. If you select this action, you can update the date and **Track query** settings of the existing query in the details flyout that opens.

### Trending campaigns tab

The **Trending campaigns** tab on the **Threat tracker** page at https://security.microsoft.com/threattrackerv2 automatically highlights new email threats that were recently received by your organization.

The following information is shown on the **Trending campaigns** tab. You can sort the entries by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Malware family**
- **Prior day message count**
- **Trend: today vs. prior week**
- **Targeting: your company vs. global**
- **Actions**: Select **Explore** to open and run the query in Threat Explorer.