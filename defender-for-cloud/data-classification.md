---
layout: Conceptual
title: Classify APIs with sensitive data exposure - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-classification
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
description: Learn how to monitor your APIs for sensitive data exposure.
ms.date: 2025-07-01T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 323b761e-47d7-581f-5b29-5d1aac61ff14
document_version_independent_id: 20e02fe1-4ea2-9107-97c3-5bacf4ec3912
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-classification.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-classification
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-classification.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: ba160752-1cf2-c533-a011-1ca5742deabf
---

# Classify APIs with sensitive data exposure - Microsoft Defender for Cloud | Microsoft Learn

Once your APIs are onboarded, Defender for APIs starts monitoring your APIs for sensitive data exposure. APIs are classified with both built-in and custom sensitive information types and labels as defined by your organization's Microsoft Purview Information Protection (MIP) governance rules. If you don't have MIP Purview configured, APIs are classified with the Microsoft Defender for Cloud default classification rule set with the following features.

Within Defender for APIs inventory experience, you can search for sensitivity labels or sensitive information types by adding a filter to identify APIs with custom classifications and information types.

[![Screenshot showing API inventory list.](media/data-classification/api-inventory.png)](media/data-classification/api-inventory.png#lightbox)

## Explore API exposure through attack paths

When the Defender Cloud Security Posture Management (CSPM) plan is enabled, API attack paths let you discover and remediate the risk of API data exposure. For more information, see [Data security posture management in Defender CSPM](concept-data-security-posture#data-security-posture-management-in-defender-cspm).

1. Select the API attack path **Internet exposed APIs that are unauthenticated carry sensitive data** and review the data path:

    [![Screenshot showing attack path analysis.](media/data-classification/attack-path-analysis.png)](media/data-classification/attack-path-analysis.png#lightbox)
2. View the attack path details by selecting the attack path published.
3. Select the **Insights** resource.
4. Expand the insight to analyze further details about this attack path:

    [![Screenshot showing attack path insights.](media/data-classification/insights.png)](media/data-classification/insights.png#lightbox)
5. For risk mitigation steps, open **Active Recommendations** and resolve unhealthy recommendations for the API endpoint in scope.

## Explore API data exposure through Cloud Security Graph

When the Defender Cloud Security Posture Management CSPM plan is enabled, you can view sensitive APIs data exposure and identify the APIs labels according to your sensitivity settings by adding the following filter:

[![Screenshot of a computer Description automatically generated.](media/data-classification/computer-description.png)](media/data-classification/computer-description.png#lightbox)

## Explore sensitive APIs in security alerts

With Defender for APIs and data sensitivity integration into API security alerts, you can prioritize API security incidents involving sensitive data exposure. For more information, see [Defender for APIs alerts](defender-for-apis-introduction#detect-threats).

In the alert's extended properties, you can find sensitivity scanning findings for the sensitivity context:

- **Sensitivity scanning time UTC**: when the last scan was performed.
- **Top sensitivity label**: the most sensitive label found in the API endpoint.
- **Sensitive information types**: information types that were found, and whether they're based on custom rules.
- **Sensitive file types**: the file types of the sensitive data.

[![Screenshot showing alert details.](media/data-classification/alert-details.png)](media/data-classification/alert-details.png#lightbox)