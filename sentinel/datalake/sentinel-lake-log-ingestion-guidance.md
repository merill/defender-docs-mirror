---
layout: Conceptual
title: Which Logs to Ingest directly into the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-lake-log-ingestion-guidance
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn which log sources to ingest into the Microsoft Sentinel data lake tier versus the analytics tier based on detection, hunting, and cost needs.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: juliango
ms.topic: concept-article
ms.date: 2026-04-23T00:00:00.0000000Z
ms.collection: ms-security
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 8198b858-18d0-8cf9-93c3-0514c17f42b1
document_version_independent_id: 50de90dc-d679-ef4e-1ac9-0cd57565f3bc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-lake-log-ingestion-guidance.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-lake-log-ingestion-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-lake-log-ingestion-guidance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 46c7161b-35fc-430b-8cfd-4c3b3510259e
---

# Which Logs to Ingest directly into the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

You can configure log sources to ingest directly into the data lake tier without mirroring to the analytics tier. Direct ingestion is useful when you have high-volume log sources that you want to retain for hunting and forensic purposes but don't need for real-time alerting.

By ingesting these sources directly into the data lake tier, you avoid analytics tier ingestion costs while still making the data available for KQL queries, Spark notebooks, and long-term analysis. This article helps you determine which log sources are good candidates for direct data lake ingestion based on their value for detection, hunting, and investigation workloads.

Configure direct data lake ingestion from the connector setup pages or the **Table management** page in the Microsoft Defender portal. For more information, see [Configure table settings in Microsoft Sentinel](../manage-table-tiers-retention).

## Which logs should you ingest into the data lake?

After you onboard to [Microsoft Sentinel data lake](sentinel-lake-overview), you can choose which log sources to send to the data lake tier, the analytics tier, or both. The analytics tier is optimized for real-time detection and alerting, while the data lake tier is optimized for cost-effective long-term retention and hunting. Use the following guidance to determine which log sources to ingest into each tier based on their value for different security workloads.

### Analytics tier use cases

You use the analytics tier to ingest log data into Microsoft Sentinel workspaces, where you can run analytics rules, custom detections, and live queries. Ingest log sources into the analytics tier when you need:

- **Real-time detection and correlation**: Alert on critical events from endpoints, identity systems, cloud security controls, and network perimeter devices.
- **Active incident investigation**: Run live queries against current data during incident response.
- **High-fidelity signals**: Ingest sources with direct detection value, such as EDR alerts, privileged access logs, authentication events, and threat intelligence indicators.

### Data lake tier use cases

You use the data lake tier to store logs at lower cost for workloads that don't require real-time alerting. Ingest log sources into the data lake tier when you need:

- **High-volume log retention**: Store sources that are useful for forensic analysis or periodic threat hunts but are too costly to retain in the analytics tier.
- **Threat hunting**: Run cross-log searches, trend analysis, and historical queries to identify patterns across extended time ranges.
- **Batch analytics and summarization**: Use Spark notebooks, KQL, or similar tools to enrich, correlate, or summarize data, then forward only high-priority signals to the analytics tier.
- **Machine learning and advanced analytics**: Apply big data techniques to identify complex relationships and anomalies in historical data.

## Analytics rules and custom detections

You can't run analytics rules or custom detections on data in the data lake tier. If you ingest logs only into the data lake tier, those logs don't generate alerts. To maintain real-time detection coverage, keep time-sensitive, high-fidelity log sources in the analytics tier.

## Choose an ingestion tier by log source type

Use the following table as a general guide to decide where to ingest each log source type. Assess your own workloads, alerting requirements, and risk tolerance when you configure log ingestion. Some of the log sources have dedicated Microsoft Sentinel connectors while others may require Syslog, CEF, API-based, or custom connectors for ingestion.

