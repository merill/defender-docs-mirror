---
layout: Conceptual
title: Overview of the extensions that collect data from your workloads - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/monitoring-components
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
description: Protect your workloads with Microsoft Defender for Cloud by learning about the extensions that collect data from your workloads.
ms.topic: concept-article
ms.date: 2025-09-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: bdff3e7f-fd94-3a71-c734-7144ac3a4f75
document_version_independent_id: 128e001e-a9b3-2d9b-2a3e-d26b8165f2d8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/monitoring-components.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/monitoring-components
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/monitoring-components.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c5d6595b-1a87-ce7a-550f-2e2a2490e5c9
---

# Overview of the extensions that collect data from your workloads - Microsoft Defender for Cloud | Microsoft Learn

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

Defender for Cloud collects data from your Azure virtual machines (VMs), Virtual Machine Scale Sets, IaaS containers, and non-Azure (including on-premises) machines to monitor for security vulnerabilities and threats. Some Defender plans require monitoring components to collect data from your workloads.

Data collection is required to provide visibility into missing updates, misconfigured OS security settings, endpoint protection status, and health and threat protection. Data collection is only needed for compute resources such as VMs, Virtual Machine Scale Sets, IaaS containers, and non-Azure computers.

You can benefit from Microsoft Defender for Cloud even if you don’t provision agents. However, you have limited security and the capabilities listed aren't supported.

Data is collected using:

- [Azure Monitor Agent (AMA)](auto-deploy-azure-monitoring-agent)
- [Microsoft Defender for Endpoint](integration-defender-for-endpoint) (MDE)
- **Security components**, such as the [Azure Policy for Kubernetes](/en-us/azure/governance/policy/concepts/policy-for-kubernetes)

## Why use Defender for Cloud to deploy monitoring components?

Visibility into the security of your workloads depends on the data that the monitoring components collect. The components ensure security coverage for all supported resources.

To save you the process of manually installing the extensions, Defender for Cloud reduces management overhead by installing all required extensions on existing and new machines. Defender for Cloud assigns the appropriate **Deploy if not exists** policy to the workloads in the subscription. This policy type ensures the extension is provisioned on all existing and future resources of that type.

Tip

Learn more about Azure Policy effects, including **Deploy if not exists**, in [Understand Azure Policy effects](/en-us/azure/governance/policy/concepts/effects).

## What plans use monitoring components?

These plans use monitoring components to collect data:

- Defender for Servers
    - [Azure Arc agent](/en-us/azure/azure-arc/servers/manage-vm-extensions) (For multicloud and on-premises servers)
    - [Microsoft Defender for Endpoint](integration-defender-for-endpoint)
    - Vulnerability assessment
- [Defender for SQL servers on machines](defender-for-sql-on-machines-vulnerability-assessment)
    - [Azure Arc agent](/en-us/azure/azure-arc/servers/manage-vm-extensions) (For multicloud and on-premises servers)
    - Azure Monitor Agent
    - Automatic SQL server discovery and registration
- Defender for Containers
    - [Azure Arc agent](/en-us/azure/azure-arc/servers/manage-vm-extensions) (For multicloud and on-premises servers)
    - [Defender sensor, Azure Policy for Kubernetes, Kubernetes audit log data](defender-for-containers-introduction)

## Availability of extensions

The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

### Azure Monitor Agent (AMA)

