---
layout: Conceptual
title: Connect Microsoft Sentinel to the Microsoft Defender portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/microsoft-sentinel-onboard
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
description: Learn how to connect your Microsoft Sentinel environment to the Defender portal to unify your security operations.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- zerotrust-solution
- msftsolution-secops
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-09-10T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1028
locale: en-us
document_id: bd1a41d5-7c1d-87f3-083d-88ee48d3bab7
document_version_independent_id: 6ecdfc9b-1f58-5035-cd8f-25918a0264ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/microsoft-sentinel-onboard.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/microsoft-sentinel-onboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/microsoft-sentinel-onboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 2558029e-dac3-0cec-4ab6-f5ee14a44de3
---

# Connect Microsoft Sentinel to the Microsoft Defender portal | Microsoft Learn

Microsoft Sentinel is available in the Microsoft Defender portal. You don't need Microsoft Defender XDR or an E5 license. When you use Microsoft Sentinel with Defender XDR in the Defender portal, you get shared incident management and advanced hunting. You can reduce tool switching and run faster, more focused investigations.

This article walks you through connecting a Microsoft Sentinel workspace to the Defender portal, including prerequisites, onboarding steps, and available features. Follow these steps if your workspaces aren't yet connected to the Defender portal. In many cases, customers onboarding to Microsoft Sentinel after **July 1, 2025** are automatically onboarded to the Defender portal.

For more information, see:

- [What are unified security operations?](/en-us/defender-xdr/isoc-overview)
- [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690)
- [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration)

## Prerequisites

Before you begin, review the following feature documentation to understand the product changes and limitations.

- [Microsoft Sentinel in the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-defender-portal)
- [Advanced hunting in the Microsoft Defender portal](/en-us/defender-xdr/advanced-hunting-microsoft-defender)
- [Alerts, incidents, and correlation in Microsoft Defender XDR](/en-us/defender-xdr/alerts-incidents-correlation)
- [Microsoft Sentinel automation in the Defender portal](/en-us/azure/sentinel/automation#automation-with-the-unified-security-operations-platform)

The Microsoft Defender portal supports a single Microsoft Entra tenant and the connection to a primary workspace and multiple secondary workspaces. If you have only one workspace when you onboard Microsoft Sentinel, that workspace is designated as the primary workspace. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579). In the context of this article, a workspace is a Log Analytics workspace with Microsoft Sentinel enabled.

### Microsoft Sentinel prerequisites

To onboard and use Microsoft Sentinel in the Defender portal for a single workspace, you need the following resources and access:

- A Log Analytics workspace that has Microsoft Sentinel enabled
- An Azure account with the appropriate roles to onboard, use, and create support requests for Microsoft Sentinel in the Defender portal. You won't see workspaces in the Defender portal to onboard where you don't have the required permissions.

