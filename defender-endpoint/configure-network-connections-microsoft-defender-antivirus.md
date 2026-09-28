---
layout: Conceptual
title: Configure and validate Microsoft Defender Antivirus network connections - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-network-connections-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure and test your connection to the Microsoft Defender Antivirus cloud protection service.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: paulinbar
ms.author: painbar
ms.topic: how-to
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: yongrhee; pahuijbr
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: bcac5464-8398-9459-c79d-915ebcbe19f7
document_version_independent_id: bcac5464-8398-9459-c79d-915ebcbe19f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-network-connections-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-network-connections-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-network-connections-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
platformId: 6ec7b139-7097-327c-74aa-ffe8a2d85225
---

# Configure and validate Microsoft Defender Antivirus network connections - Microsoft Defender for Endpoint | Microsoft Learn

Important

This article contains information about configuring network connections only for Microsoft Defender Antivirus, when used without Microsoft Defender for Endpoint. If you are using **Microsoft Defender for Endpoint** (which includes Microsoft Defender Antivirus), see [Configure device proxy and Internet connectivity settings for Defender for Endpoint](configure-proxy-internet).

To ensure Microsoft Defender Antivirus cloud-delivered protection works properly, your security team must configure your network to allow connections between your endpoints and certain Microsoft servers. This article lists which destinations must be accessible. It also provides instructions for validating connections. Configuring connectivity properly ensures your organization receives the best value from Microsoft Defender Antivirus cloud-delivered protection services.

## Prerequisites

### Supported operating systems

The following operating systems are supported:

- Windows

## Allow connections to the Microsoft Defender Antivirus cloud service

The Microsoft Defender Antivirus cloud service provides fast, strong protection for your endpoints. While it's optional to enable and use the cloud-delivered protection services provided by Microsoft Defender Antivirus, it's highly recommended because it provides important and timely protection against emerging threats on your endpoints and network. For more information, see [Enable cloud-delivered protection](cloud-protection-configure), which describes how to enable the service by using Intune, Microsoft Configuration Manager, Group Policy, PowerShell cmdlets, or individual clients in the Windows Security app.

After you've enabled Microsoft Defender Antivirus cloud-delivered protection, you need to configure your network or firewall to allow connections between network and your endpoints. Computers must have access to the internet and reach the Microsoft cloud services for proper operation.

Note

The Microsoft Defender Antivirus cloud service delivers updated protection to your network and endpoints. The cloud service should not be considered as protection for or against files that are stored in the cloud; instead, the cloud service uses distributed resources and machine learning to deliver protection for your endpoints at a faster rate than the traditional Security intelligence updates, and applies to file-based and file-less threats, regardless of where the threats originate.

## Required Microsoft Defender Antivirus services and URLs

The following table lists services and their associated website addresses (URLs).

Make sure that there are no firewall or network filtering rules denying access to the Microsoft Defender Antivirus connectivity URLs listed in the following table. Otherwise, you must create an allow rule specifically for the required Microsoft Defender Antivirus connectivity URLs. The Microsoft Defender Antivirus connectivity URLs use port `443` for communication. (Port `80` is also required for some URLs, as noted in the service and URL table.)

