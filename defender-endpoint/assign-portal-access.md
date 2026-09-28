---
layout: Conceptual
title: Manage portal access permissions in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/assign-portal-access
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Compare basic permissions and role-based access control for Microsoft Defender for Endpoint portal access, and learn how to choose or switch between them.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: da03e0d9-88c4-c63c-0e5c-4bffde883c20
document_version_independent_id: da03e0d9-88c4-c63c-0e5c-4bffde883c20
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/assign-portal-access.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: assign-portal-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/assign-portal-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 7858daba-d8c3-c4d7-9c53-b8eaface2510
---

# Manage portal access permissions in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

This article helps you understand the available permission models for Microsoft Defender for Endpoint portal access and how to switch between them. Defender for Endpoint supports two ways to manage permissions:

- **Basic permissions management**: Set permissions to either full access or read-only. See [Use basic permissions to access the portal](basic-permissions).
- **Role-based access control (RBAC)**: Set granular permissions by defining roles, assigning Microsoft Entra user groups to the roles, and granting the user groups access to device groups. For more information on RBAC, see [Manage portal access using role-based access control](rbac).

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac).

## Change from basic permissions to RBAC

Important

Switching to RBAC is irreversible. After you switch, you can't return to basic permissions management.

If you have basic permissions, you can switch to Role-based access control (RBAC) anytime. Consider the following before making the switch:

- Users who have full access are automatically assigned the default Defender for Endpoint administrator role.
- Other Microsoft Entra user groups can be assigned to the Defender for Endpoint administrator role after switching to RBAC.
- Only users who are assigned the Defender for Endpoint administrator role can manage permissions using RBAC.
- Users who have read-only access (Security Readers) lose access to the portal until they're assigned a role. Only Microsoft Entra user groups can be assigned a role under RBAC.

Important

Microsoft recommends that you use roles with the fewest permissions as it helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.