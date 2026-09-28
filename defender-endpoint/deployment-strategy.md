---
layout: Conceptual
title: Identify your architecture and select a deployment method for Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/deployment-strategy
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Select the best Microsoft Defender for Endpoint deployment strategy for your environment.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-05-26T00:00:00.0000000Z
locale: en-us
document_id: 8aded6cb-b59c-c826-f6d4-0eff0876eec2
document_version_independent_id: 8aded6cb-b59c-c826-f6d4-0eff0876eec2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/deployment-strategy.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deployment-strategy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/deployment-strategy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 0da442bf-293f-85b6-6b9a-b2278eda1858
---

# Identify your architecture and select a deployment method for Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

If you're already completed the steps to [prepare your environment for Defender for Endpoint](production-deployment), and you have [assigned roles and permissions for Defender for Endpoint](prepare-deployment), your next step is to create a plan for onboarding. This plan should begin with identifying your architecture and choosing your deployment method.

We understand that every enterprise environment is unique, so we've provided several options to give you the flexibility in choosing how to deploy the service. Deciding how to onboard endpoints to the Defender for Endpoint service comes down to two important steps:

![The deployment flow](/en-us/defender/media/defender-endpoint/onboarding-architecture-2.png)

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Step 1: Identify your architecture

Depending on your environment, some tools are better suited for certain architectures. Use the following table to decide which Defender for Endpoint architecture best suits your organization.

| Architecture | Description |
| --- | --- |
| **Cloud-native** | We recommend using Microsoft Intune to onboard, configure, and remediate endpoints from the cloud for enterprises who don't have an on-premises configuration management solution or are looking to reduce their on-premises infrastructure. |
| **Co-management** | For organizations who host both on-premises and cloud-based workloads we recommend using Microsoft's ConfigMgr and Intune for their management needs. These tools provide a comprehensive suite of cloud-powered management features, and unique co-management options to provision, deploy, manage, and secure endpoints and applications across an organization. |
| **On-premises** | For enterprises who want to take advantage of the cloud-based capabilities of Microsoft Defender for Endpoint while also maximizing their investments in Configuration Manager or Active Directory Domain Services, we recommend this architecture. |
| **Evaluation and local onboarding** | We recommend this architecture for SOCs (Security Operations Centers) who are looking to evaluate or run a Microsoft Defender for Endpoint pilot, but don't have existing management or deployment tools. This architecture can also be used to onboard devices in small environments without management infrastructure, such as a DMZ (Demilitarized Zone). |

## Step 2: Select your deployment method

Once you have determined the architecture of your environment and have created an inventory as outlined in the [requirements section](mde-planning-guide#requirements), use the table below to select the appropriate deployment tools for the endpoints in your environment. This information will help you plan the deployment effectively.

| Endpoint | Deployment tool |
| --- | --- |
| **Windows client devices** | [Defender deployment tool](defender-deployment-tool-windows)[Microsoft Intune / Mobile Device Management (MDM)](configure-endpoints-mdm)[Microsoft Configuration Manager](configure-endpoints-sccm)[Local script (up to 10 devices)](configure-endpoints-script)[Group Policy](configure-endpoints-gp)[Non-persistent virtual desktop infrastructure (VDI) devices](configure-endpoints-vdi)[Azure Virtual Desktop](onboard-windows-multi-session-device)[Defender deployment tool](defender-deployment-tool-windows), [System Center Endpoint Protection](onboard-downlevel), and [Microsoft Monitoring Agent](onboard-downlevel) (Windows 8.1) |
| **Windows Server**(Requires a server plan) | [Local script](configure-endpoints-script)[Integration with Microsoft Defender for Cloud](azure-server-integration)[Guidance for Windows Server with SAP](mde-sap-windows-server)[Defender deployment tool](defender-deployment-tool-windows) for Windows Server 2008 R2 SP1 |
| **macOS** | [Choose a macOS deployment method](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos) |
| **Linux server**(Requires a server plan) | [Defender deployment tool](linux-install-with-defender-deployment-tool)[Installer script based deployment](linux-installer-script)[Ansible](linux-install-with-ansible)[Chef](linux-deploy-defender-for-endpoint-with-chef)[Puppet](linux-install-with-puppet)[Saltstack](linux-install-with-saltack)[Manual deployment](linux-install-manually)[Direct onboarding with Defender for Cloud](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint)[Guidance for Linux with SAP](mde-linux-deployment-on-sap) |
| **Android** | [Microsoft Intune](/en-us/intune/intune-service/protect/microsoft-defender-deploy-android) |
| **iOS** | [Microsoft Intune](ios-install)[Mobile Application Manager](ios-install-unmanaged) |

Note

For devices that aren't managed by Intune or Configuration Manager, you can use the Defender for Endpoint Security Settings Management to receive security configurations directly from Intune. To onboard servers to Defender for Endpoint, [server licenses](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#microsoft-defender-for-endpoint) are required. You can choose from these options:

- [Microsoft Defender for Servers Plan 1 or Plan 2](/en-us/azure/defender-for-cloud/defender-for-servers-overview) (as part of the Defender for Cloud) offering
- Microsoft Defender for Endpoint for servers
- [Microsoft Defender for Business servers](/en-us/defender-business/get-defender-business#how-to-get-microsoft-defender-for-business-servers) (for small and medium-sized businesses only)