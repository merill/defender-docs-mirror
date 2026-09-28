---
layout: Conceptual
title: Stream data from Microsoft Defender XDR to Microsoft Sentinel in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-microsoft-365-defender
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
description: Learn how to ingest incidents, alerts, and raw event data from Microsoft Defender XDR into Microsoft Sentinel in the Azure portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0dfee91f-7a55-4057-7de0-35933ddabc33
document_version_independent_id: 67ec6822-b65f-afaa-29cc-f76aabd3c50d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-microsoft-365-defender.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-microsoft-365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-microsoft-365-defender.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: d77fe5bd-550a-97f1-e845-cf877af82d05
---

# Stream data from Microsoft Defender XDR to Microsoft Sentinel in the Azure portal | Microsoft Learn

The Defender XDR connector allows you to stream all Microsoft Defender XDR incidents, alerts, and advanced hunting events into Microsoft Sentinel and keeps incidents synchronized between both portals. This article explains how to configure the Microsoft Defender XDR connector for Microsoft Sentinel in the Azure portal. Before you start, make sure you meet the prerequisites, including licensing, permissions, and solution installation.

Note

The Defender XDR connector is automatically enabled when you onboard Microsoft Sentinel to the Defender portal. The manual configuration steps described in this article are not required if you've already onboarded Microsoft Sentinel to the Defender portal. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

Microsoft Defender XDR incidents include alerts, entities, and other relevant information from all the Microsoft Defender products and services. For details about data flow, supported components, and schema mapping, see [Microsoft Defender XDR integration with Microsoft Sentinel](microsoft-365-defender-sentinel-integration).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you begin, ensure you have the following licensing, access, and resources:

- You must have a valid license for Microsoft Defender XDR, as described in [Microsoft Defender XDR prerequisites](/en-us/microsoft-365/security/mtp/prerequisites).
- Your user must have the [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator) role on the tenant you want to stream the logs from, or the equivalent permissions.
- You must have read and write permissions on your Microsoft Sentinel workspace.
- To make any changes to the connector settings, your account must be a member of the same Microsoft Entra tenant with which your Microsoft Sentinel workspace is associated.
- Install the **Microsoft Defender XDR** solution from the **Content Hub** in Microsoft Sentinel. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy). If you're working in the Defender portal, this solution is automatically installed.
- Grant access to Microsoft Sentinel as appropriate for your organization. For more information, see [Roles and permissions in Microsoft Sentinel](roles).

For on-premises Active Directory sync via Microsoft Defender for Identity:

- Your tenant must be onboarded to Microsoft Defender for Identity.
- You must have the Microsoft Defender for Identity sensor installed.

For deployment prerequisites and sensor setup steps, see [Deploy Microsoft Defender for Identity](/en-us/defender-for-identity/deploy/deploy-defender-identity).

## Connect to Microsoft Defender XDR

In Microsoft Sentinel, select **Data connectors**. Select **Microsoft Defender XDR** from the gallery and **Open connector page**.

On the connector page, the **Configuration** section has three parts:

1. **Connect incidents and alerts** enables the basic integration between Microsoft Defender XDR and Microsoft Sentinel, synchronizing incidents and their alerts between the two platforms.
2. **Connect entities** enables the integration of on-premises Active Directory user identities into Microsoft Sentinel through Microsoft Defender for Identity.
3. **Connect events** enables the collection of raw advanced hunting events from Defender components.

For connector architecture and supported data types, see [Microsoft Defender XDR integration with Microsoft Sentinel](microsoft-365-defender-sentinel-integration).

### Connect incidents and alerts

To ingest and synchronize Microsoft Defender XDR incidents with all their alerts to your Microsoft Sentinel incidents queue, complete the following steps.

1. Mark the check box labeled **Turn off all Microsoft incident creation rules for these products. Recommended**, to avoid duplication of incidents. The **Turn off all Microsoft incident creation rules for these products** check box doesn't appear once the Microsoft Defender XDR connector is connected.
2. Select the **Connect incidents & alerts** button.
3. Verify that Microsoft Sentinel is collecting Microsoft Defender XDR incident data. In Microsoft Sentinel **Logs** in the Azure portal, run the following query in the query window to retrieve security incidents ingested from the Microsoft XDR provider:

    ```kusto
       SecurityIncident
       | where ProviderName == "Microsoft XDR"
    ```

When you enable the Microsoft Defender XDR connector, any Microsoft Defender components’ connectors that were previously connected are automatically disconnected in the background. Although those component connectors continue to *appear* connected, no data flows through them.

Note

Replacing standalone connectors with the XDR connector changes the schema of your alerts and might impact your existing queries. For a detailed comparison, see [Alert schema differences: Standalone vs. XDR connector](security-alert-schema-differences).

### Connect entities

