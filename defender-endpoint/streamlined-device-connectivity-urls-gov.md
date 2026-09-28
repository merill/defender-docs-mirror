---
layout: Conceptual
title: Microsoft Defender for Endpoint streamlined connectivity URLs - US government environments (Preview) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/streamlined-device-connectivity-urls-gov
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get a list of the streamlined connectivity URLs required to onboard and maintain devices in Microsoft Defender for Endpoint in US Government cloud environments (GCC, GCC High, DoD).
author: limwainstein
ms.author: lwainstein
ms.topic: how-to
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.reviewer: pahuijbr
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 564fe270-2f36-07cf-05bf-dfd3b59375f1
document_version_independent_id: 564fe270-2f36-07cf-05bf-dfd3b59375f1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/streamlined-device-connectivity-urls-gov.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: streamlined-device-connectivity-urls-gov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/streamlined-device-connectivity-urls-gov.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 81df4f71-a1fe-a34f-1dda-d40018605d54
---

# Microsoft Defender for Endpoint streamlined connectivity URLs - US government environments (Preview) - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

This article includes a list of the streamlined connectivity URLs required to onboard and maintain devices in Microsoft Defender for Endpoint in US Government cloud environments (GCC, GCC High, DoD). Before you configure these URLs, make sure your environment meets the prerequisites.

## Prerequisites

