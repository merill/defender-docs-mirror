---
layout: Conceptual
title: Troubleshoot problems with Network protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-np
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot false positives, false negatives, and network performance issues with Network protection in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: oogunrinde, yongrhee
ms.subservice: asr
ms.topic: how-to
ms.collection:
- m365-security
- tier3
- mde-asr
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 01695d81-1c80-7202-fd0e-c39f5686bb52
document_version_independent_id: 01695d81-1c80-7202-fd0e-c39f5686bb52
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-np.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-np
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-np.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 17c389b3-6e2c-5dcd-dd59-866e9d7f78f5
---

# Troubleshoot problems with Network protection - Microsoft Defender for Endpoint | Microsoft Learn

This article provides troubleshooting information for [network protection](network-protection), in cases, such as:

- Network protection blocks a website that is safe (false positive)
- Network protection fails to block a suspicious or known malicious website (false negative)

There are four steps to troubleshoot false positives and false negatives in network protection:

1. Confirm prerequisites
2. Use audit mode to test the rule
3. Add exclusions for the specified rule (for false positives)
4. Submit support logs

## Confirm prerequisites

Network protection works on devices with the following conditions:

- Endpoints are running Windows 10 Pro or Enterprise edition, version 1709 or higher.
- Endpoints are using Microsoft Defender Antivirus as the sole antivirus protection app. [See what happens when you're using a non-Microsoft antivirus solution](microsoft-defender-antivirus-compatibility).
- [Real-time protection](configure-real-time-protection-microsoft-defender-antivirus) is enabled.
- [Behavior Monitoring](behavior-monitor) is enabled.
- [Cloud-delivered protection](cloud-protection-configure) is enabled.
- [Cloud Protection network connectivity](configure-network-connections-microsoft-defender-antivirus) is functional.
- Audit mode isn't enabled. Use [Group Policy](enable-network-protection#group-policy) to set the rule to **Disabled** (value: **0**).

## Use audit mode

You can enable network protection in audit mode and then visit the [network protection demo site](https://smartscreentestratings2.net) to test the feature. All website connections are allowed by network protection but an event is logged to indicate any connection that would be blocked if network protection were enabled.

1. Set network protection to **Audit mode**. Audit mode allows all connections but logs any connection that would be blocked, so you can test whether blocking is causing the issue.

    ```PowerShell
    Set-MpPreference -EnableNetworkProtection AuditMode
    ```
2. Perform the connection activity that is causing an issue (for example, attempt to visit the site, or connect to the IP address you do or don't want to block).
3. [Review the network protection event logs](network-protection#review-network-protection-events-in-windows-event-viewer) to see if the feature would block the connection if it were set to **Enabled**.

    If network protection isn't blocking a connection that you're expecting it should block, run the following command to re-enable Network Protection in block mode and restore enforcement:

    ```PowerShell
    Set-MpPreference -EnableNetworkProtection Enabled
    ```

## Report a false positive or false negative

If you tested the feature with the demo site and audit mode, network protection might work on preset scenarios but not for a specific connection. To report this issue, use the [Windows Defender Security Intelligence web-based submission form](https://www.microsoft.com/wdsi/filesubmission) to submit a false negative or false positive. With an E5 subscription, you can also link to any related alert from the [Alerts queue](alerts-queue).

See [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives).

## Add exclusions

The current exclusion options are:

1. Setting up a custom allow indicator.
2. Using IP exclusions: `Add-MpPreference -ExclusionIpAddress 192.168.1.1`.
3. Excluding an entire process. For more information, see [Microsoft Defender Antivirus exclusions](microsoft-defender-antivirus-exclusions-configure).

## Troubleshoot network performance issues

A network protection component might slow down connections to Domain Controllers or Exchange servers. You might also see Event ID 5783 NETLOGON errors. These errors mean the device can't connect to a Domain Controller.

To fix slow network connections or Event ID 5783 NETLOGON errors, switch Network Protection from 'block mode' to '[audit mode](troubleshoot-np)' or 'disabled'. If that resolves the problem, disable Network Protection components one at a time to isolate which component causes the issue.

Disable the following components one at a time and test your network speed after each change:

1. [Disable Datagram Processing on Windows Server](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
2. [Disable Network Protection Perf Telemetry](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
3. [Disable FTP parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
4. [Disable SSH parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
5. [Disable RDP parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
6. [Disable HTTP parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
7. [Disable SMTP parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
8. [Disable DNS over TCP parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
9. [Disable DNS parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
10. [Disable inbound connection filtering](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)
11. [Disable TLS parsing](/en-us/powershell/module/defender/set-mppreference?view=windowsserver2022-ps&amp;preserve-view=true)

If your network performance issues persist after disabling each Network Protection component listed earlier, then the issues are probably not related to network protection. Look for other causes of your network performance issues.

## Collect diagnostic data for file submissions

When you report a problem with network protection, you're asked to collect and submit diagnostic data for Microsoft support and engineering teams to help troubleshoot issues. You collect and submit the diagnostic data by running `MpCmdrun.exe -GetFiles`, which saves the data at `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`.

For detailed instructions, see [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data).

## Resolve connectivity issues with network protection (for E5 customers)

Because network protection can't see your operating system proxy settings, network protection clients might be unable to reach the cloud service in some environments. To resolve these connectivity issues, configure one of the following registry keys so that network protection becomes aware of the proxy configuration. You can configure the registry key by using PowerShell, Microsoft Configuration Manager, or Group Policy.

If your environment uses a fixed proxy endpoint, configure Microsoft Defender to route traffic through that proxy server by setting the address and port:

```powershell
Set-MpPreference -ProxyServer <proxy IP address: Port>
```

---OR---

If your network routes traffic dynamically through a PAC file instead of a static proxy, use the following command to configure Microsoft Defender to use that PAC URL:

```powershell
Set-MpPreference -ProxyPacUrl <Proxy PAC url>
```

You can configure the registry key by using PowerShell, Microsoft Configuration Manager, or Group Policy. Here are some resources to help:

- [Working with Registry Keys](/en-us/powershell/scripting/samples/working-with-registry-keys)
- [Configure custom client settings for Endpoint Protection](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure-client)
- [Use Group Policy settings to manage Endpoint Protection](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-group-policies)