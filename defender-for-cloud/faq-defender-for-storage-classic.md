---
layout: FAQ
title: Common questions -  Defender for Storage classic - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-storage-classic
summary: >
  <p>Get answers to common questions about Microsoft Defender for Storage classic.</p>
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
description: Get answers to frequently asked questions about Microsoft Defender for Storage classic.
ms.topic: faq
ms.date: 2025-02-05T00:00:00.0000000Z
locale: en-us
document_id: e3406983-02b2-734a-1ac8-b361f54c5442
document_version_independent_id: fcb61f53-fdd5-037a-075f-5909c7cb1a51
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-storage-classic.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-storage-classic
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-storage-classic.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 51edc4b3-96d8-285c-77b1-df3a3f9665d8
---

# Common questions -  Defender for Storage classic - Microsoft Defender for Cloud | Microsoft Learn

Get answers to common questions about Microsoft Defender for Storage classic.

## Are there differences in features between the new Defender for Storage plan and the legacy Defender for Storage Classic plan?

Yes. The new Defender for Storage plan offers additional security capabilities, such as near real-time malware scanning and sensitive data threat detection. This plan also provides a more predictable pricing structure for better control over coverage and costs. Learn more about the [benefits of migrating to the new plan](defender-for-storage-classic-migrate).

## How do I estimate charges at the account level?

To get an estimate of Defender for Storage classic costs, use the [Price Estimation Workbook](https://portal.azure.com/#blade/AppInsightsExtension/UsageNotebookBlade/ComponentId/Azure%20Security%20Center/ConfigurationId/community-Workbooks%2FAzure%20Security%20Center%2FPrice%20Estimation/Type/workbook/WorkbookTemplateName/Price%20Estimation) in the Azure portal.

## Can I exclude a specific Azure Storage account from a protected subscription?

Yes, you can [exclude specific storage accounts](defender-for-storage-classic-enable#exclude-a-storage-account-from-a-protected-subscription-in-the-per-transaction-plan) from protected subscriptions in Defender for Storage (classic).

## Can I switch from the per-transaction pricing in Defender for Storage (classic) to the new Defender for Storage plan?

Yes, you can move to the new Defender for Storage plan with per-storage account pricing through the Azure portal or other supported methods. This change isn't automatic, you'll need to actively make the switch. Learn about how to [migrate to the new Defender for Storage](defender-for-storage-classic-migrate).

Note

Once you switch to the new plan, you can no longer revert to the Defender for Storage (classic) per-transaction or per-storage account plans. For more information, visit [migrate to the new plan](https://aka.ms/DF-Storage/NewPlanMigration).

## Can I exclude specific storage accounts from protection in the new Defender for Storage plan?

Yes, the new Defender for Storage plan with per-storage account pricing allows you to exclude and configure specific storage accounts within protected subscriptions. However, you'll need to set up the exclusion again after you migrate to the new plan. Learn about how to [migrate to the new Defender for Storage](defender-for-storage-classic-migrate).

## Can I switch from an existing per-transaction pricing under the Defender for Storage (classic) plan to the new per-storage account pricing under the new Defender for Storage plan?

Yes, you can migrate to the per-storage account pricing under the new Defender for Storage plan in the Azure portal or using any of the supported enablement methods.

## Can I return to per-transaction pricing in the Defender for Storage (classic) plan after switching to per-storage account pricing?

No, once you switch to the new plan, you can no longer revert to the Defender for Storage (classic) per-transaction plan.

## Under the Defender for Storage (classic) per-storage account pricing, can I exclude specific storage accounts from protections?

No, you can only enable per-storage account pricing under the Defender for Storage (classic) plan at the subscription level. All storage accounts in the subscriptions are protected.

## How long does it take for per-storage account pricing to be enabled in the Defender for Storage (classic) plan?

When you enable Microsoft Defender for Storage at the subscription level for per-storage account or per-transaction pricing under the Defender for Storage (classic) plan, it takes up to 24 hours for the plan to be enabled.

## Is there any difference in the feature set of per-storage account pricing compared to the legacy per-transaction pricing in the Defender for Storage (classic) plan?

No. Both per-storage account and per-transaction pricing under the Defender for Storage (classic) plan include the same features. The only difference is the pricing structure.

## How can I estimate the cost for each pricing under the Defender for Storage (classic) plan?

To estimate the cost according to each pricing for your environment under the Defender for Storage (classic) plan, we created a [pricing estimation workbook](https://aka.ms/dfstoragecosttool) and a PowerShell script that you can run in your environment.