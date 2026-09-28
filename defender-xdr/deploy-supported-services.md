---
layout: Conceptual
title: Deploy services supported by Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/deploy-supported-services
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the Microsoft security services that integrate with Microsoft Defender XDR, their licensing requirements, and deployment procedures
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
ms.topic: install-set-up-deploy
ms.date: 2025-04-25T00:00:00.0000000Z
locale: en-us
document_id: d7b7aae6-c2a6-2d8c-a413-f2ccc67cb586
document_version_independent_id: d7b7aae6-c2a6-2d8c-a413-f2ccc67cb586
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/deploy-supported-services.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy-supported-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/deploy-supported-services.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 36c25ec1-5655-ac00-068e-4f35895044db
---

# Deploy services supported by Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

[Microsoft Defender XDR](microsoft-365-defender) integrates various Microsoft security services to provide centralized detection, prevention, and investigation capabilities against sophisticated attacks. This article describes the supported services, their licensing requirements, the advantages, and limitations associated with deploying one or more services, and links to how you can fully deploy them individually.

## Supported services

A Microsoft 365 E5, E5 Security, A5, or A5 Security license or a valid combination of licenses provides access to the following supported services and entitles you to use Microsoft Defender. [See licensing requirements](prerequisites#licensing-requirements)

| Supported service | Description |
| --- | --- |
| Microsoft Defender for Endpoint | Endpoint protection suite built around powerful behavioral sensors, cloud analytics, and threat intelligence |
| Microsoft Defender for Office 365 | Advanced protection for your apps and data in Office 365, including email and other collaboration tools |
| Microsoft Defender for Identity | Defend against advanced threats, compromised identities, and malicious insiders using correlated Active Directory signals |
| Microsoft Defender for Cloud Apps | Identify and combat cyberthreats across your Microsoft and non-Microsoft cloud services |

## Deployed services and functionality

Microsoft Defender provides better visibility, correlation, and remediation as you deploy more supported services.

### Benefits of full deployment

To get the complete benefits of Microsoft Defender, we recommend deploying all supported services. Here are some of the key benefits of full deployment:

- Incidents are identified and correlated based on alerts and event signals from all available sensors and service-specific analysis capabilities
- Automated investigation and remediation (AIR) playbooks apply across various entity types, including devices, mailboxes, and user accounts
- A more comprehensive advanced hunting schema can be queried for event and entity data from devices, mailboxes, and other entities

### Limited deployment scenarios

Each supported service that you deploy provides an extremely rich set of raw signals and correlated information. While limited deployment doesn't cause Microsoft Defender functionality to turn off, its ability to provide comprehensive visibility across your endpoints, apps, data, and identities is affected. At the same time, any remediation capabilities only apply to entities that are managed by the services you've deployed.

The table below lists how each supported service provides additional data, opportunities to obtain additional insight by correlating the data, and better remediation and response capabilities.

| Service | Data (signals & correlated info) | Remediation & response scope |
| --- | --- | --- |
| Microsoft Defender for Endpoint | - Endpoint states and raw events- Endpoint detections and alerts, including antivirus, EDR, attack surface reduction- Info on files and other entities observed on endpoints | Endpoints |
| Microsoft Defender for Office 365 | - Mail and mailbox states and raw events- Email, attachment, and link detections | - Mailboxes- Microsoft 365 accounts |
| Microsoft Defender for Identity | - Active Directory signals, including authentication events- Identity-related behavioral detections | Identities |
| Microsoft Defender for Cloud Apps | - Detection of unsanctioned cloud apps and services (shadow IT)- Exposure of data to cloud apps- Threat activity associated with cloud apps | Cloud apps |

## Deploy the services

Deploying each service typically requires provisioning to your tenant and some initial configuration. See the following table to understand how each of these services is deployed.

| Service | Provisioning instructions | Initial configuration |
| --- | --- | --- |
| Microsoft Defender for Endpoint | [Microsoft Defender for Endpoint deployment guide](/en-us/defender-endpoint/mde-planning-guide) | *See provisioning instructions* |
| Microsoft Defender for Office 365 | *None, provisioned with Office 365* | [Configure Defender for Office 365 protection policies](/en-us/defender-office-365/mdo-deployment-guide#step-2-configure-protection-policies) |
| Microsoft Defender for Identity | [Quickstart: Create your Microsoft Defender for Identity instance](/en-us/azure-advanced-threat-protection/install-atp-step1) | *See provisioning instructions* |
| Microsoft Defender for Cloud Apps | *None* | [Quickstart: Get started with Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/getting-started-with-cloud-app-security) |

Once you've deployed the supported services, [turn on Microsoft Defender XDR](m365d-enable).