Use Microsoft Defender for Identity to sync user entities from your on-premises Active Directory to Microsoft Sentinel. This integration requires User and Entity Behavior Analytics (UEBA), which profiles entity behavior to help detect anomalous activity.

1. Select the **Go the UEBA configuration page** link.
2. In the **Entity behavior configuration** page, if you didn't enable UEBA, then at the top of the page, move the toggle to **On**.
3. Mark the **Active Directory (Preview)** check box and select **Apply**.

    ![Screenshot of UEBA configuration page for connecting user entities to Microsoft Sentinel.](media/connect-microsoft-365-defender/ueba-configuration-page.png)

### Connect events

If you want to collect advanced hunting events from Microsoft Defender for Endpoint or Microsoft Defender for Office 365, the following types of events can be collected from their corresponding advanced hunting tables.

Important

**Defender Vulnerability Management (TVM) tables aren't ingested into Microsoft Sentinel.** Tables such as `DeviceTvmSoftwareInventory` and `DeviceTvmSoftwareVulnerabilities` appear in the advanced hunting schema for autocomplete and discoverability, but Microsoft Sentinel doesn't ingest TVM data into the workspace. TVM queries can be accepted by the query editor but return no results. To query TVM data, run your queries in Defender XDR Advanced Hunting, where the data is available. To use TVM data in Microsoft Sentinel, you must build a [custom ingestion path](/en-us/azure/sentinel/create-custom-connector). For more information, see Which Defender XDR tables aren't supported in Microsoft Sentinel.

1. Mark the check boxes of the tables with the event types you wish to collect:

# [Defender for Endpoint](#tab/MDE)
| Table name | Events type |
    | --- | --- |
    | **[DeviceInfo](/en-us/microsoft-365/security/defender/advanced-hunting-deviceinfo-table)** | Machine information, including OS information |
    | **[DeviceNetworkInfo](/en-us/microsoft-365/security/defender/advanced-hunting-devicenetworkinfo-table)** | Network properties of devices, including physical adapters, IP and MAC addresses, as well as connected networks and domains |
    | **[DeviceProcessEvents](/en-us/microsoft-365/security/defender/advanced-hunting-deviceprocessevents-table)** | Process creation and related events |
    | **[DeviceNetworkEvents](/en-us/microsoft-365/security/defender/advanced-hunting-devicenetworkevents-table)** | Network connection and related events |
    | **[DeviceFileEvents](/en-us/microsoft-365/security/defender/advanced-hunting-devicefileevents-table)** | File creation, modification, and other file system events |
    | **[DeviceRegistryEvents](/en-us/microsoft-365/security/defender/advanced-hunting-deviceregistryevents-table)** | Creation and modification of registry entries |
    | **[DeviceLogonEvents](/en-us/microsoft-365/security/defender/advanced-hunting-devicelogonevents-table)** | Sign-ins and other authentication events on devices |
    | **[DeviceImageLoadEvents](/en-us/microsoft-365/security/defender/advanced-hunting-deviceimageloadevents-table)** | DLL loading events |
    | **[DeviceEvents](/en-us/microsoft-365/security/defender/advanced-hunting-deviceevents-table)** | Multiple event types, including events triggered by security controls such as Windows Defender Antivirus and exploit protection |
    | **[DeviceFileCertificateInfo](/en-us/microsoft-365/security/defender/advanced-hunting-DeviceFileCertificateInfo-table)** | Certificate information of signed files obtained from certificate verification events on endpoints |

# [Defender for Office 365](#tab/MDO)
| Table name | Events type |
    | --- | --- |
    | **[EmailAttachmentInfo](/en-us/microsoft-365/security/defender/advanced-hunting-emailattachmentinfo-table)** | Information about files attached to emails |
    | **[EmailEvents](/en-us/microsoft-365/security/defender/advanced-hunting-emailevents-table)** | Microsoft 365 email events, including email delivery and blocking events |
    | **[EmailPostDeliveryEvents](/en-us/microsoft-365/security/defender/advanced-hunting-emailpostdeliveryevents-table)** | Security events that occur post-delivery, after Microsoft 365 delivers the emails to the recipient mailbox |
    | **[EmailUrlInfo](/en-us/microsoft-365/security/defender/advanced-hunting-emailurlinfo-table)** | Information about URLs on emails |
    | **[UrlClickEvents](/en-us/defender-xdr/advanced-hunting-urlclickevents-table)** | Events involving URLs clicked, selected, or requested on Microsoft Defender for Office 365 |

