---
layout: Conceptual
title: Use role-based access control to grant fine-grained access to Microsoft Defender portal - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/rbac
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create roles and groups within your security operations to grant access to the portal.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: fb5725cf-0fff-1dda-f5cc-294300af2b25
document_version_independent_id: fb5725cf-0fff-1dda-f5cc-294300af2b25
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/rbac.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: rbac
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/rbac.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 8923f156-78d3-1595-36e0-9767b237ea41
---

# Use role-based access control to grant fine-grained access to Microsoft Defender portal - Microsoft Defender for Endpoint | Microsoft Learn

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac)

Using role-based access control (RBAC), you can create roles and groups within your security operations team to grant appropriate access to the Microsoft Defender portal. Based on the roles and groups you create, you have fine-grained control over what users with access to the Microsoft Defender portal can see and do.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

Large geo-distributed security operations teams typically adopt a tier-based model to assign and authorize access to security portals. Typical tiers include the following three levels:

| Tier | Description |
| --- | --- |
| Tier 1 | **Local security operations team / IT team** This team usually triages and investigates alerts contained within their geolocation and escalates to Tier 2 in cases where an active remediation is required. |
| Tier 2 | **Regional security operations team**This team can see all the devices for their region and perform remediation actions. |
| Tier 3 | **Global security operations team**This team consists of security experts and is authorized to see and perform all actions from the Microsoft Defender portal. |

Note

For Tier 0 assets, refer to [Privileged Identity Management](/en-us/azure/active-directory/privileged-identity-management/pim-configure) for security admins to provide more granular control of Microsoft Defender for Endpoint and Microsoft Defender.

Defender for Endpoint RBAC is designed to support your tier- or role-based model of choice and gives you granular control over what roles can see, devices they can access, and actions they can take. The RBAC framework is centered around the following controls:

- **Control who can take specific action**
    - Create custom roles and control what Defender for Endpoint capabilities they can access with granularity.
- **Control who can see information on specific device group or groups**
    - [Create device groups](machine-groups) by specific criteria such as names, tags, domains, and others, then grant role access to them using a specific Microsoft Entra user group.

        Note

        Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

To implement role-based access, you need to define admin roles, assign corresponding permissions, and assign Microsoft Entra user groups assigned to the roles.

## Before you begin

Before using RBAC, it's important that you understand which Microsoft Entra roles can grant Defender for Endpoint permissions and the consequences of turning on RBAC.

Warning

Before enabling RBAC, it's important that you have an appropriate role, such as Security Administrator assigned in Microsoft Entra ID, and that you have your Microsoft Entra groups ready to reduce the risk of being locked out of the Microsoft Defender portal.

When you first sign in to the Microsoft Defender portal, you're granted either full access or read only access. Full access rights are granted to users with the Security Administrator role in Microsoft Entra ID. Read only access is granted to users with a Security Reader role in Microsoft Entra ID.

Someone with a Defender for Endpoint Global Administrator role has unrestricted access to all devices, regardless of their device group association and the Microsoft Entra user groups assignments.

Warning

Initially, only those with Microsoft Entra Global Administrator or Security Administrator rights can create and assign roles in the Microsoft Defender portal; therefore, having the right groups ready in Microsoft Entra ID is important.

**Turning on role-based access control causes users with read-only permissions (for example, users assigned to Microsoft Entra Security reader role) to lose access until they are assigned to a role.**

Users with administrator permissions are automatically assigned the default built-in Defender for Endpoint Global Administrator role with full permissions. After opting in to use RBAC, you can assign more users who aren't Microsoft Entra Global Administrators or Security Administrators to the Defender for Endpoint Global Administrator role.

After opting in to use RBAC, you can't revert to the initial roles as when you first logged into the portal.