---
layout: Conceptual
title: Microsoft Defender for Endpoint standard connectivity URLs - commercial - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/standard-device-connectivity-urls-commercial
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get a list of the standard connectivity URLs required to onboard and maintain devices in Microsoft Defender for Endpoint in US commercial cloud environments.
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
document_id: fbf1ba55-e25d-3845-f203-e798e68c1872
document_version_independent_id: fbf1ba55-e25d-3845-f203-e798e68c1872
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/standard-device-connectivity-urls-commercial.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standard-device-connectivity-urls-commercial
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/standard-device-connectivity-urls-commercial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 40d3f024-a5ec-0bc4-4603-042772f19fd9
---

# Microsoft Defender for Endpoint standard connectivity URLs - commercial - Microsoft Defender for Endpoint | Microsoft Learn

This article lists the URLs needed to onboard and maintain devices in Microsoft Defender for Endpoint in commercial cloud environments. Use this list to set up firewall or proxy allow rules so devices can reach the required services.

## Microsoft Defender URLs

This section lists the Microsoft Defender service URLs organized by geography and category. Allow these endpoints in your firewall or proxy to ensure proper device connectivity.

| Service | Geography | Category | Port | Endpoint/URL | Endpoint/URL Description | Required or Optional | Windows 10, 11; Server 2022, 2019, 2016 (Unified Agent); Server 2012 R2 (Unified Agent) | Windows 7, 8.1 | Windows Server 2008 R2, 2012 R2, 2016 (MMA Based) | Mac | Linux | Comments |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Defender for Endpoint | WW | CRL | 80 | `crl.microsoft.com` | Certificate Revocation Lists - required to validate certificates / Used by Windows when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | CRL | 80 | `ctldl.windowsupdate.com` | Expands on the existing automatic root update mechanism technology to let certificates that are compromised or untrusted be specifically flagged as untrusted | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | WW | CRL | 80 | `www.microsoft.com/pkiops/*` | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | CRL | 80 | `www.microsoft.com/pki/*` | Used when creating the SSL connection to MAPS for updating the CRL | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | Common | 443 | `events.data.microsoft.com` | Used by the Connected User Experiences and Telemetry component and connects to the Microsoft Data Management service | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | Common | 443 | `*.wns.windows.com` | Windows Push Notification Services (WNS) - Live Response | Optional | Yes |  |  |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required) |
| Microsoft Defender for Endpoint | WW | Common | 443 | `login.microsoftonline.com` | Windows Push Notification Services (WNS) - Live Response / Vulnerability assessment for network devices / Security Management for Microsoft Defender for Endpoint - Azure Registration | Optional | Yes | Yes | Yes |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required). Required when using Security Management for Microsoft Defender for Endpoint |
| Microsoft Defender for Endpoint | WW | Common | 443 | `login.live.com` | Windows Push Notification Services (WNS) - Live Response | Optional | Yes |  |  |  |  | Required for Live Response Performance (Direct Connection or proxy bypass required) |
| Microsoft Defender for Endpoint | WW | Common | 443 | `settings-win.data.microsoft.com` | Connected User Experiences and Telemetry Channel | Optional | Yes |  |  |  |  | Only required for Windows 10 1703 and below. Not required on Windows Server. |
| Microsoft Defender for Endpoint | WW | Common (Mac/Linux) | 443 | `x.cp.wd.microsoft.com` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | Common (Mac/Linux) | 443 | `cdn.x.cp.wd.microsoft.com` | Microsoft Defender Antivirus Content Delivery Network (CDN) - Security Intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | WW | Mac | 443 | Root URL for public Microsoft CDN endpoints (referred to as ChannelURL) - for the updated URL, see [Using Custom channel and ManifestServer to control updates](/en-us/microsoft-365-apps/mac/mau-configure-organization-specific-updates) | Microsoft Office Content Delivery Network (CDN) - Product Updates | Required |  |  |  | Yes |  | New CDN endpoint starting with macOS build 101.26012.0012 |
| Microsoft Defender for Endpoint | WW | Common (Linux) | 443 | `packages.microsoft.com` | Required to download and update the MDE Linux agent | Required |  |  |  |  | Yes |  |
| Microsoft Defender for Endpoint | WW | Microsoft Defender for Endpoint | 443 | `login.windows.net` | Microsoft Defender for Endpoint Vulnerability assessment for network devices (network scanner) | Optional | Yes | Yes | Yes |  |  | Supported on Windows 8 and above and Windows Server 2012 and above |
| Microsoft Defender for Endpoint | WW | Microsoft Defender for Endpoint | 443 | `*.security.microsoft.com` | Microsoft Defender for Endpoint Vulnerability assessment for network devices (network scanner) | Optional | Yes | Yes | Yes |  |  | Supported on Windows 8 and above and Windows Server 2012 and above |
| Microsoft Defender for Endpoint | WW | Microsoft Defender for Endpoint | 443 | `reflector.defender.microsoft.com` | Used to probe IPv6 connectivity | Optional | Yes | Yes | Yes | Yes | Yes | Helps Microsoft Security Intelligence detect attacker activity |
| Microsoft Defender for Endpoint | WW | Microsoft Defender for Endpoint | 443 | `*.blob.core.windows.net/networkscannerstable/*` | Microsoft Defender for Endpoint Vulnerability assessment for network devices (network scanner) | Optional | Yes | Yes | Yes |  |  | Supported on Windows 8 and above and Windows Server 2012 and above |
| Microsoft Defender for Endpoint | WW | Security Management | 443 | `enterpriseregistration.windows.net` | Security Management for Microsoft Defender for Endpoint - Azure Registration | Optional | Yes |  |  |  |  | Only required when using Security Management for Microsoft Defender for Endpoint |
| Microsoft Defender for Endpoint | WW | Security Management | 443 | `*.dm.microsoft.com` | Security Management for Microsoft Defender for Endpoint - Enrollment, check-in, and reporting | Optional | Yes |  |  |  |  | Only required when using Security Management for Microsoft Defender for Endpoint |
| Microsoft Defender for Endpoint | WW | Microsoft Monitoring Agent (MMA) | 443 | `*.ods.opinsights.azure.com` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Required when using MMA. For Windows Server 2012 R2 and 2016, consider migrating to the [Microsoft Defender for Endpoint unified agent](onboard-server). Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | WW | Microsoft Monitoring Agent (MMA) | 443 | `*.oms.opinsights.azure.com` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Required when using MMA. For Windows Server 2012 R2 and 2016, see the [Microsoft Defender for Endpoint unified agent](onboard-server). Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | WW | Microsoft Monitoring Agent (MMA) | 443 | `*.blob.core.windows.net` | MMA for Win 7/8.1/2008R2/2012R2/2016 | Optional |  | Yes | Yes |  |  | Required when using MMA. For Windows Server 2012 R2 and 2016, see the [Microsoft Defender for Endpoint unified agent](onboard-server). Refer to steps at https://aka.ms/mde_network_requirements to eliminate wildcards (\*) |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `unitedstates.x.cp.wd.microsoft.com` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `us.vortex-win.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Optional | Yes |  |  |  |  | Not required for Windows 10 1803 (RS4) and above / Windows Server 2019 and above |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `us-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `winatp-gw-cus.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `winatp-gw-eus.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `winatp-gw-cus3.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `winatp-gw-eus3.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | Azure UAE Central (AEC) | Microsoft Defender for Endpoint AEC | 443 | `winatp-gw-aec0a.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | Azure UAE North (AEN) | Microsoft Defender for Endpoint AEN | 443 | `winatp-gw-aen0a.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `automatedirstrprdcus.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `automatedirstrprdeus.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `automatedirstrprdcus3.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `automatedirstrprdeus3.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `automatedirstrprdaen0a.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `automatedirstrprdaec0a.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus1eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus2eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus3eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus4eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `wsus1eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `wsus2eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus2westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus3westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `ussus4westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `wsus1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | US | Microsoft Defender for Endpoint US | 443 | `wsus2westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `europe.x.cp.wd.microsoft.com` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `eu.vortex-win.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Optional | Yes |  |  |  |  | Not required for Windows 10 1803 (RS4) and above / Windows Server 2019 and above |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `eu-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `winatp-gw-neu.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `winatp-gw-weu.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `winatp-gw-neu3.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `winatp-gw-weu3.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `automatedirstrprdneu.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `automatedirstrprdweu.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `automatedirstrprdneu3.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `automatedirstrprdweu3.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `usseu1northprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `wseu1northprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `usseu1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | EU | Microsoft Defender for Endpoint EU | 443 | `wseu1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `unitedkingdom.x.cp.wd.microsoft.com` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `uk.vortex-win.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Optional | Yes |  |  |  |  | Not required for Windows 10 1803 (RS4) and above / Windows Server 2019 and above |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `uk-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `winatp-gw-uks.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `winatp-gw-ukw.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `automatedirstrprduks.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `automatedirstrprdukw.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `ussuk1southprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `wsuk1southprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `ussuk1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | UK | Microsoft Defender for Endpoint UK | 443 | `wsuk1westprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `australia.x.cp.wd.microsoft.com` | Used by Microsoft Defender Antivirus to provide cloud-delivered protection and security intelligence updates | Required |  |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `au.vortex-win.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Optional | Yes |  |  |  |  | Not required for Windows 10 1803 (RS4) and above / Windows Server 2019 and above |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `au-v20.events.data.microsoft.com` | Microsoft Defender for Endpoint EDR Cyber Data | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `winatp-gw-aue.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `winatp-gw-aus.microsoft.com` | Microsoft Defender for Endpoint Command and Control | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `automatedirstrprdaue.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `automatedirstrprdaus.blob.core.windows.net` | Microsoft Defender for Endpoint AutoIR Sample Storage | Required | Yes |  |  | Yes | Yes |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `ussau1southeastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender for Endpoint | AU | Microsoft Defender for Endpoint AU | 443 | `ussau1eastprod.blob.core.windows.net` | Malware Sample Submission Storage | Required | Yes |  |  |  |  |  |
| Microsoft Defender Antivirus | WW | UTC | 443 | `vortex-win.data.microsoft.com` | Used by Windows to send client diagnostic data; Microsoft Defender Antivirus uses this for product quality monitoring purposes | Optional | Yes |  |  |  |  | Not required for Windows 10 1803 (RS4) and above / Windows Server 2019 |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `*.update.microsoft.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `*.delivery.mp.microsoft.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `*.windowsupdate.com` | MU / WU - Security intelligence and product updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `go.microsoft.com` | MU / WU - Security intelligence and product updates | Required | Yes\* | Yes\* | Yes\* | Yes | Yes | \*Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr)  Required for Mac and Linux platforms |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `definitionupdates.microsoft.com` | MU / WU - Security intelligence and product updates | Required | Yes\* | Yes\* | Yes\* | Yes | Yes | \*Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr)  Required for Mac and Linux platforms |
| Microsoft Defender Antivirus | WW | MU / WU | 443 | `https://www.microsoft.com/security/encyclopedia/adlpackages.aspx` | MU / WU - Security intelligence and product updates | Required | Yes\* | Yes\* | Yes | Yes | Yes | \*Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr)  Required for Mac and Linux platforms |
| Microsoft Defender Antivirus | WW | MU (ADL) | 443 | `*.download.windowsupdate.com` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MU (ADL) | 443 | `*.download.microsoft.com` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MU (ADL) | 443 | `fe3cr.delivery.mp.microsoft.com/ClientWebService/client.asmx` | ADL - Alternate location for Microsoft Defender Antivirus Security intelligence updates | Optional | Yes | Yes | Yes |  |  | Optional if updates are being managed internally (WSUS/FileShare/ConfigMgr) |
| Microsoft Defender Antivirus | WW | MAPS | 443 | `*.wdcp.microsoft.com` | MAPS - Used by Microsoft Defender Antivirus to provide cloud-delivered protection | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender Antivirus | WW | MAPS | 443 | `*.wd.microsoft.com` | MAPS - Used by Microsoft Defender Antivirus to provide cloud-delivered protection | Required | Yes | Yes | Yes | Yes | Yes |  |
| Microsoft Defender Antivirus | WW | Common | 443 | `*.events.data.microsoft.com` | Used by Microsoft Defender Antivirus to send Diagnostic Telemetry for Microsoft Defender Core Service | Required | Yes | No | Yes | No | No | To enhance your endpoint security experience, Microsoft is releasing the Microsoft Defender Core service to help with the stability and performance of Microsoft Defender Antivirus. Alternatively, to wildcard, can allow: us-mobile.events.data.microsoft.com/OneCollector/1.0 eu-mobile.events.data.microsoft.com/OneCollector/1.0 uk-mobile.events.data.microsoft.com/OneCollector/1.0 au-mobile.events.data.microsoft.com/OneCollector/1.0 mobile.events.data.microsoft.com/OneCollector/1.0 |
| Microsoft Defender Antivirus | WW | Common | 443 | `*ecs.office.com/config/v1/MicrosoftWindowsDefenderClient` | Used by Microsoft Defender Antivirus to download internal feature configurations (ECS) for Microsoft Defender Core service | Required | Yes | No | Yes | No | No | Microsoft Defender Core service is used to enhance stability and performance of Microsoft Defender Antivirus for customers. |
| Microsoft Defender SmartScreen | WW | Reporting and Notifications | 443 | `*.smartscreen-prod.microsoft.com` | Used for Microsoft Defender SmartScreen protection, reporting, and notifications. Microsoft Defender Antivirus Network Protection and custom URL indicators | Required | Yes |  |  | Yes | Yes | Microsoft Defender SmartScreen reporting and notifications. Network Protection and custom URL indicators |
| Microsoft Defender SmartScreen | WW | Reporting and Notifications | 443 | `*.smartscreen.microsoft.com` | Used for Microsoft Defender SmartScreen protection, reporting, and notifications. Microsoft Defender Antivirus Network Protection and custom URL indicators | Required | Yes |  |  | Yes | Yes | Microsoft Defender SmartScreen reporting and notifications. Network Protection and custom URL indicators |
| Microsoft Defender SmartScreen | WW | Reporting and Notifications | 443 | `*.checkappexec.microsoft.com` | Used for Microsoft Defender SmartScreen to check application execution for trusted apps | Optional | Yes |  |  |  |  | Microsoft Defender SmartScreen checking application execution for trusted apps |
| Microsoft Defender SmartScreen | WW | Reporting and Notifications | 443 | `*.urs.microsoft.com` | Used for Microsoft Defender SmartScreen to check application execution for trusted apps | Optional | Yes |  |  |  |  | Microsoft Defender SmartScreen checking application execution for trusted apps |
| Consolidated Defender for Endpoint services | WW | Streamlined connectivity new URL pattern | 443 | `*.endpoint.security.microsoft.com` | Used for streamlined connectivity URL consolidation as well as for future services | Required | Yes | No | Yes | Yes | Yes | Only required for streamlined connectivity initially. New services also follow this new pattern. |

