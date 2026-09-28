---
layout: Conceptual
title: Content distribution using distribution profiles in multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-distribution-profiles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about content distribution across tenants in the Microsoft Defender multitenant portal.
ms.service: defender-xdr
author: mberdugo
ms.author: monaberdugo
ms.reviewer: tbeerthuis
ms.collection:
- m365-security
- tier1
ms.topic: concept-article
ms.date: 2026-01-14T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e6fbdafb-f115-fe6c-941e-2f9c73c28bdd
document_version_independent_id: e6fbdafb-f115-fe6c-941e-2f9c73c28bdd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-distribution-profiles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-distribution-profiles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-distribution-profiles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c0a93189-fe8b-e93c-2dab-9aad006e9ab8
---

# Content distribution using distribution profiles in multitenant management - Microsoft Defender XDR | Microsoft Learn

Content distribution in the Microsoft Defender multitenant portal helps you organize and manage content at scale across your tenants, based on categories like business groups or locations. Create distribution profiles to copy existing content, like custom detection rules, from the source tenant to the target tenants. The distributed content then runs in the target tenant in the selected scope.

## Supported content for distribution

Create distribution profiles to distribute the following types of content across multiple tenants:

- [Custom detection rules](/en-us/azure/sentinel/compare-analytics-rules-custom-detections)
- [Endpoint security](/en-us/defender-endpoint/microsoft-defender-endpoint) policies, supported for Microsoft Defender for Endpoint customers only
- [Analytics rules](/en-us/azure/sentinel/scheduled-rules-overview?) for Microsoft Sentinel customers only
- [Automation rules](/en-us/azure/sentinel/create-manage-use-automation-rules)for Microsoft Sentinel customers only
- [Workbooks](/en-us/azure/sentinel/monitor-your-data) for Microsoft Sentinel customers only
- Parsers, Saved Searches and Functions

## Prerequisites

The following table lists the requirements for using content distribution in the Microsoft Defender multitenant portal.

| Requirement | Description |
| --- | --- |
| **Licensing requirements** | Your organization must have a subscription to Microsoft 365 E5 or Office E5. To distribute Microsoft Sentinel content, you must have a Microsoft Sentinel subscription |
| **Permissions** | Users must be assigned the correct roles and permission at the individual tenant level to view and manage the associated data in multitenant management.  Access to content distribution is granted through the Security settings (manage) or Security Data Basic (read) permission in [Microsoft Defender unified role-based access control (URBAC)](/en-us/defender-xdr/manage-rbac). By default, both of these roles are assigned to the **Security Administrator** and **Security Reader** Microsoft Entra built-in roles. |
| **Delegate access** | Delegated access via [Azure B2B](/en-us/entra/external-id/add-users-administrator) or [GDAP (CSP Parters only)](/en-us/microsoft-365/lighthouse/m365-lighthouse-setup-gdap) must be obtained for at least one other tenant. |

## Create distribution profiles

To create a new distribution profile:

1. In the Microsoft Defender multitenant portal, go to the [**Multi-tenant management &gt; Content distribution**](https://mto.security.microsoft.com/contentdistribution) page.
2. Select **Create** to open the **Create content distribution profile** wizard. In the wizard, enter the following details, selecting **Next** as needed to navigate through the tabs. Some tabs are only relevant if you selected that type of content to distribute.

    | Tab | Instructions |
    | --- | --- |
    | **Details** | Enter a name and optional description for your content distribution profile. |
    | **Assign tenants** | Select **Add tenant** to see a list of available tenants that you can add to your distribution profile, select the tenants you want to add, and then select **Add**. |
    | **Select content type** | Content types are all selected by default. Verify that the selection matches the content you want to distribute in this distribution profile. |
    | **Content type** | 1. Select **Add content**. 2. Select the relevant content that you want to add to the distribution profile, and then select **Add to distribution profile**. |

    At this point, you need to define your tenant's scope. Distribution profiles support a single scope for the entire profile, or separate scopes per content type. Scopes can be device groups, workspaces, or Microsoft Entra groups.

    Select **Single scope** or **Scope per content type** to toggle between these options, and **Edit scope** to make changes as needed.
3. In the **Summary** tab, review the details of the distribution profile you created. If you want to sync all authorized tenants now, leave the **Sync all authorized tenants** option checked. If you want to sync later, uncheck it.
4. Select **Submit** to finish your distribution profile creation.

If you chose to **Sync all authorized tenants**, all the tenants and scope within the tenants you have permission automatically syncs.

Your newly created distribution profile appears in the distribution profiles page after creation.

[![Screenshot of the Content distribution page with content distribution profiles created.](media/mto-tenantgroups/distribution-profiles.png)](media/mto-tenantgroups/distribution-profiles.png#lightbox)

Select a distribution profile from the list to add or remove content, add, edit, or remove tenants, or sync the distribution profile. Use the toolbar options at the top of the page to edit, remove, or sync distribution profiles.

If you're syncing the profiles, check the sync results under the **Last sync result** column. If the result is *partially successful* or *failed*, select the result to investigate the cause. When you select the result, a side pane containing the errors, recommendations, and impacted assets appears. For example:

[![Screenshot of sync results side pane.](media/mto-tenantgroups/mto-sync-results.png)](media/mto-tenantgroups/mto-sync-results.png#lightbox)

Note

The maximum number of published items per publish operation is 9,500. Published items are calculated as the number of tenants multiplied by the number of templates. For example, if you publish 10 distribution profiles with 10 target tenants and 95 content templates, then the published items equals to 9,500.

## Syncing content among distribution profiles

To sync content across distribution profiles for the tenants you have permission for:

1. On the **Multi-tenant management &gt; [Content distribution](https://mto.security.microsoft.com/contentdistribution)** page, select any distribution profiles you want to sync, and then select **Sync**.
2. At the prompt, select **Sync** again to confirm the sync operation. Once the sync is completed, you see one of the following statuses:

    - Success
    - Partially successful
    - Failure
3. If you experience a partial success or failure, select the value in the **Last sync result** column to investigate the cause.

Sync results show the number of synced tenants and content. Synced tenants indicate how many tenants had custom detection rules applied successfully.

For example, if all rules are applied in 3 out of 3 tenants, the count is **3**; if only 2 tenants succeed, the count is **2**. Synced content represents the total custom detection rules synced across all target tenants.

## Limitations

Automation rules that trigger a playbook can't be distributed

## Troubleshooting and error handling

The following are some common reasons a sync might fail:

- User doesn't have permission to create custom detection rules on the target tenant.
- User doesn't have permission to read custom detection rules from **content source**.
- User doesn't have permission for the target device scope.

If the issue is with the target tenant, try creating an identical custom detection rule for further diagnosis. If the issue is with accessing the source data, try accessing the custom detection.

A known issue exists with distribution profile errors. In some scenarios, such as when a user without the required permissions selects **See the assignment** on a policy error, an indefinite loading state might be shown without a clear error message. Users might also encounter generic or unclear error messages if Microsoft Entra is temporarily unavailable. In such cases, close the error message and verify your permissions and Microsoft Entra availability.