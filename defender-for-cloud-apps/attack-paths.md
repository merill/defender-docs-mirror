---
layout: Conceptual
title: Investigate OAuth application attack paths in Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/attack-paths
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
description: Learn how to identify, analyze, and mitigate attack paths involving OAuth applications using Microsoft Defender for Cloud Apps and Security Exposure Management.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: ca93a922-a469-7a86-f4fd-9be27945ad2a
document_version_independent_id: ca93a922-a469-7a86-f4fd-9be27945ad2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/attack-paths.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-paths
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/attack-paths.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0502fcd0-47d1-b460-c348-88fd53318985
---

# Investigate OAuth application attack paths in Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

[Microsoft Security Exposure Management](/en-us/security-exposure-management/microsoft-security-exposure-management) helps you to manage your company's attack surface and exposure risk effectively. By combining assets and techniques, [attack paths](/en-us/security-exposure-management/review-attack-paths) illustrate the end-to-end paths that attackers can use to move from an entry point within your organization to your critical assets. Microsoft Defender for Cloud Apps observed an increase in attackers using OAuth applications to access sensitive data in business-critical applications like Microsoft Teams, SharePoint, Outlook, and more. To support investigation and mitigation, these applications are integrated into the attack path and attack surface map views in Microsoft Security Exposure Management.

## Prerequisites

To get started with OAuth application attack path features in Exposure Management, make sure you meet the following requirements.

