---
layout: Conceptual
title: Detect Internet Exposed IP Addresses - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/detect-exposed-ip-addresses
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
description: Learn how to detect exposed IP addresses with cloud security explorer in Microsoft Defender for Cloud to proactively identify security risks.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 27fa9674-f36b-3371-f482-c8f488f1c426
document_version_independent_id: eccda7ac-1ff2-ba3a-da80-00b951e4ce76
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/detect-exposed-ip-addresses.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/detect-exposed-ip-addresses
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/detect-exposed-ip-addresses.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 7fdc51fa-e872-3fbf-c426-a254b29fc0bd
---

# Detect Internet Exposed IP Addresses - Microsoft Defender for Cloud | Microsoft Learn

This article shows you how to find internet-exposed IP addresses in Microsoft Defender for Cloud. You learn how to use cloud security explorer and attack path analysis to find and prioritize risk.

Defender for Cloud integrates with Microsoft Defender External Attack Surface Management. In cloud security explorer, this capability appears as Defender External Attack Surface Management (DEASM) findings. This integration provides recommendations and attack path visualizations that help reduce risk.

## Prerequisites

Before you begin, make sure that you meet the following requirements:

- You have a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You enabled the [Defender cloud security posture management (Defender CSPM) plan](tutorial-enable-cspm-plan).

## Detect internet exposed IP addresses with the cloud security explorer

Use cloud security explorer to build queries, such as outside-in scans, that detect internet-exposed IP addresses in your environment.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud**, then select **Cloud security explorer**.
3. In the dropdown menu, search for and select **IP addresses**.

    [![Screenshot that shows where to navigate to in Defender for Cloud to search for and select the IP addresses option.](media/detect-exposed-ip-addresses/search-ip-addresses.png)](media/detect-exposed-ip-addresses/search-ip-addresses.png#lightbox)
4. Select **Done**.
5. Select **+**.
6. In the select condition dropdown menu, select **DEASM Findings**.

    [![Screenshot that shows where to locate the DEASM Findings option.](media/detect-exposed-ip-addresses/deasm-findings.png)](media/detect-exposed-ip-addresses/deasm-findings.png#lightbox)
7. Select the **+** button.
8. In the select condition dropdown menu, select **Routes traffic to**.
9. In the select resource type dropdown menu, select **Select all**.

    [![Screenshot that shows where the select all option is located.](media/detect-exposed-ip-addresses/select-all.png)](media/detect-exposed-ip-addresses/select-all.png#lightbox)
10. Select **Done**.
11. Select the **+** button.
12. In the select condition dropdown menu, select **Routes traffic to**.
13. In the select resource type dropdown menu, select **Virtual machine**.
14. Select **Done**.
15. Select **Search**.

    [![Screenshot that shows the fully built query and where the search button is located.](media/detect-exposed-ip-addresses/search-results.png)](media/detect-exposed-ip-addresses/search-results.png#lightbox)
16. Select a result to review the findings.

## Detect exposed IP addresses with attack path analysis

Use attack path analysis to view paths that an attacker could use to reach critical assets.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud**, then select **Attack path analysis**.
3. Search for **Internet exposed**.
4. Review and select a result.
5. [Remediate the attack path](how-to-manage-attack-path#remediate-attack-paths).