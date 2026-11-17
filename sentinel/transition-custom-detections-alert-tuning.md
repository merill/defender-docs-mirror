---
layout: Conceptual
title: Tune alerts from migrated custom detections in Microsoft Defender | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-custom-detections-alert-tuning
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
description: Create and validate a temporary alert tuning rule to auto-resolve alerts from migrated custom detections during evaluation in Microsoft Defender.
author: omerbinyamin
ms.author: omerbinyamin
ms.localizationpriority: high
ms.collection: ms-security
ms.topic: how-to
ai-usage: ai-generated
ms.custom: msecd-doc-authoring-1032
ms.date: 2026-11-15T00:00:00.0000000Z
locale: en-us
document_id: 3c33e406-0122-7ce0-defc-54e01e046ad8
document_version_independent_id: 52d5ade2-4d12-cebb-a914-48c7d7c48cd4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-custom-detections-alert-tuning.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-custom-detections-alert-tuning
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-custom-detections-alert-tuning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: fa759975-c481-de8d-e923-5c03f7470458
---

# Tune alerts from migrated custom detections in Microsoft Defender | Microsoft Learn

Create a temporary alert tuning rule to auto-resolve evaluation alerts while you validate migrated custom detections. Migrated custom detections use `#EVAL` in their alert titles during evaluation. Match both the detection source and the title so that the rule doesn't resolve unrelated alerts.

Before you begin, review the access and Preview availability prerequisites.

## Prerequisites

- Access to **Settings &gt; Microsoft Defender XDR &gt; Alert tuning** in the Microsoft Defender portal.
- **Custom detection** available in the **Detection source** list. Detection source selection is a Preview capability, and availability can differ between tenants. Create the rule only after this option appears.
- Migrated custom detections under evaluation, with `#EVAL` in their alert titles.

## Create the temporary tuning rule

Use both matching conditions to restrict the rule to migrated custom detection evaluation alerts.

Important

Alert tuning can change alert visibility, incidents, notifications, and automation. Keep both conditions: **Detection source = Custom detection** and **Alert title** contains `#EVAL`. Don't use the title condition alone.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Settings &gt; Microsoft Defender XDR &gt; Alert tuning**.
3. Select **Create alert tuning rule**.
4. Configure the following values:

    | Setting | Value |
    | --- | --- |
    | **Rule name** | Suppress migrated custom detection evaluation alerts |
    | **Detection source** | **Custom detection** |
    | **Condition** | **Alert title** contains `#EVAL` |
    | **Action** | **Auto-resolve** |
    | **Status** | Enabled only for the migration validation period |
5. Review the scope, create the rule, and confirm that it's enabled.

## Validate matching and incident behavior

Matching alerts should be auto-resolved. Each is expected to create a resolved one-alert, or singleton, incident. Closed incidents aren't reopened or merged, so these evaluation alerts shouldn't correlate between migrated rules or into existing incidents. Validate this behavior in your tenant.

1. **Positive test:** Confirm that a `#EVAL` custom-detection alert is auto-resolved and that its incident is resolved with that alert as its only alert.
2. **Correlation test:** Generate alerts from two different `#EVAL` custom detections. Confirm that they remain in separate resolved singleton incidents and aren't added to an existing incident.
3. **Title test:** Confirm that a custom-detection alert without `#EVAL` isn't auto-resolved by this rule.
4. **Source test:** Confirm that an alert from another detection source isn't auto-resolved by this rule, even if its title contains `#EVAL`.

## Remove the rule after validation

When migration validation is complete, disable or delete the temporary tuning rule. If other migrated detections still use the same rule for evaluation, wait until their validation is complete.