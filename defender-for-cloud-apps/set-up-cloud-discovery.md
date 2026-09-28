---
layout: Conceptual
title: Cloud app discovery overview - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/set-up-cloud-discovery
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes Microsoft Defender for Cloud Apps support for cloud app discovery.
ms.date: 2023-12-20T00:00:00.0000000Z
ms.topic: concept-article
ms.reviewer: Mravela 
locale: en-us
document_id: 42cfdd3b-84ce-7d75-08d5-85bef01b4279
document_version_independent_id: 42cfdd3b-84ce-7d75-08d5-85bef01b4279
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/set-up-cloud-discovery.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: set-up-cloud-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/set-up-cloud-discovery.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: d2a7793c-88bc-0f76-fa44-20ab39114a96
---

# Cloud app discovery overview - Microsoft Defender for Cloud Apps | Microsoft Learn

Cloud discovery analyzes your traffic logs against the Microsoft Defender for Cloud Apps catalog of over 31,000 cloud apps. The apps are ranked and scored based on more than 90 risk factors to provide you with ongoing visibility into cloud use, Shadow IT, and the risk Shadow IT poses into your organization.

Tip

By default, Defender for Cloud Apps cannot discover apps that aren't in the catalog.

To see Defender for Cloud Apps data for an app that's not currently in the catalog, we recommend that you [check our roadmap](https://www.microsoft.com/en-us/microsoft-365/roadmap?filters=Microsoft%20Defender%20for%20Cloud%20Apps)) or [create a custom app](cloud-discovery-custom-apps).

## Snapshot and continuous risk assessment reports

You can generate the following types of reports:

- **Snapshot reports** - Provides ad-hoc visibility on a set on traffic logs you manually upload from your firewalls and proxies.
- **Continuous reports** - Analyze all logs that are forwarded from your network using Defender for Cloud Apps. They provide improved visibility over all data, and automatically identify anomalous use using either the Machine Learning anomaly detection engine or by using custom policies that you define. These reports can be created by connecting in the following ways:

    - [**Microsoft Defender for Endpoint integration**](mde-integration): Defender for Cloud Apps integrates with Defender for Endpoint natively, to simplify rollout of cloud discovery, extend cloud discovery capabilities beyond your corporate network, and enable machine-based investigation.
    - [**Log collector**](discovery-docker): Log collectors enable you to easily automate log upload from your network. The log collector runs on your network and receives logs over Syslog or FTP.
    - **Secure Web Gateway (SWG)**: If you work with both Defender for Cloud Apps and one of the following SWGs, you can integrate the products to enhance your security cloud discovery experience. Together, Defender for Cloud Apps and SWGs provide seamless deployment of cloud discovery, automatic blocking of unsanctioned apps, and risk assessment directly in the SWG's portal.
        - [Zscaler integration](zscaler-integration)
        - [iboss integration](iboss-integration)
        - [Corrata integration](corrata-integration)
        - [Menlo Security integration](menlo-integration)
- **[Cloud discovery API](api-discovery)** – Use the Defender for Cloud Apps cloud discovery API to automate traffic log upload and get automated cloud discovery report and risk assessment. You can also use the API to [generate block scripts](api-discovery-script) and streamline app controls directly to your network appliance.

## Log process flow: From raw data to risk assessment

The process of generating a risk assessment consists of the following steps. The process takes between a few minutes to several hours depending on the amount of data processed.

- **Upload** – Web traffic logs from your network are uploaded to the portal.
- **Parse** – Defender for Cloud Apps parses and extracts traffic data from the traffic logs with a dedicated parser for each data source.
- **Analyze** – Traffic data is analyzed against the cloud app catalog to identify more than 31,000 cloud apps and to assess their risk score. Active users and IP addresses are also identified as part of the analysis.
- **Generate report** - A risk assessment report of the data extracted from log files is generated.

Note

Discovery data is analyzed and updated four times a day.

## Supported firewalls and proxies