## Defender portal URLs

This section lists the URLs needed to open the Microsoft Defender portal in a browser.

Note

All URLs in this table are required for access to the Microsoft Defender portal.

| Service | Geography | URL |
| --- | --- | --- |
| Microsoft Defender for Endpoint | WW | `*.blob.core.windows.net` |
| Microsoft Defender for Endpoint | WW | `crl.microsoft.com` |
| Microsoft Defender for Endpoint | WW | `https://*.microsoftonline-p.com` |
| Microsoft Defender for Endpoint | WW | `https://secure.aadcdn.microsoftonline-p.com` |
| Microsoft Defender for Endpoint | WW | `https://static2.sharepointonline.com` |
| Microsoft Defender for Endpoint | WW | `https://login.microsoftonline.com` |
| Microsoft Defender for Endpoint | WW | `https://*.securitycenter.windows.com` |
| Microsoft Defender for Endpoint | WW | `https://onboardingpackagescusprd.blob.core.windows.net` |
| Microsoft 365 Defender | WW | `https://security.microsoft.com` |

## Required client processes for network connectivity

Because the Microsoft Defender for Endpoint client processes in this section generate network communications, make sure that traffic from those processes is not blocked.

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

This section summarizes recent changes to this article and its endpoint listings.

| Date | Change Log |
| --- | --- |
| 06/02/2026 | Added `reflector.defender.microsoft.com`. |
| 04/14/2026 | Replaced `officecdn-microsoft-com.akamaized.net` with new CDN ChannelURL reference for Mac/Linux product updates. New CDN endpoint starting with macOS build 101.26012.0012. |
| 04/13/2026 | Added SmartScreen URLs (`*.checkappexec.microsoft.com`, `*.urs.microsoft.com`) to Microsoft Defender URLs. |
| 03/26/2026 | Added new Azure UAE North (AEN) and Azure UAE Central (AEC) URLs to the Microsoft Defender URLs section: `winatp-gw-aec0a.microsoft.com`, `winatp-gw-aen0a.microsoft.com`, `automatedirstrprdaen0a.blob.core.windows.net`,`automatedirstrprdaec0a.blob.core.windows.net`. |
| 03/26/2026 | Renamed **Microsoft Defender processes** section to **Client processes**, and aligned the content for all URL lists. |
| 16/06/2025 | Corrected row 94, Defender Core service and ECS, to be listed as "Required".  Corrected row 93, `*.events.data.microsoft.com`, to be listed as "Required". |
| 22/01/2024 | Updates for URLs required for Microsoft Defender Core service and DLP service processes:  Added new line 93 for 1DS URL in Microsoft Defender URLs.  Added new line 94 for ECS URL in Microsoft Defender URLs.  Added new line 8 for Defender Core Service in Microsoft Defender Processes.  Added new line 9 for Purview DLP Process. |