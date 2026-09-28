---
layout: Conceptual
title: Send Microsoft Entra ID data to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-azure-active-directory
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
description: Learn how to collect data from Microsoft Entra ID, and stream Microsoft Entra sign-in, audit, and provisioning logs into Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 062ea8ca-23c4-2c7b-09a8-16ae8a0db208
document_version_independent_id: f17ad5ac-8789-7123-943a-2a0b3d47c3d5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-azure-active-directory.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-azure-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-azure-active-directory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 05dff669-f03d-fb31-c1fe-b018fc790438
---

# Send Microsoft Entra ID data to Microsoft Sentinel | Microsoft Learn

[Microsoft Entra ID](/en-us/entra/fundamentals/what-is-entra) logs provide comprehensive information about users, applications, and networks accessing your Microsoft Entra tenant. This article explains the types of logs you can collect using the Microsoft Entra ID data connector, how to enable the connector to send data to Microsoft Sentinel, and how to find your data in Microsoft Sentinel.

## Prerequisites

- A Microsoft Entra Workload ID Premium license is required to stream **[AADRiskyServicePrincipals](/en-us/azure/azure-monitor/reference/tables/aadriskyserviceprincipals)** and **[AADServicePrincipalRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadserviceprincipalriskevents)** logs to Microsoft Sentinel.
- A Microsoft Entra ID P1 or P2 license is required to ingest sign-in logs into Microsoft Sentinel. Any Microsoft Entra ID license (Free/O365/P1 or P2) is sufficient to ingest the other log types. Other per-gigabyte charges might apply for Azure Monitor (Log Analytics) and Microsoft Sentinel.
- Your user must be assigned the [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) role on the workspace.
- Your user must have the [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator) role on the tenant you want to stream the logs from, or the equivalent permissions.
- Your user must have read and write permissions to the Microsoft Entra diagnostic settings in order to be able to see the connection status.

## Microsoft Entra ID data connector data types

This table lists the logs you can send from Microsoft Entra ID to Microsoft Sentinel using the Microsoft Entra ID data connector. Microsoft Sentinel stores these logs in the Log Analytics workspace linked to your Microsoft Sentinel workspace.

| **Log type** | **Description** | **Log schema** |
| --- | --- | --- |
| [**Audit logs**](/en-us/azure/active-directory/reports-monitoring/concept-audit-logs) | System activity related to user and group management, managed applications, and directory activities. | [AuditLogs](/en-us/azure/azure-monitor/reference/tables/auditlogs) |
| [**Sign-in logs**](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins) | Interactive user sign-ins where a user provides an authentication factor. | [SigninLogs](/en-us/azure/azure-monitor/reference/tables/signinlogs) |
| [**Non-interactive user sign-in logs**](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins#non-interactive-user-sign-ins) | Sign-ins performed by a client on behalf of a user without any interaction or authentication factor from the user. | [AADNonInteractiveUserSignInLogs](/en-us/azure/azure-monitor/reference/tables/aadnoninteractiveusersigninlogs) |
| [**Service principal sign-in logs**](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins#service-principal-sign-ins) | Sign-ins by apps and service principals that don't involve any user. In these sign-ins, the app or service provides a credential on its own behalf to authenticate or access resources. | [AADServicePrincipalSignInLogs](/en-us/azure/azure-monitor/reference/tables/aadserviceprincipalsigninlogs) |
| [**Managed Identity sign-in logs**](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins#managed-identity-for-azure-resources-sign-ins) | Sign-ins by Azure resources that have secrets managed by Azure. For more information, see [What are managed identities for Azure resources?](/en-us/azure/active-directory/managed-identities-azure-resources/overview) | [AADManagedIdentitySignInLogs](/en-us/azure/azure-monitor/reference/tables/aadmanagedidentitysigninlogs) |
| [**AD FS sign-in logs**](/en-us/entra/identity/monitoring-health/concept-usage-insights-report#ad-fs-application-activity) | Sign-ins performed through Active Directory Federation Services (AD FS). | [ADFSSignInLogs](/en-us/azure/azure-monitor/reference/tables/adfssigninlogs) |
| [**Enriched Office 365 audit logs**](/en-us/entra/global-secure-access/how-to-view-enriched-logs) | Security events related to Microsoft 365 apps. | [EnrichedOffice365AuditLogs](/en-us/azure/azure-monitor/reference/tables/enrichedmicrosoft365auditlogs) |
| [**Provisioning logs**](/en-us/azure/active-directory/reports-monitoring/concept-provisioning-logs) | System activity information about users, groups, and roles provisioned by the Microsoft Entra provisioning service. | [AADProvisioningLogs](/en-us/azure/azure-monitor/reference/tables/aadprovisioninglogs) |
| [**Microsoft Graph activity logs**](/en-us/graph/microsoft-graph-activity-logs-overview) | HTTP requests accessing your tenant’s resources through the Microsoft Graph API. | [MicrosoftGraphActivityLogs](/en-us/azure/azure-monitor/reference/tables/microsoftgraphactivitylogs) |
| [**Network access traffic logs**](/en-us/entra/global-secure-access/how-to-view-traffic-logs) | Network access traffic and activities. | [NetworkAccessTraffic](/en-us/azure/azure-monitor/reference/tables/networkaccesstraffic) |
| [**Remote network health logs**](/en-us/entra/global-secure-access/how-to-remote-network-health-logs?tabs=microsoft-entra-admin-center) | Insights into the health of remote networks. | [RemoteNetworkHealthLogs](/en-us/azure/azure-monitor/reference/tables/remotenetworkhealthlogs) |
| [**User risk events**](/en-us/entra/id-protection/howto-identity-protection-investigate-risk?branch=main#risk-detections-report) | User risk events generated by Microsoft Entra ID Protection. | [AADUserRiskEvents](/en-us/azure/azure-monitor/reference/tables/aaduserriskevents) |
| [**Risky users**](/en-us/entra/id-protection/howto-identity-protection-investigate-risk#risky-users-rport) | Risky users logged by Microsoft Entra ID Protection. | [AADRiskyUsers](/en-us/azure/azure-monitor/reference/tables/aadriskyusers) |
| [**Risky service principals**](/en-us/entra/id-protection/howto-identity-protection-investigate-risk?branh=main#risk-detections-report) | Information about service principals flagged as risky by Microsoft Entra ID Protection. | [AADRiskyServicePrincipals](/en-us/azure/azure-monitor/reference/tables/aadriskyserviceprincipals) |
| [**Service principal risk events**](/en-us/entra/id-protection/howto-identity-protection-investigate-risk#risy-users-report) | Risk detections associated with service principals logged by Microsoft Entra ID Protection. | [AADServicePrincipalRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadserviceprincipalriskevents) |

Important

Some of the available log types are currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Enable the Microsoft Entra ID data connector

To enable the Microsoft Entra ID data connector, follow the steps in [Enable a data connector](configure-data-connector#enable-a-data-connector).

## Install the Microsoft Entra ID solution (optional)

Install the solution for **Microsoft Entra ID** from the **Content Hub** in Microsoft Sentinel to get prebuilt workbooks, analytics rules, playbooks, and more. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).