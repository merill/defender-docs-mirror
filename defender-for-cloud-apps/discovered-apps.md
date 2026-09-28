---
layout: Conceptual
title: View discovered apps on the Cloud discovery dashboard - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/discovered-apps
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
description: Learn how to view cloud discovery insights, app risk levels, top users, and filter dashboard data in Microsoft Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 10d693fc-e579-4a12-0664-fc5c0bbb137a
document_version_independent_id: 10d693fc-e579-4a12-0664-fc5c0bbb137a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/discovered-apps.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discovered-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/discovered-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
platformId: cc1e0cab-0b01-4c41-1511-b169e4c6e475
---

# View discovered apps on the Cloud discovery dashboard - Microsoft Defender for Cloud Apps | Microsoft Learn

The **Cloud discovery** page provides a dashboard designed to give you more insight into how cloud apps are being used in your organization. The dashboard provides an at-a-glance view of the types of apps being used, your open alerts, and the risk levels of apps in your organization. It also shows who your top app users are, and provides an **App headquarter location** map.

Filter your **Cloud discovery** data to generate specific views, depending on what interests you most. For more information, see [Discovered app filters](discovered-app-queries#discovered-app-filters).

## Prerequisites

For information about roles required, see [Manage admin access](manage-admins).

## Review the cloud discovery dashboard

This procedure describes how to get an initial, general picture of your cloud discovery apps in the **Cloud discovery** dashboard.

1. In the Microsoft Defender portal, select **Cloud apps &gt; Cloud discovery**.

    For example:

    [![Screenshot of the Cloud discovery dashboard](media/cloud-discovery-dashboard.png)](media/cloud-discovery-dashboard.png#lightbox)

    Supported apps include Windows and macOS apps, which are both listed under the **Defender - managed endpoints** stream.
2. Review the following information:

    1. Use the **High-level usage overview** to understand overall cloud app use in your organization.
    2. Dive one level deeper to understand the **top categories** that used in your org for each of the different use parameters. Note how much of this usage is by sanctioned apps.
    3. Use the **Discovered apps** tab to go even deeper and see all the apps in a specific category.
    4. Check the **top users and source IP addresses** to identify which users are the most dominant users of cloud apps in your organization.
    5. Use the **App headquarters map** to check how the discovered apps spread according to geographic location, according to their headquarter.
    6. Use the **App risk overview** to understand the risk score of discovered apps, and check the **discovery alerts status** to see how many open alerts should you investigate.

## Deep dive into discovered apps

To dive deeper in to cloud discovery data, use the filters to check for risky or commonly used apps.

For example, if you want to identify commonly used, risky cloud storage and collaboration apps, use the **Discovered apps** page to filter for the apps you want. Then, [unsanction or block discovered apps](governance-discovery) as follows:

1. In the Microsoft Defender portal, under **Cloud Apps**, select **Cloud discovery**. Then choose the **Discovered apps** tab.
2. In the **Discovered apps** tab, under **Browse by category** select both **Cloud storage** and **Collaboration**.
3. Use the advanced filters to set **Compliance risk factor** to **SOC 2** = **No**.
4. For **Usage**, set **Users** to greater than 50 users and **Transactions** to greater than 100.
5. Set the **Security risk factor** for **Data at rest encryption** equals **Not supported**. Then set **Risk score** equals 6 or lower.

    [![Screenshot of discovered app filters.](media/discovered-app-filters.png)](media/discovered-app-filters.png#lightbox)

After the results are filtered, [unsanction and block discovered apps](governance-discovery) by using the bulk action checkbox to unsanction all of those apps in one action. Once the apps are unsanctioned, use a blocking script to block those apps from being used in your environment.

You also might want to identify specific app instances that are in use by investigating the discovered subdomains. For example, differentiate between different SharePoint sites:

![Subdomain filter.](media/discovered-apps/subdomains-image.png)

Note

The feature of discovered subdomains will be deprecated by Dec 31st, 2025. After this deprecation date, no support for discovery subdomains will be provided.

Deep dives into discovered apps are supported only in firewalls and proxies that contain target URL data. For more information, see [Supported firewalls and proxies](set-up-cloud-discovery#supported-firewalls-and-proxies).

If Defender for Cloud Apps can't match the subdomain detected in the traffic logs with the data stored in the app catalog, the subdomain is tagged as **Other**.

## Discover resources and custom apps

Cloud discovery also enables you to dive into your IaaS and PaaS resources. Discover activity across your resource-hosting platforms, viewing access to data across your self-hosted apps and resources including storage accounts, infrastructure and custom apps hosted on Azure, Google Cloud Platform, and AWS. Not only can you see overall usage in your IaaS solutions, but you can get visibility into the specific resources that are hosted on each, and the overall usage of the resources, to help mitigate risk per resource.

For example, if a large amount of data is uploaded, discover which resource received the uploaded data, and drill down to see who performed the activity.

Note

Discovery of IaaS and PaaS resources is supported only in firewalls and proxies that contain target URL data. For more information, see the list of supported appliances in [Supported firewalls and proxies](set-up-cloud-discovery#supported-firewalls-and-proxies).

**To view discovered resources**:

1. In the Microsoft Defender portal, under **Cloud Apps**, select **Cloud discovery**. Then choose the **Discovered resources** tab.

    [![Screenshot that shows the discovered resources menu.](media/discovered-resources-menu.png)](media/discovered-resources-menu.png#lightbox)
2. In the **Discovered resources** page, drill down into each resource to see what kinds of transactions occurred, who accessed it, and then drill down to investigate the users even further.

    ![Screenshot that shows a list of discovered resources.](media/discovery-resources.png)
3. For custom apps, select the options menu at the end of the row and then select **Add new custom app**. This opens the **Add this app** dialog, where you can name and identify the app so it can be included in the cloud discovery dashboard.

## Generate a cloud discovery executive report

The best way to get an overview of Shadow IT use across your organization is by generating a cloud discovery executive report. This report identifies the top potential risks and helps you plan a workflow to mitigate and manage risks until they're resolved.

**To generate a cloud discovery executive report**:

1. In the Microsoft Defender portal, under **Cloud Apps**, select **Cloud discovery**.
2. From the **Cloud discovery** page, select **Actions** &gt; **Generate Cloud Discovery executive report**.
3. Optionally, change the report name, and then select **Generate**.

Note

The executive summary report is revamped to a six-pager report with a goal to provide a clear, concise & actionable overview while preserving the depth and integrity of the original analysis. Starting September 1, 2025, the Cloud Discovery Alerts data point will no longer be included in the Executive Summary Report.

## Exclude entities

If you have system users, IP addresses, or devices that are noisy but uninteresting, or entities that shouldn't be presented in the Shadow IT reports, you might want to exclude their data from the cloud discovery data that's analyzed. For example, you might want to exclude all information originating from a local host.

**To create an exclusion:**

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Exclude entities**.
2. Select either the **Excluded users**, **Excluded groups**, **Excluded IP addresses**, or **Excluded devices** tab and select the **+Add** button to add your exclusion.
3. Add a user alias, IP address, or device name. We recommend adding information about why the exclusion was made.

    [![Screenshot that shows the option to exclude users from the Cloud Discovery report.](media/exclude-user.png)](media/exclude-user.png#lightbox)

Note

- All entity exclusions apply to newly received data only. Historical data of the excluded entities remains through the retention period (90 days).
- Entity exclusion is only supported for the Global report stream. Entities from Microsoft Defender for Endpoint and the Cloud App Security proxy stream aren't supported for exclusion.

## Manage continuous reports

Custom continuous reports provide you with more granularity when monitoring your organization's cloud discovery log data. Create custom reports to filter on specific geographic locations, networks, and sites, or organizational units. By default, only the following reports appear in your cloud discovery report selector:

- The **Global report** consolidates all the information in the portal from all the data sources you included in your logs. The global report doesn't include data from Microsoft Defender for Endpoint.
- The **Data source specific report** displays only information from a specific data source.

**To create a new continuous report**:

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Continuous report** &gt; **Create report**.
2. Enter a report name.
3. Select the data sources you want to include (all or specific).
4. Set the filters you want on the data. These filters can be **User groups**, **IP address tags**, or **IP address ranges**. For more information on working with IP address tags and IP address ranges, see [Organize the data according to your needs](ip-tags).

    ![Screenshot that shows how to create a continuous report.](media/create-custom-continuous-report.png)

Note

All custom reports are limited to a maximum of 1 GB of uncompressed data. If there's more than 1 GB of data, the first 1 GB of data will be exported into the report.

## Delete cloud discovery data

We recommend deleting cloud discovery data in the following cases:

- If you manually uploaded log files, a long time passed since you updated the system with new log files, and you don't want old data affecting your results.
- When you set a new custom data view, it applies only to new data from that point forward. In such cases, you might want to erase old data and then upload your log files again to enable the custom data view to pick up events in the log file data.
- If many users or IP addresses recently started working again after being offline for some time, their activity is identified as anomalous and might give you false positive violations.

Important

Make sure you want to delete data before doing so. Deleting cloud discovery data is irreversible and deletes **all** cloud discovery data in the system.

**To delete cloud discovery data**:

1. In the Microsoft Defender Portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Delete data**.
2. Select the **Delete** button.

    [![Screenshot of deleting cloud discovery data.](media/delete-data.png)](media/delete-data.png#lightbox)

Note

The deletion process takes a few minutes and isn't immediate.