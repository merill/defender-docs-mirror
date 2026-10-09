---
layout: Conceptual
title: Review Security Initiatives in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/initiatives
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to effectively manage and track security initiatives using Microsoft Security Exposure Management to improve your organization's security posture.
ai-usage: ai-assisted
ms.topic: how-to
ms.date: 2025-07-30T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fbbb0e89-b35b-7e2c-3cef-5d47c63f9863
document_version_independent_id: fbbb0e89-b35b-7e2c-3cef-5d47c63f9863
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/initiatives.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: initiatives
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/initiatives.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 82196ae3-203b-b0f7-b623-203a2586e167
---

# Review Security Initiatives in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

[Microsoft Security Exposure Management](microsoft-security-exposure-management) offers a focused, metric-driven way of tracking exposure in specific security areas using security initiatives. This article describes how to view initiatives and their scores, set target scores, check score trends and history, and review associated metrics and recommendations. Before you start, review the prerequisites for security initiatives.

## Work with security initiatives

[Microsoft Security Exposure Management](microsoft-security-exposure-management) offers a focused, metric-driven way of tracking exposure in specific security areas using security initiatives. This article describes how to view initiatives and their scores, set target scores, check score trends and history, and review associated metrics and recommendations. Before you start, make sure you understand [security initiatives](exposure-insights-overview#security-initiatives) and review the [prerequisites and permissions needed](prerequisites) for working with Security Exposure Management.

## Prerequisites

Before working with security initiatives, review the following prerequisites and notes:

- Learn about [security initiatives in Exposure insights](exposure-insights-overview#security-initiatives) before you start.
- [Review prerequisites and permissions needed](prerequisites) for working with Security Exposure Management.
- Initiatives that are in preview are marked accordingly. These preview initiatives are still in development, and are subject to change.
- Note that with the integration of Defender for Cloud in the Defender portal, some legacy elements have been updated - for example, threat-based initiatives from the initiative catalog might have been temporarily removed and could return in future releases.

## View the security initiatives page

The [Exposure insights initiatives](https://security.microsoft.com/exposure-initiatives) page provides detailed insights into your security initiatives and their progress.

Note

All information shown on the Initiative pages that is related to Endpoints data is based on the user's scope. This includes, initiative scores, metrics progress, and history reasoning.

1. Navigate to the [Microsoft Defender portal](https://security.microsoft.com/).
2. From the Exposure management section on the navigation bar, select **Exposure insights -&gt; Initiatives** to open the [Exposure insights initiatives](https://security.microsoft.com/exposure-initiatives) page.

    ![Screenshot of the Security Exposure Management Initiatives window.](media/initiatives/initiatives-window.png)
3. Use the **Filter by device groups** positioned at the top right corner to refine the filter.

    ![Screenshot of device group filter](media/initiatives/filter-by-dg.png)
4. Choose the device groups relevant for you, and the initiatives data are recalculated (only when related to Endpoints data).

    ![Screenshot of the filter by device groups side pane.](media/initiatives/filter-by-dg-pane.png)
5. Review the initiatives listed on the page by scrolling and drilling down per your needs.
6. To mark an initiative as a favorite on the initiatives page, select the **star** icon in the initiatives window or **Mark as favorite** in the individual initiative.
7. You can review the following information for all initiatives:

    - **14 day change trend graph** highlighting how the initiative score changes over the past 14 days
    - **Initiative name**
    - **Favorite** indicator (toggle on/off)
    - **Current score** of the initiative
    - **Programs** or workloads contributing to or required by this initiative
8. Select an initiative to open the small overview and then select **Open initiative page** to review or remediate issues. The initiative page includes additional information including:

    - Your target score for the initiative
    - A means to set a custom target score appropriate to your organization's needs
    - Description
    - Associated security recommendations
    - All metrics related to the initiative, if applicable.
    - A metric trends graph and drift change, if applicable.
    - History of score changes
    - Related threats

    ![Screenshot of the ransomware initiative.](media/initiatives/initiatives-ransomware.png)

## Set a target score for a security initiative

To set a custom target score for an initiative, follow these steps:

1. To customize your initiative's target score, select **Initiatives.**
2. Select the individual initiative and then **Set target score** to open the set initiative target score window.
3. Set a new target score percentage and select **Apply**.

![Screenshot of the window to set the initiative target.](media/initiatives/set-initiative-target-score.png)

## Review security initiative score trends

The changes in your score provide you with useful feedback about how well you're meeting the goals of your initiatives.

1. From the initiative page for a specific initiative, check the overall **14 day change trend graph** and **14 day drift change** to track the changes in your initiative score, visually and as a percentage.
2. For initiatives with metrics, you can examine the trend and drift data per metric as well.

## Review security initiative history

Use the History view to examine how an initiative score changed over time:

1. Select an initiative to open the small overview and then select **Open initiative page-&gt; History** to view changes over time.
2. Browse to the time table to choose a specific time point to examine.

    1. If needed, filter for specific time points.
    2. Choose the time point and select to examine the percent effect on the initiative score and the reason for the change.
    3. Select a metric to explore the change's effect further, if applicable.
    4. Open the **Changes to exposed assets** dropdown to view up to the top 100 changed assets. The status indicates whether the asset exposure has been added or removed.

[![Screenshot of history side panel](media/exposure-insights-overview/initiatives-history-details-redcued.jpg)](media/initiatives/initiatives-history-details.png#lightbox)

## Review metrics and recommendations

Use the following views to review initiative metrics and related recommendations:

1. To review metrics associated with your initiative, select **Exposure insights -&gt; Initiatives-&gt; Security metrics**.
2. Sort by heading, as needed.
3. Select **Exposure insights &gt; Initiatives &gt; Security recommendations** to view recommendations related to your initiative.

    You only see those recommendations that are *currently* applied to assets and active in Microsoft Secure Score or Microsoft Defender for Cloud.
4. Sort by heading or filter by state, source, impact, workload, or domain, as needed.
5. Select a recommendation, such as a *not compliant* one, and then select **Manage** to remediate the recommendation in the originating workload, such as Microsoft Defender Vulnerability Management.

    ![Screenshot of the initiative's security recommendation tab.](media/initiatives/initiatives-security-recommendations.png)

## Review security events

Security events track initiative and metric score drops to help you understand how they affect your organization's security posture.

1. In the [Microsoft Defender portal](https://security.microsoft.com), select **Exposure management** &gt; **Exposure insights** &gt; **Events** to open the [Events](https://security.microsoft.com/exposure-events) page.
2. Select the time range you need in the calendar drop-down.
3. To filter by initiative score drop events or metric score drop events, select **Filter** or the score drop event quantity.
4. Select a specific event to open it in **Initiatives** or **Metrics**.