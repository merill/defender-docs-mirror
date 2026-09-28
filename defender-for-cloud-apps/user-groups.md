---
layout: Conceptual
title: Import user groups from connected apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/user-groups
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides instructions for importing your user groups from connected apps into Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Naama-Goldbart
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: eb3dac26-ed7f-a900-cf12-a98e12001ad6
document_version_independent_id: eb3dac26-ed7f-a900-cf12-a98e12001ad6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/user-groups.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: user-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/user-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: afde4b9f-df03-47bd-b361-e1d84177fd37
---

# Import user groups from connected apps - Microsoft Defender for Cloud Apps | Microsoft Learn

When you connect apps using API connectors, Microsoft Defender for Cloud Apps enables you to import user groups, for example from Microsoft 365 and Microsoft Entra ID. There are two types of user groups:

- **Automatic groups:** Automatic groups are created by default by Microsoft Defender for Cloud Apps. For example, there's an automatic user group called **External** that combines all users from all apps who are external to your organization and have access to files or were in user activities in your tenant. The following automatic groups exist in Defender for Cloud Apps:

    - External
    - Dropbox administrator
    - Microsoft 365 administrator
    - Google Workspace administrator
    - Box administrator
    - All Salesforce standard and custom profiles, for example, Salesforce System Administrator. See the full list of [Salesforce standard profiles](https://help.salesforce.com/s/articleView?id=sf.standard_profiles.htm).
- **Imported groups:** You can import any group from your connected apps. For example, you can import user groups from Microsoft 365 (Active Directory) and other connected apps. These groups enable you to look for threats in your org, not by looking at the whole org or at a specific user, but by looking at a specific group.

    Typical scenarios that use imported user groups include:

    - Investigating which docs the HR people look at.
    - Check if there's something unusual happening in the executive group.
    - Find if someone from the admin group performed an activity outside the US.

## Import a user group from a connected app

1. In the Defender portal, select **Settings &gt; Cloud Apps &gt; System &gt; User groups &gt; + Import user group**.
2. In the **Import user group** pane, select the app from which to import the user group. The apps shown depend on which connectors you've deployed.
3. Select the group you want to import. The list includes the first 50 groups from the existing user groups in the app. If you don't see your group, enter search text in the search field above the list.

    To add a new group to the list, do so in the app itself, and then return to the Microsoft Defender portal to view your new group in the list.
4. (Optional) Select to be notified by email when the import process is complete.
5. Select **Import**.

    After the import is complete, select your group from the **User groups** page to view a list of all group members. Select any group member to drill down further for more details, including the apps used and a summary of the account activities. Imported groups can also be selected as filters when investigating in the **Activity log** and when creating policies. Group members are automatically synchronized for imported groups, just as they are for Active Directory Connect.

Note

- The maximum number of imported user groups is 500.
- Only active users will be imported as part of the imported group. Any suspended, deleted, or disabled users will be ignored.
- There may be a short delay until imported user groups are available in filters.
- Only activities performed after importing a user group will be tagged as having been performed by a member of the user group.
- After the initial sync, groups are usually updated every hour. However, due to various factors there could be times where this might take several hours.
- Usernames must contain only standard alphanumeric characters (a–z, A–Z, 0–9). Usernames with special characters such as ~ or # aren't supported.

For more information on using the User group filters, see [Activities](activity-filters).