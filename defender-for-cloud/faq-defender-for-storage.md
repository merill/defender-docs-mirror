---
layout: FAQ
title: Common questions - Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-storage
summary: >
  <p>Get answers to common questions about Microsoft Defender for Storage.</p>
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
description: Get answers to frequently asked questions about Microsoft Defender for Storage.
ms.topic: faq
ms.date: 2025-05-13T00:00:00.0000000Z
locale: en-us
document_id: cc07929f-b406-c3ae-c1b7-dd08a2a1b52b
document_version_independent_id: de59cddd-c2fd-4fc6-faef-37f022a697eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-storage.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-storage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-storage.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a4a9923a-00ca-edf8-bf6c-2ee50297bb6e
---

# Common questions - Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn

Get answers to common questions about Microsoft Defender for Storage.

## Is malware scanning included in the free trial of Defender for Cloud?

Malware scanning in Defender for Storage isn't included for free in the first 30 day trial and is charged from the first day. Defender for Cloud is free for the first 30 days. Any usage beyond 30 days is automatically charged according to the pricing scheme. [Learn more](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

## Is it possible to enable Defender for Storage on a resource level?

Yes, it's possible to enable Defender for Storage at the resource level and set up malware scanning and sensitivity scanning accordingly. Keep in mind that enabling it at the subscription level is the recommended approach, since it automatically protects all new storage accounts.

## Can I exclude certain storage accounts from protection?

Yes, you can exclude storage accounts from protection.

Some storage accounts, such as Azure Databricks DBFS root storage, generate false-positive security recommendations. For guidance on identifying which recommendations to exempt and how to create exemptions using the Azure portal, CLI, or Azure Policy, see [Manage false-positive security recommendations for Defender for Storage](defender-for-storage-false-positive-recommendations).

## How long does it take for subscription-level enablement to take effect?

Enabling Defender for Storage at the subscription level might take up to 24 hours to be fully enabled across all storage accounts.

## Can I switch back to the Defender for Storage (classic)?

No, Once you switch to the new plan, you can no longer revert to the Defender for Storage (classic) per-transaction or per-storage account plans.

If you want to switch back to the Defender for Storage (classic) plan, you need to do two things. First, disable the new Defender for Storage plan that is enabled now. Second, check if there are any policies that can re-enable the new plan and turn them off too. The two Azure built-in policies enabling the new plan are **Configure Microsoft Defender for Storage to be enabled** and **Configure basic Microsoft Defender for Storage to be enabled (Activity Monitoring only).**

Note

After February 5, 2025, you can no longer enable Defender for Storage (classic), the legacy per-transaction pricing plan, in most scenarios. The only exception is for subscriptions that already have the per-transaction pricing enabled. For more information, learn how to [migrate to the new plan](https://aka.ms/DF-Storage/NewPlanMigration).

## How can I calculate the cost Defender for Storage?

To estimate the cost of Defender for Storage and add-ons like malware scanning, we provide a [pricing estimation workbook](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Workbooks/Microsoft%20Defender%20for%20Storage%20Price%20Estimation) that you can deploy in your environment. This workbook also provides visibility into your Defender for Storage and add-ons - malware scanning and sensitivity data discovery - enablement status across subscriptions. For more information about how this workbook works, visit this [Blog Post](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/microsoft-defender-for-storage-price-estimation-dashboard/ba-p/2429724). You can also check out the Defender for Cloud [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/) for more information. You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).