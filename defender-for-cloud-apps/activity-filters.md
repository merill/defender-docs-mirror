---
layout: Conceptual
title: Investigate activities in Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/activity-filters
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
description: Learn how to investigate app activities, understand activity types, and use filters to analyze events in Microsoft Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: gayasalomon
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 6957dc7e-e718-203f-c32e-cb627e367529
document_version_independent_id: 6957dc7e-e718-203f-c32e-cb627e367529
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/activity-filters.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: activity-filters
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/activity-filters.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d8485bd9-9f24-8b6d-65c5-f18722156a8e
---

# Investigate activities in Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps gives you visibility into all the activities from your connected apps. After you connect Defender for Cloud Apps to an app using the App connector, Defender for Cloud Apps scans all the activities that happened - the retroactive scan period differs per app - and then it's updated constantly with new activities.

Note

The activity types (such as `FileCreated`, `FileCreatedOnNetworkShare`, `ArchiveCreated`, or `FileDeleted`) and their associated data are sourced directly from the connected app’s third-party API (for example, Salesforce or ServiceNow).

Microsoft Defender for Cloud Apps displays these activity names and types exactly as received and doesn't define or modify them. To understand the meaning of an activity, refer to the relevant third‑party API documentation.

The action types for events and activities are determined by the source service, whether it's a first-party or third-party service. Microsoft Defender for Cloud Apps (MDA) supports a wide range of action types and isn't restricted to specific ones. For a full list of Microsoft 365 activities monitored by Defender for Cloud Apps, see [Search the audit log in the Microsoft Purview portal](/en-us/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#audited-activities).

Note

As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate. The activity log uses a separate data pipeline that isn't yet integrated with the [Identity inventory](/en-us/defender-for-identity/identity-inventory). Correlations defined in the Identity inventory don't affect the user details shown in the activity log. For a full list of affected features, see [Enable Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration).

The **Activity log** can be filtered to enable you to find specific activities. You create policies based on the activities and then define what you want to be alerted about and act on. You can search for activities performed on certain files. The type of activities and the information we get for each activity depends on the app and what kind of data the app can provide.

For example, you can use the **Activity log** to find users in your organization who are using operating systems or browsers that are out of date:

1. After you connect an app to Defender for Cloud Apps, on the **Activity log** page, select **Advanced filters**.
2. Select **User agent tag**.
3. Select **Outdated browser** or **Outdated operating system**.

[![Screenshot that shows the Activity log with an outdated browser example.](media/activity-filters/activity-example-outdated.png)](media/activity-filters/activity-example-outdated.png#lightbox)

The basic filter provides great tools to start filtering your activities.

[![Screenshot that shows the basic activity log filter.](media/activity-filters/activity-log-filter-basic.png)](media/activity-filters/activity-log-filter-basic.png#lightbox)

You can expand the basic filter by selecting **Advanced filters** to drill down into more specific activities.

![Screenshot that shows the advanced activity log filter.](media/activity-log-filter-advanced.png)

Note

- The Legacy tag is added to any activity policy that uses the older "user" filter. This filter continues to work as usual. If you want to remove the Legacy tag, you can remove the filter and add the filter again using the new **User name** filter.
- In some rare cases, the count of the events presented in the activity log might show a slightly higher number than the real number of events that apply for the filter and being presented.

## The Activity drawer

### Working with the Activity drawer

You can view more information about each activity, by selecting the Activity itself in the Activity log. This opens the Activity drawer that provides the following additional actions and insights for each activity:

- Matched policies: Select the **Matched policies** link to see a list of policies this activity matched.
- View raw data: Select **View raw data** to see the actual data that was received from the app.
- User: Select the user to view the user page for the user who performed the activity.
- Device type: Select **Device type** to view the raw user agent data.
- Location: Select the location to view the location in Bing Maps.
- IP address category and tags: Select the IP tag to view the list of IP tags found in this activity. You can then filter by all activities matching this tag.

Note

The **IP address category** is assigned automatically based on threat intelligence and can be manually overridden using [IP address ranges](ip-tags).

The fields in the Activity drawer provide contextual links to additional activities and drill-downs you might want to perform from the drawer directly. For example, if you move your cursor next to the IP address category, you can use the **add to filter** icon ![Screenshot of the Add to filter icon used to add an activity to the current filter.](media/activity-filters/add-to-filter-icon.png) to immediately add the IP address to the current page's filter. You can also use the settings cog icon ![Screenshot of the Settings control for accessing configuration settings.](media/activity-filters/contextual-settings-icon.png) that pops up to arrive directly at the settings page necessary to modify the configuration of one of the fields, such as **User groups**.

You can also use the icons at the top of the tab to:

- View activities of the same type
- View all activities of the same user
- View activities from the same IP address
- View activities from the exact geographic location
- View activities from the same period (48 hours)

[![Screenshot that shows the activity drawer.](media/activity-filters/activity-drawer.png)](media/activity-filters/activity-drawer.png#lightbox)

For a list of governance actions available, see [Activity governance actions](governance-actions#activity-governance-actions).

#### View user insights

The investigation experience includes insights about the acting user. With a single click, you can get a comprehensive overview of the user, including which location they connected from, how many open alerts they're involved with, and their metadata information.

To view user insights:

1. Select the Activity itself in the **Activity log**.
2. Then select the **User** tab. Selecting it opens the Activity drawer **User** tab provides the following insights about the user:

    - **Open alerts**: The number of open alerts that involve the user.
    - **Matches**: The number of policy matches for files owned by the user.
    - **Activities**: The number of activities performed by the user in the past 30 days.
    - **Countries**: The number of countries the user connected from in the past 30 days.
    - **ISPs**: The number of ISPs the user connected from in the past 30 days.
    - **IP addresses**: The number of IP addresses the user connected from in the past 30 days.

[![Screenshot that shows user insights, user activities, and frequent alert locations for Defender for Cloud apps.](media/user-insights.png)](media/user-insights.png#lightbox)

#### View IP address insights

Because IP address information is crucial for almost all investigations, you can view detailed information about IP addresses in the Activity drawer. From within a specific activity, you can select the IP address tab to view consolidated data about the IP address, including the number of open alerts for the particular IP address, a trend graph of recent activity, and a location map. This consolidated view enables you to drill down easily when investigating impossible travel alerts, for example. In addition, you can easily understand where the IP address was used and whether it was involved in suspicious activities. You can also perform actions directly in the IP address drawer that enable you to tag an IP address as risky, VPN, or corporate to ease future investigation and policy creation.

To view IP address insights:

1. Select the Activity itself in the **Activity log**.
2. Then select the **IP address** tab.

    This opens the Activity drawer **IP address** tab, which provides the following insights about the IP address:

    - **Open alerts**: The number of open alerts that involved the IP address.
    - **Activities**: The number of activities performed by the IP address in the past 30 days.
    - **IP location**: The geographic locations from which the IP address connected in the past 30 days.
    - **Activities**: The number of activities performed from this IP address in the past 30 days.
    - **Admin activities**: The number of administrative activities performed from this IP address in the past 30 days. You can perform the following IP address actions:

        - Set as a Corporate IP and add to allow list
        - Set as a VPN IP address and add to allow list
        - Set as a Risky IP and add to block list

[![Screenshot that shows IP address activities over the last 30 days.](media/activity-filters/ip-address-insights.png)](media/activity-filters/ip-address-insights.png#lightbox)

Note

- Internal IPv4 or IPv6 IP addresses audited by the cloud applications connected with API, might indicate internal services communications within the network of the cloud application, and shouldn't be confused with internal IPs from the source network the device connected from, as the cloud application isn't exposed to the internal IPs of the devices.
- To avoid raising [impossible travel](anomaly-detection-policy#impossible-travel) alerts when employees connect from their home locations via the corporate VPN, it's recommended to tag the IP address as **VPN**.

## Export activities

You can export all user activities to a CSV file.

In the **Activity log**, select the **Export** button in the top-left corner.

![Screenshot that shows the export button in the Activity log.](media/activity-filters/export-button.png)

Note

This article provides steps for how to delete personal data from the device or service and can be used to support your obligations under the GDPR. If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).