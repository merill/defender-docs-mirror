---
layout: Conceptual
title: Review security metrics in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/security-metrics
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to investigate metrics in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2024-11-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 220c65ed-f749-9a24-3aeb-b105ca63f576
document_version_independent_id: 220c65ed-f749-9a24-3aeb-b105ca63f576
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/security-metrics.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-metrics
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/security-metrics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a3b30940-97ba-30d6-8c80-e3019e5fafa9
---

# Review security metrics in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

Security initiative metrics in [Microsoft Security Exposure Management](microsoft-security-exposure-management) measure security exposure for a specific scope of assets or resources within a [security initiative](exposure-insights-overview). Most security initiatives (but not all) have metrics associated with them.

## Prerequisites

- Learn about [security metrics](exposure-insights-overview#working-with-metrics).
- [Review permissions and prerequisites needed](prerequisites) for working with Security Exposure Management.
- Note possible preview issues:
    - Some instances of affected assets information (largely information originating in Secure score) don't appear on the **Affected Assets** tab in an individual metric.
    - Some critical asset information for assets in the **Affected Assets** tab doesn't show.
    - Asset details are calculated on demand.
    - Cloud-related metrics are only available if Microsoft Defender for Cloud is available in the subscription, and the Defender Cloud Security Posture Management (CSPM) plan is enabled.
    - In some cases, metrics are more specific than the scope of the related recommendations. In this case, the asset detail shown doesn't align with the asset details of the related recommendations.
    - If you remove a workload, you can't refresh the metric status and the asset details for the workload's related metrics.

## Review security metrics

1. In the [Microsoft Defender portal](https://security.microsoft.com), select **Exposure management -&gt; Exposure insights -&gt; Metrics** to open the [Metrics](https://security.microsoft.com/exposure-metrics) page.

    ![Screenshot of the metrics page in Microsoft Security Exposure management.](media/metrics.png)
2. Select the metric you want to review.
3. Review the metric properties.

    - **Description**: Metric description.
    - **State**: Current state of metric.
    - **Progress**: Shows the improvement of the exposure level for the metric from 0 (high exposure) to 100 (no exposure).
    - **Last state update**: The last time metric state was updated.
    - **Affected assets**. The number of affected assets out of the total assets.
    - **Weight**: Metric weight which affects the metric impact on initiative score.
    - **Security recommendations**: Recommendations associated with the metric.

## Edit the metric weight

You can customize metric weight according to your business needs.

Note

You must have **Exposure managment (manage)** permissions and access to all assets on the tenant level to edit the weight. For more information, see, [Permissions](prerequisites#permissions)

1. To edit the metric weight, select a specific metric.
2. In the metric properties side panel, select Edit metric, then change the metric weight and apply.
3. To accept the risk described by the metric, set the metric weight to **Risk accepted**.