| Service and description | URL |
| --- | --- |
| Microsoft Defender Antivirus cloud-delivered protection service is referred to as Microsoft Active Protection Service (MAPS). Microsoft Defender Antivirus uses the MAPS service to provide cloud-delivered protection. | `*.wdcp.microsoft.com``*.wdcpalt.microsoft.com``*.wd.microsoft.com` |
| Microsoft Update Service (MU) and Windows Update Service (WU)These services allow security intelligence and product updates. | `*.update.microsoft.com``*.delivery.mp.microsoft.com``*.windowsupdate.com``ctldl.windowsupdate.com`For more information, see [Connection endpoints for Windows Update](/en-us/windows/privacy/manage-windows-1709-endpoints#windows-update). |
| Security intelligence updates Alternate Download Location (ADL)This is an alternate location for Microsoft Defender Antivirus Security intelligence updates, if the installed Security intelligence is out of date (Seven or more days behind). | `*.download.microsoft.com``*.download.windowsupdate.com` (Port 80 is required)`go.microsoft.com` (Port 80 is required)`https://www.microsoft.com/security/encyclopedia/adlpackages.aspx``https://definitionupdates.microsoft.com/download/DefinitionUpdates/``https://fe3cr.delivery.mp.microsoft.com/ClientWebService/client.asmx` |
| Malware submission storageThis is an upload location for files submitted to Microsoft via the Submission form or automatic sample submission. | `ussus1eastprod.blob.core.windows.net``ussus2eastprod.blob.core.windows.net``ussus3eastprod.blob.core.windows.net``ussus4eastprod.blob.core.windows.net``wsus1eastprod.blob.core.windows.net``wsus2eastprod.blob.core.windows.net``ussus1westprod.blob.core.windows.net``ussus2westprod.blob.core.windows.net``ussus3westprod.blob.core.windows.net``ussus4westprod.blob.core.windows.net``wsus1westprod.blob.core.windows.net``wsus2westprod.blob.core.windows.net``usseu1northprod.blob.core.windows.net``wseu1northprod.blob.core.windows.net``usseu1westprod.blob.core.windows.net``wseu1westprod.blob.core.windows.net``ussuk1southprod.blob.core.windows.net``wsuk1southprod.blob.core.windows.net``ussuk1westprod.blob.core.windows.net``wsuk1westprod.blob.core.windows.net` |
| Certificate Revocation List (CRL)Windows use this list while creating the SSL connection to MAPS for updating the CRL. | `http://www.microsoft.com/pkiops/crl/``http://www.microsoft.com/pkiops/certs``http://crl.microsoft.com/pki/crl/products``http://www.microsoft.com/pki/certs` |
| Universal GDPR ClientWindows use this client to send the client diagnostic data.Microsoft Defender Antivirus uses General Data Protection Regulation for product quality, and monitoring purposes. | The update uses SSL (TCP Port 443) to download manifests and upload diagnostic data to Microsoft that uses the following DNS endpoints:`vortex-win.data.microsoft.com``settings-win.data.microsoft.com` |

## Validate connections between your network and the cloud

After allowing the listed URLs, verify that your endpoints can connect to the Microsoft Defender Antivirus cloud service and can send and receive data correctly.

### Use the MpCmdRun command-line tool to validate cloud-delivered protection

Verify that your network can communicate with the Microsoft Defender Antivirus cloud service:

In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, the command changes the directory to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -ValidateMapsConnection
```

For more information about MpCmdRun, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

#### Common cloud validation error messages

Here are some error messages you might see. If the connectivity test starts but fails, the output begins with a timestamp and then shows a `ValidateMapsConnection` failure:

```console
Start Time: <Day_of_the_week> MM DD YYYY HH:MM:SS
MpEnsureProcessMitigationPolicy: hr = 0x1
ValidateMapsConnection
```

If the device can't reach MAPS due to a connectivity issue, the command returns an error similar to one of the following examples:

```console
ValidateMapsConnection failed to establish a connection to MAPS (hr=0x80070006 httpcore=451)
MpCmdRun.exe: hr = 0x80070006
```

If certificate validation or TLS negotiation fails, you might see output similar to the following:

```console
ValidateMapsConnection failed to establish a connection to MAPS (hr=0x80072F8F httpcore=451)
MpCmdRun.exe: hr = 0x80072F8F
```

If the connection is interrupted or times out, the validation command can return output similar to the following:

```output
ValidateMapsConnection failed to establish a connection to MAPS (hr=0x80072EFE httpcore=451)
MpCmdRun.exe: hr = 0x80072EFE
```

#### Root causes of cloud validation failures

The root cause of the `ValidateMapsConnection` error messages is that the device doesn't have its system-wide `WinHttp` proxy configured. If you don't set the system-wide WinHttp proxy, then the operating system isn't aware of the proxy and can't fetch the certificate revocation list (CRL) (the operating system does this, not Defender for Endpoint), which means that TLS connections to URLs like `http://cp.wd.microsoft.com/` don't succeed. You see successful (response 200) connections to the endpoints, but the MAPS connections would still fail.

#### Solutions for cloud validation failures

Use one of the following approaches to resolve cloud validation failures:

- **Preferred solution**: Configure the system-wide WinHttp proxy that allows the CRL check.
- **Alternate solution**: Configuring the following `SSLOption` registry key and value to Disable the CRL check for SpyNet only. The `SSLOptions` registry key doesn't affect other services. Disabling the CRL check isn't a best practice because the device no longer checks for revoked certificates or certificate pinning.

    To disable the CRL check for SpyNet, import a registry file with the following content:

    ```text
    Windows Registry Editor Version 5.00
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\Spynet]
    "SSLOptions"=dword:00000002
    ```

    The available values are:

    - **0**: Disable pinning and revocation checks.
    - **1**: Disable pinning.
    - **2**: Disable revocation checks only.
    - **3** (default): Enable revocation checks and pinning.

## Attempt to download a fake malware file from Microsoft

You can download a [cloud-delivered protection test file](defender-endpoint-demonstration-cloud-delivered-protection) that Microsoft Defender Antivirus will detect and block if your device is properly connected to the Microsoft Defender Antivirus cloud service.

Note

The downloaded file is not exactly malware. It's a fake file designed to test whether your device is properly connected to the Microsoft Defender Antivirus cloud service.

If you're properly connected, you'll see a warning Microsoft Defender Antivirus notification.

If you're using Microsoft Edge, you'll also see a notification message:

[![The notification that malware was found in Edge](/en-us/defender/media/wdav-bafs-edge.png)](/en-us/defender/media/wdav-bafs-edge.png#lightbox)

Internet Explorer also displays a malware-detected notification:

[![The Microsoft Defender Antivirus notification that malware was found](/en-us/defender/media/wdav-bafs-ie.png)](/en-us/defender/media/wdav-bafs-ie.png#lightbox)

### View the fake malware detection in your Windows Security app

To view the fake malware detection in the Windows Security app, perform the following steps:

1. On your task bar, select the Shield icon, open the **Windows Security** app. Or, search the **Start** for *Security*.
2. Select **Virus & threat protection**, and then select **Protection history**.
3. Under the **Quarantined threats** section, select **See full history** to see the detected fake malware.

    Note

    Versions of Windows 10 before version 1703 have a different user interface. See [Microsoft Defender Antivirus in the Windows Security app](microsoft-defender-security-center-antivirus).

    The Windows event log will also show Microsoft Defender Antivirus event ID 1116. For more information, see [Troubleshoot Microsoft Defender Antivirus event ID 1116](troubleshoot-microsoft-defender-antivirus).

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)