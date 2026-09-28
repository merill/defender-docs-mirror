---
layout: Conceptual
title: Identity Security Initiative - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/identity-security-initiative
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to enhance your organization's identity security using the Identity Security Initiative in Microsoft Defender XDR.
ms.topic: overview
ms.date: 2025-04-05T00:00:00.0000000Z
ms.reviewer: AbbyMSFT
ms.custom: sfi-image-nochange
locale: en-us
document_id: bb3cfb26-0fcb-025e-a6b7-5c0f05c25557
document_version_independent_id: bb3cfb26-0fcb-025e-a6b7-5c0f05c25557
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/identity-security-initiative.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-security-initiative
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/identity-security-initiative.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 05a358e4-b2a1-19c3-3f4b-80c4013c2030
---

# Identity Security Initiative - Microsoft Defender for Identity | Microsoft Learn

Identity security is the practice of protecting the digital identities of individuals and organizations. This includes protecting passwords, usernames, and other credentials that can be used to access sensitive data or systems. Identity security is essential for protecting against a wide range of cyber threats, including phishing, malware, and data breaches.

## Prerequisites

- Your organization must have a Microsoft Defender for Identity license.
- [Review prerequisites and permissions needed](/en-us/security-exposure-management/prerequisites) for working with Security Exposure Management.

## View Identity Security Initiatives

1. Navigate to the [Microsoft Defender portal](https://security.microsoft.com/).
2. From the Exposure management section on the navigation bar, select **Exposure insights** **&gt;** **Initiatives** to open the Identity Security page.

    [![Screenshot showing the Identity security initiative page.](media/identity-security-initiative/screenshot-of-the-identity-security-initiative-page.png)](media/identity-security-initiative/screenshot-of-the-identity-security-initiative-page.png#lightbox)

## Review security metrics

Metrics in security initiatives help you to measure exposure risk for different areas within the initiative. Each metric gathers together one or more recommendations for similar assets. Metrics can be associated with one or more initiatives.

On the **Metrics** tab of an initiative, or in the Metrics section of Exposure Insights, you can see the metric state, its effect, and relative importance in an initiative, and recommendations to improve the metric. We recommend that you prioritize metrics with the highest impact on Initiative Score level. This composite measure considers both the weight value of each recommendation and the percentage of noncompliant recommendations.

[![Screenshot showing the security metrics page.](media/identity-security-initiative/screenshot-of-the-security-metrics-page.png)](media/identity-security-initiative/screenshot-of-the-security-metrics-page.png#lightbox)

| Metric property | Description |
| --- | --- |
| **Metric name** | The name of the metric. |
| **Progress** | Shows the improvement of the exposure level for the metric from 0 (high exposure) to 100 (no exposure). |
| **State** | Shows if the metric needs attention or if the target was met. |
| **Total assets** | Total number of assets under the metric scope. |
| **Recommendations** | Security recommendations associated with the metric. |
| **Weight** | The relative weight (importance) of the metric within the initiative, and its effect on the initiative score. Shown as High, Medium, and Low. It can also be defined as Risk accepted. |
| **14-day trend** | Shows the metric value changes over the last 14 days. |
| **Last updated** | Shows a timestamp of when the metric was last updated. |

Note

The Affected assets experience isn't fully supported during the Preview phase.

## View Identity security recommendations

The Security recommendations tab displays a list of prioritized remediation actions related to your identity security posture. Each recommendation is evaluated for compliance and mapped to its corresponding risk impact, workload, and domain. This view helps you triage and take action based on urgency and business relevance.

[![Showing showing the security recommendations page.](media/identity-security-initiative/screenshot-showing-the-security-recommendations-page.png)](media/identity-security-initiative/screenshot-showing-the-security-recommendations-page.png#lightbox)

Sort the recommendations by any of the headings or filter them based on your task needs.

| **Column** | **Description** |
| --- | --- |
| **Name** | The name of the recommended action (for example, *Configure VPN integration*, *Enable MFA*). |
| **State** | Indicates whether the recommendation is *Compliant* or *Not Compliant*. |
| **Impact** | The security impact level (Low, Medium, or High) of implementing the recommendation. |
| **Workload** | The Microsoft service area the recommendation applies to (for example, Defender for Identity, Microsoft Entra ID). |
| **Domain** | The security domain (for example, identity, apps) associated with the recommendation. |
| **Last calculated** | The most recent time the recommendation's status was evaluated. |
| **Last state change** | When the recommendation’s compliance state last changed. |
| **Related initiatives** | Number of security initiatives impacted by this recommendation. |
| **Related metrics** | Number of security metrics that this recommendation contributes to. |

Security Exposure Management categorizes recommendations by compliance status, as follows:

- **Compliant**: Indicates that the recommendation was implemented successfully.
- **Not complaint**: Indicates that the recommendation wasn't fixed.

## Set target score

You can set a customized target score for the initiative, taking your organization’s unique set of circumstances, priorities, and risk appetite into account.

To set a target store, select the initiative, and then select **Set target score** from the top of the initiative pane.

[![Screenshot showing the set target score button.](media/identity-security-initiative/set-target-score.png)](media/identity-security-initiative/set-target-score.png#lightbox)