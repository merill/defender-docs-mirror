---
layout: Conceptual
title: Prioritize security actions by data sensitivity - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/information-protection
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
description: Use Microsoft Purview's data sensitivity classifications in Microsoft Defender for Cloud
ms.topic: overview
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 008043ec-c120-9fb8-47e1-2cd681f190ae
document_version_independent_id: ec27ea11-ae0e-24e9-4f43-0432e70bd817
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/information-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/information-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/information-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/3f837592-9b7c-422c-82fa-3523042264d7
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/f37b967c-efb8-47e1-9b0d-0ab7670e3db4
platformId: e0f92627-fa8e-4c1d-7ea6-c2c4efb7f42d
---

# Prioritize security actions by data sensitivity - Microsoft Defender for Cloud | Microsoft Learn

[Microsoft Purview Data Catalog](/en-us/azure/purview/overview), Microsoft's data governance service, provides rich insights into the *sensitivity of your data*. With automated data discovery, sensitive data classification, and end-to-end data lineage, Microsoft Purview Data Catalog helps organizations manage and govern data in hybrid and multicloud environments.

Microsoft Defender for Cloud customers using Microsoft Purview Data Catalog can benefit from another important layer of metadata in alerts and recommendations: information about any potentially sensitive data involved. This knowledge helps solve the triage challenge and ensures security professionals can focus their attention on threats to sensitive data.

This page explains the integration of Microsoft Purview Data Catalog in Defender for Cloud.

You can learn more by watching this video from the Defender for Cloud in the Field video series:

- [Integrate Microsoft Purview with Microsoft Defender for Cloud](episode-two)

Note that:

- Microsoft Defender for Cloud also provides data sensitivity context by enabling the sensitive data discovery (preview). Microsoft Purview Data Catalog and Microsoft Defender for Cloud integration offers a complementary source of data context for resources **not** covered by the sensitive data discovery feature.
- Purview Catalog provides data context **only** for resources in subscriptions not onboarded to sensitive data discovery feature or resource types not supported by this feature.
- Data context provided by Purview Catalog is provided as is and does **not** consider the [data sensitivity settings](data-sensitivity-settings).

Learn more in [Data security posture management](concept-data-security-posture).

## Availability

| Aspect | Details |
| --- | --- |
| Release state: | Preview.The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability. |
| Pricing: | You'll need a Microsoft Purview account to create the data sensitivity classifications and run the scans. There's no extra cost incurred for the integration between Purview and Microsoft Defender for Cloud, but the data is shown in Microsoft Defender for Cloud only for enabled plans. |
| Required roles and permissions: | **Security admin** and **Security contributor** |
| Clouds: | ![](media/icons/yes-icon.png) Commercial clouds (Regions: East US, East US 2, West US 2, West Central US, South Central US, Canada Central, Brazil South, North Europe, West Europe, UK South, Southeast Asia, Central India, Australia East) ![](media/icons/no-icon.png) Azure Government![](media/icons/no-icon.png) Microsoft Azure operated by 21Vianet (**Partial**: Subset of alerts and vulnerability assessment for SQL servers. Behavioral threat protections aren't available.) |

## The triage problem and Defender for Cloud's solution

Security teams regularly face the challenge of how to triage incoming issues.

Defender for Cloud includes two mechanisms to help prioritize recommendations and security alerts:

- For recommendations, we've provided **security controls** to help you understand how important each recommendation is to your overall security posture. Defender for Cloud includes a **secure score** value for each control to help you prioritize your security work. Learn more in [Security controls and their recommendations](secure-score-security-controls).
- For alerts, we've assigned **severity labels** to each alert to help you prioritize the order in which you attend to each alert. Learn more in [How are alerts classified?](alerts-overview#how-are-alerts-classified).

However, where possible, you'd want to focus the security team's efforts on risks to the organization's **data**. If two recommendations have equal impact on your secure score, but one relates to a resource with sensitive data, ideally you'd include that knowledge when determining prioritization.

Microsoft Purview's data sensitivity classifications and data sensitivity labels provide that knowledge.

## Discover resources with sensitive data

To provide information about discovered sensitive data and help ensure you have that information when you need it, Defender for Cloud displays information from Microsoft Purview in multiple locations.

Purview Catalog scans produce insights into the nature of the sensitive information so you can take action to protect that information:

- If a resource is scanned by multiple Microsoft Purview accounts, the information shown in Defender for Cloud relates to the most recent scan.
- Classifications and labels are shown for resources that were scanned within the last three months.
- Purview Catalog adds data sensitivity context **only** for resources **not** covered by the [sensitive data discovery (preview)](concept-data-security-posture) feature in Defender for Cloud.

### Alerts and recommendations pages

When you're reviewing a recommendation or investigating an alert, the information about any potentially sensitive data involved is included on the page. You can also filter the list of alerts by **Data sensitivity classifications** and **Data sensitivity labels** to help you focus on the alerts that relate to sensitive data.

This vital layer of metadata helps solve the triage challenge and ensures your security team can focus its attention on the threats to sensitive data.

### Inventory filters

The [asset inventory page](asset-inventory) has a collection of powerful filters to group your resources with outstanding alerts and recommendations according to the criteria relevant for any scenario. These filters include **Data sensitivity classifications** and **Data sensitivity labels**. Use these filters to evaluate the security posture of resources on which Purview Catalog has discovered sensitive data.

[![Screenshot of information protection filters in Microsoft Defender for Cloud's asset inventory page.](media/information-protection/information-protection-inventory-filters.png)](media/information-protection/information-protection-inventory-filters.png#lightbox)

### Resource health

When you select a single resource - whether from an alert, recommendation, or the inventory page - you reach a detailed health page showing a resource-centric view with the important security information related to that resource.

The resource health page provides a snapshot view of the overall health of a single resource. You can review detailed information about the resource and all recommendations that apply to that resource. Also, if you're using any of the Microsoft Defender plans, you can see outstanding security alerts for that specific resource too.

When reviewing the health of a specific resource, you'll see the Purview Catalog information on this page and can use it to determine what data has been discovered on this resource. To explore more details and see the list of sensitive files, select the link to launch Microsoft Purview Data Catalog.

[![Screenshot of Defender for Cloud's resource health page showing information protection labels and classifications from Microsoft Purview.](media/information-protection/information-protection-resource-health.png)](media/information-protection/information-protection-resource-health.png#lightbox)

Note

- If the data in the resource is updated and the update affects the resource classifications and labels, Defender for Cloud reflects those changes only after Purview Catalog rescans the resource.
- If Microsoft Purview account is deleted, the resource classifications and labels are still be available in Defender for Cloud.
- Defender for Cloud updates the resource classifications and labels within 24 hours of the Purview Catalog scan.

## Attack path

Some of the attack paths consider resources that contain sensitive data, such as “AWS S3 Bucket with sensitive data is publicly accessible,” based on Purview Catalog scan results.

## Security explorer

The Cloud Map shows resources that “contains sensitive data,” based on Purview scan results. You can use resources with this label to explore the map.

- To see the classification and labels of the resource, go to the [inventory](asset-inventory).
- To see the list of classified files in the resource, go to the [Microsoft Purview compliance portal](/en-us/azure/purview/overview).

## Learn more

You can check out the following blog:

- [Secure sensitive data in your cloud resources](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/secure-sensitive-data-in-your-cloud-resources/ba-p/2918646).