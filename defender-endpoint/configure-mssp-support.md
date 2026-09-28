---
layout: Conceptual
title: Configure managed security service provider support - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-mssp-support
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Take the necessary steps to configure the MSSP integration with the Microsoft Defender for Endpoint
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: article
ms.date: 2024-07-24T00:00:00.0000000Z
locale: en-us
document_id: 6c593e55-e87e-15a4-935b-6ff688436d97
document_version_independent_id: 6c593e55-e87e-15a4-935b-6ff688436d97
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-mssp-support.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-mssp-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-mssp-support.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 579ce57e-29b6-b321-3e70-3849f750ac0c
---

# Configure managed security service provider support - Microsoft Defender for Endpoint | Microsoft Learn

## Managed security service provider partnership opportunities

Security is recognized as a key component in running an enterprise; however, some organizations might not have the capacity or expertise to have a dedicated security operations team to manage the security of their endpoints and network, others may want to have a second set of eyes to review alerts in their network.

To address this demand, managed security service providers (MSSP) offer to deliver managed detection and response (MDR) services on top of Defender for Endpoint.

Defender for Endpoint adds partnership opportunities for this scenario and allows MSSPs to take the following actions:

- Get access to MSSP customer's Microsoft Defender portal
- Get email notifications
- Fetch alerts through security information and event management (SIEM) tools

Note

The following terms are used in this article to distinguish between the service provider and service consumer:

- MSSPs: Security organizations who monitor and manage security devices for organizations (customers).
- MSSP customers: Organizations who engage the services of MSSPs.

## MSSP integration

To enable MSSP integration, the MSSP customer needs to grant access to their Defender for Endpoint tenant so that the MSSP can access their Microsoft Defender portal (https://security.microsoft.com).

After access is granted, the MSSP or customer can do the other configuration steps. In general, the following table summarizes the configuration steps to complete:

| Step | Who does it |
| --- | --- |
| **Grant the MSSP access to the Microsoft Defender portal**. This action grants the MSSP access to the MSSP customer's Microsoft Defender portal. | MSSP Customer |
| **Configure alert notifications sent to MSSPs**. This action lets the MSSPs know what alerts they need to address for the MSSP customer. | MSSP customer or MSSP |
| **Fetch alerts from MSSP customer's tenant into SIEM system**. This action allows MSSPs to fetch alerts in SIEM tools. | MSSP |
| **Fetch alerts from MSSP customer's tenant using APIs**. This action allows MSSPs to fetch alerts using APIs. | MSSP |

## Multitenant access for MSSPs

For information on how to implement a multitenant delegated access, see [multitenant access for Managed Security Service Providers](https://techcommunity.microsoft.com/t5/microsoft-defender-atp/multi-tenant-access-for-managed-security-service-providers/ba-p/1533440).