---
layout: Conceptual
title: Threat Intelligence Report - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/threat-intelligence-reports
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: This page helps you to use Microsoft Defender for Cloud threat intelligence reports during an investigation to find more information about security alerts.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 325ce5cf-5ee3-f93f-b64e-41a1a61888fa
document_version_independent_id: e46a7fa1-2fa4-f986-8aeb-acde4b910d61
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/threat-intelligence-reports.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/threat-intelligence-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/threat-intelligence-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 713094d6-23d7-5765-fe4c-8457ab37e0a1
---

# Threat Intelligence Report - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's threat intelligence reports can help you learn more about a threat that triggered a security alert.

## What is a threat intelligence report?

Defender for Cloud's threat protection works by monitoring security information from your Azure resources, the network, and connected partner solutions. It analyzes this information to identify threats, often correlating information from multiple sources. For more information, see [How Microsoft Defender for Cloud detects and responds to threats](alerts-overview#detect-threats).

When Defender for Cloud identifies a threat, it triggers a [security alert](manage-respond-alerts), which contains detailed information regarding the event, including suggestions for remediation. To help incident response teams investigate and remediate threats, Defender for Cloud provides threat intelligence reports containing information about detected threats. The report includes information such as:

- Attacker identity or associations, if this information is available
- Attacker objectives
- Current and historical attack campaigns, if this information is available
- Attacker tactics, tools, and procedures
- Associated indicators of compromise (IoC) such as URLs and file hashes
- Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk
- Mitigation and remediation information

Note

The amount of information in any particular report varies. The level of detail is based on the malware's activity and prevalence.

Defender for Cloud has three types of threat reports, which can vary according to the attack. The reports available are:

- **Activity Group Report**: provides deep dives into attackers, their objectives, and tactics.
- **Campaign Report**: focuses on details of specific attack campaigns.
- **Threat Summary Report**: covers all of the items in the previous two reports.

This type of information is useful during the incident response process. For instance, you might find out when there's an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate similar threats in the future.

## How to access the threat intelligence report?

To access a threat intelligence report, perform the following steps:

1. From Defender for Cloud's menu, open the **Security alerts** page.
2. Select an alert.

    The alerts details page opens with more details about the alert.

    [![Ransomware indicators detected alert details page.](media/threat-intelligence-reports/ransomware-indicators-detected-link-to-threat-intel-report.png)](media/threat-intelligence-reports/ransomware-indicators-detected-link-to-threat-intel-report.png#lightbox)
3. Select the link to the report, and a PDF opens in your default browser.

    [![Potentially Unsafe Action alert details page.](media/threat-intelligence-reports/threat-intelligence-report.png)](media/threat-intelligence-reports/threat-intelligence-report.png#lightbox)

    You can optionally download the PDF report.

    Tip

    The amount of information available for each security alert varies according to the type of alert.