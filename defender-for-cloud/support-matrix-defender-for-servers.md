---
layout: Conceptual
title: Support for the Defender for Servers plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-servers
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
description: Review support requirements, network configurations, and feature support for the "Defender for Servers" plan in Microsoft Defender for Cloud.
ms.topic: limits-and-quotas
ms.custom: linux-related-content
ms.date: 2026-05-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 080fca50-2c2e-ad22-c511-347dc793089b
document_version_independent_id: 80c61f7f-dd2e-6e2e-40c8-41dcf774ce99
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/support-matrix-defender-for-servers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/support-matrix-defender-for-servers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/support-matrix-defender-for-servers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
platformId: 913e4aad-8fd6-4fdc-d98a-b793b922c334
---

# Support for the Defender for Servers plan - Microsoft Defender for Cloud | Microsoft Learn

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

This article summarizes support information for the Defender for Servers plan in Microsoft Defender for Cloud.

Note

This article references CentOS, a Linux distribution that reaches end of support on June 30, 2024. See [End of support guidance](/en-us/azure/virtual-machines/workloads/centos/centos-end-of-life).

## Network requirements

Validate the following endpoints are configured for outbound access so that Azure Arc extension can connect to Microsoft Defender for Cloud to send security data and events:

- For Defender for Server multicloud deployments, make sure that the [addresses and ports required by Azure Arc](/en-us/azure/azure-arc/data/connectivity#details-on-internet-addresses-ports-encryption-and-proxy-server-support) are open.
- For deployments with Google Cloud Platform (GCP) connectors, open port 443 to these URLs:

    - `osconfig.googleapis.com`
    - `compute.googleapis.com`
    - `containeranalysis.googleapis.com`
    - `agentonboarding.defenderforservers.security.azure.com`
    - `gbl.his.arc.azure.com`
- For deployments with Amazon Web Services (AWS) connectors, open port 443 to these URLs:

    - `ssm.<region>.amazonaws.com`
    - `ssmmessages.<region>.amazonaws.com`
    - `ec2messages.<region>.amazonaws.com`
    - `gbl.his.arc.azure.com`

## Azure cloud support

This table summarizes Azure cloud support for Defender for Servers features.

| **Feature/Plan** | **Azure** | **Azure Government** | **Microsoft Azure operated by 21Vianet** **21Vianet** |
| --- | --- | --- | --- |
| [Microsoft Defender for Endpoint integration](integration-defender-for-endpoint) | GA | GA ^1^ | GA |
| [Compliance standards](regulatory-compliance-dashboard)Compliance standards might differ depending on the cloud type. | GA | GA | GA |
| [Machine OS misconfiguration](apply-security-baseline) | GA | GA | GA |
| [Virtual Machines (VM) vulnerability scanning-agentless](concept-agentless-data-collection) | GA | GA | GA |
| [VM vulnerability scanning - Microsoft Defender for Endpoint sensor](deploy-vulnerability-assessment-defender-vulnerability-management) | GA | GA | GA |
| [Just-in-time VM access](just-in-time-access-usage) | GA | GA | GA |
| [File integrity monitoring](file-integrity-monitoring-overview) | GA | GA | GA |
| [Docker host hardening](harden-docker-hosts) | GA | GA | GA |
| [Agentless secret scanning](secrets-scanning) | GA | GA | GA |
| [Agentless malware scanning](agentless-malware-scanning) | GA | GA | GA |
| [Agentless assessment checks for endpoint detection and response solutions](endpoint-detection-response) | GA | GA | GA |
| [System updates and patches](enable-periodic-system-updates) | GA | GA | GA |
| [Kubernetes node protection](kubernetes-nodes-overview) | GA | GA | GA |

1: In Government Community Cloud – Moderate (GCC-M) environments on Azure public cloud, the following Microsoft Defender for Endpoint integrations aren't supported: Direct onboarding, Vulnerability Assessment recommendations, and File Integrity Monitoring (FIM).

## Windows machine support

The following table shows feature support for Windows machines in Azure, Azure Arc, and other clouds.

| **Feature** | **Azure VMs** **[Virtual Machine Scale Sets (Flexible orchestration)](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes#scale-sets-with-flexible-orchestration)**^1^ | **Azure Arc-enabled servers**(including Azure VMware solution) | **Defender for Servers required** |
| --- | --- | --- | --- |
| [Microsoft Defender for Endpoint integration](integration-defender-for-endpoint) | ✔ Available on: Windows Server 2025, 2022, 2019, 2016, 2012 R2, 2008 R2 SP1 | ✔ | Yes |
| [Virtual machine behavioral analytics (and security alerts)](alerts-reference) | ✔ | ✔ | Yes |
| [Fileless security alerts](alerts-windows-machines) | ✔ | ✔ | Yes |
| [Network-based security alerts](other-threat-protections#network-layer) | ✔ | - | Yes |
| [Just-in-time VM access](just-in-time-access-usage) | ✔ | - | Yes |
| [File Integrity Monitoring](file-integrity-monitoring-overview) | ✔ | ✔ | Yes |
| [Regulatory compliance dashboard & reports](regulatory-compliance-dashboard) | ✔ | ✔ | Yes |
| [Docker host hardening](harden-docker-hosts) | - | - | Yes |
| [Missing OS patches assessment](apply-security-baseline) | ✔ | ✔ | Azure: YesAzure Arc-enabled: Yes |
| Security misconfigurations assessment | ✔ | ✔ | Azure: NoAzure Arc-enabled: Yes |
| [Endpoint protection assessment](supported-machines-endpoint-solutions-clouds-servers#supported-endpoint-protection-solutions) | ✔ | ✔ | Azure: NoAzure Arc-enabled: Yes |
| Disk encryption assessment | ✔[supported scenarios](/en-us/azure/virtual-machines/windows/disk-encryption-windows) | - | No |
| Non-Microsoft vulnerability assessment Bring Your Own License (BYOL) | ✔ | - | No |
| [Network security assessment](protect-network-resources) | ✔ | - | No |
| [System updates and patches](enable-periodic-system-updates) | ✔ | ✔ | Yes (Plan 2) |

1: Currently, VM [Scale Sets with Uniform Orchestration](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes#scale-sets-with-uniform-orchestration) have partial feature coverage. The main supported capabilities include agentless detections, such as Network Layer Alerts, Domain Name System (DNS) alerts, and control plane alerts.

## Linux machine support

The following table shows feature support for Linux machines in Azure, Azure Arc, and other clouds.

| **Feature** | **Azure VMs** **[Virtual Machine Scale Sets (Flexible orchestration)](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes#scale-sets-with-flexible-orchestration)**^1^ | **Azure Arc-enabled machines** | **Defender for Servers required** |
| --- | --- | --- | --- |
| [Microsoft Defender for Endpoint integration](integration-defender-for-endpoint) | ✔  ([supported versions](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-linux)) | ✔ | Yes |
| [Virtual machine behavioral analytics (and security alerts)](azure-defender) | ✔ Supported versions | ✔ | Yes |
| [Fileless security alerts](alerts-windows-machines) | - | - | Yes |
| [Network-based security alerts](other-threat-protections#network-layer) | ✔ | - | Yes |
| [Just-in-time VM access](just-in-time-access-usage) | ✔ | - | Yes |
| [File Integrity Monitoring](file-integrity-monitoring-overview) | ✔ | ✔ | Yes |
| [Regulatory compliance dashboard & reports](regulatory-compliance-dashboard) | ✔ | ✔ | Yes |
| [Docker host hardening](harden-docker-hosts) | ✔ | ✔ | Yes |
| [Missing OS patches assessment](apply-security-baseline) | ✔ | ✔ | Azure: YesAzure Arc-enabled: Yes |
| Security misconfigurations assessment | ✔ | ✔ | Azure: NoAzure Arc-enabled: Yes |
| [Endpoint protection assessment](supported-machines-endpoint-solutions-clouds-servers#supported-endpoint-protection-solutions) | - | - | No |
| Disk encryption assessment | ✔[supported scenarios](/en-us/azure/virtual-machines/windows/disk-encryption-windows) | - | No |
| Non-Microsoft vulnerability assessment (BYOL) | ✔ | - | No |
| [Network security assessment](protect-network-resources) | ✔ | - | No |
| [System updates and patches](enable-periodic-system-updates) | ✔ | ✔ | Yes (Plan 2) |

1: Currently, VM [Scale Sets with Uniform Orchestration](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes#scale-sets-with-uniform-orchestration) have partial feature coverage. The main supported capabilities include agentless detections, such as Network Layer Alerts, DNS alerts, and control plane alerts.

## Multicloud machines

The following table shows feature support for AWS and GCP machines.

| **Feature** | **Availability in AWS** | **Availability in GCP** |
| --- | --- | --- |
| [Microsoft Defender for Endpoint integration](integration-defender-for-endpoint) | ✔ | ✔ |
| [Virtual machine behavioral analytics (and security alerts)](alerts-reference) | ✔ | ✔ |
| Control plane security alerts | - | - |
| [Fileless security alerts](alerts-windows-machines) | ✔ | ✔ |
| [Network-based security alerts](other-threat-protections#network-layer) | - | - |
| [Just-in-time VM access](just-in-time-access-usage) | ✔ | - |
| [File Integrity Monitoring](file-integrity-monitoring-overview) | ✔ | ✔ |
| [Regulatory compliance dashboard & reports](regulatory-compliance-dashboard) | ✔ | ✔ |
| [Docker host hardening](harden-docker-hosts) | ✔ | ✔ |
| [Missing OS patches assessment](apply-security-baseline) | ✔ | ✔ |
| Security misconfigurations assessment | ✔ | ✔ |
| [Endpoint protection assessment](supported-machines-endpoint-solutions-clouds-servers#supported-endpoint-protection-solutions) | ✔ | ✔ |
| Disk encryption assessment | ✔for [supported scenarios](/en-us/azure/virtual-machines/windows/disk-encryption-windows) | ✔for [supported scenarios](/en-us/azure/virtual-machines/windows/disk-encryption-windows) |
| Third-party vulnerability assessment | - | - |
| [Network security assessment](protect-network-resources) | - | - |
| [Cloud security explorer](how-to-manage-cloud-security-explorer) | ✔ | - |
| [Agentless secret scanning](secrets-scanning) | ✔ | ✔ |
| [Agentless malware scanning](agentless-malware-scanning) | ✔ | ✔ |
| [Endpoint detection and response](endpoint-detection-response) | ✔ | ✔ |
| [System updates and patches](enable-periodic-system-updates) | ✔  (With Azure Arc) | ✔ (With Azure Arc) |