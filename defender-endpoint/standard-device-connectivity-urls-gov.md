---
layout: Conceptual
title: Microsoft Defender for Endpoint standard connectivity URLs - US government - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/standard-device-connectivity-urls-gov
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get a list of the standard connectivity URLs required to onboard and maintain devices in Microsoft Defender for Endpoint in US government cloud environments.
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
document_id: dad00c3b-e0f1-db77-265a-183312695dc0
document_version_independent_id: dad00c3b-e0f1-db77-265a-183312695dc0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/standard-device-connectivity-urls-gov.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standard-device-connectivity-urls-gov
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/standard-device-connectivity-urls-gov.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b62b1063-619c-2bd0-0021-b08491b189df
---

# Microsoft Defender for Endpoint standard connectivity URLs - US government - Microsoft Defender for Endpoint | Microsoft Learn

This article lists the standard connectivity URLs required to onboard and maintain devices in Microsoft Defender for Endpoint in US government cloud environments, including GCC, GCC High, and DoD. Network and security administrators should allow these URLs through firewalls and proxy servers to ensure that Defender for Endpoint services can communicate correctly.

## Microsoft Defender URLs

The following table lists the Microsoft Defender URLs required for US government cloud environments, including GCC, GCC High, and DoD.

| Service | Geography | Category | Port | Endpoint/URL | Endpoint/URL Description | Required / Optional | Windows 10/11 / Server 2019 -2022 / Server 2012 R2/Server 2016 (Unified Agent) | Windows 7 / 8.1 | Windows Server 2008 R2 / 2012 R2 / 2016 (MMA Based) | Mac | Linux | Comments |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | `crl.microsoft.com/pki/crl/*` | Certificate Revocation Lists - required to validate certificates / Used by Windows when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | `ctldl.windowsupdate.com` | Expands on the existing automatic root update mechanism technology to let certificates that are compromised or untrusted be specifically flagged as untrusted | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | `www.microsoft.com/pkiops/*` | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US Gov | CRL | 80 | `http://www.microsoft.com/pki/certs` | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | `events.data.microsoft.com` | Used by the Connected User Experiences and Telemetry component and connects to the Microsoft Data Management service | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | `*.wns.windows.com` | Windows Push Notification Services (WNS) - Live Response | Required | Yes |  |  |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required) |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | `login.microsoftonline.com` | Windows Push Notification Services (WNS) - Live Response | Required | Yes |  |  |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required) |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | `login.live.com` | Windows Push Notification Services (WNS) - Live Response | Required | Yes |  |  |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required) |
| Microsoft Defender for Endpoint | US Gov | Common | 443 | `settings-win.data.microsoft.com` | Connected User Experiences and Telemetry Channel | Optional | Yes |  |  |  |  | Not required for Windows 10 1809 (RS5) and above / Windows 2019 |
| Microsoft Defender for Endpoint | US Gov | Common (Mac) (Linux) | 443 | `cdn.x.cp.wd.microsoft.com` | Microsoft Defender Antivirus Content Delivery Network (CDN) - Security Intelligence updates | Required |  |  | Yes | Yes |  |  |
| Microsoft Defender for Endpoint | WW | Common (Mac/Linux) | 443 | Root URL for public Microsoft CDN endpoints (referred to as ChannelURL) - for the updated URL, see [Using Custom channel and ManifestServer to control updates](/en-us/microsoft-365-apps/mac/mau-configure-organization-specific-updates) |  |  |  |  |  |  |  |  |
| Microsoft Defender for Endpoint | US Gov | Common (Mac/Linux) | 443 | Root URL for public Microsoft CDN endpoints (referred to as ChannelURL) - for the updated URL, see [Using Custom channel and ManifestServer to control updates](/en-us/microsoft-365-apps/mac/mau-configure-organization-specific-updates) | Microsoft Office Content Delivery Network (CDN) - Product Updates | Required |  |  |  | Yes | Yes | New CDN endpoint starting with macOS build 101.26012.0012 |
| Microsoft Defender for Endpoint | US Gov | Microsoft Monitoring Agent (MMA) | 443 | `*.ods.opinsights.azure.us` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | US Gov | Microsoft Monitoring Agent (MMA) | 443 | `*.oms.opinsights.azure.us` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | US Gov | Microsoft Monitoring Agent (MMA) | 443 | `*.blob.core.usgovcloudapi.net` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `unitedstates4.x.cp.wd.microsoft.us` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `us4-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `winatp-gw-usmt.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `winatp-gw-usmv.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `automatedirstrfmusmt.blob.core.usgovcloudapi.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `automatedirstrfmusmv.blob.core.usgovcloudapi.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `ussusg1virginiaff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `ussusg2virginiaff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `wsusg1virginiaff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `ussusg1texasff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `ussusg2texasff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC | Microsoft Defender for Endpoint GCC | 443 | `wsusg1texasff4.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `unitedstates1.x.cp.wd.microsoft.us` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `us4-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `winatp-gw-usgt.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `automatedirstrffusgv.blob.core.usgovcloudapi.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes | Yes | Yes |  |  |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `ussusg1virginiaff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `ussusg2virginiaff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `wsusg1virginiaff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `ussusg1texasff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `ussusg2texasff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | GCC High | Microsoft Defender for Endpoint GCC High | 443 | `wsusg1texasff0.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `unitedstates2.x.cp.wd.microsoft.us` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required | Yes |  |  | Yes | Yes | Yes |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `us4-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `winatp-gw-usgt.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `winatp-gw-usgv.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `automatedirstrffusgt.blob.core.usgovcloudapi.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `automatedirstrffusgv.blob.core.usgovcloudapi.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `ussusd1centralff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `ussusd2centralff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `wsusd1centralff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `ussusd1eastff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `ussusd2eastff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | DoD | Microsoft Defender for Endpoint DoD | 443 | `wsusd1eastff5.blob.core.usgovcloudapi.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender Antivirus | US Gov | MU / WU | 443 | `*.update.microsoft.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU / WU | 443 | `*.delivery.mp.microsoft.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU / WU | 443 | `*.windowsupdate.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | `*.download.windowsupdate.com` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | `*.download.microsoft.com` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | `*.definitionupdates.microsoft.com` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | US Gov | MU (ADL) | 443 | `fe3cr.delivery.mp.microsoft.com/ClientWebService/client.asmx` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | GCC | MAPS | 443 | `unitedstates4.cp.wd.microsoft.us` | MAPS - Used by Microsoft Defender Antivirus to provide cloud-delivered protection | Required | Yes |  |  |  |  |  |
| Microsoft Defender Antivirus | GCC High | MAPS | 443 | `unitedstates1.cp.wd.microsoft.us` | MAPS - Used by Microsoft Defender Antivirus to provide cloud-delivered protection | Required | Yes |  |  |  |  |  |
| Microsoft Defender Antivirus | DoD | MAPS | 443 | `unitedstates2.cp.wd.microsoft.us` | MAPS - Used by Microsoft Defender Antivirus to provide cloud-delivered protection | Required | Yes |  |  |  |  |  |
| Microsoft Defender SmartScreen | GCC | Reporting and Notifications | 443 | `unitedstates4.ss.wd.microsoft.us` | Used for Microsoft Defender SmartScreen protection, reporting, and notifications. Microsoft Defender Antivirus Network Protection and custom URL indicators | Required | Yes |  |  | Yes | Yes | Microsoft Defender SmartScreen reporting and notifications. Network Protection and custom URL indicators |
| Microsoft Defender SmartScreen | GCC High | Reporting and Notifications | 443 | `unitedstates1.ss.wd.microsoft.us` | Used for Microsoft Defender SmartScreen protection, reporting, and notifications. Microsoft Defender Antivirus Network Protection and custom URL indicators | Required | Yes |  |  | Yes | Yes | Microsoft Defender SmartScreen reporting and notifications. Network Protection and custom URL indicators |
| Microsoft Defender SmartScreen | DoD | Reporting and Notifications | 443 | `unitedstates2.ss.wd.microsoft.us` | Used for Microsoft Defender SmartScreen protection, reporting, and notifications. Microsoft Defender Antivirus Network Protection and custom URL indicators | Required | Yes |  |  | Yes | Yes | Microsoft Defender SmartScreen reporting and notifications. Network Protection and custom URL indicators |
| Consolidated Defender for Endpoint services | WW | Streamlined connectivity new URL pattern | 443 | `*.endpoint.security.microsoft.com` | Used for streamlined connectivity URL consolidation as well as for future services | Required | Yes | No | Yes | Yes | Yes | Only required for streamlined connectivity initially. New services also follow this new pattern. |