- A Microsoft Defender for Cloud Apps license with [App Governance](app-governance-get-started) enabled.
- Microsoft 365 app connector must be activated. For information about connecting and about which of the app connectors provide security recommendations, see [Connect apps to get visibility and control with Microsoft Defender for Cloud Apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- Optional: To get full access to attack path data, we recommend having an E5 security license, Defender for Endpoint or Defender for Identity license.

## Required roles and permissions

To access all Exposure Management experiences, you need either a Unified Role-Based Access Control (RBAC) role or an Entra ID role. Only one is required.

- **Exposure Management (read)** (Unified RBAC)

Alternatively, you can use one of the following **Entra ID roles**:

| Permission | Actions |
| --- | --- |
| **Security Admin** | (read and write permissions) |
| **Security Operator** | (read and limited write permissions) |
| **Global Reader** | (read permissions) |
| **Security Reader** | (read permissions) |

Note

Currently available in commercial cloud environments only. Microsoft Security Exposure Management data and capabilities are currently unavailable in U.S Government clouds - GCC, GCC High, DoD, and China Gov.

## Critical Asset Management - Service Principals

Service principals are identities that Microsoft Entra ID assigns to applications so they can authenticate and access resources on behalf of the application rather than a user. Microsoft Defender for Cloud Apps defines a set of critical privilege OAuth permissions. OAuth applications with these permissions are considered high-value assets. If a high-value OAuth application is compromised, an attacker can gain high privileges to SaaS applications. To reflect this risk, attack paths treat service principals with these permissions as target goals.

#### View permissions for critical assets

To view the full list of permissions, go to the [Microsoft Defender portal](https://security.microsoft.com) and navigate to Settings &gt; Microsoft Defender XDR &gt; Rules &gt; Critical asset management.

[![Screenshot of the Critical asset management page in the Microsoft Defender portal.](media/saas-securty-initiative/screenshot-of-the-critical-asset-management-page.png)](media/saas-securty-initiative/screenshot-of-the-critical-asset-management-page.png#lightbox)

## Investigation user flow: View attack paths involving OAuth applications

Once you understand which permissions represent high-value targets, use the following steps to investigate how these applications appear in your environment’s attack paths. For smaller organizations with a manageable number of attack paths, we recommend following this structured approach to investigate each attack path:

Note

OAuth apps show in the attack path surface map only when specific conditions are detected. For example, an OAuth app might appear in the attack path if a vulnerable component with an easily exploitable entry point is detected. This entry point allows lateral movement to service principals with high privileges.

1. Go to Exposure Management &gt; Attack surface &gt; Attack paths.
2. Filter by 'Target type: AAD Service principal'

    [![Screenshot of the attack paths service add pricipal target type](media/saas-securty-initiative/screenshot-of-the-attack-paths-aad-service-principal.png)](media/saas-securty-initiative/screenshot-of-the-attack-paths-aad-service-principal.png#lightbox)
3. Select the attack path titled: "Device with high severity vulnerabilities allows lateral movement to service principal with sensitive permissions"

    [![Screenshot of the attack path name](media/saas-securty-initiative/screenshot-of-the-attack-path-name.png)](media/saas-securty-initiative/screenshot-of-the-attack-path-name.png#lightbox)
4. Click the View in map button to see the attack path.

    [![Screenshot of the view in map button](media/saas-securty-initiative/screenshot-of-the-view-in-map-button.png)](media/saas-securty-initiative/screenshot-of-the-view-in-map-button.png#lightbox)
5. Select the + sign to expand nodes and view detailed connections.

    [![Screenshot of the attack surface map](media/saas-securty-initiative/attack-surface-map.png)](media/saas-securty-initiative/attack-surface-map.png#lightbox)
6. Hover or select nodes and edges to explore extra data such as which permissions this OAuth app has.

    ![Screenshot showing the permissions assigned to the OAuth app as shown in the attack surface map](media/saas-securty-initiative/screenshot-of-the-permissions-set-for-service-principal.png)
7. Copy the OAuth application's name and paste it into the search bar in the Applications page.

    [![Screenshot showing the OAuth applications tab](media/saas-securty-initiative/screenshot-of-the-oauth-applications-page.png)](media/saas-securty-initiative/screenshot-of-the-oauth-applications-page.png#lightbox)
8. Select the app name to review assigned permissions and usage insights, including whether high-privilege permissions are actively used.

    [![Screenshot showing the permissions assigned to the Oauth app](media/saas-securty-initiative/screenshot-of-permissions-assigned-to-the-oauth-app.png)](media/saas-securty-initiative/screenshot-of-permissions-assigned-to-the-oauth-app.png#lightbox)
9. Optional: If you determine the OAuth application should be disabled, you can disable it from the Applications page.

    Warning

    Disabling an OAuth application can cause service disruption and loss of access for users and services that depend on it. Verify the application's usage and dependencies before you disable it.

### Decision maker user flow: Prioritize attack path using choke points

For larger organizations with numerous attack paths that can't be manually investigated, we recommend using attack path data and utilizing the Choke Points experience as a prioritization tool. This approach allows you to:

- Identify assets connected with the most attack paths.
- Make informed decisions on which assets to prioritize for investigation.
- Filter by Microsoft Entra OAuth app to see which OAuth apps are involved in the most attack paths.
- Decide which OAuth applications to apply least privilege permissions to.

To get started:

1. Go to the Attack Paths &gt; Choke Points page.

    [![Screenshot showing the choke points page](media/saas-securty-initiative/screenshot-of-the-choke-point-page.png)](media/saas-securty-initiative/screenshot-of-the-choke-point-page.png#lightbox)
2. Select a choke point name to see more details about the top attack paths such as the name, entry point, and target.
3. Click View blast radius to further investigate the choke point in the Attack Surface Map. [![Screenshot showing the view blast radius button](media/saas-securty-initiative/screenshot-of-the-view-blast-radius-button.png)](media/saas-securty-initiative/screenshot-of-the-view-blast-radius-button.png#lightbox)

If the choke point is an OAuth application, continue the investigation by searching for the app by name in the **Applications** page, reviewing its assigned permissions and usage insights, and optionally disabling the app if appropriate.

## Analyze attack surface map and hunt with queries

In the [Attack surface map](/en-us/security-exposure-management/cross-workload-attack-surfaces), you can see connections from user-owned apps, OAuth apps, and service principals. Data about connections among user-owned apps, OAuth apps, and service principals is available in:

- ExposureGraphEdges table (shows connections)
- ExposureGraphNodes table (includes node properties like permissions)

Use the following Advanced Hunting query to identify all OAuth applications with critical permissions. This query joins the `ExposureGraphNodes` and `ExposureGraphEdges` tables to find Microsoft Entra OAuth app registrations that can authenticate as service principals classified as critical (criticality level 0) and that hold permissions to Microsoft Graph. Use it to discover which OAuth apps in your tenant have high-privilege access and to prioritize them for review:

```kusto
let RelevantNodes = ExposureGraphNodes
| where NodeLabel == "Microsoft Entra OAuth App" or NodeLabel == "serviceprincipal"
| project NodeId, NodeLabel, NodeName, NodeProperties;
ExposureGraphEdges
| where EdgeLabel == "has permissions to" or EdgeLabel == "can authenticate as"
| make-graph SourceNodeId --> TargetNodeId with RelevantNodes on NodeId
| graph-match (AppRegistration)-[canAuthAs]->(SPN)-[hasPermissionTo]->(Target)
        where AppRegistration.NodeLabel == "Microsoft Entra OAuth App" and
        canAuthAs.EdgeLabel == "can authenticate as" and
        SPN.NodeLabel == "serviceprincipal" and
        SPN.NodeProperties["rawData"]["criticalityLevel"]["criticalityLevel"] == 0 and
        hasPermissionTo.EdgeLabel == @"has permissions to" and
        Target.NodeLabel == "Microsoft Entra OAuth App" and
        Target.NodeName == "Microsoft Graph"
        project AppReg=AppRegistration.NodeLabel,
         canAuthAs=canAuthAs.EdgeLabel, SPN.NodeLabel, DisplayName=SPN.NodeProperties["rawData"]["accountDisplayName"],
         Enabled=SPN.NodeProperties["rawData"]["accountEnabled"], AppTenantID=SPN.NodeProperties["rawData"]["appOwnerOrganizationId"],
         hasPermissionTo=hasPermissionTo.EdgeLabel, Target=Target.NodeName,
         AppPerm=hasPermissionTo.EdgeProperties["rawData"]["applicationPermissions"]["permissions"]
| mv-apply AppPerm on (summarize AppPerm = make_list(AppPerm.permissionValue))
| project AppReg, canAuthAs, DisplayName, Enabled, AppTenantID, hasPermissionTo, Target, AppPerm
```