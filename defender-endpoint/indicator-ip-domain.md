---
layout: Conceptual
title: Create indicators for IPs and URLs/domains - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/indicator-ip-domain
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: ericlaw
description: Learn how to create custom indicators in Microsoft Defender for Endpoint to allow, block, or warn on specific IP addresses, URLs, and domains using SmartScreen and network protection.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- -asr
ms.topic: how-to
ms.subservice: 
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 36adc2af-c157-8962-48ac-f82f5d53272e
document_version_independent_id: 36adc2af-c157-8962-48ac-f82f5d53272e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/indicator-ip-domain.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: indicator-ip-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/indicator-ip-domain.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 78f4b82b-8e10-16ed-9981-a7e2d637efb2
---

# Create indicators for IPs and URLs/domains - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

By creating indicators for IPs and URLs or domains, you can now allow or block IPs, URLs, or domains based on your own threat intelligence. You can also warn users if they open a risky app. The prompt doesn't stop them from using the app; users can bypass the warning and continue to use the app if needed.

To block malicious IPs/URLs, Defender for Endpoint can use:

- Windows Defender SmartScreen for Microsoft browsers
- Network protection for non-Microsoft browsers and non-browser processes

The default threat-intelligence data set to block malicious IPs/URLs is managed by Microsoft.

You can block additional malicious IPs/URLs by configuring "**Custom network indicators**".

Before you begin, review the Prerequisites to ensure your environment is properly configured.

## Prerequisites

It's important to understand the following prerequisites before creating indicators for IPs, URLs, or domains.

Integration into Microsoft browsers is controlled by the browser's SmartScreen setting. For other browsers and applications, your organization must have:

- [Microsoft Defender Antivirus](microsoft-defender-antivirus-windows) configured in active mode.
- [Behavior Monitoring](behavior-monitor) enabled.
- [Cloud-based protection](deploy-manage-report-microsoft-defender-antivirus) turned on.
- [Cloud Protection network connectivity](configure-network-connections-microsoft-defender-antivirus).
- The anti-malware client version must be `4.18.1906.x` or later. See [Monthly platform and engine versions](microsoft-defender-antivirus-updates).

### Supported operating systems

IP, URL, and domain indicators are supported on the following operating systems:

- Windows 11
- Windows 10, version 1709 or later
- Windows Server 2025
- Windows Server 2022
- Windows Server 2019
- Windows Server 2016 running [Defender for Endpoint modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2) (requires installation through MSI)
- Windows Server 2012 R2 running [Defender for Endpoint modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2) (requires installation through MSI)
- Azure Stack HCI OS, version 23H2 and later
- macOS
- Linux
- iOS/iPadOS
- Android

### Network Protection requirements

Network allow and block indicators in Microsoft browsers are controlled by the browser's SmartScreen setting.

For other browsers and applications, network allow and block indicators require that the Microsoft Defender for Endpoint component *Network Protection* is enabled in **block mode**. For more information on Network Protection and configuration instructions, see [Enable network protection](enable-network-protection).

### Custom network indicators requirements

To start blocking IP addresses and/or URLs, turn on the "**Custom network indicators**" feature in the [Microsoft Defender portal](https://security.microsoft.com). The feature is found in **Settings** &gt; **Endpoints** &gt; **General** &gt; **Advanced features**. For more information, see [Advanced features](advanced-features).

For support of indicators on iOS, see [Microsoft Defender for Endpoint on iOS](ios-configure-features#configure-custom-indicators).

For support of indicators on Android, see [Microsoft Defender for Endpoint on Android](android-configure#configure-custom-indicators).

### Indicator list limitations

Only external IPs can be added to the indicator list; indicators can't be created for internal IPs.

### Non Microsoft Edge and Internet Explorer processes

For processes other than Microsoft Edge and Internet Explorer, web protection scenarios use Network Protection for inspection and enforcement:

- IP addresses are supported for all three protocols (TCP, HTTP, and HTTPS (TLS))
- Only single IP addresses are supported (no CIDR blocks or IP ranges) in custom indicators
- HTTP URLs (including a full URL path) can be blocked for any browser or process
- HTTPS fully qualified domain names (FQDN) can be blocked in non-Microsoft browsers (indicators specifying a full URL path can only be blocked in Microsoft Edge)
- Blocking FQDNs in non-Microsoft browsers requires that QUIC and Encrypted Client Hello be disabled in those browsers
- FQDNs loaded via HTTP2 connection coalescing can only be blocked in Microsoft Edge
- If there are conflicting URL indicator policies, the longer path is applied. For example, the URL indicator policy `https://support.microsoft.com/microsoft-365/` takes precedence over the URL indicator policy `https://support.microsoft.com`.

## Network protection implementation

In non-Microsoft Edge processes, Network Protection determines the fully qualified domain name for each HTTPS connection by examining the content of the TLS handshake that occurs after a TCP/IP handshake. This requires that the HTTPS connection use TCP/IP (not UDP/QUIC) and that the ClientHello message not be encrypted. To disable QUIC and Encrypted Client Hello in Google Chrome, see [QuicAllowed](https://chromeenterprise.google/policies/#QuicAllowed) and [EncryptedClientHelloEnabled](https://chromeenterprise.google/policies/#EncryptedClientHelloEnabled). For Mozilla Firefox, see [Disable EncryptedClientHello](https://mozilla.github.io/policy-templates/#disableencryptedclienthello) and [network.http.http3.enable](https://support.mozilla.org/ml/questions/1408003#answer-1571474).

The determination of whether to allow or block access to a site is made after the completion of the [three-way handshake via TCP/IP](/en-us/troubleshoot/windows-server/networking/three-way-handshake-via-tcpip) and any TLS handshake. Thus, when a site is blocked by network protection, you might see an action type of `ConnectionSuccess` under `NetworkConnectionEvents` in the Microsoft Defender portal, even though the site was blocked. `NetworkConnectionEvents` are reported from the TCP layer, and not from network protection. After the three-way handshake has completed, access to the site is allowed or blocked by network protection.

Here's an example of how network protection blocking is logged:

1. Suppose that a user attempts to access a website on their device. The site happens to be hosted on a dangerous domain, and it should be blocked by network protection.
2. The TCP/IP handshake commences. Before it completes, a `NetworkConnectionEvents` action is logged, and its `ActionType` is listed as `ConnectionSuccess`. However, as soon as the TCP/IP handshake process completes, network protection blocks access to the site. The handshake, logging, and blocking sequence happens quickly. A similar process occurs with [Microsoft Defender SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/); it's after the handshake completes that a determination is made, and access to a site is either blocked or allowed.
3. In the Microsoft Defender portal, an alert is listed in the [alerts queue](alerts-queue). Details of that alert include both `NetworkConnectionEvents` and `AlertEvents`. You can see that the site was blocked, even though you also have a `NetworkConnectionEvents` item with the ActionType of `ConnectionSuccess`.

### Warn mode controls

When using warn mode, you can configure the following controls:

- **Bypass ability**

    - Allow button in Microsoft Edge
    - Allow button on toast (Non-Microsoft browsers)
    - Bypass duration parameter on the indicator
    - Bypass enforcement across Microsoft and Non-Microsoft browsers
- **Redirect URL**

    - Redirect URL parameter on the indicator
    - Redirect URL in Microsoft Edge
    - Redirect URL on toast (Non-Microsoft browsers)

For more information, see [Govern apps discovered by Microsoft Defender for Endpoint](/en-us/cloud-app-security/mde-govern).

## Policy conflict handling order for IP, URL, and domain indicators

Policy conflict handling for domains, URLs, and IP addresses differs from certificate indicators, which use a separate precedence order. For details on certificate indicator policies, see [Create indicators based on certificates](indicator-certificates).

In the case where multiple different action types are set on the same indicator (for example, three indicators for Microsoft.com with the action types **block**, **warn**, and **allow**), the order those action types would take effect is:

1. Allow
2. Warn
3. Block

"Allow" overrides "warn," which overrides "block", as follows: `Allow` &gt; `Warn` &gt; `Block`. Therefore, in the previous example, `Microsoft.com` would be allowed.

### Defender for Cloud Apps Indicators

If your organization has enabled integration between Defender for Endpoint and Defender for Cloud Apps, block indicators are created in Defender for Endpoint for all unsanctioned cloud applications. If an application is put in monitor mode, warn indicators (bypassable block) are created for the URLs associated with the application. Allow indicators aren't automatically created for sanctioned applications. Indicators created by Defender for Cloud Apps use the same precedence order: `Allow` &gt; `Warn` &gt; `Block`.

## Policy precedence

Microsoft Defender for Endpoint policy has precedence over Microsoft Defender Antivirus policy. In situations when Defender for Endpoint is set to `Allow`, but Microsoft Defender Antivirus is set to `Block`, the result is `Allow`.

### Precedence for multiple active policies

Applying multiple different web content filtering policies to the same device result in the more restrictive policy applying for each category. Consider the following scenario:

- **Policy 1** blocks categories 1 and 2 and audits the rest
- **Policy 2** blocks categories 3 and 4 and audits the rest

The result is that categories 1-4 are all blocked. This scenario is illustrated in the following image.

![Diagram that shows the precedence of web content filtering policy block mode over audit mode.](media/web-content-filtering-policies-mode-precedence.png)

## Create an indicator for IPs, URLs, or domains from the settings page

Important

It can take up to 48 hours after a policy is created for a URL or IP address to be blocked on a device. In most cases, blocks take effect in under two hours.

To create an indicator for IPs, URLs, or domains from the Microsoft Defender portal, perform the following steps:

1. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Indicators** (under **Rules**).
2. Select the **IP addresses or URLs/Domains** tab.
3. Select **Add item**.
4. Specify the following details:

    - **Indicator**: Specify the entity details and define the expiration of the indicator.
    - **Action**: Specify the action to be taken and provide a description.
    - **Scope**: Specify the machine group(s) that should enforce the indicator.
5. Review the details in the **Summary** tab, then select **Save**.

Important

After you create a policy for a URL or IP address, it can take up to 48 hours for the policy to take effect. In most cases, policy changes take effect in under two hours.