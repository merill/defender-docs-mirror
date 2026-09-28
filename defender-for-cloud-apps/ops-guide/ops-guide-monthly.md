---
layout: Conceptual
title: Monthly operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ops-guide/ops-guide-monthly
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides monthly operational recommendations to help security operations teams to plan and run security activities.
ms.date: 2023-12-13T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: d013ad97-10b6-01cd-a28a-6a1fc88602e8
document_version_independent_id: d013ad97-10b6-01cd-a28a-6a1fc88602e8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ops-guide/ops-guide-monthly.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-monthly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ops-guide/ops-guide-monthly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: dd83717e-f396-4489-290c-f6cf732b2862
---

# Monthly operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn

This article lists monthly operational activities that we recommend you perform with Microsoft Defender for Cloud Apps.

Monthly activities can be performed more frequently or as needed, depending on your environment and needs.

## Review policy assessments

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Policies &gt; Policy management**

**Persona**: Security and Compliance administrators

Review the policies and make any necessary updates to ensure they're still appropriate for your organization.

- **Check for false positive and benign true positive rates, and adjust policies where rates are too high**. For example, ensure that any new corporate IP address is properly configured in your Defender for Cloud Apps settings to avoid impossible travel false positives.
- **Review business needs and assess requirements for custom policies**. For example, is the threat detected by each policy still relevant? Or is there a new, built in solution to detect that threat?
- **Clear old alerts**. For example:

    1. View alerts from the last six months. Filter out alerts that are marked as *Resolved*, and group similar alerts to make viewing simpler.
    2. Verify why each alert displayed isn't addressed.
    3. If alerts are benign, dismiss them and adjust policies as needed.

For more information, see [Control cloud apps with policies](../control-cloud-apps-with-policies).

## Review activity logs

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), under **Cloud apps**, select **Activity log**.

**Persona**: Security and Compliance administrators

You frequently review activity logs in relation to alerts and as part of threat investigations. We recommend revisiting the Activity log monthly to check for repeated activities by the same entity, such as multiple searches or sign-ins by the same user.

1. Pivot results by activity type, such as failed sign-ins, or deleting or assigning privileges.
2. Narrow down activity to an app or a user.
3. Use the results to create a new policy to help you monitor more closely and respond to potential threats.

For more information, see [Activity queries](../activity-filters-queries#activity-queries).