- Barracuda - Web App Firewall (W3C)
- Blue Coat Proxy SG - Access log (W3C)
- Check Point
- Cisco ASA with FirePOWER
- Cisco ASA Firewall (For Cisco ASA firewalls, it's necessary to set the information level to 6)
- Cisco Cloud Web Security
- Cisco FWSM
- Cisco IronPort WSA
- Cisco Meraki – URLs log
- Clavister NGFW (Syslog)
- ContentKeeper
- Corrata
- Digital Arts i-FILTER
- Forcepoint
- Fortinet Fortigate
- iboss Secure Cloud Gateway
- Juniper SRX
- Juniper SSG
- McAfee Secure Web Gateway
- Menlo Security (CEF)
- Microsoft Forefront Threat Management Gateway (W3C)
- Open Systems Secure Web Gateway
- Palo Alto series Firewall
- Sonicwall (formerly Dell)
- Sophos Cyberoam
- Sophos SG
- Sophos XG
- Squid (Common)
- Squid (Native)
- Stormshield
- Wandera
- WatchGuard
- Websense - Web Security Solutions - Internet activity log (CEF)
- Websense - Web Security Solutions - Investigative detail report (CSV)
- Zscaler

Note

Cloud discovery supports both IPv4 and IPv6 addresses.

If your log isn't supported, or if you're using a newly released log format from one of the supported data sources and the upload is failing, select **Other** as the **Data source** and specify the appliance and log you're trying to upload. Your log will be reviewed by the Defender for Cloud Apps cloud analyst team and you'll be notified if support for your log type is added. Alternatively, you can define a custom parser that matches your format. For more information, see [Use a custom log parser](custom-log-parser).

Note

The following list of supported appliances may not work with newly released log formats. If you are using a newly released format and the upload is failing, [use a custom log parser](custom-log-parser) and if required, open a support case. If you open a support case, make sure to provide the relevant firewall documentation with your case.

Data attributes (according to vendor documentation):

| Data source | Target App URL | Target App IP | Username | Origin IP | Total traffic | Uploaded bytes |
| --- | --- | --- | --- | --- | --- | --- |
| Barracuda | **Yes** | **Yes** | **Yes** | **Yes** | No | No |
| Blue Coat | **Yes** | No | **Yes** | **Yes** | **Yes** | **Yes** |
| Check Point | No | **Yes** | No | **Yes** | No | No |
| Cisco ASA (Syslog) | No | **Yes** | No | **Yes** | **Yes** | No |
| Cisco ASA with FirePOWER | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Cisco Cloud Web Security | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Cisco FWSM | No | **Yes** | No | **Yes** | **Yes** | No |
| Cisco Ironport WSA | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Cisco Meraki | **Yes** | **Yes** | No | **Yes** | No | No |
| Clavister NGFW (Syslog) | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| ContentKeeper | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Corrata | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Digital Arts i-FILTER | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| ForcePoint LEEF | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| ForcePoint Web Security Cloud\* | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Fortinet Fortigate | No | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| FortiOS | **Yes** | **Yes** | No | **Yes** | **Yes** | **Yes** |
| iboss | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Juniper SRX | No | **Yes** | No | **Yes** | **Yes** | **Yes** |
| Juniper SSG | No | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| McAfee SWG | **Yes** | No | No | **Yes** | **Yes** | **Yes** |
| Menlo Security (CEF) | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| MS TMG | **Yes** | No | **Yes** | **Yes** | **Yes** | **Yes** |
| Open Systems Secure Web Gateway | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Palo Alto Networks | No | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| SonicWall (formerly Dell) | **Yes** | **Yes** | No | **Yes** | **Yes** | **Yes** |
| Sophos | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | No |
| Squid (Common) | **Yes** | No | **Yes** | **Yes** | **Yes** | No |
| Squid (Native) | **Yes** | No | **Yes** | **Yes** | No | No |
| Stormshield | No | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Wandera | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| WatchGuard | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Websense - Internet activity log (CEF) | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Websense - Investigative detail report (CSV) | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |
| Zscaler | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** | **Yes** |

\* Versions 8.5 and later of ForcePoint Web Security Cloud aren't supported