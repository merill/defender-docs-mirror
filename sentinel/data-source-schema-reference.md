---
layout: Conceptual
title: Microsoft Sentinel data source schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/data-source-schema-reference
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
description: This article lists Azure and third-party data source schemas supported by Microsoft Sentinel, with links to their reference documentation.
author: guywi-ms
ms.author: guywild
ms.topic: reference
ms.date: 2021-11-09T00:00:00.0000000Z
locale: en-us
document_id: 920ff055-639d-1b48-57e8-5c161cedc800
document_version_independent_id: 22171b72-41b8-51f1-4f76-a884558b6c5c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/data-source-schema-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/data-source-schema-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/data-source-schema-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 015fb137-dcea-3b7e-e14e-1a79658c35bc
---

# Microsoft Sentinel data source schema reference | Microsoft Learn

This article lists supported Azure and third-party data source schemas, with links to their reference documentation.

## Azure data sources

| Type | Data source | Log Analytics tablename | Schema reference |
| --- | --- | --- | --- |
| **Azure** | Microsoft Entra ID | SigninEvents | [Microsoft Entra activity reports sign-in properties](/en-us/graph/api/resources/signin#properties) |
| **Azure** | Microsoft Entra ID | AuditLogs | [Azure Monitor AuditLogs reference](/en-us/azure/azure-monitor/reference/tables/auditlogs) |
| **Azure** | Microsoft Entra ID | AzureActivity | [Azure Monitor AzureActivity reference](/en-us/azure/azure-monitor/reference/tables/azureactivity) |
| **Azure** | Office | OfficeActivity | Office 365 Management Activity API schemas: - [Common schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#common-schema)- [Exchange Admin schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#exchange-admin-schema)- [Exchange Mailbox schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#exchange-mailbox-schema)- [SharePoint Base schema](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#sharepoint-base-schema)- [SharePoint file operations](/en-us/office/office-365-management-api/office-365-management-activity-api-schema#sharepoint-file-operations) |
| **Azure** | Azure Key Vault | AzureDiagnostics | [Azure Monitor AzureDiagnostics reference](/en-us/azure/azure-monitor/reference/tables/azurediagnostics) |
| **Host** | Linux | Syslog | [Azure Monitor Syslog reference](/en-us/azure/azure-monitor/reference/tables/syslog) |
| **Network** | IIS Logs | W3CIISLog | [Azure Monitor W3CIISLog reference](/en-us/azure/azure-monitor/reference/tables/w3ciislog) |
| **Network** | VMinsights | VMConnection | [Azure Monitor VMConnection reference](/en-us/azure/azure-monitor/reference/tables/vmconnection) |
| **Network** | Wire Data Solution | WireData | [Azure Monitor WireData reference](/en-us/azure/azure-monitor/reference/tables/wiredata) |
| **Network** | NSG Flow Logs | AzureNetworkAnalytics | [Schema and data aggregation in Traffic Analytics](/en-us/azure/network-watcher/traffic-analytics-schema) |

Note

For more information, see the entire [Azure Monitor data reference](/en-us/azure/azure-monitor/reference/).

## 3rd-party vendor data sources

The following table lists supported third-party vendors and their Syslog or Common Event Format (CEF)-mapping documentation for various supported log types, which contain CEF field mappings and sample logs for each category type.

| Type | Vendor | Product | Log Analytics tablename | CEF field-mapping reference |
| --- | --- | --- | --- | --- |
| **Network** | Palo Alto | PAN OS | CommonSecurityLog | [PAN-OS 9.0 Common Event Format Integration Guide](https://docs.paloaltonetworks.com/content/dam/techdocs/en_US/pdf/cef/pan-os-90-cef-configuration-guide.pdf) (search for *CEF- style Log Formats*) |
| **Network** | Check Point | ALL | CommonSecurityLog | [Log Fields Description](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&amp;solutionid=sk109795) |
| **Network** | Fortigate | ALL | CommonSecurityLog | [Log Schema Structure](https://docs.fortinet.com/document/fortigate/6.2.3/fortios-log-message-reference/738142/log-schema-structure) |
| **Network** | Barracuda | Web Application Firewall | CommonSecurityLog | [How to Configure Syslog and Other Logs](https://campus.barracuda.com/product/webapplicationfirewall/doc/4259935/how-to-configure-syslog-and-other-logs/) |
| **Network** | Cisco | ASA | CommonSecurityLog | [Cisco ASA Series Syslog Messages](https://www.cisco.com/c/en/us/td/docs/security/asa/syslog/b_syslog/about.html) |
| **Network** | Cisco | Firepower | CommonSecurityLog | [Cisco Firepower Threat Defense Syslog Messages](https://www.cisco.com/c/en/us/td/docs/security/firepower/Syslogs/b_fptd_syslog_guide.html) |
| **Network** | Cisco | Umbrella | Custom Logs Table | [Log Formats and Versioning](https://docs.umbrella.com/deployment-umbrella/docs/log-formats-and-versioning) |
| **Network** | Cisco | Meraki | CommonSecurityLog | [Syslog Event Types and Log Samples](https://documentation.meraki.com/zGeneral_Administration/Monitoring_and_Reporting/Syslog_Event_Types_and_Log_Samples) |
| **Network** | Zscaler | Nano Streaming Service (NSS) | CommonSecurityLog | [Formatting NSS Feeds](https://help.zscaler.com/zia/documentation-knowledgebase/analytics/nss/nss-feeds/formatting-nss-feeds) (Web, Firewall, DNS, and Tunnel logs only) |
| **Network** | F5 | BigIP LTM | CommonSecurityLog | [Event Messages and Attack Types](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/bigip-external-monitoring-implementations-13-0-0/15.html) |
| **Network** | F5 | BigIP ASM | CommonSecurityLog | [Logging Application Security Events](https://techdocs.f5.com/kb/en-us/products/big-ip_asm/manuals/product/asm-implementations-13-1-0/14.html) |
| **Network** | Citrix | Web App Firewall | CommonSecurityLog | [Common Event Format (CEF) Logging Support in the Application Firewall](https://support.citrix.com/article/CTX227310/netscaler-app-firewall-deployment-faq-and-guides) |
| **Host** | Symantec | Symantec Endpoint Protection Manager (SEPM) | CommonSecurityLog | [External Logging settings and log event severity levels for Endpoint Protection Manager](https://support.symantec.com/us/en/article.tech171741.html) |
| **Host** | Trend Micro | All | CommonSecurityLog | [Syslog Content Mapping - CEF](https://docs.trendmicro.com/en-us/enterprise/trend-micro-apex-central-2019-online-help/appendices/syslog-mapping-cef.aspx) |

Note

For more information, see also [CEF and CommonSecurityLog field mapping](cef-name-mapping).