---
layout: Conceptual
title: Migrate servers from Microsoft Defender for Endpoint to Microsoft Defender for Servers - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/migrating-mde-server-to-cloud
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to migrate servers from Microsoft Defender for Endpoint for servers to Microsoft Defender for Servers.
author: limwainstein
ms.author: lwainstein
ms.topic: how-to
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: migrationguides, msecd-doc-authoring-1016
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: be998c87-a4f7-6003-9730-da37578a4888
document_version_independent_id: be998c87-a4f7-6003-9730-da37578a4888
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/migrating-mde-server-to-cloud.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: migrating-mde-server-to-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/migrating-mde-server-to-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 8111520d-b645-1ac3-6999-0a2d9f0f4dc1
---

# Migrate servers from Microsoft Defender for Endpoint to Microsoft Defender for Servers - Microsoft Defender for Endpoint | Microsoft Learn

This article describes how to migrate your servers from Defender for Endpoint to Defender for Servers. Before you begin, review the prerequisites and migration steps for your server type.

[Defender for Endpoint](microsoft-defender-endpoint) is an endpoint security platform. It helps organizations prevent, detect, and respond to advanced threats. With a Defender for Endpoint for servers license, you can onboard a server to Defender for Endpoint.

[Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview) is part of [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction). Defender for Cloud provides cloud security posture management (CSPM) and cloud workload protection (CWP). It finds weak spots in your cloud setup and helps protect workloads across multicloud and hybrid environments.

Both products offer server protection, but Defender for Servers is our primary solution to protect servers.

## How do I migrate my servers from Defender for Endpoint to Defender for Cloud?

