---
layout: Conceptual
title: Assign Microsoft Defender for Endpoint basic permissions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/basic-permissions
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how existing Microsoft Defender for Endpoint customers can assign full or read-only portal access by using Microsoft Graph PowerShell.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.custom:
- msecd-doc-authoring-1015
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-08-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 624f5dc5-e75b-99be-fa2d-c67c34635d66
document_version_independent_id: 624f5dc5-e75b-99be-fa2d-c67c34635d66
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/basic-permissions.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: basic-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/basic-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6ff33598-ed6c-726c-e860-c0d8e6f4cc81
---

# Assign Microsoft Defender for Endpoint basic permissions - Microsoft Defender for Endpoint | Microsoft Learn

Basic permissions management gives existing Microsoft Defender for Endpoint customers two portal access levels: full access or read-only access. Use Microsoft Graph PowerShell to assign the Security Administrator role for full access or the Security Reader role for read-only access. For more granular permissions, [use role-based access control](rbac).

Important

Starting February 16, 2025, new Defender for Endpoint customers can use only Microsoft Defender unified role-based access control (RBAC). Existing customers can continue to use their current permission model. For more information, see [Microsoft Defender unified RBAC](/en-us/defender-xdr/manage-rbac).

## Prerequisites

Complete these prerequisites before you assign user access:

- Confirm that your organization still uses basic permissions management. If your organization switched to RBAC, you can't switch back to basic permissions.
- Install [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation).
- Use an account assigned the Privileged Role Administrator role or a custom role with the required role-management permissions. Privileged Role Administrator is the least-privileged Microsoft Entra built-in role supported for this operation.
- Connect to Microsoft Graph by using **Connect-MgGraph** with the delegated `RoleManagement.ReadWrite.Directory` and `User.ReadBasic.All` permissions. For authentication options, see [Microsoft Graph PowerShell authentication commands](/en-us/powershell/microsoftgraph/authentication-commands).

You don't need to run PowerShell as a local Windows administrator to assign Microsoft Entra roles through Microsoft Graph.

## Understand the basic access levels

Basic permissions management provides these access levels:

- **Full access**: Users can sign in, view system information, resolve alerts, submit files for deep analysis, and download the onboarding package. Assign the Microsoft Entra Security Administrator role to grant full access.
- **Read-only access**: Users can sign in and view alerts and related information. They can't change alert states, submit files for deep analysis, or perform other state-changing operations. Assign the Microsoft Entra Security Reader role to grant read-only access.

## Assign user access using Microsoft Graph PowerShell

Assign the appropriate Microsoft Entra role to each user who needs access to Defender for Endpoint.

Note

The following examples use the `directoryRole` membership API. Microsoft recommends the unified role-assignment API for new automation. **Get-MgDirectoryRole** returns only activated directory roles. If the command doesn't return the requested role, [assign the Microsoft Entra role in the admin center](/en-us/entra/identity/role-based-access-control/manage-roles-portal) or use the [unified role-assignment API](/en-us/graph/api/rbacapplication-post-roleassignments).

### Assign full access

Replace `secadmin@contoso.onmicrosoft.com` with the user principal name of the account that needs full access, and then run the following command:

```powershell
New-MgDirectoryRoleMemberByRef -DirectoryRoleId (Get-MgDirectoryRole -Filter "DisplayName eq 'Security Administrator'").Id -OdataId "https://graph.microsoft.com/v1.0/directoryObjects/$((Get-MgUser -UserId 'secadmin@contoso.onmicrosoft.com').Id)"
```

### Assign read-only access

Replace `reader@contoso.onmicrosoft.com` with the user principal name of the account that needs read-only access, and then run the following command:

```powershell
New-MgDirectoryRoleMemberByRef -DirectoryRoleId (Get-MgDirectoryRole -Filter "DisplayName eq 'Security Reader'").Id -OdataId "https://graph.microsoft.com/v1.0/directoryObjects/$((Get-MgUser -UserId 'reader@contoso.onmicrosoft.com').Id)"
```