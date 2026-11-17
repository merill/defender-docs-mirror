---
layout: Conceptual
title: Use Content hub with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/content-hub-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use Content hub with ISOC in Microsoft Defender to discover, install, and manage supported workspace-level and tenant-level security content.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- msftsolution-secops
ms.topic: how-to
ms.service: microsoft-sentinel
ai-usage: ai-assisted
ms.date: 2026-11-15T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: b928f9f2-8671-fbd9-9014-17102a75a1dd
document_version_independent_id: b928f9f2-8671-fbd9-9014-17102a75a1dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/content-hub-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: content-hub-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/content-hub-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 8f0ab109-61d6-f5a5-918e-5d417041de60
---

# Use Content hub with ISOC in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Use Content hub with Integrated Security Operations Center (ISOC) in Microsoft Defender to discover, install, and manage supported security content for workspaces and Microsoft Defender.

Content hub supports a unified experience for workspace-level and tenant-level content. You can view solution installation status for workspaces you have access to, install supported content into individual workspaces, and deploy supported Microsoft Defender content at tenant scope.

Solutions can include workspace-level content and Defender-level content, such as Defender workbooks and custom detections. The content available for installation depends on the deployment target and your permissions.

Note

Supported content types and deployment options vary depending on your tenant configuration and the selected deployment target.

## Prerequisites

Before you begin, make sure the following requirements are met:

- Your tenant is [eligible for ISOC](isoc-overview).
- To install workspace-level content, you have an [ISOC workspace](onboard-isoc-workspace) or an existing Microsoft Sentinel workspace.
- You have the following permissions:
    - In Defender RBAC:
        - **Content hub read** to discover available content.
        - **Content hub manage** to install and manage solutions.
    - In Azure:
        - **Deploy** permission on the resource group to install workspace-level solutions.
        - For tenant-level deployments, a management group must be configured and the appropriate deployment permissions assigned.

An ISOC workspace isn't required to install supported Defender-level content at tenant scope.

## Discover content

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Content management** &gt; **Content hub**.
3. Search for a solution or use the available filters to find content.
4. Select a solution to view its details, supported content types, and available installation targets.

Content hub provides a unified view of solution installations in workspaces you have permission to access.

- The solution list shows installation status for available targets. Hover over a solution's status to view its installed targets.
- The solution details panel shows installation status and versions for accessible workspaces.
- The package details panel provides a preview of the supported content types available for each applicable target type: Primary, Secondary, and Tenant Level.

Only workspaces and content that you're permitted and eligible to access are available.

## Install solution content

Content hub supports installing solution content into individual workspaces and deploying supported Defender-level content at tenant scope.

The installation options depend on the content types included in the solution and the deployment targets available to your organization.

### Install content in a workspace

To install supported solution content in a workspace:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Content management** &gt; **Content hub**.
3. Search for and select the solution that you want to install.
4. Select **View details**.
5. Select **Create**.
6. On the **Basics** tab, select the subscription, resource group, and workspace where you want to deploy the solution.
7. Select **Next** to review the available configuration.
8. On the **Review + create** tab, wait for validation to complete.
9. Select **Create**.

To install the same solution into multiple workspaces, repeat the installation process for each workspace.

After installation, configure any data connectors included in the solution to start ingesting data into the selected workspace.

### Install Defender-level content

For eligible tenants, Content hub also supports deploying Defender-level solution content at tenant scope.

Supported Defender-level content includes:

- **Defender workbooks**
- **Custom detections**

Defender-level content is installed at tenant scope rather than into an individual workspace. You can install supported tenant-level solutions without creating or selecting an ISOC or Microsoft Sentinel workspace.

If a solution includes both workspace-level and Defender-level content, workspace-level content requires workspace selection, while supported Defender-level content is deployed at tenant scope.

Defender-level content installed from Content hub is read-only and disabled by default. To modify or activate supported content, create a copy.

### Manage installed custom detections

Custom detections installed from Content hub are disabled by default.

To activate or modify an installed custom detection, create a copy of the detection and enable the copy.

When a solution is updated, Content hub can overwrite the original platform-managed content. Customer-created copies aren't overwritten.

## Update an installed solution

If an installed solution has an available update, you can update it from Content hub.

Updates are applied according to the solution's installation target:

- **Workspace-level content:** Update the solution separately for each workspace where it's installed.
- **Defender-level content:** Updates are applied at tenant scope.

Updating platform-managed content doesn't overwrite customer-created copies.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Content management** &gt; **Content hub**.
3. Search for and select the installed solution.
4. Select **View details**.
5. Select **Update**.
6. Review the solution configuration.
7. Select **Review + create**.
8. Wait for validation to complete.
9. Select **Update**.

Note

Available updates depend on the supported content types and installation targets for the solution.

## View and manage installed solutions

Content hub provides a unified view of solution installations for accessible workspaces and tenant-level deployment targets.

Select a solution and open its details to review installation status, deployed versions, and installation targets.

Workspace-level installations are managed independently. You can update or delete a solution installation for an individual workspace without changing installations in other workspaces.

Defender-level content is managed at tenant scope. The solution details show its installation scope alongside workspace-level installations, when applicable.

Deleting a solution doesn't delete custom detections installed as part of the solution. These custom detections remain in Microsoft Defender after the solution is deleted.