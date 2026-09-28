---
layout: Conceptual
title: Microsoft Defender for Endpoint Network protection demonstrations - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-network-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Shows how Network protection prevents employees from using any application to access dangerous domains that might host phishing scams, exploits, and other malicious content on the Internet.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- demo
ms.topic: how-to
ms.subservice: asr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 67e5333a-3e57-7552-2346-bdb897b733ed
document_version_independent_id: 67e5333a-3e57-7552-2346-bdb897b733ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-network-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-network-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-network-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 374a1d37-8e20-338d-d10b-554e55255fba
---

# Microsoft Defender for Endpoint Network protection demonstrations - Microsoft Defender for Endpoint | Microsoft Learn

Network Protection helps reduce the attack surface of your devices from Internet-based events. It prevents employees from using any application to access dangerous domains that might host phishing scams, exploits, and other malicious content on the Internet.

This article walks you through how to demonstrate and test Network Protection on Windows, macOS, and Linux devices. You'll enable Network Protection, navigate to a test site, and verify that the connection is blocked as expected.

## Prerequisites

- Client devices must be running Windows 11, Windows 10 version 1709 build 16273 or newer, or macOS
- Server devices must be running Windows Server 2012 R2 (with the new unified client) and later, Linux, or Azure Stack HCI OS, version 23H2 and later.
- Microsoft Defender Antivirus

## Windows

To enable Network Protection in block mode on Windows so that connections to dangerous domains are blocked, run the following PowerShell command:

```powershell
Set-MpPreference -EnableNetworkProtection Enabled
```

Following are the Rule states:

| State | Mode | Numeric value |
| --- | --- | --- |
| Disabled | = Off | 0 |
| Enabled | = Block mode | 1 |
| Audit | = Audit mode | 2 |

To verify that Network Protection is enabled, run the following PowerShell command and confirm that the `EnableNetworkProtection` value is set to `1` (block mode):

```powershell
Get-MpPreference
```

**Consider the following scenario**:

1. Enable Network Protection in block mode so that connections to dangerous domains are blocked during the following validation steps:

    ```powershell
    Set-MpPreference -EnableNetworkProtection Enabled
    ```
2. Using the browser of your choice (not Microsoft Edge\*), navigate to the [Network Protection website test](https://smartscreentestratings2.net/). Microsoft Edge has other security measures in place to protect from malicious or phishing websites (SmartScreen).

Following are the expected results:

Navigation to the website should be blocked and you should see a **Connection blocked** notification.

After testing, restore your device to its pre-test configuration by disabling Network Protection with the following command:

```powershell
Set-MpPreference -EnableNetworkProtection Disabled
```

## macOS/Linux

On macOS and Linux, you use the `mdatp` command-line tool to set the Network Protection enforcement level. Replace `[enforcement-level]` with `block` to actively block dangerous connections, or `audit` to log them without blocking. Run the following command from the Terminal:

```bash
mdatp config network-protection enforcement-level --value [enforcement-level]
```

For example, to set Network Protection to block mode so that connections to malicious or test destinations are actively prevented, run the following command:

```bash
mdatp config network-protection enforcement-level --value block
```

To verify that Network Protection is running, query the Defender health status by running the following command from the Terminal. The `network_protection_status` field should display `started`:

```bash
mdatp health --field network_protection_status
```

To test Network Protection on macOS/Linux:

1. Using the browser of your choice (not Microsoft Edge), navigate to the [Network Protection website test](https://smartscreentestratings2.net/). Microsoft Edge has other security measures in place to protect from this vulnerability (SmartScreen).
2. Or run the following command from the terminal:

    ```bash
    curl -o ~/Downloads/smartscreentestratings2.net https://smartscreentestratings2.net/ 
    ```

Following are the expected results:

Navigation to the website should be blocked and you should see a **Connection blocked** notification.

After testing, restore your device to its pre-test configuration by switching Network Protection back to audit mode. In audit mode, Network Protection logs connections to dangerous domains without blocking them:

```bash
mdatp config network-protection enforcement-level --value audit
```