| Log source type | Typical log volume | Value for real-time threat detection and alerting | Value for threat hunting | Value for incident investigation and forensics | Data lake only ingestion fit |
| --- | --- | --- | --- | --- | --- |
| AAA (TACACS/Radius) | Medium | High | High | High | Poor fit |
| Active Directory (on-premises) | High | High | High | High | Poor fit |
| Application Logs | High | Medium | Medium | High | Suitable fit |
| AV Logs (Windows Events 5000s & 3rd party) | Medium | High | High | High | Poor fit |
| Azure Activity | Medium | High | High | High | Poor fit |
| Biometric Access System Logs | Low | Medium | Low | High | Suitable fit |
| Building Security System Logs | Low | Low | Low | Medium | Suitable fit |
| Call Center/VoIP Logs | Medium | Low | Low | Medium | Suitable fit |
| CASB | High | High | High | High | Suitable fit |
| Citrix/Horizon/ALBs | Medium | Medium | Medium | High | Suitable fit |
| Cloud IAM | Medium | High | High | High | Poor fit |
| Cloud PaaS | High | High | High | High | Suitable fit |
| Cloud Security Controls | Medium | High | Medium | High | Poor fit |
| Cloud Storage (S3, Blob, etc.) Logs | High | Low | High | High | Poor fit |
| CRM Audit Logs | Low-Medium | Low | Low | Medium | Poor fit |
| Database Audit Tools | Medium | High | High | High | Suitable fit |
| DHCP Logs | Medium | Medium | Medium | High | Suitable fit |
| DLP Alerts | Low | High | High | High | Suitable fit |
| DNS Logs | High | High | High | High | Suitable fit |
| Endpoint Detection and Response (EDR) (Alerts) | Medium | High | High | High | Poor fit |
| Endpoint Detection and Response (EDR) (Raw) | High | High | High | High | Suitable fit |
| Email Security (3rd party alerts) | Medium | High | Medium | High | Poor fit |
| ERP Audit Logs | Low-Medium | Low | Low | Medium | Suitable fit |
| File Integrity | Low | Medium | Medium | High | Suitable fit |
| Firewall Threat/Malware/IPS/IDS | High | High | High | High | Poor fit |
| Firewall Traffic Logs | High | High | High | High | Suitable fit |
| GitHub/GitLab/Code Repo Logs | Low-Medium | Medium | Medium | High | Suitable fit |
| Google Workspace Logs | Medium | Medium | Medium | High | Suitable fit |
| Identity (Microsoft Entra ID, Okta, LDAP) | Medium | High | High | High | Poor fit |
| IIS/Apache Logs | Medium | High | High | High | Suitable fit |
| IoT Device Logs | High | Medium | Medium | Medium | Suitable fit |
| Kubernetes/Container Logs (alerts, critical) | High | High | High | High | Poor fit |
| Kubernetes/Container Logs (raw logs) | High | High | High | High | Suitable fit |
| LAN/WAN Router Switch | High | Medium | Medium | Medium | Suitable fit |
| Linux Server AuditD | Medium | High | High | High | Poor fit |
| Mobile Device Management (Microsoft Intune) | Medium | Medium | Medium | Medium | Suitable fit |
| Microsoft Office Logs (Teams, Office, SharePoint) | Medium | Medium | Medium | High | Poor fit |
| Microsoft XDR Alerts (Defender: Office, Identity, Endpoint, CloudApp) | Medium | High | High | High | Poor fit |
| Multifactor authentication (MFA) | Medium | High | Medium | High | Poor fit |
| Netflow | High | Medium | High | Medium | Suitable fit |
| Network Detection (Corelight, Vectra, Darktrace) | High | High | High | High | Poor fit |
| OT/ICS System Logs | Medium | High | High | High | Suitable fit |
| PAM (Privileged Access Management) | Low | High | High | High | Poor fit |
| PIM (Privileged Identity Management) | Low | High | High | High | Poor fit |
| POS System Logs | High | High | High | High | Suitable fit |
| Proxy Logging (URL filtering) | High | High | High | High | Suitable fit |
| Salesforce Audit Logs | Medium | Medium | Medium | High | Suitable fit |
| SD-WAN | Medium | Medium | Medium | Medium | Suitable fit |
| ServiceNow Audit Logs | Low | Low | Low | Medium | Suitable fit |
| SIEM/SOAR Platform Logs | Medium | High | High | High | Not recommended |
| Slack/Teams Collaboration Logs | Medium | Low | Medium | Medium | Suitable fit |
| Sysmon (Endpoint, for EDR complement) | Medium | High | High | High | Suitable fit |
| Threat Intelligence Indicators | Low | High | High | High | Not recommended |
| VDI Logs | Medium | Medium | Medium | High | Suitable fit |
| VPN | Medium | High | High | High | Not recommended |
| Vulnerability Scanning | Low | Medium | Medium | Medium | Suitable fit |
| Web Application Firewall (WAF) Logs | Medium | High | High | High | Suitable fit |
| Windows Server Events | High | High | High | High | Not recommended |
| XDR Source Logs (Defender: Office, Identity, Endpoint, CloudApp) | Medium | High | High | High | Not recommended |
| Zoom Meeting Logs | Low-Medium | Low | Low | Medium | Suitable fit |