## Defender portal URLs

Note

All URLs in this table are required to have access to the Microsoft Defender Security Center Portal URL.

| Service | Geography | URL |
| --- | --- | --- |
| Microsoft Defender for Endpoint | US Gov | `*.blob.core.usgovcloudapi.net` |
| Microsoft Defender for Endpoint | US Gov | `crl.microsoft.com` |
| Microsoft Defender for Endpoint | US Gov | `https://*.microsoftonline-p.com` |
| Microsoft Defender for Endpoint | US Gov | `https://secure.aadcdn.microsoftonline-p.com` |
| Microsoft Defender for Endpoint | US Gov | `https://static2.sharepointonline.com` |
| Microsoft Defender for Endpoint | GCC | `https://login.microsoftonline.com` |
| Microsoft Defender for Endpoint | GCC | `https://*.gcc.securitycenter.microsoft.us` |
| Microsoft Defender for Endpoint | GCC | `https://onboardingpckgsusmvprd.blob.core.usgovcloudapi.net` |
| Microsoft Defender for Endpoint | GCC High | `https://login.microsoftonline.us` |
| Microsoft Defender for Endpoint | GCC High | `https://*.securitycenter.microsoft.us` |
| Microsoft Defender for Endpoint | GCC High | `https://onboardingpckgsusgvprd.blob.core.usgovcloudapi.net` |
| Microsoft Defender for Endpoint | DoD | `https://login.microsoftonline.us` |
| Microsoft Defender for Endpoint | DoD | `https://onboardingpckgsusgvprd.blob.core.usgovcloudapi.net` |

