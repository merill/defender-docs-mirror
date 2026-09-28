---
layout: Conceptual
title: Configure multitenant delegated access for an MSSP in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/grant-mssp-access
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Set up delegated multitenant access for an MSSP in Microsoft Defender for Endpoint by configuring RBAC, Microsoft Entra ID groups, and Governance Access Packages.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e6039ccb-7424-3d76-840e-f2d51577012f
document_version_independent_id: e6039ccb-7424-3d76-840e-f2d51577012f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/grant-mssp-access.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: grant-mssp-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/grant-mssp-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 286e5b61-2102-6ffb-3e9e-261e6118d38e
---

# Configure multitenant delegated access for an MSSP in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft recommends that you use roles with the fewest permissions. Using roles with the fewest permissions helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To implement a multitenant delegated access solution, take the following steps:

1. Enable [role-based access control](rbac) in Defender for Endpoint and connect with Microsoft Entra ID groups.
2. Configure [Governance Access Packages](/en-us/azure/active-directory/governance/identity-governance-overview) for access request and provisioning.
3. Manage access requests and audits in [Microsoft MyAccess](/en-us/azure/active-directory/governance/entitlement-management-request-approve).

## Enable role-based access controls in Microsoft Defender for Endpoint

Complete the following steps to enable role-based access controls and connect RBAC roles with Microsoft Entra ID groups.

1. **Create access groups for MSSP resources in Customer Entra ID: Groups**

    The access groups are linked to the roles you create in Defender for Endpoint. To create the access groups, in the customer Entra ID tenant, create three groups. In our example approach, we create the following groups:

    - Tier 1 Analyst
    - Tier 2 Analyst
    - MSSP Analyst Approvers
2. Create Defender for Endpoint roles for appropriate access levels in Customer Defender for Endpoint.

    To enable RBAC in the customer [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **Permissions** &gt; **Roles**, and then select **Turn on roles**.

    Then, create RBAC roles to meet MSSP SOC Tier needs. Link these roles to the Tier 1 Analyst, Tier 2 Analyst, and MSSP Analyst Approvers Microsoft Entra ID groups via assigned user groups. There are two possible roles: Tier 1 Analysts, and Tier 2 Analysts.

    - **Tier 1 Analysts** - Perform all actions except for live response and manage security settings.
    - **Tier 2 Analysts** - Tier 1 capabilities with the addition to [live response](live-response)

    For details about role assignments and permissions, see [Role-based access control in Defender for Endpoint](rbac).

## Configure Governance Access Packages

Use the following steps to configure Governance Access Packages for MSSP access.

1. **Add MSSP as Connected Organization in Customer Entra ID: Identity Governance**

    Adding the MSSP as a connected organization allows the MSSP to request and have access provisioned.

    To add the MSSP as a connected organization, in the customer Entra ID tenant, access Identity Governance: Connected organization. Add a new organization and search for your MSSP Analyst tenant via Tenant ID or Domain. We suggest creating a separate Entra ID tenant for your MSSP Analysts.
2. **Create a resource catalog in Customer Entra ID: Identity Governance**

    Resource catalogs are a logical collection of access packages, created in the customer Entra ID tenant.

    To create a resource catalog, in the customer Entra ID tenant, access Identity Governance: Catalogs, and add **New Catalog**. In our example, it's called, **MSSP Accesses**.

    [![The new catalog page](media/goverance-catalog.png)](media/goverance-catalog.png#lightbox)

    Further more information, see [Create a catalog of resources](/en-us/azure/active-directory/governance/entitlement-management-catalog-create).
3. **Create access packages for MSSP resources Customer Entra ID: Identity Governance**

    Access packages are the collection of rights and accesses that a requestor is granted upon approval.

    To create an access package, in the customer Entra ID tenant, access Identity Governance: Access Packages, and add **New Access Package**. Create an access package for the MSSP approvers and each analyst tier. For example, a Tier 1 Analyst access package can be configured to:

    - Requires a member of the Entra ID group **MSSP Analyst Approvers** to authorize new requests
    - Has annual access reviews, where the SOC analysts can request an access extension
    - Can only be requested by users in the MSSP SOC Tenant
    - Access auto expires after 365 days

[![The New access package page](media/new-access-package.png)](media/new-access-package.png#lightbox)

    For more information, see [Create a new access package](/en-us/azure/active-directory/governance/entitlement-management-access-package-create).
4. **Provide access request link to MSSP resources from Customer Entra ID: Identity Governance**

    The My Access portal link is used by MSSP SOC analysts to request access through the MSSP access packages created in Identity Governance. The My Access portal link is durable and can be reused over time for new analysts. The analyst request goes into a queue for approval by the **MSSP Analyst Approvers**.

[![The Properties page](media/access-properties.png)](media/access-properties.png#lightbox)

    The My Access portal link is located on the overview page of each access package.

## Manage MSSP access in Microsoft Defender for Endpoint

Use the following steps to review and manage MSSP access requests in My Access.

1. Review and authorize access requests in Customer and/or MSSP MyAccess.

    Access requests are managed in the customer My Access, by members of the MSSP Analyst Approvers group.

    To review and authorize access requests, access the customer's MyAccess using: `https://myaccess.microsoft.com/@<Customer Domain>`.

    Example: `https://myaccess.microsoft.com/@M365x440XXX.onmicrosoft.com#/`
2. Approve or deny requests in the **Approvals** section of the UI.

    After a request is approved, analyst access is provisioned, and each analyst should be able to access the customer's Microsoft Defender portal: `https://security.microsoft.com/?tid=<CustomerTenantId>`