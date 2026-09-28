---
layout: Conceptual
title: Cross-tenant management - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cross-tenant-management
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to set up cross-tenant management to manage the security posture of multiple tenants in Defender for Cloud using Azure Lighthouse.
ms.topic: concept-article
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 712d7c01-4d10-cc34-1d42-955c513a6d85
document_version_independent_id: 7ff988fe-55ae-d79c-08cc-566ffc209e1e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cross-tenant-management.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cross-tenant-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cross-tenant-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d0989e16-62ed-4db0-8dd8-b1c704683638
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/677796fe-69f7-4468-8f9b-540e903c4f4e
platformId: bf338768-aeb1-29ef-52c4-532d34b22de9
---

# Cross-tenant management - Microsoft Defender for Cloud | Microsoft Learn

Cross-tenant management enables you to view and manage the security posture of multiple tenants in Defender for Cloud by using [Azure Lighthouse](/en-us/azure/lighthouse/overview). Manage multiple tenants efficiently, from a single view, without having to sign in to each tenant's directory.

- Service providers can manage the security posture of resources, for multiple customers, from within their own tenant.
- Security teams of organizations with multiple tenants can view and manage their security posture from a single location.

## Set up cross-tenant management

[Azure delegated resource management](/en-us/azure/lighthouse/concepts/architecture) is one of the key components of Azure Lighthouse. Set up cross-tenant management by delegating access to resources of managed tenants to your own tenant using these instructions from Azure Lighthouse's documentation: [Onboard a customer to Azure Lighthouse](/en-us/azure/lighthouse/how-to/onboard-customer).

## Security and access considerations

Azure Lighthouse grants identities in the managing tenant access to delegated Azure resources. The users and their Azure role assignments aren't created as local objects in the managed tenant. As a result, the users and assignments don't appear on the subscription's **Access control (IAM)** page. To review or remove delegations, use the [**Service providers** page](/en-us/azure/lighthouse/how-to/view-manage-service-providers).

The managed tenant's Azure Activity Log records actions performed through Azure Lighthouse. The **Event initiated by** field identifies the acting user, whether the user is from the managing tenant or the managed tenant. For more information, see [Monitor service provider activity](/en-us/azure/lighthouse/how-to/view-service-provider-activity).

## How cross-tenant management works in Defender for Cloud

You're able to review and manage subscriptions across multiple tenants in the same way that you manage multiple subscriptions in a single tenant.

From the top menu bar, select the filter icon, and select the subscriptions, from each tenant's directory, you'd like to view.

![Screenshot that shows where the cross tenant filter button is located.](media/cross-tenant-management/cross-tenant-filter.png)

The views and actions are basically the same. Here are some examples:

- **Manage security policies**: From one view, manage the security posture of many resources with [policies](tutorial-security-policy), take actions with security recommendations, and collect and manage security-related data.
- **Improve Secure Score and compliance posture**: Cross-tenant visibility enables you to view the overall security posture of all your tenants and where and how to best improve the [secure score](secure-score-security-controls) and [compliance posture](regulatory-compliance-dashboard) for each of them.
- **Remediate recommendations**: Monitor and remediate a [recommendation](review-security-recommendations) for many resources from various tenants at one time. You can then immediately tackle the vulnerabilities that present the highest risk across all tenants.
- **Manage Alerts**: Detect [alerts](alerts-overview) throughout the different tenants. Take action on resources that are out of compliance with actionable [remediation steps](manage-respond-alerts).
- **Manage advanced cloud defense features and more**: Manage the various threat protection services, such as [just-in-time (JIT) Virtual Machine (VM) access](just-in-time-access-usage).