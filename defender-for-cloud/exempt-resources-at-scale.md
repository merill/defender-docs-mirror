---
layout: Conceptual
title: Exempt resources at scale - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/exempt-resources-at-scale
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
description: Create exemptions at scale in Microsoft Defender for Cloud to exclude resources or recommendations from unhealthy status and secure score impact across subscriptions or management groups.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: de44916f-00ca-17de-1abc-57f22891d6d0
document_version_independent_id: 5b473f1a-43c9-0b26-1b24-32814b8c588f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/exempt-resources-at-scale.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/exempt-resources-at-scale
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/exempt-resources-at-scale.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 26c1d858-30d8-cc11-dcf2-ce055d8d1ac6
---

# Exempt resources at scale - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud shows affected resources through recommendations. Sometimes, a resource doesn't need to be included, or a recommendation appears in a scope where it isn't relevant.

For example, Defender for Cloud might not track a remediation process, or a specific subscription might not need a recommendation. Organizations might also accept risk for specific resources or recommendations. In these cases, create exemptions at scale to:

- Prevent a resource from being listed as unhealthy or affecting the secure score by excluding it. Defender for Cloud marks it as "not applicable" and displays the selected justification.
- Prevent a recommendation from affecting the secure score or appearing again by excluding a subscription or management group.
- Prevent a recommendation or resource from being listed as unhealthy. Apply the exemption to the required scope and mark the item as "mitigated" or "risk accepted".

Resource exemption is limited to 5,000 resources per subscription. If you add more than 5,000 exemptions per subscription, you might experience load issues on the exemption page.

## Create exemptions at scale

To tailor your security posture, create exemptions for recommendations that aren't applicable or are already mitigated.

To create exemptions at scale:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Environment settings** &gt; **Exemptions**.

    [![Screenshot that shows where the exemptions button is located on the environment settings screen.](media/exempt-resources-at-scale/exemptions.png)](media/exempt-resources-at-scale/exemptions.png#lightbox)
4. Select **+ Create**.
5. Enter an exemption name and, optionally, a description.

    [![Screenshot that shows the exemption creation screen.](media/exempt-resources-at-scale/create-exemption.png)](media/exempt-resources-at-scale/create-exemption.png#lightbox)
6. Select a cloud platform.
7. Select a management group, subscription, or resource (per subscription).
8. Select a category:

    - **Mitigated (resolved through a third-party service)**
    - **Waiver (risk accepted)**
9. (Optional) Select an expiry date.
10. Select **Next**.
11. Select one of the following options:

    - **Selected recommendations** and the specific recommendations to exempt.
    - **Recommendation category** and the category to exempt.
12. Select **Next**.
13. Select **Create**.

The exemption is created and applied to the selected resources or recommendations.

To view or manage existing exemptions, return to the **Exemptions** page in the Defender for Cloud menu. Select the ellipsis (**...**) next to the exemption you want to manage. You can then edit or delete the exemption as needed.