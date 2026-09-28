---
layout: Conceptual
title: Advanced Security Information Model (ASIM) security content | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-content
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: ofshezaf
description: This article outlines the Microsoft Sentinel security content that uses the Advanced Security Information Model (ASIM).
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2025-06-25T00:00:00.0000000Z
locale: en-us
document_id: 59572abf-8d82-a722-47aa-ebdd28a176e4
document_version_independent_id: daa6df2d-8cfa-6916-6474-9f1a2319eec8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 2d609271-c47c-0b44-4170-e822a3366b2e
---

# Advanced Security Information Model (ASIM) security content | Microsoft Learn

Normalized security content in Microsoft Sentinel includes analytics rules, hunting queries, and workbooks that work with unifying normalization parsers.

You can find normalized, built-in content in Microsoft Sentinel galleries and [solutions](sentinel-solutions-catalog), create your own normalized content, or modify existing content to use normalized data.

This article lists built-in Microsoft Sentinel content that has been configured to support the Advanced Security Information Model (ASIM). While links to the Microsoft Sentinel GitHub repository are provided as a reference, you can also find these rules in the [Microsoft Sentinel Analytics rule gallery](detect-threats-built-in). Use the linked GitHub pages to copy any relevant hunting queries.

To understand how normalized content fits within the ASIM architecture, refer to the [ASIM architecture diagram](normalization#asim-components).

## Authentication security content

The following built-in authentication content is supported for ASIM normalization.

### Analytics rules

- [Potential Password Spray Attack (Uses Authentication Normalization)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimAuthentication/imAuthPasswordSpray.yaml)
- [Brute force attack against user credentials (Uses Authentication Normalization)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimAuthentication/imAuthBruteForce.yaml)
- [User login from different countries/regions within 3 hours (Uses Authentication Normalization)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimAuthentication/imAuthSigninsMultipleCountries.yaml)
- [Sign-ins from IPs that attempt sign-ins to disabled accounts (Uses Authentication Normalization)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimAuthentication/imSigninAttemptsByIPviaDisabledAccounts.yaml)

## File Activity security content

The following built-in file activity content is supported for ASIM normalization.

- [Legacy IOC Based Threat Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-ioclegacy?tab=Overview)

### Analytics Rules

- [SUNBURST and SUPERNOVA backdoor hashes (Normalized File Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimFileEvent/imFileESolarWindsSunburstSupernova.yaml)

## Registry activity security content

The following built-in registry activity content is supported for ASIM normalization.

### Analytics rules

- [Potential Fodhelper UAC Bypass (ASIM Version)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/MultipleDataSources/PotentialFodhelperUACBypass%28ASIMVersion%29.yaml)

### Hunting queries

- [Persisting Via IFEO Registry Key](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Endpoint%20Threat%20Protection%20Essentials/Hunting%20Queries/PersistViaIFEORegistryKey.yaml)

## DNS query security content

The following built-in DNS query content is supported for ASIM normalization.

| Solutions | Analytics rules |
| --- | --- |
| [DNS Essentials](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-dns-domain?tab=Overview)[Log4j Vulnerability Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-apachelog4jvulnerability?tab=Overview)[Legacy IOC Based Threat Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-ioclegacy?tab=Overview) | [TI map Domain entity to DNS Events (ASIM DNS Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Threat%20Intelligence/Analytic%20Rules/imDns_DomainEntity_DnsEvents.yaml)[TI map IP entity to DNS Events (ASIM DNS Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Threat%20Intelligence/Analytic%20Rules/imDns_IPEntity_DnsEvents.yaml)[Potential DGA detected (ASimDNS)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimDNS/imDns_HighNXDomainCount_detection.yaml)[Excessive NXDOMAIN DNS Queries (ASIM DNS Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimDNS/imDns_ExcessiveNXDOMAINDNSQueries.yaml)[DNS events related to mining pools (ASIM DNS Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimDNS/imDNS_Miners.yaml)[DNS events related to ToR proxies (ASIM DNS Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimDNS/imDNS_TorProxies.yaml)[Known Forest Blizzard group domains - July 2019](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/MultipleDataSources/ForestBlizzardJuly2019IOCs.yaml) |

## Network session security content

The following built-in network session related content is supported for ASIM normalization.

| Solutions | Analytics rules | Hunting queries |
| --- | --- | --- |
| [Network Session Essentials](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-networksession?tab=Overview)[Log4j Vulnerability Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-apachelog4jvulnerability?tab=Overview)[Legacy IOC Based Threat Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-ioclegacy?tab=Overview) | [Log4j vulnerability exploit aka Log4Shell IP IOC](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Apache%20Log4j%20Vulnerability%20Detection/Analytic%20Rules/Log4J_IPIOC_Dec112021.yaml)[Excessive number of failed connections from a single source (ASIM Network Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Network%20Session%20Essentials/Analytic%20Rules/ExcessiveHTTPFailuresFromSource.yaml)[Potential beaconing activity (ASIM Network Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Network%20Session%20Essentials/Analytic%20Rules/PossibleBeaconingActivity.yaml)[TI map IP entity to Network Session Events (ASIM Network Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Threat%20Intelligence/Analytic%20Rules/IPEntity_imNetworkSession.yaml)[Port scan detected (ASIM Network Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Network%20Session%20Essentials/Analytic%20Rules/PortScan.yaml)[Known Forest Blizzard group domains - July 2019](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/MultipleDataSources/ForestBlizzardJuly2019IOCs.yaml) | [Connection from external IP to OMI related Ports](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Legacy%20IOC%20based%20Threat%20Protection/Hunting%20Queries/NetworkConnectiontoOMIPorts.yaml) |

## Process activity security content

The following built-in process activity content is supported for ASIM normalization.

| Solutions | Analytics rules | Hunting queries |
| --- | --- | --- |
| [Endpoint Threat Protection Essentials](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-endpointthreat?tab=Overview)[Legacy IOC Based Threat Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-ioclegacy?tab=Overview) | [Probable AdFind Recon Tool Usage (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimProcess/imProcess_AdFind_Usage.yaml)[Base64 encoded Windows process command-lines (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimProcess/imProcess_base64_encoded_pefile.yaml)[Malware in the recycle bin (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimProcess/imProcess_malware_in_recyclebin.yaml)[Midnight Blizzard - suspicious rundll32.exe execution of vbscript (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimProcess/imProcess_MidnightBlizzard_SuspiciousRundll32Exec.yaml)[SUNBURST suspicious SolarWinds child processes (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimProcess/imProcess_SolarWinds_SUNBURST_Process-IOCs.yaml) | [Cscript script daily summary breakdown (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_cscript_summary.yaml)[Enumeration of users and groups (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_enumeration_user_and_group.yaml)[Exchange PowerShell Snapin Added (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_ExchangePowerShellSnapin.yaml)[Host Exporting Mailbox and Removing Export (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_HostExportingMailboxAndRemovingExport.yaml)[Invoke-PowerShellTcpOneLine Usage (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_Invoke-PowerShellTcpOneLine.yaml)[Nishang Reverse TCP Shell in Base64 (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_NishangReverseTCPShellBase64.yaml)[Summary of users created using uncommon/undocumented commandline switches (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_persistence_create_account.yaml)[Powercat Download (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_PowerCatDownload.yaml)[PowerShell downloads (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_powershell_downloads.yaml)[Entropy for Processes for a given Host (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_ProcessEntropy.yaml)[SolarWinds Inventory (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_SolarWindsInventory.yaml)[Suspicious enumeration using Adfind tool (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_Suspicious_enumeration_using_adfind.yaml)[Windows System Shutdown/Reboot (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_Windows%20System%20Shutdown-Reboot%28T1529%29.yaml)[Certutil (LOLBins and LOLScripts, Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_Certutil-LOLBins.yaml)[Rundll32 (LOLBins and LOLScripts, Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/inProcess_SignedBinaryProxyExecutionRundll32.yaml)[Uncommon processes - bottom 5% (Normalized Process Events)](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/ASimProcess/imProcess_uncommon_processes.yaml)[Unicode Obfuscation in Command Line](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/UnicodeObfuscationInCommandLine.yaml) |

## Web session security content

The following built-in web session related content is supported for ASIM normalization.

| Solutions | Analytics rules |
| --- | --- |
| [Log4j Vulnerability Detection](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-apachelog4jvulnerability?tab=Overview)[Threat Intelligence](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-threatintelligence-taxii?tab=Overview) | [TI map Domain entity to Web Session Events (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Threat%20Intelligence/Analytic%20Rules/DomainEntity_imWebSession.yaml)[TI map IP entity to Web Session Events (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Threat%20Intelligence/Analytic%20Rules/IPEntity_imWebSession.yaml)[Potential communication with a Domain Generation Algorithm (DGA) based hostname (ASIM Network Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/PossibleDGAContacts.yaml)[A client made a web request to a potentially harmful file (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/PotentiallyHarmfulFileTypes.yaml)[A host is potentially running a crypto miner (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/UnusualUACryptoMiners.yaml)[A host is potentially running a hacking tool (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/UnusualUAHackTool.yaml)[A host is potentially running PowerShell to send HTTP(S) requests (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/UnusualUAPowershell.yaml)[Discord CDN Risky File Download (ASIM Web Session Schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/DiscordCDNRiskyFileDownload_ASim.yaml)[Excessive number of HTTP authentication failures from a source (ASIM Web Session schema)](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/ASimWebSession/ExcessiveNetworkFailuresFromSource.yaml)[User agent search for Log4j exploitation attempt](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Apache%20Log4j%20Vulnerability%20Detection/Analytic%20Rules/UserAgentSearch_log4j.yaml) |