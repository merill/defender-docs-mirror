---
layout: Conceptual
title: Critical assets protection (Preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/critical-assets-protection
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
description: Learn how to identify and protect your critical assets in Microsoft Defender for Cloud with Microsoft Security Exposure Management.
ms.topic: concept-article
ms.date: 2025-05-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: f77b8015-2615-de8a-c00e-47abf9da0258
document_version_independent_id: 6ba51854-7070-213e-7c3e-904ce2849d1b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/critical-assets-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/critical-assets-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/critical-assets-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 436305e3-0c3c-039f-b1eb-f39436dde966
---

# Critical assets protection (Preview) - Microsoft Defender for Cloud | Microsoft Learn

Critical assets protection enables security administrators to automatically tag the "crown jewel" resources that are most critical to their organizations, allowing Defender for Cloud to provide them with the highest level of protection and prioritize security issues on these assets above anything else.

Defender for Cloud suggests pre-defined classification rules that were developed by our research team to discover critical assets automatically, and allows you to create custom classification rules based on your business and organizational conventions.

Critical asset rules are bi-directionally synced with Microsoft Security Exposure Management - rules that were created in Microsoft Security Exposure Management are synced to Defender for Cloud, and vice versa. [Learn more about critical assets protection in Microsoft Security Exposure Management](/en-us/security-exposure-management/critical-asset-management).

## Availability

| Aspect | Details |
| --- | --- |
| Release state | General Availability |
| Prerequisites | Defender Cloud Security Posture Management (CSPM) enabled |
| Required Microsoft Entra ID built-in roles: | To create/edit/read classification rules: Security Operator or higher  To read classification rules: Global Reader, Security Reader |
| Clouds: | All commercial clouds |

## Set up critical asset rules

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment Settings**.
3. Select the **Resource criticality** tile.

    [![Screenshot of the resource criticality tile.](media/critical-assets-protection/resource-criticality-tile.png)](media/critical-assets-protection/resource-criticality-tile.png#lightbox)
4. The **Critical asset management** pane opens. Select **Open Microsoft Defender portal.**"

    [![Screenshot of the critical asset management pane.](media/critical-assets-protection/critical-asset-management-pane.png)](media/critical-assets-protection/critical-asset-management-pane.png#lightbox)
5. You then arrive at the **Critical asset management** page in the **Microsoft Defender XDR** portal.

    [![Screenshot of critical asset management page.](media/critical-assets-protection/critical-asset-management-page.png)](media/critical-assets-protection/critical-asset-management-page.png#lightbox)
6. To create custom critical asset rules to tag your resources as **Critical resources** in Defender for Cloud, select the **Create a new classification** button.

    [![Screenshot of Create a new classification button.](media/critical-assets-protection/create-new-classification.png)](media/critical-assets-protection/create-new-classification.png#lightbox)
7. Add a name and description for your new classification, and use under **Query builder**, select **Cloud resource** to build your critical assets rule. Then select **Next**.

    [![Screenshot of how to create critical asset classification.](media/critical-assets-protection/create-critical-asset-classification.png)](media/critical-assets-protection/create-critical-asset-classification.png#lightbox)
8. On the **Preview assets** page, you can see a list of assets that match the rule you created. After reviewing the page, select **Next**.

    [![Screenshot of Preview assets page, showing a list of all assets that match the rule.](media/critical-assets-protection/preview-assets.png)](media/critical-assets-protection/preview-assets.png#lightbox)
9. On the **Assign criticality** page, assign the criticality level to all assets matching the rule. Then select **Next**.

    [![A screenshot of the Assign criticality page.](media/critical-assets-protection/assign-criticality.png)](media/critical-assets-protection/assign-criticality.png#lightbox)
10. You can then see the **Review and finish** page. Review the results, and once you approve, select **Submit**.

    [![Screenshot of the Review and finish page.](media/critical-assets-protection/review-finish.png)](media/critical-assets-protection/review-finish.png#lightbox)
11. After you select **Submit**, you can close the **Microsoft Defender XDR** portal. You should wait for up to two hours until all assets matching your rule are tagged as **Critical**.

Note

Your critical asset rules apply to all the resources in the tenant that match the rule's condition.

## View and protect your critical assets in Defender for Cloud

1. Once your assets are updated, go to the [Attack path analysis](how-to-manage-attack-path) page in Defender for Cloud. You can see all the attack paths to your critical assets.

    [![Screenshot of attack path analysis page.](media/critical-assets-protection/attack-path-analysis.png)](media/critical-assets-protection/attack-path-analysis.png#lightbox)
2. If you select an attack path title, you can see its details. Select the target, and under **Insights - Critical resource**, you can see the critical asset tagging information.

    [![Screenshot of critical resource insights.](media/critical-assets-protection/critical-resource-insights.png)](media/critical-assets-protection/critical-resource-insights.png#lightbox)
3. In the **Recommendations** page of Defender for Cloud, select the **Preview available** banner to see all the recommendations, which are now prioritized based on asset criticality.

    [![Screenshot of the recommendations page, showing critical resources.](media/critical-assets-protection/recommendations-page.png)](media/critical-assets-protection/recommendations-page.png#lightbox)
4. Select a recommendation, and then choose the **Graph** tab. Then choose the target, and select the **Insights** tab. You can see the critical asset tagging information.

    [![Screenshot of critical asset insights for recommendations.](media/critical-assets-protection/recommendation-insights.png)](media/critical-assets-protection/recommendation-insights.png#lightbox)
5. In the **Inventory** page of Defender for Cloud, you can see the critical assets in your organization.

    [![Screenshot of inventory page with critical assets tagged.](media/critical-assets-protection/inventory-page.png)](media/critical-assets-protection/inventory-page.png#lightbox)
6. To run custom queries on your critical assets, go to the **Cloud Security Explorer** page in Defender for Cloud.

    [![Screenshot of Cloud Security Explorer page with query for critical assets.](media/critical-assets-protection/cloud-security-explorer-page.png)](media/critical-assets-protection/cloud-security-explorer-page.png#lightbox)