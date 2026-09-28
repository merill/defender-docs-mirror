---
layout: Conceptual
title: Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Microsoft Defender portal.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: overview
ms.date: 2026-05-27T00:00:00.0000000Z
locale: en-us
document_id: 955a1fd6-222a-9c0a-8ac7-e63a580c05b2
document_version_independent_id: 955a1fd6-222a-9c0a-8ac7-e63a580c05b2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: b678d6a7-778c-44ea-8fa6-c024db99e753
---

# Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

Multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal provides your security operations teams with a single, unified view of all the tenants you manage. This view enables your teams to quickly investigate incidents and perform advanced hunting across data from multiple tenants, improving your security operations.

## Microsoft Sentinel support

For each tenant, the Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel. In the context of this article, a workspace is a Log Analytics workspace with Microsoft Sentinel enabled.

If you have tenants with Microsoft Sentinel workspaces onboarded to the Defender portal, you can:

- Triage incidents and alerts across Security Information and Event Management (SIEM) and eXtended Detection and Response (XDR) data.
- Proactively search for SIEM and XDR data across multiple tenants.
- Manage cases across multiple tenants.

Each workspace must be onboarded to the Defender portal for each of your tenants separately, as you would in a single-tenant scenario.

For more information, see:

- [Connect Microsoft Sentinel to Microsoft Defender XDR](/en-us/azure/sentinel/microsoft-sentinel-onboard)
- [Multitenant organizations documentation](/en-us/azure/active-directory/multi-tenant-organizations/)
- [Multiple Microsoft Sentinel workspaces in the Defender portal](/en-us/azure/sentinel/workspaces-defender-portal)

## Feature availability

Multitenant management is also available to US government customers. Refer to the following table for specific scenarios for GCC, GCC High, DoD, and Commercial customers.

| Scenario | Availability |
| --- | --- |
| Multitenant management | Available to all GCC, GCC High, DoD, and Commercial customers. |
| Cross-cloud collaboration | - Both DoD and GCC High customers can manage tenants in each other's clouds.  - GCC customers can manage tenants in the Commercial cloud. |

## Benefits of multitenant management

Some of the key benefits you get with multitenant management for Defender XDR and the Microsoft Sentinel in the Defender portal include:

- **A centralized place to manage incidents and cases across tenants**: A unified view provides SOC analysts with all the information they need to investigate incidents and cases across multiple tenants, eliminating the need to sign in and out of each one.
- **Streamlined threat hunting**: Multi-tenancy support enables SOC teams use Microsoft Defender XDR advanced hunting capabilities to create Kusto Query Language (KQL) queries that proactively hunt for threats across multiple tenants.
- **Multi-customer management for partners**: Managed Security Service Provider (MSSP) partners can now gain visibility into cases, security incidents, alerts, and threat hunting across multiple customers through a single pane of glass.

## What does multitenant management include?

The following key capabilities are available for each tenant you have access to in multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal:

| Capability | Description |
| --- | --- |
| **Incidents & alerts** &gt; **[Incidents](mto-incidents-alerts)** | Manage incidents originating from multiple tenants. |
| **Incidents & alerts** &gt; **[Alerts](mto-incidents-alerts)** | Manage alerts originating from multiple tenants. |
| **[Cases](mto-manage-cases)** | Manage cases originating from multiple tenants. |
| **Hunting** &gt; **[Advanced hunting](mto-advanced-hunting)** | Proactively hunt for intrusion attempts and breach activity across multiple tenants at the same time. |
| **Hunting** &gt; **[Custom detection rules](/en-us/defender-xdr/custom-detections-overview)** | View and manage custom detection rules across multiple tenants. |
| **Assets** &gt; **Devices** &gt; **[Tenants](mto-tenant-devices)** | For all tenants and at a tenant-specific level, explore the device counts across different values such as device type, device value, onboarding status, and risk status. |
| **Endpoints** &gt;**Vulnerability Management** &gt; **[Dashboard](mto-dashboard)** | The Microsoft Defender Vulnerability Management dashboard provides both security administrators and security operations teams with aggregated vulnerability management information across multiple tenants. |
| **Endpoints** &gt; **Vulnerability management** &gt; **[Tenants](mto-dashboard)** | For all tenants and at a tenant-specific level, explore vulnerability management information across different values such as exposed devices, security recommendations, weaknesses, and critical CVEs. |
| **Configuration** &gt; **Settings** | Lists the tenants you have access to. Use this page to view and manage your tenants. |
| **Multi-tenant management** &gt; **[Tenant groups](mto-tenant-groups)** | Organize the tenants you manage into named groups and switch the multitenant view between those groups. |

## Limitations

Mutitenant management supports multitenant single workspaces. This means that you can query multiple tenants and their primary workspace through Advanced Hunting without Lighthouse. [Azure Lighthouse](/en-us/azure/lighthouse/) is required when you want to query a secondary workspace in a different tenant (from Advanced Hunting, analytic rules, workbooks, etc.). For these queries, use the workspace() operator from either the multitenant management portal or `security.microsoft.com`.