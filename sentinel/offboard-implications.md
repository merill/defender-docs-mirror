---
layout: Conceptual
title: Implications - remove Microsoft Sentinel from workspace | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/offboard-implications
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
description: Learn about the impact of removing a Microsoft Sentinel instance from a Log Analytics workspace in the Azure or Defender portal.
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2025-02-06T00:00:00.0000000Z
ms.author: edbaynash
locale: en-us
document_id: f2dd6a43-d85d-efc1-f5a5-09696b9d4039
document_version_independent_id: d9b7b600-062d-784d-5636-6518b6b433e4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/offboard-implications.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/offboard-implications
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/offboard-implications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e2e0c09b-ab3a-3ef2-8816-c4a898619652
---

# Implications - remove Microsoft Sentinel from workspace | Microsoft Learn

If you decide that you no longer want to use your Microsoft Sentinel instance associated with a Log Analytics workspace, remove Microsoft Sentinel from the workspace. But before you do, consider the implications described in this article.

It can take up to 48 hours for Microsoft Sentinel to be removed from the Log Analytics workspace. Data connector configuration and Microsoft Sentinel tables are deleted. Other resources and data are retained for a limited time.

Your subscription continues to be registered with the Microsoft Sentinel resource provider. But, you can remove it manually.

If you don't want to keep the workspace and the data collected for Microsoft Sentinel, delete the resources associated with the workspace in the Azure portal.

## Pricing changes

When Microsoft Sentinel is removed from a workspace, there might still be costs associated with the data in Azure Monitor Log Analytics. For more information on the effect to commitment tier costs, see [Simplified billing offboarding behavior](enroll-simplified-pricing-tier#offboarding-behavior).

## Data connector configurations removed

The configurations for the following data connector are removed when you remove Microsoft Sentinel from your workspace.

- Microsoft 365
- Amazon Web Services
- Microsoft services security alerts:

    - Microsoft Defender for Identity
    - Microsoft Defender for Cloud Apps including Cloud Discovery Shadow IT reporting
    - Microsoft Entra ID Protection
    - Microsoft Defender for Endpoint
    - Microsoft Defender for Cloud
- Threat Intelligence
- Common security logs including CEF-based logs, Barracuda, and Syslog. If you get security alerts from Microsoft Defender for Cloud, these logs continue to be collected.
- Windows Security Events. If you get security alerts from Microsoft Defender for Cloud, these logs continue to be collected.

Within the first 48 hours, the data and analytics rules, which include real-time automation configuration, are no longer accessible or queryable in Microsoft Sentinel.

## Resources removed

The following resources are removed after 30 days:

- Incidents (including investigation metadata)
- Analytics rules
- Bookmarks

Your playbooks, saved workbooks, saved hunting queries, and notebooks aren't removed. Some of these resources might break due to the removed data. Remove those resources manually.

After you remove the service, there's a grace period of 30 days to re-enable Microsoft Sentinel. Your data and analytics rules are restored, but the configured connectors that were disconnected must be reconnected.

## Microsoft Sentinel tables deleted

When you remove Microsoft Sentinel from your workspace, all Microsoft Sentinel tables are deleted. The data in these tables aren't accessible or queryable. But, the data retention policy set for those tables applies to the data in the deleted tables. So, if you re-enable Microsoft Sentinel on the workspace within the data retention time period, the retained data is restored to those tables.

The tables and related data that are inaccessible when you remove Microsoft Sentinel include but aren't limited to the following tables:

- `AlertEvidence`
- `AlertInfo`
- `Anomalies`
- `ASimAuditEventLogs`
- `ASimAuthenticationEventLogs`
- `ASimDhcpEventLogs`
- `ASimDnsActivityLogs`
- `ASimFileEventLogs`
- `ASimNetworkSessionLogs`
- `ASimProcessEventLogs`
- `ASimRegistryEventLogs`
- `ASimUserManagementActivityLogs`
- `ASimWebSessionLogs`
- `AWSCloudTrail`
- `AWSCloudWatch`
- `AWSGuardDuty`
- `AWSVPCFlow`
- `CloudAppEvents`
- `CommonSecurityLog`
- `ConfidentialWatchlist`
- `DataverseActivity`
- `DeviceEvents`
- `DeviceFileCertificateInfo`
- `DeviceFileEvents`
- `DeviceImageLoadEvents`
- `DeviceInfo`
- `DeviceLogonEvents`
- `DeviceNetworkEvents`
- `DeviceNetworkInfo`
- `DeviceProcessEvents`
- `DeviceRegistryEvents`
- `DeviceTvmSecureConfigurationAssessment`
- `DeviceTvmSecureConfigurationAssessmentKB`
- `DeviceTvmSoftwareInventory`
- `DeviceTvmSoftwareVulnerabilities`
- `DeviceTvmSoftwareVulnerabilitiesKB`
- `DnsEvents`
- `DnsInventory`
- `Dynamics365Activity`
- `DynamicSummary`
- `EmailAttachmentInfo`
- `EmailEvents`
- `EmailPostDeliveryEvents`
- `EmailUrlInfo`
- `GCPAuditLogs`
- `GoogleCloudSCC`
- `HuntingBookmark`
- `IdentityDirectoryEvents`
- `IdentityLogonEvents`
- `IdentityQueryEvents`
- `LinuxAuditLog`
- `McasShadowItReporting`
- `MicrosoftPurviewInformationProtection`
- `NetworkSessions`
- `OfficeActivity`
- `PowerAppsActivity`
- `PowerAutomateActivity`
- `PowerBIActivity`
- `PowerPlatformAdminActivity`
- `PowerPlatformConnectorActivity`
- `PowerPlatformDlpActivity`
- `ProjectActivity`
- `SecurityAlert`
- `SecurityEvent`
- `SecurityIncident`
- `SentinelAudit`
- `SentinelHealth`
- `ThreatIntelIndicators`
- `UrlClickEvents`
- `Watchlist`
- `WindowsEvent`

## Related resources

- [Remove Microsoft Sentinel from your Log Analytics workspace](offboard)
- [Offboard Microsoft Sentinel from the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard#offboard-microsoft-sentinel).