The following table shows some of the key roles needed for a single workspace setup. For permissions related to multiple workspaces, see [Permissions to manage workspaces and view workspace data](/en-us/azure/sentinel/workspaces-defender-portal#permissions-to-manage-workspaces-and-view-workspace-data).

For onboarding, the [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role assignment must be unconditional at the subscription scope.

![Screenshot of Azure Add role assignment conditions showing Owner set to Allow user to assign all roles (highly privileged).](media/microsoft-sentinel-onboard/owner-unconditional-role-assignment.png)

| Task | Microsoft Entra or Azure built-in role required | Scope |
| --- | --- | --- |
| **Onboard Microsoft Sentinel to the Defender portal**^1^ | At least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) (unconditional role assignment) OR [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Tenant- Subscription for Owner role |
| **View Microsoft Sentinel in the Defender portal** | [Microsoft Sentinel Reader](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) | Subscription, resource group, or workspace resource |
| **Query Microsoft Sentinel data tables or view incidents** | [Microsoft Sentinel Reader](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader) or a role with the following actions:- Microsoft.OperationalInsights/workspaces/read- Microsoft.OperationalInsights/workspaces/query/read- Microsoft.SecurityInsights/Incidents/read- Microsoft.SecurityInsights/incidents/comments/read- Microsoft.SecurityInsights/incidents/relations/read- Microsoft.SecurityInsights/incidents/tasks/read | Subscription, resource group, or workspace resource |
| **Take investigative actions on incidents** | [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) or a role with the following actions:- Microsoft.OperationalInsights/workspaces/read- Microsoft.OperationalInsights/workspaces/query/read- Microsoft.SecurityInsights/incidents/read- Microsoft.SecurityInsights/incidents/write- Microsoft.SecurityInsights/incidents/comments/read- Microsoft.SecurityInsights/incidents/comments/write- Microsoft.SecurityInsights/incidents/relations/read- Microsoft.SecurityInsights/incidents/relations/write- Microsoft.SecurityInsights/incidents/tasks/read- Microsoft.SecurityInsights/incidents/tasks/write | Subscription, resource group, or workspace resource |
| **Create a support request** | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) or [Support request contributor](/en-us/azure/role-based-access-control/built-in-roles#support-request-contributor) or a custom role with Microsoft.Support/\* | Subscription |

^1^ If your tenant has exactly one workspace with Microsoft Sentinel enabled, use the permissions listed in the table. If your tenant has [more than one workspace with Microsoft Sentinel enabled](/en-us/azure/sentinel/workspaces-defender-portal#permissions-to-manage-workspaces-and-view-workspace-data), you must also be at least a [Security administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID.

If you're working with multiple tenants, note that [granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction) with [Azure Lighthouse](/en-us/azure/sentinel/multiple-tenants-service-providers) isn't supported for Microsoft Sentinel data in the Defender portal. Instead, use [Microsoft Entra B2B authentication](/en-us/entra/external-id/what-is-b2b). For more information, see [Set up Microsoft Defender multitenant management](/en-us/defender-xdr/mto-requirements#review-the-requirements).

After you connect Microsoft Sentinel to the Defender portal, your existing Azure role-based access control (RBAC) permissions allow you to work with the Microsoft Sentinel features that you have access to. Continue to manage roles and permissions for your Microsoft Sentinel users from the Azure portal, as any Azure RBAC changes are reflected in the Defender portal.

For more information, see [Roles and permissions in Microsoft Sentinel](/en-us/azure/sentinel/roles) and [Manage access to Microsoft Sentinel data by resource](/en-us/azure/sentinel/resource-context-rbac).

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization.

### Unified security operations prerequisites

To unify Microsoft Defender XDR and Microsoft Sentinel security operations in the Defender portal, you must have the following resources and access:

- Licensing for Defender XDR, as described in [Microsoft Defender XDR prerequisites](/en-us/microsoft-365/security/mtp/prerequisites)
- Account for Defender XDR is a member of the same Microsoft Entra tenant with which Microsoft Sentinel is associated
- Access to Microsoft Defender XDR in the Defender portal, as described in [Microsoft Defender XDR prerequisites](/en-us/microsoft-365/security/mtp/prerequisites#required-permissions)

If applicable, complete these service-specific prerequisites for unified security operations:

| Service | Prerequisite |
| --- | --- |
| **Microsoft Purview Insider Risk Management** | If your organization uses Microsoft Purview Insider Risk Management, integrate that data by enabling the data connector **Microsoft 365 Insider Risk Management** on your primary workspace for Microsoft Sentinel. Disable that connector on any secondary workspaces for Microsoft Sentinel that you plan to onboard to the Defender portal. - Install the **Microsoft Purview Insider Risk Management** solution from the **Content hub** on the primary workspace.- Configure the data connector. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](/en-us/azure/sentinel/sentinel-solutions-deploy). |
| **Microsoft Defender for Cloud** | To stream Defender for Cloud incidents that are correlated across all subscriptions of the tenant to the primary workspace for Microsoft Sentinel: - Connect the **Tenant-based Microsoft Defender for Cloud (Preview)** data connector in the primary workspace. - Disconnect the **Subscription-based Microsoft Defender for Cloud (Legacy)** alerts connector from all workspaces in the tenant. If you don't want to stream correlated tenant data for Defender for Cloud to the primary workspace, continue to use the **Subscription-based Microsoft Defender for Cloud (Legacy)** connector on your workspaces. For more information, see [Ingest Microsoft Defender for Cloud incidents with Microsoft Defender XDR integration](/en-us/azure/sentinel/ingest-defender-for-cloud-incidents). |

## Onboard Microsoft Sentinel

This procedure describes how to onboard a Microsoft Sentinel-enabled workspace to the Defender portal.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com/) and sign in.
2. Select **System** &gt; **Settings** &gt; **Microsoft Sentinel** &gt; **Connect a workspace**.
3. Select the workspaces you want to connect and select **Next**.
4. Select the **Primary workspace**.
5. Read and understand the product changes associated with connecting your workspace.
6. Select **Connect**.

After your workspace is connected, the banner on the **Home** page shows that your environment is ready. The **Home** page is updated with new sections that include metrics from Microsoft Sentinel, like the number of data connectors and automation rules.

## Explore Microsoft Sentinel features in the Defender portal

After you connect your workspace, **Microsoft Sentinel** appears in the left-side navigation pane. If Defender XDR is enabled, pages like **Home**, **Incidents**, and **Advanced Hunting** show combined data from Microsoft Sentinel and Defender XDR. Without Defender XDR, those pages show only Microsoft Sentinel data. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

Many Microsoft Sentinel features are built into the Defender portal. For the integrated features listed in the following table, the experience is similar to the Azure portal. Use the articles in the following table to get started. When you use the linked articles, start from the [Defender portal](https://security.microsoft.com/) instead of the Azure portal.

| Feature category | Links |
| --- | --- |
| **Search** | - [Search across long time spans in large datasets](/en-us/azure/sentinel/search-jobs?tabs=defender-portal)- [Restore archived logs from search](/en-us/azure/sentinel/restore) |
| **Threat management** | - [Visualize and monitor your data by using workbooks](/en-us/azure/sentinel/monitor-your-data?tabs=defender-portal)- [Conduct end-to-end threat hunting with Hunts](/en-us/azure/sentinel/hunts)- [Use hunting bookmarks for data investigations](/en-us/azure/sentinel/bookmarks)- [Use hunting Livestream in Microsoft Sentinel to detect threat](/en-us/azure/sentinel/livestream)- [Hunt for security threats with Jupyter notebooks](/en-us/azure/sentinel/notebooks-hunt)- [Add indicators in bulk to Microsoft Sentinel threat intelligence from a CSV or JSON file](/en-us/azure/sentinel/indicators-bulk-file-import?tabs=defender-portal)- [Work with threat indicators in Microsoft Sentinel](/en-us/azure/sentinel/work-with-threat-indicators?tabs=defender-portal)- [Understand security coverage by the MITRE ATT&CK framework](/en-us/azure/sentinel/mitre-coverage) |
| **Content management** | - [Discover and manage Microsoft Sentinel out-of-the-box content](/en-us/azure/sentinel/sentinel-solutions-deploy?tabs=defender-portal)- [Microsoft Sentinel content hub catalog](/en-us/azure/sentinel/sentinel-solutions-catalog)- [Deploy custom content from your repository](/en-us/azure/sentinel/ci-cd) |
| **Configuration** | - [Find your Microsoft Sentinel data connector](/en-us/azure/sentinel/data-connectors-reference)- [Create custom analytics rules to detect threats](/en-us/azure/sentinel/create-analytics-rules?tabs=defender-portal)- [Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel](/en-us/azure/sentinel/create-nrt-rules?tabs=defender-portal)- [Create watchlists](/en-us/azure/sentinel/watchlists-create?tabs=defender-portal)- [Manage watchlists in Microsoft Sentinel](/en-us/azure/sentinel/watchlists-manage)- [Create automation rules](/en-us/azure/sentinel/create-manage-use-automation-rules)- [Create and customize Microsoft Sentinel playbooks from content templates](/en-us/azure/sentinel/use-playbook-templates)- [Generate playbooks by using AI](/en-us/azure/sentinel/automation/generate-playbook) |

After onboarding, [alert promotion (preview)](/en-us/defender-xdr/investigate-alerts#alert-promotion-preview) automatically creates Microsoft Defender XDR alerts from supported third-party alerts ingested into your workspace. Review the supported sources and guidance for managing unwanted or duplicate alerts.

Find Microsoft Sentinel settings in the Defender portal under **System** &gt; **Settings** &gt; **Microsoft Sentinel**.

## Change the primary workspace

You can only have one primary workspace connected to the Defender portal at a time. But you can change the primary workspace.

1. In the [Defender portal](https://security.microsoft.com/), go to **System** &gt; **Settings** &gt; **Microsoft Sentinel** &gt; **Workspaces**.
2. Select the name of the workspace that you want to make primary.
3. Select **Set as primary**.
4. Read and understand the product changes associated with changing the primary workspace.
5. Select **Confirm and proceed**.

When you switch the primary workspace for Microsoft Sentinel, the Defender XDR connector is connected to the new primary and disconnected from the former one automatically. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579).

## Offboard Microsoft Sentinel

Warning

If your workspace has the [Microsoft Defender XDR connector](/en-us/azure/sentinel/connect-microsoft-365-defender) configured, offboarding the workspace from the Defender portal also disconnects the Microsoft Defender XDR connector. Make sure to reconnect the Microsoft Defender XDR connector if you want to receive Defender XDR incidents in Microsoft Sentinel again.

To offboard a workspace from the Defender portal, disconnect the workspace from the settings for Microsoft Sentinel.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com/) and sign in.
2. In the Defender portal, under **System**, select **Settings** &gt; **Microsoft Sentinel**.
3. On the **Workspaces** page, select the connected workspace and **Disconnect workspace**.
4. Provide a reason why you're disconnecting the workspace.
5. Confirm your selection.

    When your workspace is disconnected, the **Microsoft Sentinel** section is removed from the left-hand side navigation of the Defender portal. Data from Microsoft Sentinel is no longer included on the **Home** page.

If you want to connect a different workspace, on the **Workspaces** page, select **Connect a workspace**, and then choose the workspace you want to connect.