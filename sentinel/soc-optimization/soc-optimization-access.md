---
layout: Conceptual
title: Optimize security operations | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/soc-optimization/soc-optimization-access
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: yohasson
description: Use Microsoft Sentinel SOC optimization recommendations to optimize your security operations center (SOC) team activities.
ms.author: monaberdugo
author: mberdugo
ms.collection:
- usx-security
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 04afaee2-dc28-952d-e56f-cfe6a06fa23c
document_version_independent_id: aef16cfa-9ab7-e5ca-4756-858074a4dbd2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/soc-optimization/soc-optimization-access.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/soc-optimization/soc-optimization-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/soc-optimization/soc-optimization-access.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 55205b7e-37a8-a28a-0221-e839230503bc
---

# Optimize security operations | Microsoft Learn

Security operations center (SOC) teams look for ways to improve processes and outcomes and ensure you have the data needed to address risks without extra ingestion costs. SOC teams want to make sure that you have all the necessary data to act against risks, without paying for *more* data than needed. At the same time, SOC teams must also adjust security controls as threats and business priorities change, doing so quickly and efficiently to maximize your return on investment.

SOC optimizations are actionable recommendations that surface ways that you can optimize your security controls, gaining more value from Microsoft security services as time goes on. Recommendations help you reduce costs without affecting SOC needs or coverage, and can help you add security controls and data where needed. These optimizations are tailored to your environment and based on your current coverage and threat landscape.

Use SOC optimization recommendations to help you close coverage gaps against specific threats and tighten your ingestion rates against data that doesn't provide security value. SOC optimizations help you optimize your Microsoft Sentinel workspace, without having your SOC teams spend time on manual analysis and research.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

Watch the following video for an overview and demo of SOC optimization in the Microsoft Defender portal. If you just want a demo, jump to minute 8:14. 

## Prerequisites

Before you use SOC optimization, make sure the following prerequisites are in place:

- SOC optimization uses standard Microsoft Sentinel roles and permissions. For more information, see [Roles and permissions in Microsoft Sentinel](../roles).
- To use SOC optimization in the Defender portal, onboard Microsoft Sentinel to the Defender portal. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

## Access the SOC optimization page

Choose the instructions for your portal — Microsoft Defender portal or Azure portal. When your workspace is onboarded to the Defender portal, SOC optimizations include coverage from across Microsoft security services.

# [Defender portal](#tab/defender-portal)
In the Defender portal, select **SOC optimization**.

