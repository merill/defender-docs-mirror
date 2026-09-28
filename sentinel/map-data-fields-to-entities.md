---
layout: Conceptual
title: Map Data Fields to Microsoft Sentinel Entities | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/map-data-fields-to-entities
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Map table data fields to Microsoft Sentinel entities in scheduled analytics rules to enrich alerts and incidents with structured investigation data. Includes guidance for adding or updating entity mappings in existing rules.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: fc93f6e5-44a0-65e1-c154-d07104eaeb8e
document_version_independent_id: 8e35cd34-c007-1cbc-0c4f-e19c6b4f56da
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/map-data-fields-to-entities.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/map-data-fields-to-entities
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/map-data-fields-to-entities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 8760b197-eaf3-1c80-0cf6-489eff235972
---

# Map Data Fields to Microsoft Sentinel Entities | Microsoft Learn

Entity mapping is an integral part of the configuration of [scheduled analytics rules](scheduled-rules-overview). It enriches the rules' output (alerts and incidents) with essential information that serves as the building blocks of any investigative processes and remedial actions that follow.

Use the following procedure to add or change entity mappings in an existing analytics rule, or while creating a new scheduled analytics rule.

Important

> 
> - See Notes on the new version for important information about backward compatibility and differences between the new and old versions of entity mapping.
> - After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).
> 

## How to map entities

To map entities in an analytics rule, perform the following steps:

1. Enter the **Analytics** page in the portal through which you access Microsoft Sentinel:

# [Azure portal](#tab/azure)
From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.

# [Defender portal](#tab/defender)
From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.

---
2. Select a scheduled query rule and select **Edit** from the details pane. Or create a new rule by clicking **Create &gt; Scheduled query rule** at the top of the screen.
3. Select the **Set rule logic** tab. If a new rule, type a query in the **Rule query** window.
4. In the **Alert enhancement** section, expand **Entity mapping**.

    ![Expand entity mapping](media/map-data-fields-to-entities/alert-enrichment.png)
5. In the now-expanded **Entity mapping** section, select **Add new entity**.

    ![Screenshot shows how to add a new entity.](media/map-data-fields-to-entities/add-new-entity.png)
6. Select an entity type from the **Entity** drop-down list.

    ![Choose an entity type](media/map-data-fields-to-entities/choose-entity-type.png)
7. Select an identifier for the entity. Identifiers are attributes of an entity that can sufficiently identify it. Choose one from the **Identifier** drop-down list, and then choose a data field from the **Value** drop-down list that will correspond to the identifier. With some exceptions, the **Value** list is populated by the data fields in the table defined as the subject of the rule query.

    You can define up to three identifiers for a given entity mapping. Some identifiers are required, others are optional. You must choose at least one required identifier. If you don't, a warning message will instruct you which identifiers are required. For best results—for maximum unique identification—you should use strong identifiers whenever possible, and using multiple strong identifiers will enable greater correlation between data sources. See the full list of available [entities and identifiers](entities-reference).

    ![Map fields to entities](media/map-data-fields-to-entities/map-entities.png)
8. Select **Add new entity** to map more entities. You can define up to 10 entity mappings in a single analytics rule. You can also map more than one of the same type. For example, you can map two **IP** entities, one from a *source IP address* field and one from a *destination IP address* field. By mapping both fields, you can track both IP entities.

    If you change your mind, or if you made a mistake, you can remove an entity mapping by clicking the trash can icon next to the entity drop-down list.
9. When you have finished mapping entities, click the **Review and create** tab. Once the rule validation is successful, click **Save**.

Note

- *Up to 500 entities collectively* can be identified in a single alert, divided equally across all entity mappings defined in the rule.

    - For example, if two entity mappings are defined in the rule, each mapping can identify up to 250 entities; if five mappings are defined, each one can identify up to 100 entities, and so on.
    - Multiple mappings of a single entity type (say, source IP and destination IP) each count separately.
    - If an alert contains items in excess of this limit, those excess items will not be recognized and extracted as entities.
- The size limit for the entire *entities* area of an alert (the **Entities** field) is *64 KB*.

    - *Entities* fields that grow larger than 64 KB will be truncated. As entities are identified, they are added to the alert one by one until the field size reaches 64 KB, and any entities yet unidentified are dropped from the alert.

## Notes on the new version

The entity mapping experience was updated from an older version. Keep the following backward-compatibility details in mind:

- As the new version is now generally available (GA), the feature-flag workaround to use the old version is no longer available.
- If you had previously defined entity mappings for this analytics rule using the old version, they will be automatically converted to the new version.