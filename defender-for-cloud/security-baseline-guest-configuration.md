---
layout: Conceptual
title: Set up Azure Policy Guest Configuration on Machines Protected by Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/security-baseline-guest-configuration
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
description: Learn how to install the guest configuration on machines protected by Microsoft Defender for Cloud to assess operating system misconfiguration.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: b41154b1-3fff-5b0d-a989-b1e5763e8803
document_version_independent_id: 69c9db2b-a246-7ea1-44cb-cfb5e488dea0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/security-baseline-guest-configuration.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/security-baseline-guest-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/security-baseline-guest-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: a6ae3800-fe11-3dbd-a198-3c33e5d737f8
---

# Set up Azure Policy Guest Configuration on Machines Protected by Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud assesses operating system configuration against the [Windows security baseline](/en-us/azure/governance/policy/samples/guest-configuration-baseline-windows) and [Linux security baseline](/en-us/azure/governance/policy/samples/guest-configuration-baseline-linux) compute security baselines in the [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction).

The Azure machine configuration extension, formerly known as the Azure Policy guest configuration, collects the information needed for assessment.

This article describes how to deploy the Azure machine configuration extension.

## Prerequisites

| Requirement | Details |
| --- | --- |
| **Plan** | To receive operating system recommendations based on MCSB compute security baselines, enable [Defender for Servers Plan 2](defender-for-servers-overview). |
| **Machine support** | Review supported Azure virtual machines (VMs) and Azure Arc VMs running [Windows machine support](support-matrix-defender-for-servers#windows-machine-support) and [Linux machine support](support-matrix-defender-for-servers#linux-machine-support). |
| **Extension requirements** | Review [extension deployment requirements](/en-us/azure/governance/machine-configuration/overview#enable-machine-configuration) for Azure VMs. |
| **Permissions** | To view the recommendations and explore the operating system baseline data, you need **Read** permission on the relevant Azure subscription. |

Note

Collection by using the machine configuration extension replaces the older method of data collection that used the Log Analytics agent, also known as the Microsoft Monitoring Agent (MMA). Use of the MMA was supported until November 2024.

## Install on AWS/GCP

For Amazon Web Services (AWS) or Google Cloud Platform (GCP) machines, the machine configuration is installed by default when you select **Arc provisioning** in the [onboard AWS machines](quickstart-onboard-aws) or [onboard GCP machines](quickstart-onboard-gcp) connector.

## Install on on-premises machines

For on-premises machines, the machine configuration is enabled by default when you [onboard on-premises VMs as Azure Arc-enabled VMs](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).

## Install on Azure machines

When you enable Defender for Servers Plan 2, you can install the machine configuration extension on machines by using a Defender for Cloud recommendation.

1. Search for the appropriate recommendations.

    - **Azure machines**: Search for the recommendation [Guest Configuration extension should be installed on machines](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/6c99f570-2ce7-46bc-8175-cde013df43bc).
    - **Azure VMs**: On Azure VMs only, you must assign a managed identity to the machine. To do this, search for the recommendation [virtual machines Guest Configuration extension should be deployed with system-assigned managed identity](https://portal.azure.com/#blade/Microsoft_Azure_Security/RecommendationsBlade/assessmentKey/69133b6b-695a-43eb-a763-221e19556755)
2. Remediate the recommendations as needed.

### Autoprovision the guest configuration extension

For Azure VMs, you can autoprovision the guest configuration extension on Azure VMs across the entire subscription.

1. In Defender for Cloud, open **Environment settings** &gt; **Your subscription** &gt; **Settings & Monitoring**.
2. Under **Settings**, select **Guest Configuration**.

    [![Screenshot that shows the location of the settings and monitoring button.](media/prepare-deprecation-log-analytics-mma-agent/setting-and-monitoring.png)](media/prepare-deprecation-log-analytics-mma-agent/setting-and-monitoring.png#lightbox)
3. Toggle the Guest Configuration agent (preview) to **On**.

    [![Screenshot that shows the location of the toggle button to enable the Guest Configuration agent.](media/prepare-deprecation-log-analytics-mma-agent/toggle-guest.png)](media/prepare-deprecation-log-analytics-mma-agent/toggle-guest.png#lightbox)
4. Select **Continue**.

With the machine configuration extension enabled on a machine, that machine can be assessed against [Windows security baseline](/en-us/azure/governance/policy/samples/guest-configuration-baseline-windows) and [Linux security baseline](/en-us/azure/governance/policy/samples/guest-configuration-baseline-linux).