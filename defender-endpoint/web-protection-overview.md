---
layout: Conceptual
title: Web protection in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/web-protection-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Overview of web threat protection, web content filtering, and custom indicators in Microsoft Defender for Endpoint, including browser support, precedence rules, and advanced hunting queries.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.reviewer: ericlaw
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: partner-contribution, msecd-doc-authoring-1016
ms.topic: how-to
ms.subservice: asr
ai-usage: ai-assisted
locale: en-us
document_id: 450697f7-5887-d5c9-f632-715ef6fc634e
document_version_independent_id: 450697f7-5887-d5c9-f632-715ef6fc634e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/web-protection-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: web-protection-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/web-protection-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: e79f3066-13ea-a5a5-def5-cc0869eb096d
---

# Web protection in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how web protection in Microsoft Defender for Endpoint helps secure your devices against web threats and regulate unwanted content. It covers the core capabilities—web threat protection, web content filtering, and custom indicators—along with browser support, policy precedence rules, troubleshooting, and advanced hunting queries. This information is intended for security administrators and IT professionals who manage Defender for Endpoint.

## Overview

Web protection in Microsoft Defender for Endpoint is a capability made up of [Web threat protection](web-threat-protection), [Web content filtering](web-content-filtering), and [Custom indicators](indicators-overview). Web protection lets you secure your devices against web threats and helps you regulate unwanted content. You can find Web protection reports in the Microsoft Defender portal by going to **Reports &gt; Web protection**.