# [Defender for Identity](#tab/MDI)
| Table name | Events type |
    | --- | --- |
    | **[IdentityDirectoryEvents](/en-us/microsoft-365/security/defender/advanced-hunting-identitydirectoryevents-table)** | Various identity-related events, like password changes, password expirations, and user principal name (UPN) changes, captured from an on-premises Active Directory domain controllerAlso includes system events on the domain controller |
    | **[IdentityLogonEvents](/en-us/microsoft-365/security/defender/advanced-hunting-identitylogonevents-table)** | Authentication activities made through your on-premises Active Directory, as captured by Microsoft Defender for Identity Authentication activities related to Microsoft online services, as captured by Microsoft Defender for Cloud Apps |
    | **[IdentityQueryEvents](/en-us/microsoft-365/security/defender/advanced-hunting-identityqueryevents-table)** | Information about queries performed against Active Directory objects such as users, groups, devices, and domains |

# [Defender for Cloud Apps](#tab/MDCA)
| Table name | Events type |
    | --- | --- |
    | **[CloudAppEvents](/en-us/microsoft-365/security/defender/advanced-hunting-cloudappevents-table)** | Information about activities in various cloud apps and services covered by Microsoft Defender for Cloud Apps |

# [Defender alerts](#tab/MDA)
| Table name | Events type |
    | --- | --- |
    | **[AlertInfo](/en-us/microsoft-365/security/defender/advanced-hunting-alertinfo-table)** | Alerts from Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Cloud App Security, and Microsoft Defender for Identity, including severity information and threat categorization |
    | **[AlertEvidence](/en-us/microsoft-365/security/defender/advanced-hunting-alertevidence-table)** | Information about various entities - files, IP addresses, URLs, users, devices - associated with alerts from Microsoft Defender XDR components |

---
2. Select **Apply Changes**.

To run a query in the advanced hunting tables in Log Analytics, enter the table name in the query window.

## Verify data ingestion

The data graph in the connector page indicates that you're ingesting data. Notice that it shows one line each for incidents, alerts, and events, and the events line is an aggregation of event volume across all enabled tables. After you enable the connector, use the following KQL queries to generate more specific graphs.

Use the following KQL query for a graph of the incoming Microsoft Defender XDR incidents:

```kusto
let Now = now(); 
(range TimeGenerated from ago(14d) to Now-1d step 1d 
| extend Count = 0 
| union isfuzzy=true ( 
    SecurityIncident
    | where ProviderName == "Microsoft XDR"
    | summarize Count = count() by bin_at(TimeGenerated, 1d, Now) 
) 
| summarize Count=max(Count) by bin_at(TimeGenerated, 1d, Now) 
| sort by TimeGenerated 
| project Value = iff(isnull(Count), 0, Count), Time = TimeGenerated, Legend = "Events") 
| render timechart 
```

Use the following KQL query to build a 14-day daily trend of event volume for a single advanced hunting table. This time series helps you validate ingestion consistency after enabling the connector. Replace the *DeviceEvents* table name with the table you want to monitor:

```kusto
let Now = now();
(range TimeGenerated from ago(14d) to Now-1d step 1d
| extend Count = 0
| union isfuzzy=true (
    DeviceEvents
    | summarize Count = count() by bin_at(TimeGenerated, 1d, Now)
)
| summarize Count=max(Count) by bin_at(TimeGenerated, 1d, Now)
| sort by TimeGenerated
| project Value = iff(isnull(Count), 0, Count), Time = TimeGenerated, Legend = "Events")
| render timechart
```

## Which Defender XDR tables aren't supported in Microsoft Sentinel

The following advanced hunting tables are **not ingested** into Microsoft Sentinel, even though they appear in the schema:

### Defender Vulnerability Management (TVM) tables

The following TVM tables aren't ingested into Microsoft Sentinel:

- `DeviceTvmBrowserExtensions`
- `DeviceTvmBrowserExtensionsKB`
- `DeviceTvmCertificateInfo`
- `DeviceTvmHardwareFirmware`
- `DeviceTvmInfoGathering`
- `DeviceTvmInfoGatheringKB`
- `DeviceTvmSecureConfigurationAssessment`
- `DeviceTvmSecureConfigurationAssessmentKB`
- `DeviceTvmSoftwareEvidenceBeta`
- `DeviceTvmSoftwareInventory`
- `DeviceTvmSoftwareVulnerabilities`
- `DeviceTvmSoftwareVulnerabilitiesKB`

These tables are critical for security vulnerability management, but data is not currently streamed to Microsoft Sentinel through the Defender XDR connector. If you need to use this data in Microsoft Sentinel for analytics or detections, you must implement a [custom ingestion solution](/en-us/azure/sentinel/create-custom-connector). Otherwise, query the data in Defender XDR Advanced Hunting, where it’s available.

See more information on the following items used in the incident and event-volume KQL queries in the Verify data ingestion section, in the Kusto documentation:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***union*** operator](/en-us/kusto/query/union-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***render*** operator](/en-us/kusto/query/render-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***iff()*** function](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***max()*** aggregation function](/en-us/kusto/query/max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)