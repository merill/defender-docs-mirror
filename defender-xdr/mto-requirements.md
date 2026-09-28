---
layout: Conceptual
title: Set up Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-requirements
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn what steps you need to take to get started with multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4e2721e9-1ea6-bfb8-1abd-e0a421db2978
document_version_independent_id: 4e2721e9-1ea6-bfb8-1abd-e0a421db2978
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-requirements.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-requirements.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ad05b602-7f17-051b-0f03-e5812de12d60
---

# Set up Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

This article describes the steps you need to take to start using multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal.

1. Review the requirements
2. Verify your tenant access
3. Set up Microsoft Defender multitenant management

Note

- In multitenant management, interactions between the multitenant user and the managed tenants could involve accessing data and managing configurations. The ability to undertake these actions is determined by the permissions a managed tenant has granted the multitenant user.
- [Data privacy](/en-us/defender-xdr/data-privacy), [role-based access control (RBAC)](/en-us/defender-xdr/m365d-permissions) and [Licensing](/en-us/defender-xdr/prerequisites#licensing-requirements) are respected by Microsoft Defender multi-tenant management.

## Review the requirements

The following table lists the basic requirements you need to use multitenant management for Microsoft Defender XDR and Microsoft Sentinel in the Defender portal.

| Requirement | Description |
| --- | --- |
| Microsoft Defender XDR prerequisites | Verify you meet the [Microsoft Defender XDR prerequisites](/en-us/defender-xdr/prerequisites) |
| Microsoft Defender XDR for US Government customers | Check if you have the following applicable [licensing requirements](/en-us/defender-xdr/usgov#licensing-requirements) |
| Multitenant access | To view and manage the data you have access to in multitenant management, you need to ensure you have the necessary access. **For Microsoft Defender data**, you must have either: - [Granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction)- [Microsoft Entra B2B authentication](/en-us/azure/active-directory/external-identities/what-is-b2b)**To run cross-tenant queries on Microsoft Sentinel data**, you must set up [Azure Lighthouse](/en-us/azure/lighthouse/overview). For example, to run cross-workspace queries with the `workspace()` operator in advanced hunting and analytics rules. |
| Permissions | Users must be assigned the correct roles and permissions at the individual tenant level, in order to view and manage the associated data in multitenant management. To learn more, see:  - [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](/en-us/defender-xdr/m365d-permissions) - [Custom roles in role-based access control for Microsoft Defender XDR](/en-us/defender-xdr/custom-roles) To learn how to grant permissions for multiple users at scale, see [What is entitlement management](/en-us/azure/active-directory/governance/entitlement-management-overview). |
| Security information and event management (SIEM) data (Optional) | To include SIEM data with the extended detection and response (XDR) data, one or more tenants must include a Microsoft Sentinel workspace onboarded to Microsoft Defender. For more information, see [Connect Microsoft Sentinel to Microsoft Defender XDR](/en-us/azure/sentinel/microsoft-sentinel-onboard).The Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel. For more information, see [Multiple Microsoft Sentinel workspaces in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2310579). Access to Microsoft Sentinel data is available through [Microsoft Entra B2B authentication](/en-us/azure/active-directory/external-identities/what-is-b2b). Microsoft Sentinel doesn't support [granular delegated admin privileges (GDAP)](/en-us/partner-center/gdap-introduction) at this time. |

We recommend that you set up [multifactor authentication trust](/en-us/azure/active-directory/external-identities/authentication-conditional-access) for each tenant to avoid missing data in Microsoft Defender multitenant management.

## Verify your tenant access

In order to view and manage the data you have access to in Microsoft Defender multitenant management, you need to ensure you have the necessary permissions. For each tenant you want to view and manage, you need to either:

- Verify your tenant access with Microsoft Entra B2B
- Verify your tenant access with GDAP

### Verify your tenant access with Microsoft Entra B2B

Perform the following steps to verify your tenant access with Microsoft Entra B2B:

1. Go to [My account](https://myaccount.microsoft.com/organizations).
2. Under **Organizations &gt; Other organizations you collaborate with** see the list of organizations you have guest access to.

    [![Screenshot of organizations in the myaccount portal](media/mto-requirements/mto-myaccount.png)](media/mto-requirements/mto-myaccount.png#lightbox)
3. Verify all the tenants you plan to manage appear in the list.
4. For each tenant, go to the [Microsoft Defender portal](https://security.microsoft.com/?tid=tenant_id) and sign in to validate you can successfully access the tenant.

### Verify your tenant access with GDAP

GDAP is not supported for Microsoft Sentinel data, and provides access to Defender data only.

1. Go to the [Microsoft Partner Center](https://partner.microsoft.com/commerce/granularadminaccess/list).
2. Under **Customers** you can find the list of organizations you have guest access to.
3. Verify all the tenants you plan to manage appear in the list.
4. For each tenant, go to the [Microsoft Defender portal](https://security.microsoft.com/?tid=tenant_id) and sign in to validate you can successfully access the tenant.

## Set up multitenant management

The first time you use Microsoft Defender multitenant management, you need setup the tenants you want to view and manage. To get started:

1. Sign in to [Microsoft Defender multitenant management](https://mto.security.microsoft.com/)
2. Select **Add tenants**.

    [![Screenshot of the Microsoft Defender multi-tenant portal setup screen](media/mto-requirements/mto-add-tenants.png)](media/mto-requirements/mto-add-tenants.png#lightbox)
3. Choose the tenants you want to manage and select **Add**

Note

The Microsoft Defender multitenant view currently has a limit of 100 target tenants.

The features available in multitenant management now appear on the navigation bar and you're ready to view and manage security data across all your tenants.

[![Screenshot of Microsoft Defender multitenant management.](media/mto-requirements/mto-tenant-selection.png)](media/mto-requirements/mto-tenant-selection.png#lightbox)