[![The web protection cards](media/web-protection.png)](media/web-protection.png#lightbox)

### Web threat protection

The cards that make up web threat protection are **Web threat detections over time** and **Web threat summary**.

Web threat protection includes:

- Comprehensive visibility into web threats affecting your organization.
- Investigation capabilities over web-related threat activity through alerts and comprehensive profiles of URLs and the devices that access these URLs.
- A full set of security features that track general access trends to malicious and unwanted websites.

Note

For processes other than Microsoft Edge and Internet Explorer, web protection scenarios leverage Network Protection for inspection and enforcement:

- IP addresses are supported for all three protocols (TCP, HTTP, and HTTPS (TLS)).
- Only single IP addresses are supported (no CIDR blocks or IP ranges) in custom indicators.
- HTTP URLs (including a full URL path) can be blocked for any browser or process
- HTTPS fully-qualified domain names (FQDN) can be blocked in non-Microsoft browsers (indicators specifying a full URL path can only be blocked in Microsoft Edge)
- Blocking FQDNs in non-Microsoft browsers requires that QUIC and Encrypted Client Hello be disabled in those browsers
- FQDNs loaded via HTTP2 connection coalescing can only be blocked in Microsoft Edge.
- Network Protection will block connections on all ports (not just 80 and 443).

In non-Microsoft Edge processes, Network Protection determines the fully qualified domain name for each HTTPS connection by examining the content of the TLS handshake that occurs after a TCP/IP handshake. This requires that the HTTPS connection use TCP/IP (not UDP/QUIC) and that the ClientHello message not be encrypted. To disable QUIC and Encrypted Client Hello in Google Chrome, see [QuicAllowed](https://chromeenterprise.google/policies/#QuicAllowed) and [EncryptedClientHelloEnabled](https://chromeenterprise.google/policies/#EncryptedClientHelloEnabled). For Mozilla Firefox, see [Disable EncryptedClientHello](https://mozilla.github.io/policy-templates/#disableencryptedclienthello) and [network.http.http3.enable](https://support.mozilla.org/ml/questions/1408003#answer-1571474).

There might be up to two hours of latency (usually less) between the time an indicator is added and it being enforced on the client. For more information, see [Web threat protection](web-threat-protection).

### Custom indicators

Custom indicator detections are summarized in web threat reports under **Web threat detections over time** and **Web threat summary**.

Custom indicators provide:

- The ability to create IP and URL-based indicators of compromise to protect your organization against threats.
- The ability to specify Allow, Block, or Warn behavior.
- Investigative capabilities over activities related to your custom IP/URL indicators and the devices that access these URLs.

For more information, see [Create indicators for IPs and URLs/domains](indicator-ip-domain)

### Web content filtering

Web content filtering blocks are summarized under **Web activity by category**, **Web content filtering summary**, and **Web activity summary**.

Web content filtering provides:

- The ability to block users from accessing websites in blocked categories, whether they're browsing on-premises or away.
- Support for targeting different policies to different device groups defined in the [Microsoft Defender for Endpoint role-based access control settings](rbac). 
    Note

    Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.
- Web reporting in the same central location, with visibility into both blocks and web usage.

For more information, see [Web content filtering](web-content-filtering).

## Order of precedence

When multiple web protection policies could apply to the same URL or IP request, the order of precedence determines which policy wins. Web protection is made up of the following components, listed in order of precedence. Each of these components is enforced by the SmartScreen client in Microsoft Edge and by the Network Protection client in all other browsers and processes.

- Custom indicators (IP/URL, Microsoft Defender for Cloud Apps policies)

    - Allow
    - Warn
    - Block
- Web threats (malware, phish)

    - SmartScreen Intel
- Web Content Filtering (WCF)

Note

Microsoft Defender for Cloud Apps currently generates indicators only for blocked URLs.

The order of precedence describes the sequence in which web protection components (custom indicators, web threat protection, and web content filtering) evaluate a URL or IP. For example, if you have a web content filtering policy you can create exclusions through custom IP/URL indicators. Custom Indicators of compromise (IoC) are higher in the order of precedence than WCF blocks.

Similarly, during a conflict between indicators, allows always take precedence over blocks (override logic). That means that an allow indicator takes precedence over any block indicator that is present.

The following table summarizes some common configurations that would present conflicts within the web protection stack. It also identifies the resulting determinations based on the order of precedence for web protection components.

| Custom Indicator policy | Web threat policy | WCF policy | Defender for Cloud Apps policy | Result |
| --- | --- | --- | --- | --- |
| Allow | Block | Block | Block | Allow (Web protection override) |
| Allow | Allow | Block | Block | Allow (WCF exception) |
| Warn | Block | Block | Block | Warn (override) |

Internal IP addresses aren't supported by custom indicators. For a warn policy when bypassed by the end user, the site is unblocked for 24 hours for that user by default. This time frame can be modified by the Admin and is passed down by the SmartScreen cloud service. The ability to bypass a warning can also be disabled in Microsoft Edge using CSP for web threat blocks (malware/phishing). For more information, see [Microsoft Edge SmartScreen Settings](/en-us/DeployEdge/microsoft-edge-policies#smartscreen-settings-policies).

## Protect browsers

In all web protection scenarios, SmartScreen and Network Protection can be used together to ensure protection across both Microsoft and non-Microsoft browsers and processes. SmartScreen is built directly into Microsoft Edge, while Network Protection monitors traffic in non-Microsoft browsers and processes. The following diagram illustrates how SmartScreen and Network Protection work together across Microsoft and non-Microsoft browsers and processes. This diagram of the two clients working together to provide multiple browser/app coverages is accurate for all features of Web Protection (Indicators, Web Threats, Content Filtering).

> 
> [![The usage of smartScreen and Network Protection together](/en-us/defender/media/web-protection-protect-browsers.png)](/en-us/defender/media/web-protection-protect-browsers.png#lightbox)

## Troubleshoot endpoint blocks

Responses from the SmartScreen cloud are standardized. Tools like Telerik Fiddler can be used to inspect the response from the cloud service, which helps determine the source of the block.

When the SmartScreen cloud service responds with an allow, block, or warn response, a response category and server context is relayed back to the client. In Microsoft Edge, the response category is what is used to determine the appropriate block page to show (malicious, phishing, organizational policy).

The following table shows the responses and their correlated features.

| ResponseCategory | Feature responsible for the block |
| --- | --- |
| CustomPolicy | WCF |
| CustomBlockList | Custom indicators |
| CasbPolicy | Defender for Cloud Apps |
| Malicious | Web threats |
| Phishing | Web threats |

## Advanced hunting for web protection

Kusto queries in advanced hunting can be used to summarize web protection blocks in your organization for up to 30 days. These queries use the response categories from the Troubleshoot endpoint blocks table to distinguish between the various sources of blocks and summarize them in a user-friendly manner. For example, to find Web Content Filtering (WCF) blocks detected by SmartScreen in Microsoft Edge, run the following query. This query filters `DeviceEvents` for SmartScreen URL warning actions and extracts key fields such as device name, timestamp, URL, and the experience category to identify web content filtering blocks.

```kusto
DeviceEvents
| where ActionType == "SmartScreenUrlWarning"
| extend ParsedFields=parse_json(AdditionalFields)
| project DeviceName, ActionType, Timestamp, RemoteUrl, InitiatingProcessFileName, Experience=tostring(ParsedFields.Experience)
| where Experience == "CustomPolicy"
```

To identify WCF blocks enforced by Network Protection in non-Microsoft browsers, use the following query. In this query, the `ActionType` is `ExploitGuardNetworkProtectionBlocked` and the filter field is `ResponseCategory` instead of `Experience`.

```kusto
DeviceEvents
| where ActionType == "ExploitGuardNetworkProtectionBlocked"
| extend ParsedFields=parse_json(AdditionalFields)
| project DeviceName, ActionType, Timestamp, RemoteUrl, InitiatingProcessFileName, ResponseCategory=tostring(ParsedFields.ResponseCategory)
| where ResponseCategory == "CustomPolicy"
```

To list blocks that are due to other features (like Custom Indicators), refer to the ResponseCategory table. The ResponseCategory table outlines each feature and its respective response category. These queries can be modified to search for telemetry related to specific machines in your organization. The ActionType shown in each query shows only those connections that were blocked by a Web Protection feature, and not all network traffic.

## What users see when web protection blocks content

If a user visits a web page that poses a risk of malware, phishing, or other web threats, Microsoft Edge displays a block page that resembles the following image:

[![Screenshot showing new block notification for a website.](media/web-protection-indicators-new-block-page.jpg)](media/web-protection-indicators-new-block-page.jpg#lightbox)

Beginning with Microsoft Edge 124, the following block page is shown for all Web Content Filtering category blocks.

[![Screenshot showing content blocked.](media/web-protection-new-content-blocked-page.jpg)](media/web-protection-new-content-blocked-page.jpg#lightbox)

In any case, no block pages are shown in non-Microsoft browsers, and the user instead sees a "Secure Connection Failed" page along with a Windows toast notification. Depending on the policy responsible for the block, a user sees a different message in the toast notification. For example, web content filtering displays the message, "This content is blocked."

## Report false positives

To report a false positive for sites that have been deemed dangerous by SmartScreen, use the link that appears on the Microsoft Edge block page.

For Web content filtering (WCF), you can override a block using an Allow indicator, and optionally dispute the category of a domain. Navigate to the **Domains** tab of the WCF reports. You see an ellipsis beside each of the domains. Hover over this ellipsis and select **Dispute Category**. A flyout opens. Set the priority of the incident and provide some other details, such as the suggested category. For more information on how to turn on WCF and how to dispute categories, see [Web content filtering](web-content-filtering).

For more information on how to submit false positives/negatives, see [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives).