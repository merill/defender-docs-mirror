---
layout: Conceptual
title: Use network protection to help prevent Linux connections to bad sites - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/network-protection-linux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Protect your network by preventing Linux users from accessing known malicious and suspicious network addresses
ms.service: defender-endpoint
ms.localizationpriority: medium
author: paulinbar
ms.author: painbar
ms.subservice: linux
ms.topic: overview
ms.collection:
- m365-security
- tier2
- mde-linux
ms.date: 2025-03-31T00:00:00.0000000Z
locale: en-us
document_id: 90d9d5af-91da-16b7-9b61-4e3622b9ad90
document_version_independent_id: 90d9d5af-91da-16b7-9b61-4e3622b9ad90
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/network-protection-linux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: network-protection-linux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/network-protection-linux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 7b0fdf9f-7fae-856f-75be-834eba851e49
---

# Use network protection to help prevent Linux connections to bad sites - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Network protection helps reduce the attack surface of your devices from Internet-based events. It prevents employees from using any application to access dangerous domains that might host:

- phishing scams
- exploits
- other malicious content on the Internet

Network protection expands the scope of Microsoft Defender [SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/) to block all outbound HTTP(s) traffic that attempts to connect to low-reputation sources. The blocks on outbound HTTP(s) traffic are based on the domain or hostname.

Important

The network protection feature requires Microsoft Defender for Endpoint Linux client version: 101.78.13 or later, **and is supported only on the insiders slow or insiders fast channels**. It isn't supported on the production channel.

## Web content filtering for Linux

You can use web content filtering for testing with network protection for Linux. See [Web content filtering](web-content-filtering).

### Known issues

- Network protection is implemented as a virtual private network (VPN) tunnel. Advanced packet routing options using custom nftables/iptables scripts are available.
- Currently, the block/warn end-user experience isn't available.

Note

Most server installations of Linux lack a graphical user interface and web browser. To evaluate the effectiveness of web threat protection with Linux, we recommend testing on a nonproduction server with a graphical user interface and web browser.

### Prerequisites

- Licensing: You must have a paid or trial subscription of Defender for Endpoint tenant.
- Prerequisites: [Prerequisites for Defender for Endpoint on Linux](mde-linux-prerequisites)
- Microsoft Defender for Endpoint Linux client version 101.78.13 or later **on the insiders slow or insiders fast channels**.

Important

In order to evaluate network protection for Linux, send an email to `xplatpreviewsupport@microsoft.com` with your Org ID. We'll enable the feature on your tenant per request basis. Network Protection feature is available in preview only for AMD64 based Linux servers.

## Instructions

Deploy Linux manually, see [Deploy Microsoft Defender for Endpoint on Linux manually](linux-install-manually)

The following example shows the sequence of commands needed to the mdatp package on ubuntu 20.04 for insiders-Fast channel.

```bash
curl -o microsoft.list https://packages.microsoft.com/config/ubuntu/20.04/insiders-fast.list
sudo mv ./microsoft.list /etc/apt/sources.list.d/microsoft-insiders-fast.list
sudo apt-get install gpg
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt install -y mdatp
```

### Device Onboarding

To onboard the device, you must download the Python onboarding package for Linux server from the Microsoft Defender portal. Go to **Settings** &gt; **Device Management** &gt; **Onboarding**, and then run the following command:

```bash
sudo python3 MicrosoftDefenderATPOnboardingLinuxServer.py
```

### Validation

1. Check Network Protection has effect on always blocked sites:

    - http://smartscreentestratings2.net
    - https://smartscreentestratings2.net
2. Inspect diagnostic logs

    ```bash
    sudo mdatp log level set --level debug
    sudo tail -f /var/log/microsoft/mdatp/microsoft_defender_np_ext.log
    ```

#### To exit the validation mode

Disable network protection and restart the network connection:

```bash
sudo mdatp config network-protection enforcement-level --value disabled
```

## Advanced configuration

By default, Linux network protection is active on the default gateway; routing and tunneling are internally configured. To customize the network interfaces, change the **networkSetupMode** parameter from the **/opt/microsoft/mdatp/conf/** configuration file and restart the service:

```bash
sudo systemctl restart  mdatp
```

The configuration file also enables the user to customize:

- proxy setting
- SSL certificate stores
- tunneling device name
- IP
- and more

The default values were tested for all distributions as described in [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)

### Microsoft Defender portal

Also, make sure that in **Microsoft Defender** &gt; **Settings** &gt; **Endpoints** &gt; **Advanced features** that **'Custom network indicators'** toggle is set *enabled*.

Important

The above **'Custom network indicators'** toggle controls **Custom Indicators** enablement **for ALL platforms** with Network Protection support, including Windows. Reminder that—on Windows—for indicators to be enforced you also must have Network Protection explicitly enabled.

[![MEM Create Profile](media/network-protection-linux-defender-security-center-advanced-features-settings.png)](media/network-protection-linux-defender-security-center-advanced-features-settings.png#lightbox)

## How to explore the features

1. Learn how to [Protect your organization against web threats](web-threat-protection) using web threat protection.

    - Web threat protection is part of web protection in Microsoft Defender for Endpoint. It uses network protection to secure your devices against web threats.
2. Run through the [Custom Indicators of Compromise](indicator-ip-domain) flow to get blocks on the Custom Indicator type.
3. Explore [Web content filtering](web-content-filtering).

    Note

    If you're removing a policy or changing device groups at the same time, this might cause a delay in policy deployment. Pro tip: You can deploy a policy without selecting any category on a device group. This action creates an audit only policy, to help you understand user behavior before creating a block policy.

    Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.
4. [Integrate Microsoft Defender for Endpoint with Defender for Cloud Apps](/en-us/defender-cloud-apps/mde-integration) and your network protection-enabled macOS devices will have endpoint policy enforcement capabilities.

    Note

    Discovery and other features are currently not supported on these platforms.

## Scenarios

The following scenarios are supported during public preview:

### Web threat protection

Web threat protection is part of Web protection in Microsoft Defender for Endpoint. It uses network protection to secure your devices against web threats. By integrating with Microsoft Edge and popular third-party browsers like Chrome and Firefox, web threat protection stops web threats without a web proxy. Web threat protection can protect devices while they're on premises or away. Web threat protection stops access to the following types of sites:

- phishing sites
- malware vectors
- exploit sites
- untrusted or low-reputation sites
- sites you've blocked in your custom indicator list

[![Web Protection reports web threat detections.](media/network-protection-reports-web-protection.png)](media/network-protection-reports-web-protection.png#lightbox)

For more information, see [Protect your organization against web threat](web-threat-protection)

#### Custom Indicators of Compromise

Indicator of compromise (IoCs) matching is an essential feature in every endpoint protection solution. This capability gives SecOps the ability to set a list of indicators for detection and for blocking (prevention and response).

Create indicators that define the detection, prevention, and exclusion of entities. You can define the action to be taken as well as the duration for when to apply the action and the scope of the device group to apply it to.

Currently supported sources are the cloud detection engine of Defender for Endpoint, the automated investigation and remediation engine, and the endpoint prevention engine (Microsoft Defender Antivirus).

[![Shows network protection add URL or domain indicator.](media/network-protection-add-url-domain-indicator.png)](media/network-protection-add-url-domain-indicator.png#lightbox)

For more information, see: [Create indicators for IPs and URLs/domains](indicator-ip-domain).

### Web content filtering

Web content filtering is part of the [Web protection](web-protection-overview) capabilities in Microsoft Defender for Endpoint and Microsoft Defender for Business. Web content filtering enables your organization to track and regulate access to websites based on their content categories. Many of these websites (even if they're not malicious) might be problematic because of compliance regulations, bandwidth usage, or other concerns.

Configure policies across your device groups to block certain categories. Blocking a category prevents users within specified device groups from accessing URLs associated with the category. For any category that's not blocked, the URLs are automatically audited. Your users can access the URLs without disruption, and you'll gather access statistics to help create a more custom policy decision. Your users will see a block notification if an element on the page they're viewing is making calls to a blocked resource.

Web content filtering is available on the major web browsers, with blocks performed by Windows Defender SmartScreen (Microsoft Edge) and Network Protection (Chrome, Firefox, Brave, and Opera). For more information about browser support, see Prerequisites.

[![Shows network protection web content filtering add policy.](media/network-protection-wcf-add-policy.png)](media/network-protection-wcf-add-policy.png#lightbox)

For more information about reporting, see [Web content filtering](web-content-filtering).

### Microsoft Defender for Cloud Apps

The Microsoft Defender for Cloud Apps / Cloud App Catalog identifies apps you would want end users to be warned upon accessing with Microsoft Defender XDR for Endpoint, and mark them as *Monitored*. The domains listed under monitored apps would be later synced to Microsoft Defender XDR for Endpoint:

[![Shows network protection mcas monitored apps.](media/network-protection-macos-mcas-monitored-apps.png)](media/network-protection-macos-mcas-monitored-apps.png#lightbox)

Within 10-15 minutes, these domains will be listed in Microsoft Defender XDR under Indicators &gt; URLs/Domains with Action=Warn. Within the enforcement SLA (see details at the end of this article).

[![Shows network protection mcas cloud app security.](media/network-protection-macos-mcas-cloud-app-security.png)](media/network-protection-macos-mcas-cloud-app-security.png#lightbox)

## Troubleshooting

If network protection doesn't start, or shows "unsupported release ring", it means the device is using the production channel, which isn't supported for network protection. Network protection on Linux requires that the device be on the insider slow or insider fast channel.

To resolve this issue, move the device to one of the insider channels. Alternatively, disable network protection on devices that must remain on the production channel.