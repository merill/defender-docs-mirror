---
layout: Conceptual
title: Investigate domains and URLs associated with an alert - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-domain
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the investigation options to see if devices and servers have been communicating with malicious domains.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.subservice: edr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 18d068b2-9688-3eec-164a-caf1c9d6328e
document_version_independent_id: 18d068b2-9688-3eec-164a-caf1c9d6328e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-domain.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-domain.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 8fe0cc5a-067c-f8f4-7495-8159059c4243
---

# Investigate domains and URLs associated with an alert - Microsoft Defender for Endpoint | Microsoft Learn

Investigate a domain to see if the devices and servers in your enterprise network have been communicating with a known malicious domain.

You can investigate a URL or domain by using the search feature, from the incident experience (in evidence tab, or from the alert story), from advanced hunting, from the email page and side panel, or by clicking on the URL or domain link from the **Device timeline**.

You can see information from the following sections in the URL and domain view:

- Domain details, registrant contact information
- Microsoft verdict
- Incidents and alerts related to this URL or domain
- Prevalence of the URL or domain in the organization
- Most recent observed devices with URL or domain
- Most recent emails containing the URL or domain
- Most recent clicks to the URL or domain

[![The main URL/domain page](/en-us/defender/media/investigate-urls/investigate-url.png)](/en-us/defender/media/investigate-urls/investigate-url.png#lightbox)

## Review the domain entity page

You can pivot to the domain page from the domain details in the URL page or side panel, just click on **View domain page** link. The domain entity shows an aggregation of all the data from the URLs with the fully qualified domain name (FQDN). For example, if one device is observed communicating with `sub.domain.tld/path1`, and another device is observed communicating with `sub.domain.tld/path2`, each of those URLs will show one device observation, and the domain will show the two device observations. However, a device that communicated with a different subdomain such as `othersub.domain.tld/path` won't correlate to the `sub.domain.tld` domain page, but to `othersub.domain.tld`.

## Overview of the URL and domain page

The URL overview section lists the URL, a link to further details at whois, the number of related open incidents, and the number of active alerts, the number of affected devices, emails, and the number of user clicks observed.

### URL summary details

Displays the original URL (existing URL information), with the query parameters and the application-level protocol. The domain details section includes the full domain details, such as registration date, modification date, and registrant contact info.

The URL and domain page also shows the Microsoft verdict of the URL or domain, device prevalence, emails, and user clicks. In the device prevalence section, you can see the number of devices that communicated with the URL or domain in the last 30 days, and pivot to the first or last event in the device timeline right away. To investigate initial access or if there's still a malicious activity in your environment.

### Incidents and alerts overview

The Incident and alerts section displays a bar chart of all active alerts in incidents over the past 180 days.

### Microsoft verdict

The Microsoft verdict section displays the verdict of the URL or domain from the Microsoft Threat Intelligence (TI) library. It shows if the URL or domain is already known as phishing or malicious entity.

### Prevalence

The Prevalence section provides the details on the prevalence of the URL within the organization, over the last 30 days, such and trend chart – which shows the number of distinct devices that communicated with the URL or domain over a specific period of time. Below you can find details of the first and last device observations communicated with the URL in the last 30 days, where you can pivot to the device timeline right away, to investigate initial access from the phish link, or if there's still a malicious communication in your environment.

## Incidents and alerts

Use the **Incidents and alerts** tab to review incidents associated with the URL or domain.

![Screenshot of the Incidents and alerts tab listing incidents associated with the URL or domain.](media/domain-incidents.png)

The incident and alerts tab provides a list of incidents that are associated with the URL or domain. The incidents table on the **Incidents and alerts** tab is a filtered version of the incidents visible on the Incident queue screen, showing only incidents associated with the URL or domain, their severity, impacted assets and more.

The incidents and alerts tab can be adjusted to show more or less information, by selecting **Customize columns** from the action menu above the column headers. The number of items displayed can also be adjusted, by selecting items per page on the same menu.

## View devices associated with a URL or domain

![Screenshot of the Devices tab showing the number of distinct devices that communicated with the URL or domain over time.](media/domain-device-overview.png)

The Devices tab provides a chronological view of all the devices that were observed for a specific URL or a domain. The Devices tab includes a trend chart and a customizable table listing device details, such as risk level, domain, and more. The Devices tab also shows the first and last event times where the device interacted with the URL or domain, and the action type for each event. Using the menu next to the device name, you can quickly pivot to the device timeline to further investigate what happened before or after the event that involved this URL or domain.

Although the default time period is the past 30 days, you can customize the time period from the drop-down available at the corner of the card. The shortest range available is for prevalence over the past day, while the longest range is over the past six months.

Using the export button above the table, you can export all the data into a .csv file (including the first and last event time and action type), for further investigation and reporting.

## Review emails associated with a URL or domain

The Emails tab provides a detailed view of all the emails observed in the last 30 days that contained the URL or domain. The Emails tab includes a trend chart and a customizable table listing email details, such as subject, sender, recipient, and more.

[![The email tab for investigating a URL/domain](/en-us/defender/media/investigate-urls/investigate-url-email-view.png)](/en-us/defender/media/investigate-urls/investigate-url-email-view.png#lightbox)

## Review click activity for a URL or domain

The Clicks tab provides a detailed view of all the clicks to the URL or domain observed in the last 30 days.

### Investigate a URL or domain

Use the following steps to investigate a URL or domain:

1. Select **URL** from the **Search bar** drop-down menu.
2. Enter the URL in the **Search** field. Alternatively, you can navigate to the URL or domain from the **Incident attack story tab**, from the **device timeline**, through **advanced hunting**, or from the **email side panel and page**.
3. Click the search icon or press **Enter**. Details about the URL are displayed.

    Note

    Search results will only be returned for URLs observed in communications from devices in the organization.
4. Use the search filters to define the search criteria. You can also use the timeline search box to filter the displayed results of all devices in the organization observed communicating with the URL, the file associated with the communication and the last date observed.
5. Clicking any of the device names will take you to that device's view, where you can continue to investigate reported alerts, behaviors, and events.
6. If you disagree with the verdict of a URL or domain, you can report it to Microsoft as *clean*, *phishing*, or *malicious* by selecting **Submit to Microsoft for analysis**.

[![Submit for analysis option in the URL/domain page](/en-us/defender/media/investigate-urls/investigate-url-submission.png)](/en-us/defender/media/investigate-urls/investigate-url-submission.png#lightbox)