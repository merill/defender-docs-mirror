---
layout: Conceptual
title: Manage multiple Microsoft Sentinel workspaces with workspace manager | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/workspace-manager
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
description: Learn how to centrally manage multiple Microsoft Sentinel workspaces within one or more Azure tenants with workspace manager. This article takes you through provisioning and usage of Workspace Manager to help you gain operational efficiency and operate at scale.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.custom: template-how-to, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bad9bafa-f4f4-3465-c292-f6a6df00fb94
document_version_independent_id: 48139fc6-9e64-b85a-73a5-b6f9bcde9ebe
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/workspace-manager.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/workspace-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/workspace-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c5c1c4db-a0d0-7dd1-588c-1db84242572f
---

# Manage multiple Microsoft Sentinel workspaces with workspace manager | Microsoft Learn

Learn how to centrally manage multiple Microsoft Sentinel workspaces within one or more Azure tenants with workspace manager. This article takes you through provisioning and usage of workspace manager. Whether you're a global enterprise or a Managed Security Services Provider (MSSP), workspace manager helps you operate at scale efficiently.

Here are the active content types supported with workspace manager:

- Analytics rules
- Automation rules (excluding Playbooks)
- Parsers, Saved Searches and Functions
- Hunting queries
- Workbooks

Important

Support for workspace manager is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

If you onboard Microsoft Sentinel to the Microsoft Defender portal, see [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).

## Prerequisites

- You need at least two Microsoft Sentinel workspaces. One workspace to manage from and at least one other workspace to be managed.
- The [Microsoft Sentinel Contributor role assignment](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) is required on the central workspace (where workspace manager is enabled on), and on the member workspace(s) the contributor needs to manage. To learn more about roles in Microsoft Sentinel, see [Roles and permissions in Microsoft Sentinel](roles).
- Enable Azure Lighthouse if you're managing workspaces across multiple Microsoft Entra tenants. To learn more, see [Manage Microsoft Sentinel workspaces at scale](/en-us/azure/lighthouse/how-to/manage-sentinel-workspaces).

## Workspace manager considerations

Configure a central workspace to be the environment where you consolidate content items and configurations to be published at scale to member workspaces. Create a new Microsoft Sentinel workspace or utilize an existing one to serve as the central workspace.

Depending on your scenario, consider these architectures:

- **Direct-link** is the least complex setup. Control all member workspaces with only one central workspace.
- **Co-Management** supports scenarios where more than one central workspace needs to manage a member workspace. For example, workspaces simultaneously managed by an in-house SOC team and an MSSP.
- **N-Tier** supports complex scenarios where a central workspace controls another central workspace. For example, a conglomerate that manages multiple subsidiaries, where each subsidiary also manages multiple workspaces.

![A diagram showing various architecture choices for workspace manager in Microsoft Sentinel.](media/workspace-manager/architectures.png)

## Enable workspace manager on the central workspace

Enable the central workspace once you have decided which Microsoft Sentinel workspace should be the workspace manager.

1. Navigate to the **Settings** blade in the parent workspace, and toggle **On** the workspace manager configuration setting to "Make this workspace a parent".
2. Once enabled, a new menu **Workspace manager (preview)** appears under **Configuration**.

    ![Screenshot shows the workspace manager configuration settings. The menu item added for workspace manager is highlighted and the toggle button on.](media/workspace-manager/enable-workspace-manager-on.png)

## Onboard member workspaces

Member workspaces are the set of workspaces managed by workspace manager. Onboard some or all of the workspaces in the tenant, and across multiple tenants as well (if Azure Lighthouse is enabled).

