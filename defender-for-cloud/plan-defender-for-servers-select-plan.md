---
layout: Conceptual
title: Select a Defender for Servers plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-select-plan
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
description: This article helps you understand which Defender for Servers plan to deploy in Microsoft Defender for Cloud.
ms.topic: concept-article
ms.date: 2025-02-23T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 37037d89-8567-b057-4ab7-5b4b8394a69a
document_version_independent_id: 102f436d-0352-dfb6-5084-4779159dcb14
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers-select-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers-select-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers-select-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 47886230-d974-301c-0bb7-0970343fb922
---

# Select a Defender for Servers plan - Microsoft Defender for Cloud | Microsoft Learn

This article helps you understand which [Defender for Servers plan](defender-for-servers-overview) to deploy in Microsoft Defender for Cloud.

## Before you begin

This article is the *third* in the Defender for Servers planning guide. Before you begin, review the earlier articles:

1. Start [planning your deployment](plan-defender-for-servers).
2. Review [Defender for Servers access roles](plan-defender-for-servers-roles).

## Review plans

Defender for Servers offers two paid plans:

- **Defender for Servers Plan 1** is entry-level, and focuses on the endpoint detection and response (EDR) capabilities provided by the Defender for Endpoint integration with Defender for Cloud.
- **Defender for Servers Plan 2** provides the same features as Plan 1, and more:

    - [Agentless scanning](concept-agentless-data-collection) for machine posture scanning, vulnerability assessment, threat protection, malware scanning, and secrets scanning.
    - [Compliance assessment](regulatory-compliance-dashboard) against various regulatory standards. Available with Defender for Servers Plan 2 or any other paid plan.
    - Capabilities provided by [premium Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management-capabilities).
    - [A free data ingestion benefit](data-ingestion-benefit) for specific data types.
    - [OS configuration assessment](operating-system-misconfiguration) against compute security baselines in the Microsoft Cloud Security Benchmark.
    - [OS updates assessment](enable-periodic-system-updates) with Azure Updates integrated into Defender for Servers.
    - [File integrity monitoring](file-integrity-monitoring-overview) to examine files and registries for changes that might indicate an attack.
    - [Just-in-time machine access](just-in-time-access-overview) to lock down machine ports and reduce attack surfaces.
    - [Network map](protect-network-resources) to get a geographical view of network recommendations.

