---
layout: Conceptual
title: Operating System Misconfigurations - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/operating-system-misconfiguration
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
description: Apply security recommendations to harden operating system baseline configurations with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 896f2949-5c2f-1981-3d9d-184dce6e4974
document_version_independent_id: ce6883e7-7a3d-0d52-4cb2-743a2e5bfdb8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/operating-system-misconfiguration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/operating-system-misconfiguration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/operating-system-misconfiguration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: d5fa1506-f9be-2104-26c5-0033e6b69cd9
---

# Operating System Misconfigurations - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides security recommendations to improve organizational security posture and reduce risk. An important element in risk reduction is to harden machines for your business environment. You can assess and remediate operating system (OS) baseline misconfigurations using the Azure Machine Configuration extension and Defender Vulnerability Management.

## Assessment (Azure Machine Configuration extension)

Defender for Cloud uses [built-in Azure policy initiatives](policy-reference) to assess and apply security configurations. The default initiative is the [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction).

MCSB includes compute security baselines for [Windows](/en-us/azure/governance/policy/samples/guest-configuration-baseline-windows) and [Linux](/en-us/azure/governance/policy/samples/guest-configuration-baseline-linux) operating systems.

These OS baseline recommendations aren't part of the [free security posture features](concept-cloud-security-posture-management#cspm-plans) in Defender for Cloud.

- The recommendations are available when Defender for Servers Plan 2 is enabled.
- When you enable Defender for Servers Plan 2, you also enable relevant Azure policies on the subscription:

    - **Windows machines should meet requirements of the Azure compute security baseline**
    - **Linux machines should meet requirements for the Azure compute security baseline**
- Don't remove these policies. You won't be able to use the machine configuration extension that collects machine data.

### Data collection

The Azure machine configuration extension, formerly known as the Azure Policy guest configuration, runs on the machine and gathers machine information for assessment.

### Installing the machine configuration extension

Install the machine configuration extension as follows:

- **Azure**: On Azure machines, install the extension by remediating the recommendation [Guest Configuration extension should be installed on machines](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/6c99f570-2ce7-46bc-8175-cde013df43bc).
- **AWS/GCP**: On AWS and GCP machines, the machine configuration installs by default when you select Arc provisioning in the [AWS](quickstart-onboard-aws) or [GCP](quickstart-onboard-gcp) connector.
- **On-premises**: For on-premises machines, machine configuration is enabled by default when you [onboard on-premises VMs as Azure Arc-enabled VMs](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).
- **Azure VMs**: On Azure virtual machines (VMs) only, not Arc-enabled VMs, assign a managed identity to the machine by remediating the recommendation [Virtual machines Guest Configuration extension should be deployed with system-assigned managed identity](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/69133b6b-695a-43eb-a763-221e19556755).

### What's not included

This pricing doesn't include other features provided by the machine configuration extension outside Defender for Cloud. These features are subject to Azure Policy machine configuration pricing. For example, [remediation](/en-us/azure/governance/machine-configuration/concepts/remediation-options) and [custom policies](/en-us/azure/governance/machine-configuration/how-to/create-policy-definition). For more information, see [Azure Policy machine configuration pricing details](https://azure.microsoft.com/pricing/details/azure-policy/?msockid=06fc23a2aac2601229353214abbf61f1).

## Assessment (Defender Vulnerability Management)

Defender for Cloud integrates with Microsoft Defender for Endpoint and Microsoft Defender Vulnerability Management. This integration gives machines vulnerability protection and endpoint detection and response (EDR) features.

As part of the integration with Defender Vulnerability Management, it provides [security baselines assessment](/en-us/defender-vulnerability-management/tvm-security-baselines).

Security baselines assessment uses custom baseline profiles. Each profile is a template of device settings and benchmarks to compare them against.

### Supported systems and requirements

The following requirements and limitations apply to security baselines assessment:

- Assessing devices against the Defender Vulnerability Management security baselines assessment profiles is currently available in public preview.
- You must enable Defender for Servers Plan 2 and run the Defender for Endpoint agent on machines you want to assess.
- Assessment supports machines running security baseline profiles:

    - windows\_server\_2008\_r2
    - windows\_server\_2016
    - windows\_server\_2019
    - windows\_server\_2022

### Reviewing recommendations

To review recommendations made by security baseline assessments, search for the recommendation **Machines should be configured securely (powered by MDVM)**, and view the recommendation for all resources.