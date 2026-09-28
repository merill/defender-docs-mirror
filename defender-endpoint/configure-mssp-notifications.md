---
layout: Conceptual
title: Configure alert notifications that are sent to MSSPs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-mssp-notifications
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure alert notifications that are sent to MSSPs
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: article
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: bd9c7c0f-91a2-ddad-8613-d3dfe278da6c
document_version_independent_id: bd9c7c0f-91a2-ddad-8613-d3dfe278da6c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-mssp-notifications.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-mssp-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-mssp-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: aa128cf0-0512-8e92-e2df-bffe946aed22
---

# Configure alert notifications that are sent to MSSPs - Microsoft Defender for Endpoint | Microsoft Learn

Note

This step can be done by either the MSSP customer or MSSP. MSSPs must be granted the appropriate permissions to configure this on behalf of the MSSP customer.

After access the portal is granted, alert notification rules can be created so that emails are sent to MSSPs when alerts associated with the tenant are created and set conditions are met.

For more information, see [Create rules for alert notifications](/en-us/defender-xdr/configure-email-notifications#create-rules-for-alert-notifications).

These check boxes must be checked:

- **Include organization name** - The customer name will be added to email notifications
- **Include tenant-specific portal link** - Alert link URL will have tenant specific parameter (tid=target\_tenant\_id) that allows direct access to target tenant portal