Before using the streamlined connectivity URLs listed in this article, ensure your devices meet the required OS versions, have up-to-date antimalware platform and EDR sensor components, and are onboarded using a supported method. For full details, see the prerequisites for [streamlined connectivity](configure-device-connectivity#prerequisites).

### Notes

The following notes describe device versions that still require legacy or expanded URL lists.

- Devices running Defender for Endpoint delivered via the Microsoft Monitoring Agent (MMA, also known as the Log Analytics Agent - specifically, Windows 7 SP1, Windows 8.1, Windows Server 2008 R2 and those Windows Server 2012 R2, 2016 devices not upgraded to the modern unified solution) will continue using the associated legacy method. For the list of additional URLs, refer to the Windows 7, 8.1, 2008R2 (MMA) tab in [Onboard devices using streamlined connectivity for Microsoft Defender for Endpoint](configure-device-connectivity).
- Devices running Windows version 1607, 1703, 1709, 1803 can onboard using the new onboarding package but still require a longer list of URLs. The Windows 1607 to 1803 tab in [Onboard devices using streamlined connectivity for Microsoft Defender for Endpoint](configure-device-connectivity) lists the additional URLs required.

## US Gov URLs

The following tables list the required streamlined connectivity endpoints for US Government cloud environments, organized by function.

### General URLs

Note

Make sure your devices meet all component (app/antimalware platform, engine, EDR sensor) update versions and OS requirements else onboarding might be unsuccessful. You can re-onboard devices to switch them to streamlined connectivity if they meet these requirements.

| Service | Geography | Category | Port | Endpoint/URL | Description | Required | Win 11/10/Server (Unified) | Win 7/8.1 | Server (MMA) | Mac | Linux |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Consolidated Defender for Endpoint services | USGov | Streamlined connectivity URL | 443 | \*.endpoint.security.microsoft.us | Streamlined connectivity URL consolidation and future services | Required | Yes | No | Yes | Yes | Yes |
| Microsoft Defender SmartScreen | GCC | Reporting and Notifications | 443 | unitedstates4.ss.wd.microsoft.us | SmartScreen protection, reporting, notifications, Network Protection, custom URL indicators | Required | Yes |  |  | Yes | Yes |
| Microsoft Defender SmartScreen | GCC High | Reporting and Notifications | 443 | unitedstates1.ss.wd.microsoft.us | SmartScreen protection, reporting, notifications, Network Protection, custom URL indicators | Required | Yes |  |  | Yes | Yes |
| Microsoft Defender SmartScreen | DoD | Reporting and Notifications | 443 | unitedstates2.ss.wd.microsoft.us | SmartScreen protection, reporting, notifications, Network Protection, custom URL indicators | Required | Yes |  |  | Yes | Yes |
| Defender for Endpoint | DoD | Internal configuration management | 443 | https://config.ecs.dod.teams.microsoft.us/config/v1 | This URL must be allowed to enable Defender on Linux endpoints to receive internal configurations from the cloud. | Required |  |  |  |  | Yes |
| Defender for Endpoint | GCC High | Internal configuration management | 443 | https://config.ecs.gov.teams.microsoft.us/config/v1 | This URL must be allowed to enable Defender on Linux endpoints to receive internal configurations from the cloud. | Required |  |  |  |  | Yes |
| Defender for Endpoint | GCC Mod | Internal configuration management | 443 | https://gccmod.ecs.office.com/config/v1 | This URL must be allowed to enable Defender on Linux endpoints to receive internal configurations from the cloud. | Required |  |  |  |  | Yes |

### URLs used for updates

Note

Depending on your environment, you may apply updates from a file share or update server and don't need to allow (all) direct connections from devices, or these connections are already required and allowed in your environment for other purposes such as Windows updates.

This table lists URL endpoints used by Microsoft Defender Antivirus. These endpoints are optional when updates are managed internally using WSUS, Configuration Manager, or a file share.

| Service | Geography | Category | Port | Endpoint/URL | Description | Required/Optional | Win 11/10/Server (Unified) | Win 7/8.1 | Server (MMA) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Defender Antivirus | US Gov | MU/WU | 443 | \*.update.microsoft.com | Security intelligence and product updates | Optional | Yes | Yes | Yes |
| Microsoft Defender Antivirus | US Gov | MU/WU | 443 | \*.delivery.mp.microsoft.com | Security intelligence and product updates | Optional | Yes | Yes | Yes |
| Microsoft Defender Antivirus | US Gov | MU/WU | 443 | \*.windowsupdate.com | Security intelligence and product updates | Optional | Yes | Yes | Yes |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | \*.download.windowsupdate.com | Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | \*.download.microsoft.com | Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | fe3cr.delivery.mp.microsoft.com/ClientWebService/client.asmx | Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |

## URLs used for certificate validation checks

Note

Certificate validation is performed through the Windows operating system, helping to prevent abuse of compromised certificates. This means the operating system must be able to connect to these destinations, or, should be updated with the latest certificate trust lists if they can't retrieve them from Microsoft directly. For more information, see [Configure trusted roots and disallowed certificates in Windows](/en-us/windows-server/identity/ad-cs/configure-trusted-roots-disallowed-certificates).

| Service | Geography | Category | Port | Endpoint/URL | Description | Required/Optional | Win 11/10/Server (Unified) | Win 7/8.1 | Server (MMA) | Mac | Linux |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | crl.microsoft.com/pki/crl/\* | Certificate Revocation Lists - required to validate certificates / Used by Windows when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | ctldl.windowsupdate.com | Expands on the existing automatic root update mechanism technology to let certificates that are compromised or untrusted be specifically flagged as untrusted | Required | Yes |  |  |  |  |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | www.microsoft.com/pkiops/\* | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | http://www.microsoft.com/pki/certs | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |

### Live Response and notification URLs

Note

The following Live Response performance URLs are required (Direct Connection/Proxy bypass required)

| Service | Geography | Category | Port | Endpoint/URL | Description | Required/Optional | Win 11/10/Server (Unified) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | \*.wns.windows.com | Windows Push Notification Services (WNS) - Live Response | Required | Yes |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | login.microsoftonline.us | Windows Push Notification Services (WNS) - Live Response | Required | Yes |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | login.live.com | Windows Push Notification Services (WNS) - Live Response | Required | Yes |

## Defender portal URLs

Note

The following table lists the required URL endpoints for accessing the Microsoft Defender portal.

| Service | Geography | URL |
| --- | --- | --- |
| Microsoft Defender for Endpoint | US Gov | \*.blob.core.usgovcloudapi.net |
| Microsoft Defender for Endpoint | US Gov | crl.microsoft.com |
| Microsoft Defender for Endpoint | US Gov | https://\*.microsoftonline-p.com |
| Microsoft Defender for Endpoint | US Gov | https://secure.aadcdn.microsoftonline-p.com |
| Microsoft Defender for Endpoint | US Gov | https://static2.sharepointonline.com |
| Microsoft Defender for Endpoint | GCC | https://login.microsoftonline.com |
| Microsoft Defender for Endpoint | GCC | https://\*.gcc.securitycenter.microsoft.us |
| Microsoft Defender for Endpoint | GCC | https://onboardingpckgsusmvprd.blob.core.usgovcloudapi.net |
| Microsoft Defender for Endpoint | GCC High | https://login.microsoftonline.us |
| Microsoft Defender for Endpoint | GCC High | https://\*.securitycenter.microsoft.us |
| Microsoft Defender for Endpoint | GCC High | https://onboardingpckgsusgvprd.blob.core.usgovcloudapi.net |
| Microsoft Defender for Endpoint | DoD | https://login.microsoftonline.us |
| Microsoft Defender for Endpoint | DoD | https://\*.securitycenter.microsoft.us |
| Microsoft Defender for Endpoint | DoD | https://onboardingpckgsusgvprd.blob.core.usgovcloudapi.net |

## Client processes that require network connectivity

The following Microsoft Defender for Endpoint client processes generate network communications. Make sure that communications from each of these processes are not blocked. The included list identifies specific executable processes (such as `MsSense.exe` and `MsMpEng.exe`) that must be permitted through firewalls and proxies for Defender for Endpoint to function correctly.

Select the tab for information about exclusions for that operating system.

The processes in this section are exclusively for Microsoft Defender for Endpoint for Windows platforms, including down-level OS. This list doesn't account for any other Windows communications requirements.

# [Windows](#tab/Windows)
The specific exclusions to configure depend on which version of Windows your endpoints or devices are running, and are listed in the following table.

| OS | Exclusions |
| --- | --- |
| Windows 11Windows 10, version 1803 or later (See Windows 10 release information)Windows 10, version 1703 or 1709 with KB4493441 installedWindows Server 2025  Azure Stack HCI OS, version 23H2 and later Windows Server 2022Windows Server 2019Windows Server, version 1803Windows Server 2016 running the modern unified solutionWindows Server 2012 R2 running the modern unified solution | **EDR exclusions**: `C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCncProxy.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseSampleUploader.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseIR.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCM.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseNdr.exe``C:\Program Files\Windows Defender Advanced Threat Protection\Classification\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection``C:\Program Files\Windows Defender Advanced Threat Protection\SenseTVM.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseTracer.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseDlpProcessor.exe`**Registry path**:`HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection\*`**Antivirus exclusions**:`C:\Program Files\Windows Defender\MsMpEng.exe``C:\Program Files\Windows Defender\NisSrv.exe``C:\Program Files\Windows Defender\ConfigSecurityPolicy.exe``C:\Program Files\Windows Defender\MpCmdRun.exe``C:\Program Files\Windows Defender\MpDefenderCoreService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MsMpEng.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\NisSrv.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\ConfigSecurityPolicy.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCopyAccelerator.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCmdRun.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDefenderCoreService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\mpextms.exe`**Endpoint Data Loss Prevention (Endpoint DLP) exclusions**:`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpService.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpCmd.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MipDlp.exe``C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\DlpUserAgent.exe` |
| Windows Server 2016 or Windows Server 2012 R2 running the [modern unified solution](/en-us/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fswitch-to-mde-phase-2.md/main/76b249d7-f914-4c03-3eaf-48aa43b2fa4a/onboard-server.md) | The following **additional** exclusions are required after updating the Sense EDR component using [KB5005292](https://support.microsoft.com/servicing/Management-Tools/microsoft-defender/update/microsoft-defender-for-endpoint-update-for-edr-sensor): `C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\MsSense.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCnCProxy.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseIR.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseSampleUploader.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCM.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseTVM.exe` |
| [Windows 8.1](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)[Windows 7](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1)[Windows Server 2008 R2 SP1](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) | `C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Monitoring Host Temporary Files 6\45\MsSenseS.exe`( Monitoring Host Temporary Files 6\45 can be different numbered subfolders.) `C:\Program Files\Microsoft Monitoring Agent\Agent\AgentControlPanel.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HealthService.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HSLockdown.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MOMPerfSnapshotHelper.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MonitoringHost.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\TestCloudConnection.exe` |

# [macOS](#tab/macOS)
For macOS devices, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
| --- | --- |
| `wdavdaemon_enterprise`EDR engine | `/Library/Application Support/Microsoft/Defender/` |
| `wdavdaemon_unprivileged`Antivirus engine | `/Library/Application Support/Microsoft/Defender/` |
| `telemetryd_v1`Telemetry daemon for EDR | `/Library/Application Support/Microsoft/Defender/` |
| `Netext`Network extension | `/Library/SystemExtensions/*/com.microsoft.wdav.netext.systemextension/Contents/MacOS/` |
| `Epsext`Endpoint security extension | `/Library/SystemExtensions/*/com.microsoft.wdav.epsext.systemextension/Contents/MacOS/` |
| `msupdate`Microsoft AutoUpdate update tool | `/Library/Application\ Support/Microsoft/MAU2.0/Microsoft\ AutoUpdate.app/Contents/MacOS` |

# [Linux](#tab/Linux)
For Linux servers, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
| --- | --- |
| `wdavdaemon`Core daemon (service). Uses FANotify for both antimalware and EDR purposes (TALPA on older RHEL). | `/opt/microsoft/mdatp/sbin/` |
| `wdavdaemon enterprise`EDR engine. Used for enrichment. | `/opt/microsoft/mdatp/sbin/` |
| `wdavdaemon unprivileged` Antivirus engine | `/opt/microsoft/mdatp/sbin/` |
| `crashpad_handler`Collects crash dumps | `/opt/microsoft/mdatp/sbin/` |
| `mdatp`Command line utility | `/opt/microsoft/mdatp/sbin/Wdavdaemonclient` |
| `mde_netfilter`Packet filter for Network protection, also used for response capabilities | `/opt/microsoft/mde_netfilter/sbin` |

---

## Changelog

| Date | Change log |
| --- | --- |
| 03/23/2026 | Renamed **Microsoft Defender process exclusions** section to **Client processes**, and aligned the content for all URL lists. |
| 03/03/2026 | Added Linux URLs to General URLs for internal configuration management: `config.ecs.dod.teams.microsoft.us` (DoD), `config.ecs.gov.teams.microsoft.us` (GCC High), `gccmod.ecs.office.com` (GCC Mod). |
| 10/23/2025 | Initial page published (Preview). |