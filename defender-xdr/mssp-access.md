---
layout: Conceptual
title: Provide managed security service provider (MSSP) access - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mssp-access
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to grant managed security service providers (MSSPs) delegated access to Microsoft Defender using role-based access control and Microsoft Entra ID Governance.
ms.service: defender-xdr
ms.localizationpriority: medium
ms.author: guywild
author: guywi-ms
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c9c43fb9-e24e-0aac-2923-c7b28d4f887b
document_version_independent_id: c9c43fb9-e24e-0aac-2923-c7b28d4f887b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mssp-access.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mssp-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mssp-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 96e8c31f-627c-4bef-3688-f44e438c06fd
---

# Provide managed security service provider (MSSP) access - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Important

Procedures in this article use features that require at a minimum Microsoft Entra ID P2 [for each user under scope of management](/en-us/entra/id-governance/licensing-fundamentals#how-can-i-license-usage-of-microsoft-entra-id-governance-features-for-business-guests).

To implement a multitenant delegated access solution, take the following steps:

1. Enable [role-based access control](/en-us/defender-endpoint/rbac) for Defender for Endpoint via the Microsoft Defender portal and connect with Microsoft Entra groups.
2. Configure [entitlement management for external users](/en-us/azure/active-directory/governance/entitlement-management-external-users) within Microsoft Entra ID Governance to enable access requests and provisioning.
3. Manage access requests and audits in [Microsoft Myaccess](/en-us/azure/active-directory/governance/entitlement-management-request-approve).

## Enable role-based access controls in Microsoft Defender for Endpoint in Microsoft Defender portal {#enable-role-based-access-controls-in-microsoft-defender-for-endpoint-in-microsoft-365-defender-portal}

1. **Create access groups for MSSP resources in Customer Microsoft Entra ID: Groups**

    These groups are linked to the Roles you create in Defender for Endpoint in Microsoft Defender portal. To create these access groups, in the customer AD tenant, create three groups. In our example approach, we create the following groups:

    - Tier 1 Analyst
    - Tier 2 Analyst
    - MSSP Analyst Approvers
2. Create Defender for Endpoint roles for appropriate access levels in Customer Defender for Endpoint in Microsoft Defender portal roles and groups.

    To enable RBAC in the customer Microsoft Defender portal, access **Permissions &gt; Endpoints roles & groups &gt; Roles** with a user account with Security Administrator rights.

    [![The details of the MSSP access in the Microsoft Defender portal](media/mssp-access/mssp-access.png)](media/mssp-access/mssp-access.png#lightbox)

    Then, create RBAC roles to meet MSSP SOC Tier needs. Link these roles to the created user groups via "Assigned user groups".

    Two possible roles:

    - **Tier 1 Analysts** Perform all actions except for live response and manage security settings.
    - **Tier 2 Analysts** Tier 1 capabilities with the addition to [live response](/en-us/defender-endpoint/live-response).

    For more information, see [Manage portal access using role-based access control](/en-us/defender-endpoint/rbac).

## Configure Governance Access Packages

1. **Add MSSP as Connected Organization in Customer Microsoft Entra ID: Identity Governance**

    Adding the MSSP as a connected organization allows the MSSP to request and have accesses provisioned.

    To add the MSSP as a connected organization, in the customer AD tenant, access Identity Governance: Connected organization. Add a new organization and search for your MSSP Analyst tenant via Tenant ID or Domain. We suggest creating a separate AD tenant for your MSSP Analysts.
2. **Create a resource catalog in Customer Microsoft Entra ID: Identity Governance**

    Resource catalogs are a logical collection of access packages, created in the customer AD tenant.

    To create a resource catalog, in the customer AD tenant, access Identity Governance: Catalogs, and add **New Catalog**. In our example, we'll call it **MSSP Accesses**.

    [![A new catalog in the Microsoft Defender portal](media/mssp-access/goverance-catalog.png)](media/mssp-access/goverance-catalog.png#lightbox)

    Further more information, see [Create a catalog of resources](/en-us/azure/active-directory/governance/entitlement-management-catalog-create).
3. **Create access packages for MSSP resources Customer Microsoft Entra ID: Identity Governance**

    Access packages are the collection of rights and accesses that a requestor grants upon approval.

    To create an access package, in the customer AD tenant, access Identity Governance: Access Packages, and add **New Access Package**. Create an access package for the MSSP approvers and each analyst tier. For example, the following Tier 1 Analyst configuration creates an access package that:

    - Requires a member of the AD group **MSSP Analyst Approvers** to authorize new requests
    - Has annual access reviews, where the SOC analysts can request an access extension
    - Can only be requested by users in the MSSP SOC Tenant
    - Access auto expires after 365 days

    [![The details of a new access package in the Microsoft Defender portal](media/mssp-access/new-access-package.png)](media/mssp-access/new-access-package.png#lightbox)

    For more information, see [Create a new access package](/en-us/azure/active-directory/governance/entitlement-management-access-package-create).
4. **Provide access request link to MSSP resources from Customer Microsoft Entra ID: Identity Governance**

    The My Access portal link is used by MSSP SOC analysts to request access via the MSSP access packages. The My Access request link is durable, meaning it can be reused over time for new analysts. The analyst request goes into a queue for approval by the **MSSP Analyst Approvers**.

    [![The access properties in the Microsoft Defender portal](media/mssp-access/access-properties.png)](media/mssp-access/access-properties.png#lightbox)

    The My Access request link is located on the overview page of each access package.

## Manage MSSP access requests

1. Review and authorize access requests in Customer and/or MSSP myaccess.

    Access requests are managed in the customer My Access, by members of the MSSP Analyst Approvers group.

    To review and authorize access requests, access the customer's myaccess using: `https://myaccess.microsoft.com/@<Customer Domain>`.

    Example: `https://myaccess.microsoft.com/@M365x440XXX.onmicrosoft.com#/`
2. Approve or deny requests in the **Approvals** section of the UI.

    At this point, analyst access has been provisioned, and each analyst should be able to access the customer's Microsoft Defender portal:

    `https://security.microsoft.com/?tid=<CustomerTenantId>` with the permissions and roles they were assigned.

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).