1. Navigate to workspace manager and select "Add workspaces" [![Screenshot shows the add workspace menu.](media/workspace-manager/add-workspace.png)](media/workspace-manager/add-workspace.png#lightbox)
2. Select the member workspace(s) you would like to onboard to workspace manager. ![Screenshot shows the add workspace selection menu.](media/workspace-manager/add-workspace-select.png)
3. Once successfully onboarded, the **Members** count increases and your member workspaces are reflected in the **Workspaces** tab. ![Screenshot shows the added workspaces and the Members count incremented to 2.](media/workspace-manager/add-workspace-selected.png)

## Create a workspace manager group

Workspace manager groups allow you to organize workspaces together based on business groups, verticals, geography, etc. Use groups to pair content items relevant to the workspaces.

Tip

Make sure you have at least one active content item deployed in the central workspace. Having at least one active content item deployed allows you to select content items from the central workspace to be published in the member workspace(s) in the subsequent steps.

1. To create a group:

    - To add one workspace, select **Add** &gt; **Group**.
    - To add multiple workspaces, select the workspaces and **Add** &gt; **Group from selected**. ![Screenshot shows the add group menu.](media/workspace-manager/add-group.png)
2. On the **Create or update group** page, enter a **Name** and **Description** for the group. ![Screenshot shows the group create or update configuration page.](media/workspace-manager/add-group-name.png)
3. In the **Select workspaces** tab, select **Add** and select the member workspaces that you would like to add to the group.
4. In the **Select content** tab, you have 2 ways to add content items.

    - Method 1: Select the **Add** menu and choose **All content**. All active content currently deployed in the central workspace is added. This list is a point-in-time snapshot that selects only active content, not templates.
    - Method 2: Select the **Add** menu and choose **Content**. A **Select content** window opens to custom select the content added. ![Screenshot shows the group content selection.](media/workspace-manager/add-group-content.png)
5. Filter the content as needed before you **Review + create**.
6. Once created, the **Group count** increases and your groups are reflected in the **Groups tab**.

## Publish the group definition

After you create the group, the selected content items haven't been published to the member workspace(s) yet.

Note

The publish action will fail if the maximum publish operations are exceeded. Consider splitting up member workspaces into additional groups if you approach this limit.

1. Select the group &gt; **Publish content**.

    ![Screenshot shows the group publish window.](media/workspace-manager/publish-group.png)

    To bulk publish, multi-select the desired groups and select **Publish**. ![Screenshot shows the multi-select group publishing window.](media/workspace-manager/publish-groups.png)
2. The **Last publish status** column updates to reflect **In progress**. ![Screenshot shows the multi group publishing progress column.](media/workspace-manager/publish-groups-in-progress.png)
3. If successful, the **Last publish status** updates to reflect **Succeeded**. The selected content items now exist in the member workspaces. ![Screenshot shows the last published column with entries that succeeded.](media/workspace-manager/publish-groups-success.png)

    If just one content item fails to publish for the entire group, the **Last publish status** updates to reflect **Failed**.

### Troubleshooting

Each publish attempt has a link to help with troubleshooting if content items fail to publish.

1. Select the **Failed** hyperlink to open the job failure details window. A status for each content item and target workspace pair is displayed.
2. Filter the **Status** for failed item pairs.

    [![Screenshot shows the job details of a group publishing failure event.](media/workspace-manager/publish-groups-job-details-failure.png)](media/workspace-manager/publish-groups-job-details-failure.png#lightbox)

Common reasons for failure include:

- Content items referenced in the group definition no longer exist at the time of publish (have been deleted).
- Permissions have changed at the time of publish. For example, the user is no longer a Microsoft Sentinel Contributor or doesn't have sufficient permissions on the member workspace anymore.
- A member workspace has been deleted.

### Known limitations

Be aware of the following limitations when using workspace manager:

- The maximum published operations per group is 2000. *Published operations* = (*member workspaces*) \* (*content items*).For example, if you have 10 member workspaces in a group and you publish 20 content items in that group,*published operations* = *10* \* *20* = *200*.
- Playbooks attributed or attached to analytics and automation rules aren't currently supported.
- Workbooks stored in bring-your-own-storage aren't currently supported.
- Workspace manager only manages content items published from the central workspace. It doesn't manage content created locally from member workspace(s).
- Currently, deleting content residing in member workspace(s) centrally via workspace manager isn't supported.

### Workspace manager API reference

- [Workspace Manager Assignment Jobs](/en-us/rest/api/securityinsights/workspace-manager-assignment-jobs)
- [Workspace Manager Assignments](/en-us/rest/api/securityinsights/workspace-manager-assignments)
- [Workspace Manager Configurations](/en-us/rest/api/securityinsights/workspace-manager-configurations)
- [Workspace Manager Groups](/en-us/rest/api/securityinsights/workspace-manager-groups)
- [Workspace Manager Members](/en-us/rest/api/securityinsights/workspace-manager-members)