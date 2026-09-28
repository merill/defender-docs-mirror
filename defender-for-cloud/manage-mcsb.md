---
layout: Conceptual
title: Manage the Microsoft Cloud Security Benchmark in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/manage-mcsb
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
description: Learn how to manage Microsoft Cloud Security Benchmark recommendations, configure parameters, and resolve policy conflicts in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 4fc8ad3e-8864-4cb7-9621-a64f265cfe59
document_version_independent_id: 0e539882-50c5-7b83-fffb-de8218eb09f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/manage-mcsb.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/manage-mcsb
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/manage-mcsb.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 448e8faa-f8ed-bbfa-4d45-20ed6beb727d
---

# Manage the Microsoft Cloud Security Benchmark in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud assesses resources against [security policies and standards in Defender for Cloud](security-policy-concept). By default, when you onboard cloud accounts to Defender for Cloud, the [Microsoft Cloud Security Benchmark (MCSB) standard](concept-regulatory-compliance) is enabled. Defender for Cloud starts assessing the security posture of your resource against controls in the MCSB standard, and issues security recommendations based on the assessments.

This article describes how you can manage recommendations provided by MCSB.

## Prerequisites

There are two specific roles in Defender for Cloud that can view and manage security elements:

- **Security reader**: Has rights to view Defender for Cloud items such as recommendations, alerts, policy, and health. Can't make changes.
- **Security admin**: Has the same view rights as *security reader*. Can also update security policies, and dismiss alerts.

### Deny and enforce recommendations

- **Deny** is used to prevent deployment of resources that don't comply with MCSB. For example, if you have a Deny control that specifies that a new storage account must meet a certain criteria, a storage account can't be created if it doesn't meet that criteria.
- **Enforce** lets you take advantage of the **DeployIfNotExist** effect in Azure Policy, and automatically remediate noncompliant resources upon creation.

    Note

    Enforce and Deny are applicable to Azure recommendations and are supported on a subset of recommendations.

To review which recommendations you can deny and enforce, in the **Security policies** page, on the **Standards** tab, select **Microsoft cloud security benchmark** and drill into a recommendation to see if the deny or enforce actions are available.

## Manage recommendation settings

Note

If you disable a recommendation, you also disable all its subrecommendations.

**Disabled** and **Deny** effects are available only for the Azure environment.

1. In the Defender for Cloud portal, open **Environment settings**.
2. Select the cloud account or management account where you want to manage MCSB recommendations.
3. Open **Security policies**, and select the MCSB standard. Turn on the standard.
4. Select the ellipses &gt; **Manage recommendations**.

    [![Screenshot showing the manage effect and parameters screen for a given recommendation.](media/manage-mcsb/select-benchmark.png)](media/manage-mcsb/select-benchmark.png#lightbox)
5. Next to the relevant recommendation, select the ellipses menu, and then select **Manage effect and parameters**.

    - To turn on a recommendation, select **Audit**.
    - To turn off a recommendation, select **Disabled**.
    - To deny or enforce a recommendation, select **Deny**.

### Enforce a recommendation

You can only enforce a recommendation from the recommendation details page.

1. In the Defender for Cloud portal, open the **Recommendations** page, and select the relevant recommendation.
2. In the top menu, select **Enforce**.

    [![Screenshot showing how to enforce a given recommendation.](media/manage-mcsb/enforce-recommendation.png)](media/manage-mcsb/enforce-recommendation.png#lightbox)
3. Select **Save**.

The enforce setting takes effect immediately, but recommendations update based on their freshness interval, up to 12 hours.

## Modify additional recommendation parameters

You might want to configure extra parameters for some recommendations. For example, diagnostic logging recommendations have a default retention period of one day. You can change the default retention period value.

In the recommendation details page, the **Additional parameters** column indicates whether a recommendation has associated extra parameters.

- **Default**. The recommendation runs with the default configuration.
- **Configured**. The recommendation's configuration is modified from its default values.
- **None**. The recommendation doesn't require any extra configuration.

1. Next to the MCSB recommendation, select the ellipses menu, and then select **Manage effect and parameters**.
2. In **Additional parameters**, configure the available parameters with new values.
3. Select **Save**.

If you want to revert changes, select **Reset to default** to restore the default value for the recommendation.

## Identify conflicts between recommendation settings

Potential conflicts can arise when you have multiple assignments of standards with different values.

1. To identify conflicts in effect actions, in **Add**, select **Effect conflict** &gt; **Has conflict** to identify any conflicts.

    [![Screenshot showing how to manage assignment of standards with different values.](media/manage-mcsb/effect-conflict.png)](media/manage-mcsb/effect-conflict.png#lightbox)
2. To identify conflicts in additional parameters, in **Add**, select **Additional parameters conflict** &gt; **Has conflict** to identify any conflicts.
3. If conflicts are found, in **Recommendation settings**, select the required value, and save.

All standard assignments in the selected scope are aligned with the value you selected in **Recommendation settings**, resolving the conflict.