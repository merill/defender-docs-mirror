---
layout: Conceptual
title: Monitoring web browsing security in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/web-protection-monitoring
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Monitor web browsing security in Microsoft Defender for Endpoint by using web protection reports in the Microsoft Defender portal. Learn about available threat detection metrics and summary views.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 37fa4558-ed17-594c-b78c-eb8d85be01e2
document_version_independent_id: 37fa4558-ed17-594c-b78c-eb8d85be01e2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/web-protection-monitoring.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: web-protection-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/web-protection-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b52ccde7-befb-c14e-f07e-fedbf139041a
---

# Monitoring web browsing security in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Web protection lets you monitor your organization's web browsing security through reports under **Reports &gt; Web protection** in the Microsoft Defender portal. The report contains cards that provide web threat detection statistics.

- **Web threat protection detections over time** - this trending card displays the number of web threats detected by type during the selected time period (Last 30 days, Last 3 months, Last 6 months)

    [![The card showing web threats protection detections over time](media/wtp-blocks-over-time.png)](media/wtp-blocks-over-time.png#lightbox)
- **Web threat protection summary** - this card displays the total web threat detections in the past 30 days, showing distribution across the different types of web threats. Selecting a slice opens the list of the domains that were found with malicious or unwanted websites.

    [![The card showing web threats protection summary](media/wtp-summary.png)](media/wtp-summary.png#lightbox)

Note

It can take up to 12 hours before a block is reflected in the cards or the domain list.

## Types of web threats

Web protection categorizes malicious and unwanted websites as:

- **Phishing** - websites that contain spoofed web forms and other phishing mechanisms designed to trick users into divulging credentials and other sensitive information
- **Malicious** - websites that host malware and exploit code
- **Custom indicator** - websites whose URLs or domains you've added to your [custom indicator list](indicators-overview) for blocking

## View the domain list

Select a specific web threat category in the **Web threat protection summary** card to open the **Domains** page. The **Domains** page displays the list of the domains under that threat category. The **Domains** page provides the following information for each domain:

- **Access count** - number of requests for URLs in the domain
- **Blocks** - number of times requests were blocked
- **Access trend** - change in number of access attempts
- **Threat category** - type of web threat
- **Devices** - number of devices with access attempts

Select a domain to view the list of devices that have attempted to access URLs in that domain and the list of URLs.