For a full list, review [Defender for Servers plan features](defender-for-servers-overview#plan-protection-features).

## Decide on deployment scope

We recommend enabling Defender for Servers at the subscription level, but you can enable and disable Defender for Servers plans at the resource level if you need deployment granularity.

| **Scope** | **Plan 1** | **Plan 2** |
| --- | --- | --- |
| **Enable for Azure subscription** | Yes | Yes |
| **Enable for resource** | Yes | No |
| **Disable for resource** | Yes | Yes |

- Plan 1 can be enabled and disabled at resource level. A server is defined as a device running a server operating system. For information, refer to [Common questions about Defender for Servers](faq-defender-for-servers).
- Plan 2 can't be enabled at the resource level, but you can disable the plan at the resource level.

Here are some use case examples to help you decide on Defender for Servers deployment scope.

| **Use case** | **Enabled in subscription** | **Details** | **Method** |
| --- | --- | --- | --- |
| **Turn on for a subscription** | Yes | We recommend this option. | Turn on in the portal. You can also turn off the plan for an entire subscription in the portal. |
| **Turn on Plan 1 for multiple machines** | No | You can use a script or policy to enable Plan 1 for a group of machines without turning on the plan for an entire subscription. | In the [script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level), specify the relevant machines using a resource tag or resource group. Then follow the on-screen instruction.With the [policy](/en-us/azure/governance/policy/samples/built-in-policies#security-center---granular-pricing), create the assignment on a resource group, or specify the relevant machines using a resource tag. The tag is customer specific. |
| **Turn on Plan 1 for multiple machines** | Yes | If Defender for Servers Plan 2 is enabled in a subscription, you can use a script or policy assignment to downgrade a group of machines to Defender for Servers Plan 1. | In the [script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level), specify the relevant machines using a resource tag or resource group. Then follow the on-screen instruction.With the [policy](/en-us/azure/governance/policy/samples/built-in-policies#security-center---granular-pricing), create the assignment on a resource group, or specify the relevant machines using a resource tag. The tag is customer specific. |
| **Turn on Plan 1 for individual machines** | No | When Defender for Servers isn't enabled in a subscription, you can use the API to turn on Plan 1 for individual machines. | Use the Azure Microsoft Security [Pricings operation group](/en-us/rest/api/defenderforcloud-composite/pricings?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).In [Update Pricings](/en-us/rest/api/defenderforcloud-composite/pricings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true#update-pricing-on-resource-%28example-for-virtualmachines-plan%29), use a PUT request to set the pricingTier property to *standard* and the subplan to **P1**. The pricingTier property indicates whether the plan is enabled on the selected scope. |
| **Turn on Plan 1 for individual machines** | Yes | When Defender for Servers Plan 2 is enabled in a subscription, you can use the API to turn on Plan 1, instead of Plan 2, for individual machines in the subscription. | Use the Azure Microsoft Security [Pricings operation group](/en-us/rest/api/defenderforcloud-composite/pricings?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).In [Update Pricings](/en-us/rest/api/defenderforcloud-composite/pricings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true#update-pricing-on-resource-%28example-for-virtualmachines-plan%29), use a PUT request to set the pricingTier property to *standard* and the subplan to **P1**. The pricingTier property indicates whether the plan is enabled on the selected scope. |
| **Turn off a plan for multiple machines** | Yes/No | Regardless of whether a plan is turned on or off in a subscription, you can turn off the plan for a group of machines. | Use the [script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level) or [policy](/en-us/azure/governance/policy/samples/built-in-policies#security-center---granular-pricing) to specify the relevant machines using a resource tag or resource group. |
| **Turn off a plan for specific machines** | Yes/No | Regardless of whether a plan is turned on or off in a subscription, you can turn off a plan for a specific machine. | In [Update Pricings](/en-us/rest/api/defenderforcloud-composite/pricings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true#update-pricing-on-resource-%28example-for-virtualmachines-plan%29), use a PUT request to set the pricingTier property to *free* and the subplan to **P1**. |
| **Delete the plan configuration on individual machines** | Yes/No | Remove the configuration from a machine to make the subscription-wide setting effective. | In Update Pricings, use a [Delete](/en-us/rest/api/defenderforcloud-composite/pricings/delete?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true) request to remove the configuration. |
| **Delete the plan on multiple resources** |  | Remove the configuration from a group of resources to make the the subscription-wide setting effective. | In the [script](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/Defender%20for%20Servers%20on%20resource%20level), specify the relevant machines using a resource group or tag. Then follow the on-screen instructions. |

[Learn more](tutorial-enable-servers-plan) about how to deploy the plan on a subscription and on specific resources.

## Workspace considerations

Defender for Servers needs a Log Analytics workspace when:

- You deploy Defender for Servers Plan 2 and you want to take advantage of free daily ingestion for specific data types. [Learn more](data-ingestion-benefit).
- You deploy Defender for Servers Plan 2 and you're using file integrity monitoring. [Learn more](file-integrity-monitoring-overview).

## Azure Arc onboarding

We recommend that you onboard machine in non-Azure clouds and on-premises to Azure as Azure Arc-enabled VMs. Enabling as Azure Arc VMs allows machines to take full advantage of Defender for Servers features. Azure Arc-enabled machines have the Azure Arc Connected Machine agent installed on them.

- When you use the Defender for Cloud multicloud connector to connect to [Amazon Web Service (AWS) accounts](quickstart-onboard-aws) and [Google Cloud Platform (GCP) projects](quickstart-onboard-gcp), you can automatically onboard the Azure Arc agent to AWS or GCP servers.
- We recommend that you [onboard on-premises machines as Azure Arc-enabled](quickstart-onboard-machines).
- Although you onboard [on-premises machines by directly installing the Defender for Endpoint agent](onboard-machines-with-defender-for-endpoint) instead of onboarding machines with Azure Arc, Defender for Servers Plan functionality remains available. For Defender for Servers Plan 2, in addition to Plan 1 features, only the premium Defender Vulnerability Management features are available.

Before you deploy Azure Arc:

- [Review a full list](/en-us/azure/azure-arc/servers/prerequisites#supported-operating-systems) of operating systems supported by Azure Arc.
- Review the Azure Arc [planning recommendations](/en-us/azure/azure-arc/servers/plan-at-scale-deployment) and [deployment prerequisites](/en-us/azure/azure-arc/servers/prerequisites).
- [Review networking requirements](/en-us/azure/azure-arc/servers/arc-gateway) for the Connected Machine agent.
- Open the [network ports for Azure Arc](support-matrix-defender-for-servers#network-requirements) in your firewall.
- Review requirements for the Connected Machine agent:
    - [Agent components and data collected from machines](/en-us/azure/azure-arc/servers/agent-overview#agent-resources).
    - [Network and internet access](/en-us/azure/azure-arc/servers/network-requirements) for the agent.
    - [Connection options](/en-us/azure/azure-arc/servers/deployment-options) for the agent.