| Aspect | Details |
| --- | --- |
| Release state: | Generally available (GA) |
| Relevant Defender plan: | [Defender for SQL Servers on Machines](defender-for-sql-introduction) |
| Required roles and permissions (subscription-level): | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Supported destinations: | ![](media/icons/yes-icon.png) Azure virtual machines![](media/icons/yes-icon.png) Azure Arc-enabled machines |
| Policy-based: | ![](media/icons/yes-icon.png) Yes |
| Clouds: | ![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet |

Learn more about [using the Azure Monitor Agent with Defender for Cloud](auto-deploy-azure-monitoring-agent).

### Microsoft Defender for Endpoint

| Aspect | Linux | Windows |
| --- | --- | --- |
| Release state: | Generally available (GA) | Generally available (GA) |
| Relevant Defender plan: | [Microsoft Defender for Servers](defender-for-servers-introduction) | [Microsoft Defender for Servers](defender-for-servers-introduction) |
| Required roles and permissions (subscription-level): | - To enable/disable the integration: [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin) or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner)- To view Defender for Endpoint alerts in Defender for Cloud: [Security reader](/en-us/azure/role-based-access-control/built-in-roles), [Reader](/en-us/azure/role-based-access-control/built-in-roles), **Resource Group Contributor**, **Resource Group Owner**, [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), **Subscription owner**, or **Subscription Contributor** | - To enable/disable the integration: [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin) or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner)- To view Defender for Endpoint alerts in Defender for Cloud: [Security reader](/en-us/azure/role-based-access-control/built-in-roles), [Reader](/en-us/azure/role-based-access-control/built-in-roles), **Resource Group Contributor**, **Resource Group Owner**, [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), **Subscription owner**, or **Subscription Contributor** |
| Supported destinations: | ![](media/icons/yes-icon.png) Azure Arc-enabled machines![](media/icons/yes-icon.png) Azure virtual machines | ![](media/icons/yes-icon.png) Azure Arc-enabled machines![](media/icons/yes-icon.png) Azure VMs running Windows Server 2022, 2019, 2016, 2012 R2, 2008 R2 SP1, [Azure Virtual Desktop](/en-us/azure/virtual-desktop/overview), [Windows 10 Enterprise multi-session](/en-us/azure/virtual-desktop/windows-10-multisession-faq)![](media/icons/no-icon.png) Azure VMs running Windows 10 |
| Policy-based: | ![](media/icons/no-icon.png) No | ![](media/icons/no-icon.png) No |
| Clouds: | ![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet | ![](media/icons/yes-icon.png) Commercial clouds![](media/icons/yes-icon.png) Azure Government, Microsoft Azure operated by 21Vianet |

Learn more about [Microsoft Defender for Endpoint](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint).

### Vulnerability assessment

| Aspect | Details |
| --- | --- |
| Release state: | Generally available (GA) |
| Relevant Defender plan: | [Microsoft Defender for Servers](defender-for-servers-introduction) |
| Required roles and permissions (subscription-level): | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Supported destinations: | ![](media/icons/yes-icon.png) Azure virtual machines![](media/icons/yes-icon.png) Azure Arc-enabled machines |
| Policy-based: | ![](media/icons/yes-icon.png) Yes |
| Clouds: | ![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet |

### Guest Configuration

| Aspect | Details |
| --- | --- |
| Release state: | Preview |
| Relevant Defender plan: | No plan required |
| Required roles and permissions (subscription-level): | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) |
| Supported destinations: | ![](media/icons/yes-icon.png) Azure virtual machines |
| Clouds: | ![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet |

Learn more about Azure's [Guest Configuration extension](/en-us/azure/governance/machine-configuration/overview).

### Defender for Containers extensions

This table shows the availability details for the components required by the protections offered by [Microsoft Defender for Containers](defender-for-containers-introduction).

By default, the required extensions are enabled when you enable Defender for Containers from the Azure portal.

| Aspect | Azure Kubernetes Service clusters | Azure Arc-enabled Kubernetes clusters |
| --- | --- | --- |
| Release state: | • Defender sensor: GA • Azure Policy for Kubernetes: Generally available (GA) | • Defender sensor: Preview • Azure Policy for Kubernetes: Preview |
| Relevant Defender plan: | [Microsoft Defender for Containers](defender-for-containers-introduction) | [Microsoft Defender for Containers](defender-for-containers-introduction) |
| Required roles and permissions (subscription-level): | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) or [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) |
| Supported destinations: | The AKS Defender sensor only supports [AKS clusters that have RBAC enabled](/en-us/azure/aks/concepts-identity#kubernetes-rbac). | [See Kubernetes distributions supported for Arc-enabled Kubernetes](support-matrix-defender-for-containers) |
| Policy-based: | ![](media/icons/yes-icon.png) Yes | ![](media/icons/yes-icon.png) Yes |
| Clouds: | **Defender sensor**:![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet**Azure Policy for Kubernetes**:![](media/icons/yes-icon.png) Commercial clouds![](media/icons/yes-icon.png) Azure Government, Microsoft Azure operated by 21Vianet | **Defender sensor**:![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet**Azure Policy for Kubernetes**:![](media/icons/yes-icon.png) Commercial clouds![](media/icons/no-icon.png) Azure Government, Microsoft Azure operated by 21Vianet |

Learn more about the [roles used to provision Defender for Containers extensions](permissions#roles-used-to-automatically-configure-agents-and-extensions).

## Troubleshooting

- To identify manual onboarding issues, see [How to troubleshoot Operations Management Suite onboarding issues](https://techcommunity.microsoft.com/t5/system-center-blog/operations-management-suite-onboarding-troubleshooting-steps/ba-p/349464).