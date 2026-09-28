---
layout: Conceptual
title: Protect your Applications with Microsoft Defender for App Service - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-app-service-plan
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
description: Learn how to enable the Microsoft Defender for App Service plan on your Azure subscription to detect threats targeting your web apps and APIs.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ca0234ce-f549-6076-5cb3-bac753f27499
document_version_independent_id: 3d608c76-1d2b-7081-0210-92d38e8a7161
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-app-service-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-app-service-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-app-service-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 9624f900-e75e-6f44-420e-884d1b8559cc
---

# Protect your Applications with Microsoft Defender for App Service - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for App Service uses cloud scale to identify attacks that target applications running on [Azure App Service](https://azure.microsoft.com/services/app-service/). Requests to Azure applications pass through gateways that inspect and log traffic before routing it to your environment. The logged traffic data helps identify exploits and attackers, and it helps learn new patterns.

When you enable Defender for App Service, you get these capabilities:

- **Secure**: Defender for App Service assesses the resources covered by your App Service plan and generates security recommendations based on its findings. Use the detailed instructions in these recommendations to harden your App Service resources.
- **Detect**: Defender for App Service detects many threats to your App Service resources by monitoring:

    - The virtual machine (VM) instance in which your App Service runs and its management interface
    - The requests and responses sent to and from your App Service apps.
    - The underlying sandboxes and VMs.
    - App Service internal logs, which are available because of the visibility that Azure has as a cloud provider.

As a cloud-native solution, Defender for App Service can identify attack methods that apply to multiple targets. From a single host, a single host can't easily identify a distributed attack from a small subset of Internet Protocol (IP) addresses that crawl similar endpoints across multiple hosts.

Together, the log data and infrastructure can show the full attack story, from a new attack in the wild to compromises on customer machines. Even if you deploy Microsoft Defender for App Service after a web app is exploited, it might still detect ongoing attacks.

Learn more about Defender for Cloud pricing on the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Prerequisites

- Use an Azure subscription. If you don't have one, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Enable [Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- Use an App Service plan on any App Service tier.

    For more information on App Service plans and tiers, see [Azure App Service plans](/en-us/azure/app-service/overview-hosting-plans).
- For billing details, Defender for App Service billing applies for all App Service plan tiers. Billing is calculated according to the total compute instances for all App Service plan tiers.
- For deep alert investigation, consider enabling diagnostic settings on your App Service resources so you can review HTTP traffic, application events, and platform activity during incidents. Consider your expected log volume and destination because these diagnostics can incur additional storage costs. For investigation guidance specific to Defender for App Service, see [App Service diagnostics for alert investigation](defender-for-app-service-introduction#app-service-diagnostics-for-alert-investigation). For setup steps and destination options, see [Enable diagnostic logging for apps in Azure App Service](/en-us/azure/app-service/troubleshoot-diagnostic-logs).

## Enable the Defender for App Service plan

When you enable Defender for Cloud, you can add the Defender for App Service plan to your subscription to get security monitoring and threat detection for your web apps and application programming interfaces (APIs).

To enable Defender for App Service on your subscription:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant subscription.
5. On the Defender plans page, toggle the App Service plan to **On**.

    [![Screenshot of the Microsoft Defender for Cloud Environment settings page showing the Defender plans section with the App Service plan toggle switched to On.](media/tutorial-enable-app-service-plan/enable-app-service.png)](media/tutorial-enable-app-service-plan/enable-app-service.png#lightbox)
6. Select **Save**.