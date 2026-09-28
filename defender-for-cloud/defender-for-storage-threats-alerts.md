---
layout: Conceptual
title: Understand Defender for Storage security threats and alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-threats-alerts
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
description: Learn about the security threats and alerts Microsoft Defender for Storage provides to detect and respond to potential security risks.
ms.date: 2025-07-15T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 74e661eb-d7c8-caa3-7dad-a949e12a56dd
document_version_independent_id: 28d2f6a6-a8ca-ded1-f09f-af6f8186f766
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-threats-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-threats-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-threats-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: caa219c8-1c06-52be-d43b-ff99d21b46a3
---

# Understand Defender for Storage security threats and alerts - Microsoft Defender for Cloud | Microsoft Learn

Data security becomes a top priority as organizations shift data to cloud storage solutions like Azure Storage. This document outlines common security threats and risks linked to misconfigured settings. It also explains the security alerts that Microsoft Defender for Storage provides to detect and respond to potential security threats.

## Security threats in cloud-based storage services

Azure Storage is a widely used cloud storage solution, and like any cloud-based service, it's susceptible to various security threats. Common security threats in Azure Storage include:

- Access token abuse and leakage
- Lateral movement from compromised workloads
- Compromised third-party partners with privileged permissions
- Credentials theft
- Reconnaissance with search engines
- Data collection by blob hunting
- Insider threats with existing permissions

These threats can result in malware uploads, data corruption, and sensitive data exfiltration, posing significant risks.

![Diagram showing common risks to data that can result from malware.](media/defender-for-storage-threats-alerts/malware-risks.png)

In addition to security threats, configuration errors might inadvertently expose sensitive resources. Some common misconfiguration issues include:

- Inadequate access controls and networking rules, leading to unintended data exposure on the internet
- Insufficient authentication mechanisms
- Lack of data encryption protocols for both data in transit and at rest

To minimize the risk of security breaches and configuration errors, security teams employ a combination of posture management tools and workload protection tools. These tools ensure Azure Storage stays secure by providing visibility into early signs of breaches. They help prevent attacks and maintain secure configurations.

Microsoft security researchers analyzed the attack surface of storage services. The potential security risks are described in the [threat matrix for cloud-based storage services](https://www.microsoft.com/security/blog/2021/04/08/threat-matrix-for-storage/), which are based on the [MITRE ATT&CK® framework](https://attack.mitre.org/techniques/enterprise/), a knowledge base for the tactics and techniques employed in cyber-attacks.

For a comparison between malware scanning and hash reputation analysis, see [Understanding the differences between these methods](defender-for-storage-introduction#understand-the-differences-between-malware-scanning-and-hash-reputation-analysis).

## What kind of security alerts does Microsoft Defender for Storage provide?

Tip

For a comprehensive list of all Defender for Storage alerts, see the [alerts reference guide](alerts-azure-storage) page. This is useful for workload owners who want to know what threats can be detected and help SOC teams gain familiarity with detections before investigating them. Learn more about [Defender for Cloud security alerts and how to respond to them](manage-respond-alerts).

Security alerts are triggered in the following scenarios:

| Scenario | Description |
| --- | --- |
| Malicious content upload | [Malware scanning](defender-for-storage-malware-scan) scans every blob uploaded to your storage accounts. It detects ransomware, viruses, spyware, and other malware uploaded to the storage account, helping you prevent it from entering the organization and spreading. The classic malware hash analysis alert operates differently from malware scanning. It compares the uploaded blob/file hash with a list of known malicious hash signatures rather than analyzing the file contents for malware. |
| Sensitive data exposure event | Detection of access level change allowing unauthenticated public access to blob containers with sensitive data from the internet |
| Suspicious activities on resources with sensitive data | Detection of suspicious activities occurring on blob containers containing sensitive data |
| Compromised, misconfigured, and unusual authentication tokens | Detection of compromised SAS tokens used for data plane authentication and operations, and detection of unusual SAS tokens that can be generated by a malicious actor |
| Data and permissions inspection | Detection of unusual exploration of the data and inspection of access permissions |
| Data exfiltration | Detection of unusual extraction of data from storage accounts |
| Data deletion | Detection of unusual deletions in storage accounts |
| Blob-hunting attempts | Detection of collection attempts by scanning and enumerating resources for publicly exposed storage resources.Read more on [how to detect, investigate, and prevent blob-hunting](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/protect-your-storage-resources-against-blob-hunting/ba-p/3735238). |
| Unusual access patterns | Detection of unusual access to storage accounts from unusual locations, applications, and with unusual authentication |
| Suspicious access signatures | Detection of known suspicious IP addresses by Microsoft Threat Intelligence, known Tor exit nodes, and known suspicious applications |
| Phishing campaigns | Detection of phishing content hosted on storage accounts and identified as part of a phishing attack impacting Microsoft 365 users |

Security alerts include details of the suspicious activity, relevant investigation steps, remediation actions, and security recommendations. Alerts can be exported to Microsoft Sentinel or any other third-party SIEM/XDR tool. Learn more about [how to stream alerts to a SIEM, SOAR, or IT Service Management solution](export-to-siem).

## Accelerated threat detection with Storage aggregated logs

Storage aggregated logs in Defender XDR's Advanced Hunting give security teams a powerful way to spot patterns and anomalies across large volumes of storage activity. Instead of analyzing raw events one by one, the new `CloudStorageAggregatedEvents` table delivers summarized insights, such as spikes in failed operations, unusual authentication types, or suspicious access from unexpected locations, helping teams quickly identify potential threats and prioritize investigations. This capability reduces noise, accelerates detection, and strengthens protection for cloud storage at scale. This capability is included only in the new Defender for Storage per-storage account plan. For the full schema and field details, see the [CloudStorageAggregatedEvents reference table.](/en-us/defender-xdr/advanced-hunting-cloudstorageaggregatedevents-table)