---
layout: Conceptual
title: Use the Microsoft Sentinel Overview dashboard to view incidents, data, and analytics | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/get-visibility
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
description: Learn how to quickly view and monitor what's happening across your environment by using Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 36fb1c10-0f7d-a2c0-5535-98a873fff334
document_version_independent_id: 34ab4453-4554-871a-3f27-e7e9fea93565
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/get-visibility.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/get-visibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/get-visibility.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 34ea8a51-72c8-433f-2d5c-aa14ea7b4493
---

# Use the Microsoft Sentinel Overview dashboard to view incidents, data, and analytics | Microsoft Learn

Use the Microsoft Sentinel **Overview** page to view, monitor, and analyze activities across your environment. This article describes the widgets and graphs available on Microsoft Sentinel's **Overview** dashboard, including insights into incidents, automation efficiency, data ingestion, and analytics rule status to help you quickly assess the security posture of your environment. Before you start, make sure you meet the prerequisites, including connecting your data sources to Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you access the Overview page, make sure you meet the following prerequisite:

- Make sure that you have reader access to Microsoft Sentinel resources. For more information, see [Roles and permissions in Microsoft Sentinel](roles).

## Access the Overview page

If your workspace is onboarded to the Microsoft Defender portal, select **General &gt; Overview**. Otherwise, select **Overview** directly. For example:

![Screenshot of the Microsoft Sentinel Overview dashboard.](media/get-visibility/dashboard.png)

Data for each section of the Overview dashboard is precalculated, and the last refresh time is shown at the top of each section. Select **Refresh** at the top of the page to refresh the entire page.

## View incident data

To help reduce noise and minimize the number of alerts you need to review and investigate, Microsoft Sentinel uses a fusion technique to correlate alerts into *incidents*. Incidents are actionable groups of related alerts for you to investigate and resolve.

The following image shows an example of the **Incidents** section on the **Overview** dashboard:

[![Screenshot of the Incidents section in the Microsoft Sentinel Overview page.](media/qs-get-visibility/incidents.png)](media/qs-get-visibility/incidents.png#lightbox)

The **Incidents** section lists the following data:

- The number of new, active, and closed incidents over the last 24 hours.
- The total number of incidents of each severity.
- The number of closed incidents of each type of closing classification.
- Incident statuses by creation time, in four hour intervals.
- The mean time to acknowledge an incident and the mean time to close an incident, with a link to the **SOC efficiency** workbook. For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](monitor-your-data).

Select **Manage incidents** to jump to the Microsoft Sentinel **Incidents** page for more details.

## View automation data

After deploying automation with Microsoft Sentinel, monitor your workspace's automation in the **Automation** section of the **Overview** dashboard.

[![Screenshot of the Automation section in the Microsoft Sentinel Overview page.](media/qs-get-visibility/automation.png)](media/qs-get-visibility/automation.png#lightbox)

- Start with a summary of the automation rules activity: Incidents closed by automation, the time the automation saved, and related playbooks health.

    Microsoft Sentinel calculates the time saved by automation by finding the average time that a single automation saved, multiplied by the number of incidents resolved by automation. Microsoft Sentinel uses the following formula to calculate time saved by automation:

    `(avgWithout - avgWith) * resolvedByAutomation`

    Where:

    - **avgWithout** is the average time it takes for an incident to be resolved without automation.
    - **avgWith** is the average time it takes for an incident to be resolved by automation.
    - **resolvedByAutomation** is the number of incidents that are resolved by automation.
- The automation actions graph summarizes the numbers of actions performed by automation, by type of action.
- The section also includes a count of the active automation rules with a link to the **Automation** page.

Select the **configure automation rules** link to the jump the **Automation** page, where you can configure more automation.

## View status of data records, data collectors, and threat intelligence

In the **Data** section of the **Overview** dashboard, track information on data records, data collectors, and threat intelligence.

[![Screenshot of the Data section in the Microsoft Sentinel Overview page.](media/qs-get-visibility/data.png)](media/qs-get-visibility/data.png#lightbox)

View the following details:

- The number of records that Microsoft Sentinel collected in the last 24 hours, compared to the previous 24 hours, and anomalies detected in that time period.
- A summary of your data connector status, divided by unhealthy and active connectors. **Unhealthy connectors** indicate how many connectors have errors. **Active connectors** are connectors with data streaming into Microsoft Sentinel, as measured by a query included in the connector.
- Threat intelligence records in Microsoft Sentinel, by indicator of compromise.

Select **Manage connectors** to jump to the **Data connectors** page, where you can view and manage your data connectors.

## View analytics data

Track data for your analytics rules in the **Analytics** section of the **Overview** dashboard.

![Screenshot of the Analytics section in the Microsoft Sentinel Overview page.](media/qs-get-visibility/analytics.png)

The number of analytics rules in Microsoft Sentinel are shown by status, including enabled, disabled, and autodisabled.

Select the **MITRE view** link to jump to the **MITRE ATT&CK**, where you can view how your environment is protected against MITRE ATT&CK tactics and techniques. Select the **manage analytics rules** link to jump to the **Analytics** page, where you can view and manage the rules that configure how alerts are triggered.