[![Screenshot of the SOC optimization page in the Defender portal.](media/soc-optimization-access/soc-optimization-xdr.png)](media/soc-optimization-access/soc-optimization-xdr.png#lightbox)

# [Azure portal](#tab/azure-portal)
In Microsoft Sentinel in the Azure portal, under **Threat management**, select **SOC optimization**.

![Screenshot of the SOC optimization page in the Azure portal.](media/soc-optimization-access/soc-optimization-azure.png)

---

## Understand SOC optimization overview metrics

Optimization metrics shown at the top of the **Overview** tab give you a high level understanding of how efficiently you're using your data, and will change over time as you implement recommendations.

Supported metrics at the top of the **Overview** tab include:

# [Defender portal](#tab/defender-portal)
In the Defender portal, the **Overview** tab shows the following optimization metrics:

| Title | Description |
| --- | --- |
| **Recent optimization value** | Shows value gained based on recommendations you recently implemented |
| **Data ingested** | Shows the total data ingested in your workspace over the last 90 days. |
| **Threat-based coverage optimizations** | Shows one of the following coverage indicators, based on the number of analytics rules found in your workspace, compared with the number of rules recommended by the Microsoft research team: - **High**: Over 75% of recommended rules are activated - **Medium**: 30%-74% of recommended rules are activated - **Low**: 0%-29% of recommended rules are activated. Select **View all threat scenarios** to view the full list of relevant threat and risk-based scenarios, active and recommended detections, and coverage levels. Then, select a threat scenario to drill down for more details about the recommendation on a separate, threat scenario details page. |
| **Optimization status** | Shows the number of recommended optimizations that are currently active, completed, and dismissed. |

# [Azure portal](#tab/azure-portal)
In the Azure portal, the **Overview** tab includes the following optimization metrics:

| Title | Description |
| --- | --- |
| **Ingested data over the last 3 months** | Shows the total data ingested in your workspace over the last three months. |
| **Optimizations status** | Shows the number of recommended optimizations that are currently active, completed, and dismissed. |

Select **See all threat scenarios** to view the full list of relevant threat and risk-based scenarios, percentages of active and recommended analytics rules, and coverage levels.

---

## View and manage optimization recommendations

Use the following views to locate and review SOC optimization recommendations in each portal.

# [Defender portal](#tab/defender-portal)
In the Defender portal, SOC optimization recommendations are listed in the **Your Optimizations** area on the **SOC optimizations** tab.

[![Screenshot of the SOC optimization Overview tab in the Defender portal.](media/soc-optimization-access/soc-optimization-overview-defender.png)](media/soc-optimization-access/soc-optimization-overview-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
In the Azure portal, SOC optimization recommendations are listed on the **SOC optimization &gt; Overview** tab.

For example:

[![Screenshot of the SOC optimization Overview tab in the Azure portal.](media/soc-optimization-access/soc-optimization-overview-azure.png)](media/soc-optimization-access/soc-optimization-overview-azure.png#lightbox)

---

SOC optimization recommendations are calculated every 24 hours. Each optimization card includes the status, title, the date it was created, a high-level description, and the workspace it applies to.

### Filter optimizations

Filter the optimizations based on optimization type, or search for a specific optimization title using the search box on the side. Optimization types include:

- **Coverage**: Includes recommendations to help you close coverage gaps against specific threats and tighten your ingestion rates against data that doesn't provide security value. Coverage recommendations include:
    - **Threat-based recommendations** for adding security controls to help close coverage gaps for various types of attacks.
    - **AI MITRE ATT&CK recommendations** for adding tagging recommendations to help close coverage gaps for various types of attacks, based on the MITRE ATT&CK framework.
    - **Risk-based recommendations** for adding security controls to help close coverage gaps for various types of business risks.
- **Data value**: Includes recommendations that suggest ways to improve your data usage for maximizing security value from ingested data, or suggest a better data plan for your organization.

### View optimization details and take action

Choose the instructions for your portal — Microsoft Defender portal or Azure portal:

# [Defender portal](#tab/defender-portal)
1. In each optimization card, select **View details** to see a full description of the observation that led to the recommendation, and the value you see in your environment when that recommendation is implemented.
2. For threat-based coverage optimizations:

    - Toggle between the spider charts to understand your coverage across different tactics and techniques, based on the user-defined and out-of-the-box detections active in your environment.
    - Select **View threat scenario in MITRE ATT&CK** to jump to the [**MITRE ATT&CK** page in Microsoft Sentinel](../mitre-coverage?tabs=defender-portal), prefiltered for your threat scenario. For more information, see [Understand security coverage by the MITRE ATT&CK® framework](../mitre-coverage).
3. Scroll down to the bottom of the optimization details pane for a link to where you can take the recommended actions. For example:

    - If an optimization includes recommendations to add analytics rules, select **Go to Content Hub**.
    - If an optimization includes recommendations to move a table to basic logs, select **Change plan**.
    - For threat-based coverage optimizations, select **View full threat scenario** to see the full list of relevant threats, active and recommended detections, and coverage levels. From there you can jump directly to the **Content hub** to activate any recommended detections, or to the **MITRE ATT&CK** page to view the [full MITRE ATT&CK coverage for the selected scenario](../mitre-coverage?tabs=defender-portal#view-current-mitre-coverage). For example:

    [![Screenshot of the SOC optimization threat scenario page.](media/soc-optimization-access/threat-scenario-page.png)](media/soc-optimization-access/threat-scenario-page.png#lightbox)

# [Azure portal](#tab/azure-portal)
In each optimization card, select **View details** to see a full description of the observation that led to the recommendation, and the value you see in your environment when that recommendation is implemented.

Scroll down to the bottom of the details pane for a link to where you can take the recommended actions. For example:

- If an optimization includes recommendations to add analytics rules, select **Go to Content Hub**.
- If an optimization includes recommendations to move a table to basic logs, select **Change plan**.

---

If you install an analytics rule template from the Content hub without the solution installed, only the installed template appears in the solution.

Install the full solution to see all available content items from the selected solution. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy).

### Manage optimizations

By default, optimization statuses are **Active**. Change their statuses as your teams progress through triaging and implementing recommendations.

Either select the options menu or select **View details** to take one of the following actions:

| Action | Description |
| --- | --- |
| **Complete** | Complete an optimization when you completed each recommended action. If a change in your environment is detected that makes the recommendation irrelevant, the optimization is automatically completed and moved to the **Completed** tab. For example, you might have an optimization related to a previously unused table. If your table is now used in a new analytics rule, the optimization recommendation is now irrelevant. When an environment change makes a recommendation irrelevant, a banner shows in the **Overview** tab with the number of automatically completed optimizations since your last visit. |
| **Mark as in progress** / **Mark as active** | Mark an optimization as in progress or active to notify other team members that you're actively working on it. Use these two statuses flexibly, but consistently, as needed for your organization. |
| **Dismiss** | Dismiss an optimization if you're not planning to take the recommended action and no longer want to see it in the list. |
| **Provide feedback** | We invite you to share your thoughts on the recommended actions with the Microsoft team! When sharing your feedback, be careful not to share any confidential data. For more information, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement). |

## View completed and dismissed optimizations

If you marked a specific optimization as *Completed* or *Dismissed*, or if an optimization is automatically completed, it's listed on the **Completed** and **Dismissed** tabs, respectively.

On the **Completed** or **Dismissed** tab, either select the options menu or select **View full details** to take one of the following actions:

- **Reactivate the optimization**, sending it back to the **Overview** tab. Reactivated optimizations are recalculated to provide the most updated value and action. Recalculating these details can take up to an hour, so wait before checking the details and recommended actions again.

    Reactivated optimizations might also move directly to the **Completed** tab if, after recalculating the details, they're found to be no longer relevant.
- **Provide further feedback** to the Microsoft team. When sharing your feedback, be careful not to share any confidential data. For more information, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).

## SOC optimization usage flow

The following sample flow shows how to use SOC optimizations in either the Defender or Azure portal:

1. On the **SOC optimization** page, start by understanding the dashboard:

    - Observe the top metrics for overall optimization status.
    - Review optimization recommendations for data value and threat-based coverage.
2. Use the optimization recommendations to identify tables with low usage, indicating that they're not being used for detections. Select **View full details** to see the size and cost of unused data. Consider one of the following actions:

    - Add analytics rules to use the table for enhanced protection. To use this option, select **Go to the Content Hub** to view and configure specific out-of-the-box analytic rule templates that use the selected table. In the Content hub, you don't need to search for the relevant rule, as you're taken directly to the relevant rule.

        If new analytic rules require extra log sources, consider ingesting them to improve threat coverage.

        For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy) and [Detect threats out-of-the-box](../detect-threats-built-in).
    - Change your commitment tier for cost savings. For more information, see [Reduce costs for Microsoft Sentinel](../billing-reduce-costs).
3. Use the optimization recommendations to improve coverage against specific threats. For example, for a human-operated ransomware optimization:

    1. Select **View full details** to see the current coverage and suggested improvements.
    2. Select **View all MITRE ATT&CK technique improvement** to drill down and analyze the relevant tactics and techniques, helping you understand the coverage gap.
    3. Select **Go to Content hub** to view all recommended security content, filtered specifically for this optimization.
4. After configuring new rules or making changes, mark the recommendation as completed or let the system update automatically.