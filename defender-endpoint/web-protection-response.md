---
layout: Conceptual
title: Respond to web threats in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/web-protection-response
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Respond to alerts related to malicious and unwanted websites. Understand how web threat protection informs end users through their web browsers and Windows notifications
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: concept-article
ms.subservice: asr
ms.date: 2024-09-21T00:00:00.0000000Z
locale: en-us
document_id: 30a70330-b4d0-29b5-d07f-b54ff968d899
document_version_independent_id: 30a70330-b4d0-29b5-d07f-b54ff968d899
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/web-protection-response.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: web-protection-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/web-protection-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 70d9bee5-bd68-6c6a-3c37-584f4abc7be7
---

# Respond to web threats in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Web protection in Microsoft Defender for Endpoint lets you efficiently investigate and respond to alerts related to malicious websites and websites in your custom indicator list.

## View web threat alerts

Microsoft Defender for Endpoint generates the following [alerts](/en-us/defender-xdr/investigate-alerts?toc=/defender-endpoint/toc.json&amp;bc=/defender-endpoint/breadcrumb/toc.json#manage-alerts) for malicious or suspicious web activity:

- **Suspicious connection blocked by network protection**: This alert is generated when network protection (in block mode) stops an attempt to access a malicious website or a website in your custom indicator list.
- **Suspicious connection detected by network protection**: This alert is generated when network protection (in audit mode) detects an attempt to access a malicious website or a website in your custom indicator list.

Each alert provides the following information:

- Device that attempted to access the blocked website
- Application or program used to send the web request
- Malicious URL or URL in the custom indicator list
- Recommended actions for responders

[![The alert related to web threat protection](media/wtp-alert.png)](media/wtp-alert.png#lightbox)

Note

To reduce the volume of alerts, Microsoft Defender for Endpoint consolidates web threat detections for the same domain on the same device each day to a single alert. Only one alert is generated and counted into the [web protection report](web-protection-monitoring).

## Inspect website details

You can dive deeper by selecting the URL or domain of the website in the alert. This opens a page about that particular URL or domain with various information, including:

- Devices that attempted to access website
- Incidents and alerts related to the website
- How frequent the website was seen in events in your organization

    [![The domain or URL entity details page](media/wtp-website-details.png)](media/wtp-website-details.png#lightbox)

For more information, see [About URL or domain entity pages](investigate-domain).

## Inspect the device

You can also check the device that attempted to access a blocked URL. Selecting the name of the device on the alert page opens a page with comprehensive information about the device.

For more information, see [About device entity pages](investigate-machines).

## Web browser and Windows notifications for end users

With web protection in Defender for Endpoint, your end users are prevented from visiting malicious or unwanted websites using Microsoft Edge or other browsers. Because blocking is done by [network protection](network-protection) and not their web browser, users see a generic error from the web browser. They also see a notification from Windows.

[![The Microsoft Edge showing a 403 error, and the Windows notification](media/wtp-browser-blocking-page.png)](media/wtp-browser-blocking-page.png#lightbox)

*Web threat blocked on Microsoft Edge*

[![The Chrome web browser showing a secure connection warning, and the Windows notification](media/wtp-chrome-browser-blocking-page.png)](media/wtp-chrome-browser-blocking-page.png#lightbox)*Web threat blocked on Chrome*