If you have servers onboarded to Defender for Endpoint, the migration steps depend on the machine type. However, all machines share a set of prerequisites. Defender for Cloud is a subscription-based service in the [Microsoft Azure portal](https://portal.azure.com). You must enable Defender for Cloud and a Defender for Servers plan (Plan 1 or Plan 2) on your Azure subscriptions.

### Before you enable Defender for Cloud

Before you enable Defender for Cloud, it's important to know how to manage antivirus policies and define any needed exclusions. See the following articles:

- [Use Microsoft Defender for Endpoint Security Settings Management to manage Microsoft Defender Antivirus](/en-us/intune/intune-service/protect/mde-security-integration)
- [Manage Microsoft Defender Antivirus in your business](configuration-management-reference-microsoft-defender-antivirus)
- [Defender for Endpoint exclusions](defender-endpoint-exclusions-overview)
- [Managing exclusions reference](defender-endpoint-exclusions-configuration-reference)
- [Troubleshoot performance issues related to real-time protection](troubleshoot-performance-issues)
- [Review event logs and error codes to troubleshoot issues with Microsoft Defender Antivirus](troubleshoot-microsoft-defender-antivirus)

### Enable Defender for Servers for Azure VMs and non-Azure machines

To enable Defender for Servers for Azure VMs and non-Azure servers connected through [Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/overview), follow this guidance:

1. If you aren't already using Azure, plan your environment following the [Azure Well-Architected Framework](/en-us/azure/architecture/framework/).
2. Enable [Defender for Cloud](/en-us/azure/defender-for-cloud/get-started) on your subscription.
3. [Enable a Defender for Servers plan on your subscription](/en-us/azure/defender-for-cloud/enable-enhanced-security). In case you're using Defender for Servers Plan 2, make sure to also enable it on the Log Analytics workspace your machines are connected to. Enabling Defender for Servers Plan 2 on the Log Analytics workspace lets you use optional features, like [File Integrity Monitoring](/en-us/azure/defender-for-cloud/file-integrity-monitoring-overview).
4. Make sure the [Defender for Endpoint integration](/en-us/azure/defender-for-cloud/integration-defender-for-endpoint) is enabled on your subscription. If you have preexisting Azure subscriptions, you might see one or both opt-in buttons for **Allow MDE access to EWACS data** and **Allow MDE Unified Agent for EWACS** as shown in the following image:

    [![Screenshot that shows how to enable Defender for Endpoint integration.](media/mde-integration.png)](media/mde-integration.png#lightbox)

    If you see either of these opt-in buttons in your environment, make sure to enable integration for both. On new subscriptions, both options are enabled by default, and the buttons don't appear.
5. If you plan to use Azure Arc, check that the connectivity requirements are met. Defender for Cloud requires all on-premises and non-Azure machines to connect through the Azure Arc agent. Azure Arc doesn't support every operating system that Defender for Endpoint supports. For planning help, see [Azure Arc deployments](/en-us/azure/azure-arc/servers/plan-at-scale-deployment).
6. (*Recommended*) If you want to see vulnerability findings in Defender for Cloud, make sure to enable [vulnerability assessment](/en-us/azure/defender-for-cloud/monitoring-components?tabs=autoprovision-va#vulnerability-assessment) in Defender for Cloud.

    [![Screenshot that shows how to enable vulnerability management.](media/enable-threat-and-vulnerability-management.png)](media/enable-threat-and-vulnerability-management.png#lightbox)

## How do I migrate existing Azure VMs to Defender for Cloud?

For Azure VMs, no extra steps are required. These devices are automatically onboarded to Defender for Cloud because of the native integration between the Azure platform and Defender for Cloud.

See [Connect your non-Azure machines to Microsoft Defender for Cloud with Defender for Endpoint](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint).

## How do I migrate on-premises machines to Defender for Servers?

For on-premises machines, you have several onboarding options:

- Use direct onboarding in Defender for Cloud. See [Connect your non-Azure machines to Microsoft Defender for Cloud with Defender for Endpoint](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint).
- Create a connection to Azure using Azure Arc. See [Connect your non-Azure machines to Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/quickstart-onboard-machines).

## How do I migrate VMs from AWS or GCP environments?

If you're using Amazon Web Services (AWS) or Google Cloud Platform (GCP), follow these steps to migrate those VMs:

1. Create a multicloud connector on your subscription. To learn more, see [AWS accounts](/en-us/azure/defender-for-cloud/quickstart-onboard-aws?pivots=env-settings) or [GCP projects](/en-us/azure/defender-for-cloud/quickstart-onboard-gcp?pivots=env-settings).
2. On the connector, turn on Defender for Servers for [AWS connectors](/en-us/azure/defender-for-cloud/quickstart-onboard-aws?pivots=env-settings#prerequisites) or [GCP connectors](/en-us/azure/defender-for-cloud/quickstart-onboard-gcp?pivots=env-settings#configure-the-servers-plan).
3. Turn on autoprovisioning on the connector for the Azure Arc agent, the Defender for Endpoint extension, and Vulnerability Assessment. If you use Defender for Servers Plan 2, also turn on agentless machine scanning.

    [![Screenshot that shows how to enable autoprovisioning for Azure Arc agent.](media/select-plans-aws-gcp.png)](media/select-plans-aws-gcp.png#lightbox)

To learn more about multicloud support and onboarding non-Azure machines, see [Defender for Cloud's multicloud capabilities](https://aka.ms/mdcmc) and [Connect your non-Azure machines to Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/quickstart-onboard-machines).

## What happens once all migration steps are completed?

After you complete the migration steps, Defender for Cloud deploys the Defender for Endpoint extension for Windows (`MDE.Windows`) or Linux (`MDE.Linux`) to your Azure VMs and Arc-connected non-Azure machines. This includes VMs in AWS and GCP.

The extension serves as a management interface. It wraps the Defender for Endpoint install scripts inside the operating system and reports its status to the Azure management plane. If Defender for Endpoint is already installed, the process detects it and connects it to Defender for Cloud by adding Defender for Endpoint service tags.

Some devices might run Windows Server 2012 R2 or Windows Server 2016 with the legacy, Log Analytics-based Defender for Endpoint solution. For these devices, Defender for Cloud deploys the Defender for Endpoint [unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2). It then stops and disables the legacy process (`MsSense.exe`) on those machines.