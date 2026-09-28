---
layout: Conceptual
title: Manage access to Microsoft Defender XDR with Microsoft Entra global roles - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-permissions
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to manage access to Microsoft Defender XDR capabilities with Microsoft Entra global roles.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: concept-article
ms.date: 2024-05-08T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: f8c6a706-ab75-fb3e-93a7-f3e2d6d4872c
document_version_independent_id: f8c6a706-ab75-fb3e-93a7-f3e2d6d4872c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-permissions.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 550c0ea9-ba9c-200f-ae98-d0b2dbdcf8ae
---

# Manage access to Microsoft Defender XDR with Microsoft Entra global roles - Microsoft Defender XDR | Microsoft Learn

Note

Microsoft Defender XDR users can now take advantage of a centralized permissions management solution to control user access and permissions across different Microsoft security solutions. Learn more about the [Microsoft Defender unified role-based access control (RBAC)](manage-rbac).

There are two ways to manage access to Microsoft Defender XDR:

- **Global Microsoft Entra roles**
- **Custom role access**

Accounts assigned the following **Global Microsoft Entra roles** can access Microsoft Defender XDR functionality and data:

- Global Administrator
- Security Administrator
- Security Operator
- Global Reader
- Security Reader

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To review accounts with these roles, [view Permissions in the Microsoft Defender portal](https://security.microsoft.com/permissions).

**Custom role** access is a capability in Microsoft Defender XDR that allows you to manage access to specific data, tasks, and capabilities in Microsoft Defender XDR. Custom roles offer more control than global Microsoft Entra roles, providing users only the access they need with the least-permissive roles necessary. Custom roles can be created in addition to global Microsoft Entra roles. [Learn more about custom roles](custom-roles).

Note

This article applies only to managing global Microsoft Entra roles. For more information about using custom role-based access control, see [Custom roles for role-based access control](custom-roles)

## Access to functionality

Access to specific functionality is determined by your [Microsoft Entra role](/en-us/azure/active-directory/roles/permissions-reference). Contact a Global Administrator if you need access to specific functionality that requires you or your user group be assigned a new role.

### Approve pending automated tasks

[Automated investigation and remediation](m365d-autoir-actions) can take action on emails, forwarding rules, files, persistence mechanisms, and other artifacts found during investigations. To approve or reject pending actions that require explicit approval, you must have certain roles assigned in Microsoft 365. To learn more, see [Action center permissions](m365d-action-center#required-permissions-for-action-center-tasks).

## Access to data

Access to Microsoft Defender XDR data can be controlled using the scope assigned to user groups in Microsoft Defender for Endpoint role-based access control (RBAC). If your access hasn't been scoped to a specific set of devices in the Defender for Endpoint, you'll have full access to data in Microsoft Defender XDR. However, once your account is scoped, you'll only see data about the devices in your scope.

For example, if you belong to only one user group with a Microsoft Defender for Endpoint role and that user group has been given access to sales devices only, you'll see only data about sales devices in Microsoft Defender XDR. [Learn more about RBAC settings in Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection/microsoft-defender-atp/rbac)

### Microsoft Defender for Cloud Apps access controls

During the preview, Microsoft Defender XDR doesn't enforce access controls based on Defender for Cloud Apps settings. Access to Microsoft Defender XDR data isn't affected by these settings.