## Required client processes

The following Defender for Endpoint-related client processes generate network communications. Make sure that communications from these processes are not blocked.

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

The following table summarizes recent changes to this article.

| Date | Change log |
| --- | --- |
| 04/14/2026 | Replaced `officecdn-microsoft-com.akamaized.net` with new CDN ChannelURL reference for Mac/Linux product updates. New CDN endpoint starting with macOS build 101.26012.0012. |
| 03/23/2026 | Renamed **Microsoft Defender processes** section to **Client processes**, and aligned the content for all URL lists. |
| 15/08/2023 | Removed URL: `https://msdl.microsoft.com/download/symbols`. |
| 05/12/2022 | URL details updated:Updated line 58: Updated from required to optional.Updated line 62: Changed from optional to required. Guidance text updated. Added Mac and Linux.Updated line 63: Changed from optional to required. Guidance text updated. Added Mac and Linux.Updated line 64: Changed from optional to required. Guidance text updated. Added Mac and Linux. |
| 27/05/2022 | Removed preview status from Server 2012 R2 and Server 2016 Unified Agent references.Updated line 4: URL required for Mac and Linux platforms.Updated line 5: URL required for Mac and Linux platforms. |
| 25/01/2022 | Duplicate URLs consolidated.Optional field added.US Gov, GCC, and GCC High guidance moved to separate spreadsheet.URLs removed:`eu-cdn.x.cp.wd.microsoft.com`; `wu-cdn.x.cp.wd.microsoft.com`; `*.azure-automation.net`; `*.notify.windows.com` |