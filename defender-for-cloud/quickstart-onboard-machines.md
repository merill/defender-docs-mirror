---
layout: Conceptual
title: Connect on-premises machines - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-onboard-machines
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
description: Learn how to connect your non-Azure machines to Microsoft Defender for Cloud and monitor their security posture using Azure Arc and Defender for Endpoint.
ms.topic: install-set-up-deploy
ms.date: 2025-03-13T00:00:00.0000000Z
ms.custom: mode-other
ai-usage: ai-assisted
locale: en-us
document_id: cb148219-4291-6b26-8ac2-6842cbd9badc
document_version_independent_id: e8f34ded-655c-1209-3669-7e468b8fbee8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/quickstart-onboard-machines.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/quickstart-onboard-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/quickstart-onboard-machines.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a35bb124-aa91-9bb5-5d5c-ce2d119996a9
---

# Connect on-premises machines - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud monitors the security posture of non-Azure machines, but first you need to connect them to Azure.

Connect non-Azure computers in any of the following ways:

- Onboarding with Azure Arc:
    - By using Azure Arc-enabled servers (recommended)
    - By using the Azure portal
- [Onboarding directly with Microsoft Defender for Endpoint](onboard-machines-with-defender-for-endpoint)

This article describes the methods for onboarding with Azure Arc.

If you're connecting machines from other cloud providers, see [Connect your AWS account](quickstart-onboard-aws) or [Connect your GCP project](quickstart-onboard-gcp). The multicloud connectors for Amazon Web Services (AWS) and Google Cloud Platform (GCP) in Defender for Cloud handle the Azure Arc deployment for you.

Note

The instructions on this page focus on connecting on-premises machines to Microsoft Defender for Cloud. The same guidance applies to machines in Azure VMware Solution (AVS). Learn more about [integrating Azure VMware Solution machines with Microsoft Defender for Cloud](/en-us/azure/azure-vmware/azure-security-integration).

## Prerequisites

To complete the procedures in this article, you need:

- A Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) set up on your Azure subscription.
- Access to an on-premises machine.

## Connect on-premises machines by using Azure Arc

A machine with [Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/overview) becomes an Azure resource. Once connected to an Azure subscription with Defender for Servers enabled, it appears in Defender for Cloud, like your other Azure resources.

Azure Arc-enabled servers provide enhanced capabilities, such as enabling guest configuration policies on the machine and simplifying deployment with other Azure services. For an overview of the benefits of Azure Arc-enabled servers, see [Supported cloud operations](/en-us/azure/azure-arc/servers/overview#supported-cloud-operations).

Note

As part of the transition to individual recommendations, for AWS EC2 instances connected to Defender for Cloud through Azure Arc, CVE information is populated only on the corresponding Azure Arc-enabled server resource, and not on the AWS EC2 resource.

To deploy Azure Arc on one machine, follow the instructions in [Quickstart: Connect hybrid machines with Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).

To deploy Azure Arc on multiple machines at scale, follow the instructions in [Connect hybrid machines to Azure at scale](/en-us/azure/azure-arc/servers/onboard-service-principal).

## Microsoft Defender for Endpoint integration

Defender for Servers uses an [integration with Microsoft Defender for Endpoint](integration-defender-for-endpoint) to provide real-time threat detection, automated response capabilities, vulnerability assessments, software inventory, and more. To ensure servers are secure and receive all the security benefits of Defender for Servers, verify that the [Defender for Endpoint integration](enable-defender-for-endpoint) is enabled on your subscriptions.

## Verify that your machines are connected

Your Azure and on-premises machines are available to view in one location.

To verify that your machines are connected:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. On the Defender for Cloud menu, select **Inventory** to show the [asset inventory](asset-inventory).
4. Filter the page to view the relevant resource types. These icons distinguish the types:

    ![Defender for Cloud icon for an on-premises machine.](media/quickstart-onboard-machines/security-center-monitoring-icon1.png) Non-Azure machine

    ![Defender for Cloud icon for an Azure machine.](media/quickstart-onboard-machines/security-center-monitoring-icon2.png) Azure VM

    ![Defender for Cloud icon for an Azure Arc-enabled server.](media/quickstart-onboard-machines/arc-enabled-machine-icon.png) Azure Arc-enabled server

## Integrate with Microsoft Defender XDR

When you enable Defender for Cloud, Defender for Cloud's alerts are automatically integrated into the Microsoft Defender Portal.

The integration between Microsoft Defender for Cloud and Microsoft Defender XDR brings cloud environments into Microsoft Defender XDR. With Defender for Cloud's alerts and cloud correlations integrated into Microsoft Defender XDR, SOC teams can now access all security information from a single interface.

Learn more about Defender for Cloud's [alerts in Microsoft Defender XDR](concept-integration-365).

## Clean up resources

There's no need to clean up any resources for this article.