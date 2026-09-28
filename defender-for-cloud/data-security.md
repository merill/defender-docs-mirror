---
layout: Conceptual
title: Microsoft Defender for Cloud data security - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-security
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
description: Learn how data is managed and safeguarded in Microsoft Defender for Cloud to ensure the security of your data.
ms.topic: overview
ms.date: 2024-07-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ff709c3d-d7b2-8da7-ecc7-5fa1f17a9f35
document_version_independent_id: 19dce596-0ccb-5da7-67f5-4866bfca3c32
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-security.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b0a02ad8-2dea-6afb-e6e4-f18a981ecce4
---

# Microsoft Defender for Cloud data security - Microsoft Defender for Cloud | Microsoft Learn

To help customers prevent, detect, and respond to threats, Microsoft Defender for Cloud collects and processes security-related data, including configuration information, metadata, event logs, and more. Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.

This article explains how data is managed and safeguarded in Defender for Cloud.

## Data sources

Defender for Cloud analyzes data from the following sources to provide visibility into your security state, identify vulnerabilities and recommend mitigations, and detect active threats:

- **Azure services**: Uses information about the configuration of Azure services you have deployed by communicating with that service’s resource provider. For Azure AI resources, this includes prompts and responses used for AI threat detection.
- **Network traffic**: Uses sampled network traffic metadata from Microsoft’s infrastructure, such as source/destination IP/port, packet size, and network protocol.
- **Partner solutions**: Uses security alerts from integrated partner solutions, such as firewalls and antimalware solutions.
- **Your machines**: Uses configuration details and information about security events, such as Windows event and audit logs, and syslog messages from your machines.

## Data sharing

When you enable Defender for Storage malware scanning, it might share metadata, including metadata classified as customer data (e.g. SHA-256 hash), with Microsoft Defender for Endpoint.

Microsoft Defender for Cloud running the [Defender for Cloud Security Posture Management (CSPM) plan](concept-cloud-security-posture-management) shares data that is integrated into Microsoft Security Exposure Management recommendations.

Note

Microsoft Security Exposure Management is currently in public preview.

## Data protection

### Data segregation

Data is kept logically separate on each component throughout the service. All data is tagged per organization. This tagging persists throughout the data lifecycle, and it's enforced at each layer of the service.

### Data access

To provide security recommendations and investigate potential security threats, Microsoft personnel might access information collected or analyzed by Azure services, including process creation events, AI prompts and other artifacts, which might unintentionally include customer data or personal data from your machines.

We adhere to the [Microsoft Online Services Data Protection Addendum](https://www.microsoftvolumelicensing.com/Downloader.aspx?DocumentId=17880), which states that Microsoft won't use Customer Data or derive information from it for any advertising or similar commercial purposes. We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services. You retain all rights to Customer Data.

### Data use

Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://privacy.microsoft.com/privacystatement).

Microsoft Defender for Cloud does not use Customer Data to train AI models without user consent. As per the Microsoft Product Terms: Microsoft Defender for Cloud or Microsoft Generative AI Services do not use Customer Data to train any generative AI foundation model, unless pursuant to the Customer’s documented instructions.

## Manage data collection from machines

When you enable Defender for Cloud in Azure, data collection is turned on for each of your Azure subscriptions. You can also enable data collection for your subscriptions in Defender for Cloud. Defender for Servers uses Defender for Endpoint to collect data from your machines.

If you aren't using Microsoft Defender for Cloud's enhanced security features, you can also disable data collection from virtual machines in the Security Policy. Data Collection is required for subscriptions that are protected by enhanced security features. VM disk snapshots and artifact collection will still be enabled even if data collection has been disabled.

You can specify the workspace and region where data collected from your machines is stored. The default is to store data collected from your machines in the nearest workspace as shown in the following table:

| VM Geo | Workspace Geo |
| --- | --- |
| United States, Brazil, South Africa | United States |
| Canada | Canada |
| Europe (excluding United Kingdom) | Europe |
| United Kingdom | United Kingdom |
| Asia (excluding India, Japan, Korea, China) | Asia Pacific |
| Korea | Asia Pacific |
| India | India |
| Japan | Japan |
| China | China |
| Australia | Australia |

Note

**Microsoft Defender for Storage** stores artifacts regionally according to the location of the related Azure resource. Learn more in [Overview of Microsoft Defender for Storage](defender-for-storage-introduction).

## Data consumption

Customers can access Defender for Cloud related data from the following data streams:

| Stream | Data types |
| --- | --- |
| [Azure Activity log](/en-us/azure/azure-monitor/essentials/activity-log) | All security alerts, approved Defender for Cloud [just-in-time](just-in-time-access-usage) access requests. |
| [Azure Monitor logs](/en-us/azure/azure-monitor/data-platform) | All security alerts. |
| [Azure Resource Graph](/en-us/azure/governance/resource-graph/overview) | Security alerts, security recommendations, vulnerability assessment results, secure score information, status of compliance checks, and more. |
| [Microsoft Defender for Cloud REST API](/en-us/rest/api/defenderforcloud-composite/operation-groups?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true) | Security alerts, security recommendations, and more. |

Note

If there are no Defender plans enabled on the subscription, data will be removed from Azure Resource Graph after 30 days of inactivity in the Microsoft Defender for Cloud portal. After interaction with artifacts in the portal related to the subscription, the data should be visible again within 24 hours.

## Data retention

When the cloud security graph collects data from Azure and multicloud environments and other data source, it retains the data for a 14 day period. After 14 days, the data is deleted.

Calculated data, such as attack paths, might be kept for an additional 14 days. Calculated data consist of data that is derived from the raw data collected from the environment. For example, the attack path is derived from the raw data collected from the environment.

This information is collected in accordance with the privacy commitments described in our [Privacy Statement](https://privacy.microsoft.com/privacystatement).

Defender for Cloud AI threat protection plan includes storing of prompts and model responses of the protected subscriptions. The data is stored securelyand retained for purpose of pattern recognition and anomaly detections and stored for a duration of 30 days

## Defender for Cloud and Microsoft Defender 365 Defender integration

When you enable any of Defender for Cloud's paid plans you automatically gain all of the benefits of Microsoft Defender XDR. Information from Defender for Cloud will be shared with Microsoft Defender XDR. This data might contain customer data and will be stored according to [Microsoft 365 data handling guidelines](/en-us/microsoft-365/security/defender/data-privacy).