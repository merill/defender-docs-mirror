---
layout: Conceptual
title: Microsoft Sentinel tables and associated connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-tables-connectors-reference
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
description: This article lists the tables ingested into Microsoft Sentinel via data connectors, and the connectors that ingest them.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: reference
ms.date: 2026-02-02T00:00:00.0000000Z
locale: en-us
document_id: c373984c-e5e3-1058-b340-f17d8ffe220a
document_version_independent_id: f1262e44-8332-e7ba-60a8-97c7899c4cf4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-tables-connectors-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-tables-connectors-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-tables-connectors-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: efd4bf0a-5ce8-df8d-0d82-990f16171a54
---

# Microsoft Sentinel tables and associated connectors | Microsoft Learn

The following table lists the tables ingested into Microsoft Sentinel via data connectors, and the connectors that ingest them. Select the table name or the connector name for more information.

| Table | Connectors | Supports DCR | Lake-only ingestion supported |
| --- | --- | --- | --- |
| [AADManagedIdentitySignInLogs](/en-us/azure/azure-monitor/reference/tables/AADManagedIdentitySignInLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADNonInteractiveUserSignInLogs](/en-us/azure/azure-monitor/reference/tables/AADNonInteractiveUserSignInLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADProvisioningLogs](/en-us/azure/azure-monitor/reference/tables/AADProvisioningLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADRiskyServicePrincipals](/en-us/azure/azure-monitor/reference/tables/AADRiskyServicePrincipals) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADRiskyUsers](/en-us/azure/azure-monitor/reference/tables/AADRiskyUsers) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADServicePrincipalRiskEvents](/en-us/azure/azure-monitor/reference/tables/AADServicePrincipalRiskEvents) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADServicePrincipalSignInLogs](/en-us/azure/azure-monitor/reference/tables/AADServicePrincipalSignInLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [AADUserRiskEvents](/en-us/azure/azure-monitor/reference/tables/AADUserRiskEvents) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| [ABAPAuditLog](/en-us/azure/azure-monitor/reference/tables/ABAPAuditLog) | [Pathlock Inc.: Threat Detection and Response for SAP](/en-us/azure/sentinel/data-connectors-reference#pathlock-inc-threat-detection-and-response-for-sap)[SAP S/4HANA Cloud Public Edition](/en-us/azure/sentinel/data-connectors-reference#sap-s4hana-cloud-public-edition)[SecurityBridge Solution for SAP](/en-us/azure/sentinel/data-connectors-reference#securitybridge-solution-for-sap) | Yes | Yes |
| ABNORMAL\_CASES\_CL | [AbnormalSecurity (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#abnormalsecurity--using-azure-functions) | Yes | Yes |
| ABNORMAL\_SECURITY\_ABUSE\_MAILBOX\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_ATO\_CASE\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_AUDIT\_LOG\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_CASE\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_LOGS\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_POSTURE\_CHANGE\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_REMEDIATION\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_THREAT\_LOG\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_SECURITY\_VENDOR\_CASE\_CL | [Abnormal Security (Push)](/en-us/azure/sentinel/data-connectors-reference#abnormal-security-push) | Yes | Yes |
| ABNORMAL\_THREAT\_MESSAGES\_CL | [AbnormalSecurity (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#abnormalsecurity--using-azure-functions) | Yes | Yes |
| [ADFSSignInLogs](/en-us/azure/azure-monitor/reference/tables/ADFSSignInLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| ADOAuditLogs\_CL | [Azure DevOps Audit Logs (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#azure-devops-audit-logs-via-codeless-connector-platform) | Yes | Yes |
| AgariAPDPolicyLog\_CL | [Fortra Agari Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#fortra-agari-data-connector-via-codeless-connector-framework) | No | No |
| AgariAPDTCLog\_CL | [Fortra Agari Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#fortra-agari-data-connector-via-codeless-connector-framework) | No | No |
| AgariBPAlertsLog\_CL | [Fortra Agari Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#fortra-agari-data-connector-via-codeless-connector-framework) | No | No |
| AgariBPThreatFeedSubs\_CL | [Fortra Agari Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#fortra-agari-data-connector-via-codeless-connector-framework) | No | No |
| AirlockDigitalExecutionHistories | [Airlock Digital connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-connector-via-codeless-connector-framework) | No | No |
| AirlockDigitalExecutionHistories\_CL | [Airlock Digital (Poll - SaaS)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-poll---saas)[Airlock Digital (Poll)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-poll)[Airlock Digital (Push)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-push) | No | No |
| AirlockDigitalFileActivitySummary | [Airlock Digital connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-connector-via-codeless-connector-framework) | No | No |
| AirlockDigitalPolicyChanges\_CL | [Airlock Digital (Push)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-push) | No | No |
| AirlockDigitalServerActivities | [Airlock Digital connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-connector-via-codeless-connector-framework) | No | No |
| AirlockDigitalServerActivities\_CL | [Airlock Digital (Poll - SaaS)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-poll---saas)[Airlock Digital (Poll)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-poll)[Airlock Digital (Push)](/en-us/azure/sentinel/data-connectors-reference#airlock-digital-push) | No | No |
| AIShield\_CL | [AIShield](/en-us/azure/sentinel/data-connectors-reference#aishield) | No | No |
| AkamaiSIEMEvent | [Akamai Security Events (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#akamai-security-events-via-codeless-connector-framework) | No | No |
| [AlertEvidence](/en-us/azure/azure-monitor/reference/tables/AlertEvidence) | [Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| alertscompromisedcredentialdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsctepdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsdlpdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsmalsitedata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsmalwaredata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertspolicydata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsquarantinedata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsremediationdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertssecurityassessmentdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| alertsubadata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| AlibabaCloudVPCFlowLogs | [Alibaba Cloud Networking Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#alibaba-cloud-networking-data-connector-via-codeless-connector-framework) | No | No |
| AliCloud\_CL | [AliCloud (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#alicloud-using-azure-functions) | No | No |
| AliCloudActionTrailLogs\_CL | [Alibaba Cloud ActionTrail (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#alibaba-cloud-actiontrail-via-codeless-connector-framework) | Yes | Yes |
| Anvilogic\_Alerts\_CL | [Anvilogic](/en-us/azure/sentinel/data-connectors-reference#anvilogic) | Yes | Yes |
| ApacheHTTPServer\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| apifirewall\_log\_1\_CL | [API Protection](/en-us/azure/sentinel/data-connectors-reference#api-protection) | No | No |
| ARGOS\_CL | [ARGOS Cloud Security](/en-us/azure/sentinel/data-connectors-reference#argos-cloud-security) | No | No |
| argsentdc\_CL | [Check Point Cyberint Alerts Connector (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#check-point-cyberint-alerts-connector-via-codeless-connector-platform) | Yes | Yes |
| Armis\_Activities\_CL | [Armis Alerts Activities (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#armis-alerts-activities-using-azure-functions) | Yes | Yes |
| Armis\_Alerts\_CL | [Armis Alerts Activities (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#armis-alerts-activities-using-azure-functions) | Yes | Yes |
| Armis\_Devices\_CL | [Armis Devices (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#armis-devices-using-azure-functions) | Yes | Yes |
| [ASimAuditEventLogs](/en-us/azure/azure-monitor/reference/tables/ASimAuditEventLogs) | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework)[Workday User Activity (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#workday-user-activity-via-codeless-connector-framework) | Yes | Yes |
| [ASimDnsActivityLogs](/en-us/azure/azure-monitor/reference/tables/ASimDnsActivityLogs) | [Windows DNS Events via AMA](/en-us/azure/sentinel/data-connectors-reference#windows-dns-events-via-ama) | Yes | Yes |
| [ASimNetworkSessionLogs](/en-us/azure/azure-monitor/reference/tables/ASimNetworkSessionLogs) | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| [ASimWebSessionLogs](/en-us/azure/azure-monitor/reference/tables/ASimWebSessionLogs) | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| AtlassianAuditEvents | [Atlassian Organization Audit Events (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#atlassian-organization-audit-events-via-codeless-connector-framework) | No | No |
| Audit\_CL | [Mimecast Audit](/en-us/azure/sentinel/data-connectors-reference#mimecast-audit) | Yes | Yes |
| [AuditLogs](/en-us/azure/azure-monitor/reference/tables/AuditLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| Audits\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| Auth0AM\_CL | [\[DEPRECATED\] Auth0 Logs (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-auth0-logs-using-azure-function-using-azure-functions) | Yes | Yes |
| Auth0Logs\_CL | [Auth0 Logs (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#auth0-logs-via-codeless-connector-framework) | Yes | Yes |
| Awareness\_Performance\_Details\_CL | [Mimecast Awareness Training](/en-us/azure/sentinel/data-connectors-reference#mimecast-awareness-training) | Yes | Yes |
| Awareness\_SafeScore\_Details\_CL | [Mimecast Awareness Training](/en-us/azure/sentinel/data-connectors-reference#mimecast-awareness-training) | Yes | Yes |
| Awareness\_User\_Data\_CL | [Mimecast Awareness Training](/en-us/azure/sentinel/data-connectors-reference#mimecast-awareness-training) | Yes | Yes |
| Awareness\_Watchlist\_Details\_CL | [Mimecast Awareness Training](/en-us/azure/sentinel/data-connectors-reference#mimecast-awareness-training) | Yes | Yes |
| AWSALBAccessLogsData | [Amazon Web Services Elastic Load Balancing (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-elastic-load-balancing-via-codeless-connector-framework) | No | No |
| AWSCloudFront\_AccessLog\_CL | [Amazon Web Services CloudFront (via Codeless Connector Framework) (Preview)](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-cloudfront-via-codeless-connector-framework-preview) | Yes | Yes |
| [AWSCloudTrail](/en-us/azure/azure-monitor/reference/tables/AWSCloudTrail) | [Amazon Web Services S3](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3)[Amazon Web Services](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services) | Yes | Yes |
| [AWSCloudWatch](/en-us/azure/azure-monitor/reference/tables/AWSCloudWatch) | [Amazon Web Services S3](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3) | Yes | Yes |
| AWSEKSLogs\_CL | [AWS EKS Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#aws-eks-data-connector-via-codeless-connector-framework) | Yes | Yes |
| [AWSGuardDuty](/en-us/azure/azure-monitor/reference/tables/AWSGuardDuty) | [Amazon Web Services S3](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3) | Yes | Yes |
| [AWSNetworkFirewallFlow](/en-us/azure/azure-monitor/reference/tables/AWSNetworkFirewallFlow) | [Amazon Web Services NetworkFirewall (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-networkfirewall-via-codeless-connector-framework) | Yes | Yes |
| [AWSRoute53Resolver](/en-us/azure/azure-monitor/reference/tables/AWSRoute53Resolver) | [Amazon Web Services S3 DNS Route53 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3-dns-route53-via-codeless-connector-framework) | Yes | Yes |
| [AWSS3ServerAccess](/en-us/azure/azure-monitor/reference/tables/AWSS3ServerAccess) | [AWS S3 Server Access Logs (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#aws-s3-server-access-logs-via-codeless-connector-framework) | Yes | Yes |
| [AWSSecurityHubFindings](/en-us/azure/azure-monitor/reference/tables/AWSSecurityHubFindings) | [AWS Security Hub Findings (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#aws-security-hub-findings-via-codeless-connector-framework) | Yes | Yes |
| [AWSVPCFlow](/en-us/azure/azure-monitor/reference/tables/AWSVPCFlow) | [Amazon Web Services S3](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3) | Yes | Yes |
| [AWSWAF](/en-us/azure/azure-monitor/reference/tables/AWSWAF) | [Amazon Web Services S3 WAF](/en-us/azure/sentinel/data-connectors-reference#amazon-web-services-s3-waf) | Yes | Yes |
| [AZFWApplicationRule](/en-us/azure/azure-monitor/reference/tables/AZFWApplicationRule) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWDnsQuery](/en-us/azure/azure-monitor/reference/tables/AZFWDnsQuery) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWFatFlow](/en-us/azure/azure-monitor/reference/tables/AZFWFatFlow) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWFlowTrace](/en-us/azure/azure-monitor/reference/tables/AZFWFlowTrace) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWIdpsSignature](/en-us/azure/azure-monitor/reference/tables/AZFWIdpsSignature) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWInternalFqdnResolutionFailure](/en-us/azure/azure-monitor/reference/tables/AZFWInternalFqdnResolutionFailure) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWNatRule](/en-us/azure/azure-monitor/reference/tables/AZFWNatRule) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWNetworkRule](/en-us/azure/azure-monitor/reference/tables/AZFWNetworkRule) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AZFWThreatIntel](/en-us/azure/azure-monitor/reference/tables/AZFWThreatIntel) | [Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall) | Yes | Yes |
| [AzureActivity](/en-us/azure/azure-monitor/reference/tables/AzureActivity) | [Azure Activity](/en-us/azure/sentinel/data-connectors-reference#azure-activity) | No | No |
| [AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/AzureDiagnostics) | [Azure Batch Account](/en-us/azure/sentinel/data-connectors-reference#azure-batch-account)[Azure Cognitive Search](/en-us/azure/sentinel/data-connectors-reference#azure-cognitive-search)[Azure DDoS Protection](/en-us/azure/sentinel/data-connectors-reference#azure-ddos-protection)[Azure Event Hub](/en-us/azure/sentinel/data-connectors-reference#azure-event-hub)[Azure Firewall](/en-us/azure/sentinel/data-connectors-reference#azure-firewall)[Azure Key Vault](/en-us/azure/sentinel/data-connectors-reference#azure-key-vault)[Azure Kubernetes Service (AKS)](/en-us/azure/sentinel/data-connectors-reference#azure-kubernetes-service-aks)[Azure Logic Apps](/en-us/azure/sentinel/data-connectors-reference#azure-logic-apps)[Azure SQL Databases](/en-us/azure/sentinel/data-connectors-reference#azure-sql-databases)[Azure Service Bus](/en-us/azure/sentinel/data-connectors-reference#azure-service-bus)[Azure Stream Analytics](/en-us/azure/sentinel/data-connectors-reference#azure-stream-analytics)[Azure Web Application Firewall (WAF)](/en-us/azure/sentinel/data-connectors-reference#azure-web-application-firewall-waf)[Network Security Groups](/en-us/azure/sentinel/data-connectors-reference#network-security-groups) | No | No |
| [AzureMetrics](/en-us/azure/azure-monitor/reference/tables/AzureMetrics) | [Azure Storage Account](/en-us/azure/sentinel/data-connectors-reference#azure-storage-account) | No | No |
| BeyondTrustPM\_ActivityAudits\_CL | [BeyondTrust PM Cloud](/en-us/azure/sentinel/data-connectors-reference#beyondtrust-pm-cloud) | Yes | Yes |
| BeyondTrustPM\_ClientEvents\_CL | [BeyondTrust PM Cloud](/en-us/azure/sentinel/data-connectors-reference#beyondtrust-pm-cloud) | Yes | Yes |
| BHEAttackPathsData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BHEAttackPathsTimelineData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BHEAuditLogsData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BHEFindingTrendsData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BHEPostureHistoryData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BHETierZeroAssetsData\_CL | [BloodHound Enterprise Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bloodhound-enterprise-data-connector-using-azure-functions) | No | No |
| BigIDDSPMCatalog\_CL | [BigID DSPM connector](/en-us/azure/sentinel/data-connectors-reference#bigid-dspm-connector) | No | No |
| BitglassLogs\_CL | [Bitglass (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#bitglass-using-azure-functions) | No | No |
| BitwardenEventLogs | [Bitwarden Event Logs](/en-us/azure/sentinel/data-connectors-reference#bitwarden-event-logs) | No | No |
| blacklens\_CL | [blacklens.io](/en-us/azure/sentinel/data-connectors-reference#blacklensio) | Yes | Yes |
| BoxEvents\_CL | [\[DEPRECATED\] Box Events (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-box-events-using-azure-function-using-azure-functions) | No | No |
| BoxEventsV2\_CL | [Box Events (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#box-events-via-codeless-connector-framework) | Yes | Yes |
| BV\_ClaudeCompliance\_ComplianceActivities\_CL | [BV-ClaudeCompliance (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#bv-claudecompliance-via-codeless-connector-framework) | Yes | Yes |
| CarbonBlack\_Alerts\_CL | [VMware Carbon Black Cloud via AWS S3 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#vmware-carbon-black-cloud-via-aws-s3-via-codeless-connector-framework) | No | No |
| CarbonBlackAuditLogs\_CL | [\[DEPRECATED\] VMware Carbon Black Cloud (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-vmware-carbon-black-cloud-using-azure-function-using-azure-functions) | No | No |
| CarbonBlackEvents\_CL | [\[DEPRECATED\] VMware Carbon Black Cloud (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-vmware-carbon-black-cloud-using-azure-function-using-azure-functions) | No | No |
| CarbonBlackNotifications\_CL | [\[DEPRECATED\] VMware Carbon Black Cloud (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-vmware-carbon-black-cloud-using-azure-function-using-azure-functions) | No | No |
| CatoNetworksEvents\_CL | [Cato Networks Events (Push)](/en-us/azure/sentinel/data-connectors-reference#cato-networks-events-push) | Yes | Yes |
| CayosoftThreatAlerts\_CL | [Cayosoft Guardian Threat Alerts](/en-us/azure/sentinel/data-connectors-reference#cayosoft-guardian-threat-alerts) | No | No |
| CBSLog\_AzureV2\_CL | [CTM360 CyberBlindSpot (Serverless)](/en-us/azure/sentinel/data-connectors-reference#ctm360-cyberblindspot-serverless) | Yes | Yes |
| CheckPointEmailSecAntiPhishingExceptions\_CL | [Check Point Email Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#check-point-email-security-via-codeless-connector-framework) | Yes | Yes |
| CheckPointEmailSecurityAuditLogs\_CL | [Check Point Email Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#check-point-email-security-via-codeless-connector-framework) | Yes | Yes |
| CheckPointEmailSecurityEvents\_CL | [Check Point Email Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#check-point-email-security-via-codeless-connector-framework) | Yes | Yes |
| CheckPointEmailSecuritySpamExceptions\_CL | [Check Point Email Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#check-point-email-security-via-codeless-connector-framework) | Yes | Yes |
| Cisco\_Umbrella\_audit\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_cloudfirewall\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | Yes | Yes |
| Cisco\_Umbrella\_dlp\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_dns\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | Yes | Yes |
| Cisco\_Umbrella\_fileevent\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_firewall\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | Yes | Yes |
| Cisco\_Umbrella\_intrusion\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_ip\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | Yes | Yes |
| Cisco\_Umbrella\_proxy\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | Yes | Yes |
| Cisco\_Umbrella\_ravpnlogs\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_ztaflow\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| Cisco\_Umbrella\_ztna\_CL | [Cisco Cloud Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-azure-functions)[Cisco Cloud Security (using elastic premium plan) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cisco-cloud-security-using-elastic-premium-plan-using-azure-functions) | No | No |
| CiscoETD\_CL | [Cisco ETD](/en-us/azure/sentinel/data-connectors-reference#cisco-etd) | No | No |
| CiscoETDv2\_CL | [Cisco Email Threat Defense (ETD)](/en-us/azure/sentinel/data-connectors-reference#cisco-email-threat-defense-etd) | Yes | Yes |
| CiscoMerakiAirMarshalEvents\_CL | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| CiscoMerakiFileScannedEvents\_CL | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| CiscoMerakiNetworkClients\_CL | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| CiscoMerakiOrganizationNetworks\_CL | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| CiscoMerakiOrganizations\_CL | [Cisco Meraki Events (using REST API) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-meraki-events-using-rest-api-via-codeless-connector-framework) | Yes | Yes |
| CiscoSDWANNetflow\_CL | [Cisco Software Defined WAN](/en-us/azure/sentinel/data-connectors-reference#cisco-software-defined-wan) | No | No |
| CiscoSecureEndpointAuditLogsV2\_CL | [Cisco Secure Endpoint (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-secure-endpoint-via-codeless-connector-framework) | Yes | Yes |
| CiscoSecureEndpointEventsV2\_CL | [Cisco Secure Endpoint (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-secure-endpoint-via-codeless-connector-framework) | Yes | Yes |
| CiscoUmbrellaAdminAudit\_CL | [Cisco Umbrella (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cisco-umbrella-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_CVAD\_Events\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_indicatorEventDetails\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_indicatorSummary\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_riskScoreChange\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_SPA\_Events\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixAnalytics\_userProfile\_V1\_CL | [Citrix Analytics (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-analytics-via-codeless-connector-framework) | Yes | Yes |
| CitrixDaaSConfigOps\_CL | [Citrix DaaS Audit & Sessions (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-daas-audit--sessions-via-codeless-connector-framework) | Yes | Yes |
| CitrixDaaSSessions\_CL | [Citrix DaaS Audit & Sessions (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#citrix-daas-audit--sessions-via-codeless-connector-framework) | Yes | Yes |
| Cloud\_Integrated\_CL | [Mimecast Cloud Integrated](/en-us/azure/sentinel/data-connectors-reference#mimecast-cloud-integrated) | Yes | Yes |
| [CloudAppEvents](/en-us/azure/azure-monitor/reference/tables/CloudAppEvents) | [Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| Cloudflare\_CL | [Cloudflare (Preview) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cloudflare-preview-using-azure-functions) | Yes | Yes |
| CloudflareV2\_CL | [Cloudflare (Using Blob Container) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#cloudflare-using-blob-container-via-codeless-connector-framework) | Yes | Yes |
| CloudGuard\_SecurityEvents\_CL | [Check Point CloudGuard CNAPP Connector for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#check-point-cloudguard-cnapp-connector-for-microsoft-sentinel) | Yes | Yes |
| CognniIncidents\_CL | [Cognni](/en-us/azure/sentinel/data-connectors-reference#cognni) | Yes | Yes |
| Cohesity\_CL | [Cohesity (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cohesity-using-azure-functions) | Yes | Yes |
| [CommonSecurityLog](/en-us/azure/azure-monitor/reference/tables/CommonSecurityLog) | [Cisco ASA/FTD via AMA](/en-us/azure/sentinel/data-connectors-reference#cisco-asaftd-via-ama)[Claroty xDome](/en-us/azure/sentinel/data-connectors-reference#claroty-xdome)[Infoblox Cloud Data Connector via AMA](/en-us/azure/sentinel/data-connectors-reference#infoblox-cloud-data-connector-via-ama)[Infoblox IQ for Threat Defense Insight Data Connector via AMA](/en-us/azure/sentinel/data-connectors-reference#infoblox-iq-for-threat-defense-insight-data-connector-via-ama)[Silverfort Admin Console](/en-us/azure/sentinel/data-connectors-reference#silverfort-admin-console)[VirtualMetric DataStream for Microsoft Sentinel data lake](/en-us/azure/sentinel/data-connectors-reference#virtualmetric-datastream-for-microsoft-sentinel-data-lake)[VirtualMetric DataStream for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#virtualmetric-datastream-for-microsoft-sentinel)[VirtualMetric Director Proxy](/en-us/azure/sentinel/data-connectors-reference#virtualmetric-director-proxy)[Zscaler Internet Access Cloud NSS Audit Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-audit-log-push-connector)[Zscaler Internet Access Cloud NSS CASB Activity Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-activity-log-push-connector)[Zscaler Internet Access Cloud NSS CASB CRM Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-crm-log-push-connector)[Zscaler Internet Access Cloud NSS CASB Cloud Storage Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-cloud-storage-log-push-connector)[Zscaler Internet Access Cloud NSS CASB Collaboration Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-collaboration-log-push-connector)[Zscaler Internet Access Cloud NSS CASB Email Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-email-log-push-connector)[Zscaler Internet Access Cloud NSS CASB File Sharing Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-file-sharing-log-push-connector)[Zscaler Internet Access Cloud NSS CASB ITSM Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-itsm-log-push-connector)[Zscaler Internet Access Cloud NSS CASB Repo Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-casb-repo-log-push-connector)[Zscaler Internet Access Cloud NSS DNS Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-dns-log-push-connector)[Zscaler Internet Access Cloud NSS Email DLP Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-email-dlp-log-push-connector)[Zscaler Internet Access Cloud NSS Endpoint DLP Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-endpoint-dlp-log-push-connector)[Zscaler Internet Access Cloud NSS Firewall Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-firewall-log-push-connector)[Zscaler Internet Access Cloud NSS Tunnel Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-tunnel-log-push-connector)[Zscaler Internet Access Cloud NSS Web Log Push Connector](/en-us/azure/sentinel/data-connectors-reference#zscaler-internet-access-cloud-nss-web-log-push-connector) | Yes | Yes |
| CommvaultAlerts\_CL | [CommvaultSecurityIQ](/en-us/azure/sentinel/data-connectors-reference#commvaultsecurityiq) | Yes | Yes |
| CommvaultAlertsCCF\_CL | [Commvault Security IQ (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#commvault-security-iq-via-codeless-connector-framework) | Yes | Yes |
| ConfluenceAuditLogs | [Atlassian Confluence Audit (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#atlassian-confluence-audit-via-codeless-connector-framework) | No | No |
| ContraForceEvents\_CL | [ContraForce Events](/en-us/azure/sentinel/data-connectors-reference#contraforce-events) | No | No |
| ContrastADRAttackEvents\_CL | [Contrast ADR Push Connector](/en-us/azure/sentinel/data-connectors-reference#contrast-adr-push-connector) | Yes | Yes |
| ContrastADRIncidents\_CL | [Contrast ADR Push Connector](/en-us/azure/sentinel/data-connectors-reference#contrast-adr-push-connector) | Yes | Yes |
| [CopilotActivity](/en-us/azure/azure-monitor/reference/tables/CopilotActivity) | [Microsoft Copilot](/en-us/azure/sentinel/data-connectors-reference#microsoft-copilot) | No | Yes |
| Corelight | [Corelight Connector Exporter](/en-us/azure/sentinel/data-connectors-reference#corelight-connector-exporter) | No | No |
| CortexXDR\_Incidents\_CL | [Cortex XDR - Incidents](/en-us/azure/sentinel/data-connectors-reference#cortex-xdr---incidents) | Yes | Yes |
| CortexXpanseAlerts\_CL | [Palo Alto Cortex Xpanse (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xpanse-via-codeless-connector-framework) | Yes | Yes |
| CriblInternal\_CL | [Cribl](/en-us/azure/sentinel/data-connectors-reference#cribl) | No | No |
| CrowdStrike\_Additional\_Events\_CL | [CrowdStrike Falcon Data Replicator (User Managed AWS-S3) (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#crowdstrike-falcon-data-replicator-user-managed-aws-s3-via-codeless-connector-framework) | Yes | Yes |
| CrowdStrikeAlertsV2\_CL | [CrowdStrike API Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#crowdstrike-api-data-connector-via-codeless-connector-framework) | Yes | Yes |
| CrowdStrikeReplicatorV2 | [CrowdStrike Falcon Data Replicator (CrowdStrike Managed AWS-S3) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#crowdstrike-falcon-data-replicator-crowdstrike-managed-aws-s3-using-azure-functions) | No | No |
| CyberArk\_AuditEvents\_CL | [Idira Audit](/en-us/azure/sentinel/data-connectors-reference#idira-audit) | Yes | Yes |
| CyberArk\_EPMEvents\_CL | [CyberArk EPM](/en-us/azure/sentinel/data-connectors-reference#cyberark-epm) | Yes | Yes |
| CyberArkEPM\_Events\_CL | [CyberArkEPM (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cyberarkepm-using-azure-functions) | Yes | Yes |
| CyberpionActionItems\_CL | [IONIX Security Logs (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#ionix-security-logs-via-codeless-connector-framework)[\[DEPRECATED\] IONIX Security Logs (Push)](/en-us/azure/sentinel/data-connectors-reference#deprecated-ionix-security-logs-push) | Yes | Yes |
| CyberSixgill\_Alerts\_CL | [Cybersixgill Actionable Alerts (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cybersixgill-actionable-alerts-using-azure-functions) | No | No |
| CybleVisionAlerts\_CL | [Cyble Vision Alerts](/en-us/azure/sentinel/data-connectors-reference#cyble-vision-alerts) | No | No |
| CyeraAssets\_CL | [Cyera DSPM Microsoft Sentinel Data Connector](/en-us/azure/sentinel/data-connectors-reference#cyera-dspm-microsoft-sentinel-data-connector) | No | No |
| CyeraAssets\_MS\_CL | [Cyera DSPM Microsoft Sentinel Data Connector](/en-us/azure/sentinel/data-connectors-reference#cyera-dspm-microsoft-sentinel-data-connector) | No | No |
| CyeraClassifications\_CL | [Cyera DSPM Microsoft Sentinel Data Connector](/en-us/azure/sentinel/data-connectors-reference#cyera-dspm-microsoft-sentinel-data-connector) | No | No |
| CyeraIdentities\_CL | [Cyera DSPM Microsoft Sentinel Data Connector](/en-us/azure/sentinel/data-connectors-reference#cyera-dspm-microsoft-sentinel-data-connector) | No | No |
| CyeraIssues\_CL | [Cyera DSPM Microsoft Sentinel Data Connector](/en-us/azure/sentinel/data-connectors-reference#cyera-dspm-microsoft-sentinel-data-connector) | No | No |
| CyfirmaASCertificatesAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaASCloudWeaknessAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaASConfigurationAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaASDomainIPReputationAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaASDomainIPVulnerabilityAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaASOpenPortsAlerts\_CL | [CYFIRMA Attack Surface](/en-us/azure/sentinel/data-connectors-reference#cyfirma-attack-surface) | Yes | Yes |
| CyfirmaBIDomainITAssetAlerts\_CL | [CYFIRMA Brand Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-brand-intelligence) | Yes | Yes |
| CyfirmaBIExecutivePeopleAlerts\_CL | [CYFIRMA Brand Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-brand-intelligence) | Yes | Yes |
| CyfirmaBIMaliciousMobileAppsAlerts\_CL | [CYFIRMA Brand Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-brand-intelligence) | Yes | Yes |
| CyfirmaBIProductSolutionAlerts\_CL | [CYFIRMA Brand Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-brand-intelligence) | Yes | Yes |
| CyfirmaBISocialHandlersAlerts\_CL | [CYFIRMA Brand Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-brand-intelligence) | Yes | Yes |
| CyfirmaCampaigns\_CL | [CYFIRMA Cyber Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-cyber-intelligence) | Yes | Yes |
| CyfirmaCompromisedAccounts\_CL | [CYFIRMA Compromised Accounts](/en-us/azure/sentinel/data-connectors-reference#cyfirma-compromised-accounts) | Yes | Yes |
| CyfirmaDBWMDarkWebAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaDBWMPhishingAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaDBWMRansomwareAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaIndicators\_CL | [CYFIRMA Cyber Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-cyber-intelligence) | Yes | Yes |
| CyfirmaMalware\_CL | [CYFIRMA Cyber Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-cyber-intelligence) | Yes | Yes |
| CyfirmaSPEConfidentialFilesAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaSPEPIIAndCIIAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaSPESocialThreatAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaSPESourceCodeAlerts\_CL | [CYFIRMA Digital Risk](/en-us/azure/sentinel/data-connectors-reference#cyfirma-digital-risk) | Yes | Yes |
| CyfirmaThreatActors\_CL | [CYFIRMA Cyber Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-cyber-intelligence) | Yes | Yes |
| CyfirmaVulnerabilities\_CL | [CYFIRMA Vulnerabilities Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyfirma-vulnerabilities-intelligence) | Yes | Yes |
| Cymru\_Scout\_Account\_Usage\_Data\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_Domain\_Data\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Communications\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Details\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Fingerprints\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Foundation\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_OpenPorts\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_PDNS\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Summary\_Certs\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Summary\_Details\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Summary\_Fingerprints\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Summary\_OpenPorts\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_Summary\_PDNS\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| Cymru\_Scout\_IP\_Data\_x509\_CL | [Team Cymru Scout Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#team-cymru-scout-data-connector-using-azure-functions) | No | No |
| CynerioEvent\_CL | [Cynerio Security Events](/en-us/azure/sentinel/data-connectors-reference#cynerio-security-events) | No | No |
| Cyren\_Indicators\_CL | [Cyren Threat Intelligence](/en-us/azure/sentinel/data-connectors-reference#cyren-threat-intelligence) | No | No |
| D3SOARIncidents\_CL | [D3 Smart SOAR Incidents](/en-us/azure/sentinel/data-connectors-reference#d3-smart-soar-incidents) | No | No |
| darktrace\_model\_alerts\_CL | [Darktrace Connector for Microsoft Sentinel REST API (Legacy)](/en-us/azure/sentinel/data-connectors-reference#darktrace-connector-for-microsoft-sentinel-rest-api-legacy) | Yes | Yes |
| DarktraceASM\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| DarktraceEMAIL\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| DarktraceIncidents\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| DarktraceModelAlerts\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| DarktraceResponseActions\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| DarktraceSystemStatusAlerts\_CL | [Darktrace ActiveAI Security Platform Connector](/en-us/azure/sentinel/data-connectors-reference#darktrace-activeai-security-platform-connector) | Yes | Yes |
| databahn\_alerts\_CL | [DataBahn](/en-us/azure/sentinel/data-connectors-reference#databahn) | No | No |
| databahn\_audit\_logs\_CL | [DataBahn](/en-us/azure/sentinel/data-connectors-reference#databahn) | No | No |
| databahn\_device\_inventory\_CL | [DataBahn](/en-us/azure/sentinel/data-connectors-reference#databahn) | No | No |
| DataminrPulse\_Alerts\_CL | [Dataminr Pulse Alerts Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#dataminr-pulse-alerts-data-connector-using-azure-functions) | No | No |
| [DataverseActivity](/en-us/azure/azure-monitor/reference/tables/DataverseActivity) | [Microsoft Dataverse](/en-us/azure/sentinel/data-connectors-reference#microsoft-dataverse) | Yes | Yes |
| datawizaserveraccess\_CL | [Datawiza DAP](/en-us/azure/sentinel/data-connectors-reference#datawiza-dap) | No | No |
| Detections\_Data\_CCF\_CL | [Vectra RUX Security Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#vectra-rux-security-data-connector-via-codeless-connector-framework) | Yes | Yes |
| Detections\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| [DeviceEvents](/en-us/azure/azure-monitor/reference/tables/DeviceEvents) | [Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| DigitalShadows\_V2\_CL | [Digital Shadows Searchlight](/en-us/azure/sentinel/data-connectors-reference#digital-shadows-searchlight) | No | No |
| [DnsEvents](/en-us/azure/azure-monitor/reference/tables/DnsEvents) | [DNS](/en-us/azure/sentinel/data-connectors-reference#dns) | Yes | Yes |
| [DnsInventory](/en-us/azure/azure-monitor/reference/tables/DnsInventory) | [DNS](/en-us/azure/sentinel/data-connectors-reference#dns) | Yes | Yes |
| DomainToolsThreatIntelDomains\_CL | [DomainTools Threat Intelligence Domain Feed](/en-us/azure/sentinel/data-connectors-reference#domaintools-threat-intelligence-domain-feed) | No | No |
| DoppelTable\_CL | [Doppel Data Connector](/en-us/azure/sentinel/data-connectors-reference#doppel-data-connector) | No | No |
| dossier\_atp\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_atp\_threat\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_dns\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_geo\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_infoblox\_web\_cat\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_inforank\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_malware\_analysis\_v3\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_nameserver\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_nameserver\_matches\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_ptr\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_rpz\_feeds\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_rpz\_feeds\_records\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_threat\_actor\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_tld\_risk\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_whitelist\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| dossier\_whois\_CL | [Infoblox Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-data-connector-via-rest-api) | No | No |
| DragonCopilot | [Dragon Copilot](/en-us/azure/sentinel/data-connectors-reference#dragon-copilot) | Yes | Yes |
| DragosAlerts\_CL | [Dragos Notifications via Cloud Sitestore](/en-us/azure/sentinel/data-connectors-reference#dragos-notifications-via-cloud-sitestore) | Yes | Yes |
| DruvaSecurityEvents\_CL | [Druva Events Connector](/en-us/azure/sentinel/data-connectors-reference#druva-events-connector) | Yes | Yes |
| DuoActivity\_CL | [Cisco Duo Activity Logs](/en-us/azure/sentinel/data-connectors-reference#cisco-duo-activity-logs) | Yes | Yes |
| DuoAuthentication\_CL | [Cisco Duo Authentication](/en-us/azure/sentinel/data-connectors-reference#cisco-duo-authentication) | Yes | Yes |
| DuoTelephony\_CL | [Cisco Duo Telephony Logs](/en-us/azure/sentinel/data-connectors-reference#cisco-duo-telephony-logs) | Yes | Yes |
| Dynamics365Activity | [Dynamics365](/en-us/azure/sentinel/data-connectors-reference#dynamics365) | Yes | No |
| DynatraceAttacks\_CL | [\[Deprecated\] Dynatrace Attacks V1](/en-us/azure/sentinel/data-connectors-reference#deprecated-dynatrace-attacks-v1) | No | No |
| DynatraceAttacksV2\_CL | [Dynatrace Attacks V2](/en-us/azure/sentinel/data-connectors-reference#dynatrace-attacks-v2) | No | No |
| DynatraceAttacksV3\_CL | [Dynatrace Attacks V3](/en-us/azure/sentinel/data-connectors-reference#dynatrace-attacks-v3) | No | No |
| DynatraceAuditLogs\_CL | [\[Deprecated\] Dynatrace Audit Logs V1](/en-us/azure/sentinel/data-connectors-reference#deprecated-dynatrace-audit-logs-v1) | Yes | Yes |
| DynatraceAuditLogsV2\_CL | [Dynatrace Audit Logs V2](/en-us/azure/sentinel/data-connectors-reference#dynatrace-audit-logs-v2) | No | No |
| DynatraceAuditLogsV3\_CL | [Dynatrace Audit Logs V3](/en-us/azure/sentinel/data-connectors-reference#dynatrace-audit-logs-v3) | No | No |
| DynatraceProblems\_CL | [\[Deprecated\] Dynatrace Problems V1](/en-us/azure/sentinel/data-connectors-reference#deprecated-dynatrace-problems-v1) | No | No |
| DynatraceProblemsV2\_CL | [Dynatrace Problems V2](/en-us/azure/sentinel/data-connectors-reference#dynatrace-problems-v2) | Yes | Yes |
| DynatraceProblemsV3\_CL | [Dynatrace Problems V3](/en-us/azure/sentinel/data-connectors-reference#dynatrace-problems-v3) | No | No |
| DynatraceSecurityProblems\_CL | [\[Deprecated\] Dynatrace Runtime Vulnerabilities V1](/en-us/azure/sentinel/data-connectors-reference#deprecated-dynatrace-runtime-vulnerabilities-v1) | No | No |
| DynatraceSecurityProblemsV2\_CL | [Dynatrace Runtime Vulnerabilities V2](/en-us/azure/sentinel/data-connectors-reference#dynatrace-runtime-vulnerabilities-v2) | No | No |
| DynatraceSecurityProblemsV3\_CL | [Dynatrace Runtime Vulnerabilities V3](/en-us/azure/sentinel/data-connectors-reference#dynatrace-runtime-vulnerabilities-v3) | No | No |
| EgressDefend\_CL | [Egress Defend](/en-us/azure/sentinel/data-connectors-reference#egress-defend) | Yes | Yes |
| EgressDefend\_v4\_CL | [Egress Defend v2](/en-us/azure/sentinel/data-connectors-reference#egress-defend-v2) | No | No |
| ElasticAgentEvent | [Elastic Agent](/en-us/azure/sentinel/data-connectors-reference#elastic-agent) | No | No |
| ElasticAgentLogsV2\_CL | [Elastic Agent (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#elastic-agent-via-codeless-connector-framework) | No | No |
| [EmailEvents](/en-us/azure/azure-monitor/reference/tables/EmailEvents) | [Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| emiocintel\_CL | [Check Point EM ThreatCloud Intelligence Feed Connector](/en-us/azure/sentinel/data-connectors-reference#check-point-em-threatcloud-intelligence-feed-connector) | No | No |
| Entities\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| Entity\_Scoring\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| ErmesBrowserSecurityEvents\_CL | [Ermes Browser Security Events](/en-us/azure/sentinel/data-connectors-reference#ermes-browser-security-events) | Yes | Yes |
| ESIExchangeConfig\_CL | [Exchange Security Insights On-Premises Collector](/en-us/azure/sentinel/data-connectors-reference#exchange-security-insights-on-premises-collector) | No | No |
| ESIExchangeOnlineConfig\_CL | [Exchange Security Insights Online Collector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#exchange-security-insights-online-collector-using-azure-functions) | Yes | Yes |
| [Event](/en-us/azure/azure-monitor/reference/tables/Event) | [Automated Logic WebCTRL](/en-us/azure/sentinel/data-connectors-reference#automated-logic-webctrl)[Microsoft Exchange Admin Audit Logs by Event Logs](/en-us/azure/sentinel/data-connectors-reference#microsoft-exchange-admin-audit-logs-by-event-logs)[Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#microsoft-exchange-logs-and-events)[\[Deprecated\] Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#deprecated-microsoft-exchange-logs-and-events) | Yes | No |
| eventsapplicationdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| eventsauditdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| eventsconnectiondata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| eventsincidentdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| eventsnetworkdata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| eventspagedata\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| ExchangeHttpProxy\_CL | [Microsoft Exchange HTTP Proxy Logs](/en-us/azure/sentinel/data-connectors-reference#microsoft-exchange-http-proxy-logs)[\[Deprecated\] Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#deprecated-microsoft-exchange-logs-and-events) | Yes | Yes |
| ExtraHop\_Detections\_CL | [ExtraHop Detections Data Connector](/en-us/azure/sentinel/data-connectors-reference#extrahop-detections-data-connector) | Yes | Yes |
| F5Telemetry\_ASM\_CL | [F5 BIG-IP](/en-us/azure/sentinel/data-connectors-reference#f5-big-ip) | No | No |
| F5Telemetry\_LTM\_CL | [F5 BIG-IP](/en-us/azure/sentinel/data-connectors-reference#f5-big-ip) | Yes | Yes |
| F5Telemetry\_system\_CL | [F5 BIG-IP](/en-us/azure/sentinel/data-connectors-reference#f5-big-ip) | Yes | Yes |
| FCRisks\_CL | [FireCompass Risks](/en-us/azure/sentinel/data-connectors-reference#firecompass-risks) | No | No |
| FilewallExchange\_CL | [Filewall for Microsoft 365](/en-us/azure/sentinel/data-connectors-reference#filewall-for-microsoft-365) | Yes | Yes |
| FinanceOperationsActivity\_CL | [Dynamics 365 Finance and Operations](/en-us/azure/sentinel/data-connectors-reference#dynamics-365-finance-and-operations) | Yes | Yes |
| FireworkV2\_CL | [Flare Push Connector](/en-us/azure/sentinel/data-connectors-reference#flare-push-connector) | Yes | Yes |
| fluentbit\_CL | [Azure CloudNGFW By Palo Alto Networks](/en-us/azure/sentinel/data-connectors-reference#azure-cloudngfw-by-palo-alto-networks) | Yes | Yes |
| ForcepointDLPEvents\_CL | [Forcepoint DLP](/en-us/azure/sentinel/data-connectors-reference#forcepoint-dlp) | No | No |
| ForescoutEvent | [Forescout](/en-us/azure/sentinel/data-connectors-reference#forescout) | No | No |
| FortinetFortiNdrCloudRaw\_CL | [Fortinet FortiNDR Cloud](/en-us/azure/sentinel/data-connectors-reference#fortinet-fortindr-cloud) | No | No |
| FortyTwoCrunchAPIProtectionV2 | [42Crunch API Protection (Push Connector via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#42crunch-api-protection-push-connector-via-codeless-connector-framework) | No | No |
| GambitPoliciesIssues\_CL | [Gambit Security Policy Issues (Push)](/en-us/azure/sentinel/data-connectors-reference#gambit-security-policy-issues-push) | No | No |
| Garrison\_ULTRARemoteLogs\_CL | [Garrison ULTRA Remote Logs (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#garrison-ultra-remote-logs-using-azure-functions) | No | No |
| [GCPApigee](/en-us/azure/azure-monitor/reference/tables/GCPApigee) | [Google ApigeeX (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-apigeex-via-codeless-connector-framework) | Yes | Yes |
| [GCPAuditLogs](/en-us/azure/azure-monitor/reference/tables/GCPAuditLogs) | [GCP Pub/Sub Audit Logs](/en-us/azure/sentinel/data-connectors-reference#gcp-pubsub-audit-logs) | Yes | Yes |
| [GCPCDN](/en-us/azure/azure-monitor/reference/tables/GCPCDN) | [Google Cloud Platform CDN (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-cdn-via-codeless-connector-framework) | Yes | Yes |
| [GCPCloudRun](/en-us/azure/azure-monitor/reference/tables/GCPCloudRun) | [GCP Cloud Run (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#gcp-cloud-run-via-codeless-connector-framework) | Yes | Yes |
| [GCPCloudSQL](/en-us/azure/azure-monitor/reference/tables/GCPCloudSQL) | [GCP Cloud SQL (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#gcp-cloud-sql-via-codeless-connector-framework) | Yes | Yes |
| [GCPComputeEngine](/en-us/azure/azure-monitor/reference/tables/GCPComputeEngine) | [Google Cloud Platform Compute Engine (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-compute-engine-via-codeless-connector-framework) | Yes | Yes |
| [GCPDNS](/en-us/azure/azure-monitor/reference/tables/GCPDNS) | [Google Cloud Platform DNS (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-dns-via-codeless-connector-framework) | Yes | Yes |
| [GCPIAM](/en-us/azure/azure-monitor/reference/tables/GCPIAM) | [Google Cloud Platform IAM (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-iam-via-codeless-connector-framework) | Yes | Yes |
| [GCPIDS](/en-us/azure/azure-monitor/reference/tables/GCPIDS) | [Google Cloud Platform Cloud IDS (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-cloud-ids-via-codeless-connector-framework) | Yes | Yes |
| GCPLoadBalancerLogs\_CL | [GCP Pub/Sub Load Balancer Logs (via Codeless Connector Platform).](/en-us/azure/sentinel/data-connectors-reference#gcp-pubsub-load-balancer-logs-via-codeless-connector-platform) | Yes | Yes |
| [GCPMonitoring](/en-us/azure/azure-monitor/reference/tables/GCPMonitoring) | [Google Cloud Platform Cloud Monitoring (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-cloud-monitoring-via-codeless-connector-framework) | Yes | Yes |
| [GCPNAT](/en-us/azure/azure-monitor/reference/tables/GCPNAT) | [Google Cloud Platform NAT (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-nat-via-codeless-connector-framework) | Yes | Yes |
| [GCPNATAudit](/en-us/azure/azure-monitor/reference/tables/GCPNATAudit) | [Google Cloud Platform NAT (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-nat-via-codeless-connector-framework) | Yes | Yes |
| [GCPResourceManager](/en-us/azure/azure-monitor/reference/tables/GCPResourceManager) | [Google Cloud Platform Resource Manager (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-cloud-platform-resource-manager-via-codeless-connector-framework) | Yes | Yes |
| [GCPVPCFlow](/en-us/azure/azure-monitor/reference/tables/GCPVPCFlow) | [GCP Pub/Sub VPC Flow Logs (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#gcp-pubsub-vpc-flow-logs-via-codeless-connector-framework) | Yes | Yes |
| GigamonV2\_CL | [Gigamon AMX Connector](/en-us/azure/sentinel/data-connectors-reference#gigamon-amx-connector) | No | No |
| GitHubAdvancedSecurityAlerts\_CL | [GitHub (using Webhooks) V2](/en-us/azure/sentinel/data-connectors-reference#github-using-webhooks-v2) | Yes | Yes |
| GitHubAuditLogPolling\_CL | [\[Deprecated\] GitHub Enterprise Audit Log](/en-us/azure/sentinel/data-connectors-reference#deprecated-github-enterprise-audit-log) | Yes | Yes |
| GitHubAuditLogsV2\_CL | [GitHub Enterprise Audit Log (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#github-enterprise-audit-log-via-codeless-connector-framework) | Yes | Yes |
| GitHubAuditLogsV3\_CL | [GitHub Enterprise Audit Log (via Azure Storage)](/en-us/azure/sentinel/data-connectors-reference#github-enterprise-audit-log-via-azure-storage) | Yes | Yes |
| githubscanaudit\_CL | [GitHub (using Webhooks)](/en-us/azure/sentinel/data-connectors-reference#github-using-webhooks) | Yes | Yes |
| [GKEAudit](/en-us/azure/azure-monitor/reference/tables/GKEAudit) | [Google Kubernetes Engine (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-kubernetes-engine-via-codeless-connector-framework) | Yes | Yes |
| [GoogleCloudSCC](/en-us/azure/azure-monitor/reference/tables/GoogleCloudSCC) | [Google Security Command Center](/en-us/azure/sentinel/data-connectors-reference#google-security-command-center) | Yes | Yes |
| [GoogleWorkspaceReports](/en-us/azure/azure-monitor/reference/tables/GoogleWorkspaceReports) | [Google Workspace Activities (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#google-workspace-activities-via-codeless-connector-framework) | Yes | Yes |
| GTI\_Vulnerabilities\_CL | [Google Threat Intelligence Vulnerabilities (CCF)](/en-us/azure/sentinel/data-connectors-reference#google-threat-intelligence-vulnerabilities-ccf) | Yes | Yes |
| GuardicoreAgents\_CL | [Akamai Guardicore](/en-us/azure/sentinel/data-connectors-reference#akamai-guardicore) | No | No |
| GuardicoreApplications\_CL | [Akamai Guardicore](/en-us/azure/sentinel/data-connectors-reference#akamai-guardicore) | No | No |
| GuardicoreAssets\_CL | [Akamai Guardicore](/en-us/azure/sentinel/data-connectors-reference#akamai-guardicore) | No | No |
| GuardicorePolicyRules\_CL | [Akamai Guardicore](/en-us/azure/sentinel/data-connectors-reference#akamai-guardicore) | No | No |
| GzSecurityEvents\_CL | [GravityZone Data Connector](/en-us/azure/sentinel/data-connectors-reference#gravityzone-data-connector) | Yes | Yes |
| HackerViewLog\_AzureV2\_CL | [CTM360 HackerView (Serverless)](/en-us/azure/sentinel/data-connectors-reference#ctm360-hackerview-serverless) | Yes | Yes |
| HalcyonAlertUpdatesV2\_CL | [Halcyon Connector (v2)](/en-us/azure/sentinel/data-connectors-reference#halcyon-connector-v2) | Yes | Yes |
| HalcyonEventsV2\_CL | [Halcyon Connector (v2)](/en-us/azure/sentinel/data-connectors-reference#halcyon-connector-v2) | Yes | Yes |
| Health\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| [IdentityLogonEvents](/en-us/azure/azure-monitor/reference/tables/IdentityLogonEvents) | [Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| Illumio\_Auditable\_Events\_CL | [Illumio SaaS (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#illumio-saas-using-azure-functions) | Yes | Yes |
| Illumio\_Flow\_Events\_CL | [Illumio SaaS (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#illumio-saas-using-azure-functions) | Yes | Yes |
| IllumioInsights\_CL | [Illumio Insights](/en-us/azure/sentinel/data-connectors-reference#illumio-insights) | Yes | Yes |
| IllumioInsightsGraph | [Illumio Insights Graph](/en-us/azure/sentinel/data-connectors-reference#illumio-insights-graph) | No | No |
| IllumioInsightsSummary\_CL | [Illumio Insights Summary](/en-us/azure/sentinel/data-connectors-reference#illumio-insights-summary) | No | No |
| ImpervaWAFCloud | [Imperva Cloud WAF (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#imperva-cloud-waf-via-codeless-connector-framework) | No | No |
| ImpervaWAFCloud\_CL | [Imperva Cloud WAF (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#imperva-cloud-waf-using-azure-functions) | Yes | Yes |
| InfobloxInsight\_CL | [Infoblox IQ for Threat Defense Insight Data Connector via REST API](/en-us/azure/sentinel/data-connectors-reference#infoblox-iq-for-threat-defense-insight-data-connector-via-rest-api) | No | No |
| InfoSecAnalytics\_CL | [InfoSecGlobal Data Connector](/en-us/azure/sentinel/data-connectors-reference#infosecglobal-data-connector) | No | No |
| IntegrationTable\_CL | [ESET Protect Platform (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#eset-protect-platform-using-azure-functions) | Yes | Yes |
| IntegrationTableIncidents\_CL | [ESET Protect Platform (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#eset-protect-platform-using-azure-functions) | Yes | Yes |
| iocsent\_CL | [Check Point Cyberint IOC Connector](/en-us/azure/sentinel/data-connectors-reference#check-point-cyberint-ioc-connector) | Yes | Yes |
| Ipinfo\_Abuse\_CL | [IPinfo Abuse Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-abuse-data-connector) | No | No |
| Ipinfo\_ASN\_CL | [IPinfo ASN Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-asn-data-connector) | No | No |
| Ipinfo\_Carrier\_CL | [IPinfo Carrier Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-carrier-data-connector) | No | No |
| Ipinfo\_Company\_CL | [IPinfo Company Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-company-data-connector) | No | No |
| Ipinfo\_CORE\_CL | [IPinfo Core Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-core-data-connector) | No | No |
| Ipinfo\_Country\_CL | [IPinfo Country ASN Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-country-asn-data-connector) | No | No |
| Ipinfo\_Domain\_CL | [IPinfo Domain Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-domain-data-connector) | No | No |
| Ipinfo\_Location\_CL | [IPinfo Iplocation Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-iplocation-data-connector) | No | No |
| Ipinfo\_Location\_extended\_CL | [IPinfo Iplocation Extended Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-iplocation-extended-data-connector) | No | No |
| Ipinfo\_PLUS\_CL | [IPinfo Plus Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-plus-data-connector) | No | No |
| Ipinfo\_Privacy\_CL | [IPinfo Privacy Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-privacy-data-connector) | No | No |
| Ipinfo\_Privacy\_extended\_CL | [IPinfo Privacy Extended Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-privacy-extended-data-connector) | No | No |
| Ipinfo\_RESIDENTIAL\_PROXY\_CL | [IPinfo ResProxy Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-resproxy-data-connector) | No | No |
| Ipinfo\_RIRWHOIS\_CL | [IPinfo RIRWHOIS Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-rirwhois-data-connector) | No | No |
| Ipinfo\_RWHOIS\_CL | [IPinfo RWHOIS Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-rwhois-data-connector) | No | No |
| Ipinfo\_WHOIS\_ASN\_CL | [IPinfo WHOIS ASN Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-whois-asn-data-connector) | No | No |
| Ipinfo\_WHOIS\_MNT\_CL | [IPinfo WHOIS MNT Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-whois-mnt-data-connector) | No | No |
| Ipinfo\_WHOIS\_NET\_CL | [IPinfo WHOIS NET Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-whois-net-data-connector) | No | No |
| Ipinfo\_WHOIS\_ORG\_CL | [IPinfo WHOIS ORG Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-whois-org-data-connector) | No | No |
| Ipinfo\_WHOIS\_POC\_CL | [IPinfo WHOIS POC Data Connector](/en-us/azure/sentinel/data-connectors-reference#ipinfo-whois-poc-data-connector) | No | No |
| Island\_Admin\_CL | [Island Enterprise Browser Admin Events (Legacy)](/en-us/azure/sentinel/data-connectors-reference#island-enterprise-browser-admin-events-legacy) | Yes | Yes |
| Island\_User\_CL | [Island Enterprise Browser User Events (Legacy)](/en-us/azure/sentinel/data-connectors-reference#island-enterprise-browser-user-events-legacy) | Yes | Yes |
| Island\_UserEvents\_V2\_CL | [Island Enterprise Browser V2](/en-us/azure/sentinel/data-connectors-reference#island-enterprise-browser-v2) | Yes | Yes |
| jamfprotectalerts\_CL | [Jamf Protect Push Connector](/en-us/azure/sentinel/data-connectors-reference#jamf-protect-push-connector) | Yes | Yes |
| jamfprotecttelemetryv2\_CL | [Jamf Protect Push Connector](/en-us/azure/sentinel/data-connectors-reference#jamf-protect-push-connector) | Yes | Yes |
| jamfprotectunifiedlogs\_CL | [Jamf Protect Push Connector](/en-us/azure/sentinel/data-connectors-reference#jamf-protect-push-connector) | Yes | Yes |
| JBossEvent\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | No | No |
| Jira\_Audit\_CL | [Atlassian Jira Audit (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#atlassian-jira-audit-using-azure-functions) | Yes | Yes |
| Jira\_Audit\_v2\_CL | [Atlassian Jira Audit (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#atlassian-jira-audit-via-codeless-connector-framework) | Yes | Yes |
| JuniperIDP\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| KeeperSecurityEventNewLogs\_CL | [Keeper Security Push Connector](/en-us/azure/sentinel/data-connectors-reference#keeper-security-push-connector) | Yes | Yes |
| LastPassNativePoller\_CL | [LastPass Enterprise - Reporting (Polling CCP)](/en-us/azure/sentinel/data-connectors-reference#lastpass-enterprise---reporting-polling-ccp) | Yes | Yes |
| LightningAttackPathLinksV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| LightningAttackPaths\_CL | [Semperis Lightning Logs](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-logs) | No | No |
| LightningAttackPathsV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| LightningIndicatorExecutionsV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| LightningIOEResults\_CL | [Semperis Lightning Logs](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-logs) | No | No |
| LightningIOEsMetadataV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| LightningTier0AttackersV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| LightningTier0Nodes\_CL | [Semperis Lightning Logs](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-logs) | No | No |
| LightningTier0NodesV2\_CL | [Semperis Lightning (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#semperis-lightning-via-codeless-connector-framework) | No | No |
| Lockdown\_Data\_CL | [Vectra XDR (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vectra-xdr-using-azure-functions) | Yes | Yes |
| Lookout\_CL | [\[DEPRECATED\] Lookout](/en-us/azure/sentinel/data-connectors-reference#deprecated-lookout) | No | No |
| LookoutMtdV2\_CL | [Lookout Mobile Threat Detection Connector (via Codeless Connector Framework) (Preview)](/en-us/azure/sentinel/data-connectors-reference#lookout-mobile-threat-detection-connector-via-codeless-connector-framework-preview) | Yes | Yes |
| MailGuard365\_Threats\_CL | [MailGuard 365](/en-us/azure/sentinel/data-connectors-reference#mailguard-365) | Yes | Yes |
| MailRiskEventEmails\_CL | [MailRisk by Secure Practice](/en-us/azure/sentinel/data-connectors-reference#mailrisk-by-secure-practice) | Yes | Yes |
| MarkLogicAudit\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | No | No |
| McasShadowItReporting​ | [Microsoft Defender for Cloud Apps](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-cloud-apps) | No | No |
| MDBALogTable\_CL | [MongoDB Atlas Logs](/en-us/azure/sentinel/data-connectors-reference#mongodb-atlas-logs) | Yes | Yes |
| meraki\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| meshStackEventLogs\_CL | [meshStack Event Logs](/en-us/azure/sentinel/data-connectors-reference#meshstack-event-logs) | No | No |
| MessageTrackingLog\_CL | [Microsoft Exchange Message Tracking Logs](/en-us/azure/sentinel/data-connectors-reference#microsoft-exchange-message-tracking-logs)[\[Deprecated\] Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#deprecated-microsoft-exchange-logs-and-events) | Yes | Yes |
| [MicrosoftPurviewInformationProtection](/en-us/azure/azure-monitor/reference/tables/MicrosoftPurviewInformationProtection) | [Microsoft Purview Information Protection](/en-us/azure/sentinel/data-connectors-reference#microsoft-purview-information-protection) | Yes | Yes |
| MimecastAudit\_CL | [Mimecast Audit & Authentication (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-audit--authentication-using-azure-functions) | No | No |
| MimecastDLP\_CL | [Mimecast Secure Email Gateway (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-secure-email-gateway-using-azure-functions) | No | No |
| MimecastSIEM\_CL | [Mimecast Secure Email Gateway (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-secure-email-gateway-using-azure-functions) | No | No |
| MimecastTTPAttachment\_CL | [Mimecast Targeted Threat Protection (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection-using-azure-functions) | No | No |
| MimecastTTPImpersonation\_CL | [Mimecast Targeted Threat Protection (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection-using-azure-functions) | No | No |
| MimecastTTPUrl\_CL | [Mimecast Targeted Threat Protection (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection-using-azure-functions) | No | No |
| MongoDBAudit\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| MuleSoft\_Cloudhub\_CL | [MuleSoft Cloudhub](/en-us/azure/sentinel/data-connectors-reference#mulesoft-cloudhub) | No | No |
| MulesoftCloudhubAlerts\_CL | [Mulesoft CloudHub Alerts Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#mulesoft-cloudhub-alerts-connector-via-codeless-connector-framework) | Yes | Yes |
| MuleSoftCloudhubLogs | [MuleSoft CloudHub Logs (Push Connector via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#mulesoft-cloudhub-logs-push-connector-via-codeless-connector-framework) | No | No |
| NCProtectUAL\_CL | [NC Protect](/en-us/azure/sentinel/data-connectors-reference#nc-protect) | No | No |
| Netskope\_WebTx\_metrics\_CL | [Netskope Data Connector](/en-us/azure/sentinel/data-connectors-reference#netskope-data-connector) | No | No |
| NetskopeAISecOps\_CL | [Netskope AI SecOps](/en-us/azure/sentinel/data-connectors-reference#netskope-ai-secops) | No | No |
| NetskopeAlerts\_CL | [Netskope Alerts and Events](/en-us/azure/sentinel/data-connectors-reference#netskope-alerts-and-events) | Yes | Yes |
| NetskopeClientStatus\_CL | [Netskope Client Status](/en-us/azure/sentinel/data-connectors-reference#netskope-client-status) | No | No |
| NetskopeWebTransactions\_CL | [Netskope Web Transactions (via Blob Storage)](/en-us/azure/sentinel/data-connectors-reference#netskope-web-transactions-via-blob-storage) | Yes | Yes |
| NetskopeWebtxData\_CL | [\[DEPRECATED\] Netskope Web Transactions Data Connector (using Azure Function)](/en-us/azure/sentinel/data-connectors-reference#deprecated-netskope-web-transactions-data-connector-using-azure-function) | No | No |
| NetskopeWebtxErrors\_CL | [\[DEPRECATED\] Netskope Web Transactions Data Connector (using Azure Function)](/en-us/azure/sentinel/data-connectors-reference#deprecated-netskope-web-transactions-data-connector-using-azure-function) | No | No |
| [NetworkAccessTraffic](/en-us/azure/azure-monitor/reference/tables/NetworkAccessTraffic) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| NexposeInsightVMCloud\_assets\_CL | [Rapid7 Insight Platform Vulnerability Management Reports (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rapid7-insight-platform-vulnerability-management-reports-using-azure-functions) | Yes | Yes |
| NexposeInsightVMCloud\_vulnerabilities\_CL | [Rapid7 Insight Platform Vulnerability Management Reports (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rapid7-insight-platform-vulnerability-management-reports-using-azure-functions) | Yes | Yes |
| NGINX\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| NordPassEventLogs\_CL | [NordPass](/en-us/azure/sentinel/data-connectors-reference#nordpass) | Yes | Yes |
| NordStellar\_CL | [NordStellar (Push)](/en-us/azure/sentinel/data-connectors-reference#nordstellar-push) | Yes | Yes |
| ObsidianActivity\_CL | [Obsidian Datasharing Connector](/en-us/azure/sentinel/data-connectors-reference#obsidian-datasharing-connector) | No | No |
| ObsidianThreat\_CL | [Obsidian Datasharing Connector](/en-us/azure/sentinel/data-connectors-reference#obsidian-datasharing-connector) | No | No |
| OCI\_LogsV2\_CL | [Oracle Cloud Infrastructure (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#oracle-cloud-infrastructure-via-codeless-connector-framework) | Yes | Yes |
| [OfficeActivity](/en-us/azure/azure-monitor/reference/tables/OfficeActivity) | [Microsoft 365 (formerly, Office 365)](/en-us/azure/sentinel/data-connectors-reference#microsoft-365-formerly-office-365) | Yes | Yes |
| OktaSSO | [Okta Single Sign-On (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#okta-single-sign-on-via-codeless-connector-framework) | No | No |
| Onapsis\_Defend\_CL | [Onapsis Defend: Integrate Unmatched SAP Threat Detection & Intel with Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#onapsis-defend-integrate-unmatched-sap-threat-detection--intel-with-microsoft-sentinel) | Yes | Yes |
| OneLoginEventsV2\_CL | [OneLogin IAM Platform (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#onelogin-iam-platform-via-codeless-connector-framework) | Yes | Yes |
| OneLoginUsersV2\_CL | [OneLogin IAM Platform (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#onelogin-iam-platform-via-codeless-connector-framework) | Yes | Yes |
| OnePasswordEventLogs\_CL | [1Password (Serverless)](/en-us/azure/sentinel/data-connectors-reference#1password-serverless)[1Password](/en-us/azure/sentinel/data-connectors-reference#1password) | Yes | Yes |
| OneTrustMetadataV3\_CL | [OneTrust](/en-us/azure/sentinel/data-connectors-reference#onetrust) | Yes | Yes |
| OpenAIAuditLogs | [OpenAI (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#openai-via-codeless-connector-framework) | No | No |
| OracleWebLogicServer\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| OrcaAlerts\_CL | [Orca Security Alerts (via Microsoft Entra ID)](/en-us/azure/sentinel/data-connectors-reference#orca-security-alerts-via-microsoft-entra-id)[Orca Security Alerts](/en-us/azure/sentinel/data-connectors-reference#orca-security-alerts) | Yes | Yes |
| PaloAltoCortexXDR\_Alerts\_CL | [Palo Alto Cortex XDR](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xdr) | Yes | Yes |
| PaloAltoCortexXDR\_Audit\_Agent\_CL | [Palo Alto Cortex XDR](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xdr) | Yes | Yes |
| PaloAltoCortexXDR\_Audit\_Management\_CL | [Palo Alto Cortex XDR](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xdr) | Yes | Yes |
| PaloAltoCortexXDR\_Endpoints\_CL | [Palo Alto Cortex XDR](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xdr) | Yes | Yes |
| PaloAltoCortexXDR\_Incidents\_CL | [Palo Alto Cortex XDR](/en-us/azure/sentinel/data-connectors-reference#palo-alto-cortex-xdr) | Yes | Yes |
| PaloAltoPrismaCloudAlertV2\_CL | [Palo Alto Prisma Cloud CSPM (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#palo-alto-prisma-cloud-cspm-via-codeless-connector-framework) | Yes | Yes |
| PanoraysCompanyFindingPOC\_CL | [Panorays](/en-us/azure/sentinel/data-connectors-reference#panorays) | Yes | Yes |
| Perimeter81\_CL | [Perimeter 81 Activity Logs](/en-us/azure/sentinel/data-connectors-reference#perimeter-81-activity-logs) | No | No |
| Phosphorus\_CL | [Phosphorus Devices](/en-us/azure/sentinel/data-connectors-reference#phosphorus-devices) | No | No |
| PingOne\_AuditActivitiesV2\_CL | [Ping One (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#ping-one-via-codeless-connector-framework) | Yes | Yes |
| PostgreSQL\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| [PowerAutomateActivity](/en-us/azure/azure-monitor/reference/tables/PowerAutomateActivity) | [Microsoft Power Automate](/en-us/azure/sentinel/data-connectors-reference#microsoft-power-automate) | Yes | Yes |
| [PowerBIActivity](/en-us/azure/azure-monitor/reference/tables/PowerBIActivity) | [Microsoft PowerBI](/en-us/azure/sentinel/data-connectors-reference#microsoft-powerbi) | Yes | Yes |
| [PowerPlatformAdminActivity](/en-us/azure/azure-monitor/reference/tables/PowerPlatformAdminActivity) | [Microsoft Power Platform Admin Activity](/en-us/azure/sentinel/data-connectors-reference#microsoft-power-platform-admin-activity) | Yes | Yes |
| prancer\_CL | [Prancer Data Connector](/en-us/azure/sentinel/data-connectors-reference#prancer-data-connector) | No | No |
| PrismaCloudCompute\_CL | [Palo Alto Prisma Cloud CWPP (using REST API)](/en-us/azure/sentinel/data-connectors-reference#palo-alto-prisma-cloud-cwpp-using-rest-api) | Yes | Yes |
| PRODAFTUstaCompromisedCards\_CL | [PRODAFT USTA - Payment Card Fraud Intelligence (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#prodaft-usta---payment-card-fraud-intelligence-via-codeless-connector-framework) | Yes | Yes |
| PRODAFTUstaCompromisedCredentials\_CL | [PRODAFT USTA - Account Takeover Prevention (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#prodaft-usta---account-takeover-prevention-via-codeless-connector-framework) | Yes | Yes |
| [ProjectActivity](/en-us/azure/azure-monitor/reference/tables/ProjectActivity) | [Microsoft Project](/en-us/azure/sentinel/data-connectors-reference#microsoft-project) | Yes | Yes |
| ProofpointPODMailLog\_CL | [Proofpoint On Demand Email Security (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-on-demand-email-security-via-codeless-connector-platform) | Yes | Yes |
| ProofpointPODMessage\_CL | [Proofpoint On Demand Email Security (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-on-demand-email-security-via-codeless-connector-platform) | Yes | Yes |
| ProofPointTAPClicksBlockedV2\_CL | [Proofpoint TAP (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-tap-via-codeless-connector-platform) | Yes | Yes |
| ProofPointTAPClicksPermittedV2\_CL | [Proofpoint TAP (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-tap-via-codeless-connector-platform) | Yes | Yes |
| ProofPointTAPMessagesBlockedV2\_CL | [Proofpoint TAP (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-tap-via-codeless-connector-platform) | Yes | Yes |
| ProofPointTAPMessagesDeliveredV2\_CL | [Proofpoint TAP (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#proofpoint-tap-via-codeless-connector-platform) | Yes | Yes |
| [PurviewDataSensitivityLogs](/en-us/azure/azure-monitor/reference/tables/PurviewDataSensitivityLogs) | [Microsoft Purview](/en-us/azure/sentinel/data-connectors-reference#microsoft-purview) | Yes | Yes |
| QscoutAppEvents\_CL | [QscoutAppEventsConnector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#qscoutappeventsconnector-via-codeless-connector-framework) | No | No |
| QualysHostDetectionV3\_CL | [Qualys Vulnerability Management (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#qualys-vulnerability-management-via-codeless-connector-framework) | Yes | Yes |
| QualysKB\_CL | [Qualys VM KnowledgeBase (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#qualys-vm-knowledgebase-using-azure-functions) | Yes | Yes |
| [QualysKnowledgeBase](/en-us/azure/azure-monitor/reference/tables/QualysKnowledgeBase) | [Qualys Knowledge Base (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#qualys-knowledge-base-via-codeless-connector-framework) | Yes | Yes |
| RadiflowEvent | [Radiflow iSID via AMA](/en-us/azure/sentinel/data-connectors-reference#radiflow-isid-via-ama) | No | No |
| [Rapid7InsightVMCloudAssets](/en-us/azure/azure-monitor/reference/tables/Rapid7InsightVMCloudAssets) | [Rapid7 Insight Platform Vulnerability Management Reports (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#rapid7-insight-platform-vulnerability-management-reports-via-codeless-connector-framework) | Yes | Yes |
| [Rapid7InsightVMCloudVulnerabilities](/en-us/azure/azure-monitor/reference/tables/Rapid7InsightVMCloudVulnerabilities) | [Rapid7 Insight Platform Vulnerability Management Reports (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#rapid7-insight-platform-vulnerability-management-reports-via-codeless-connector-framework) | Yes | Yes |
| RecordedFutureClassicAlerts\_V2\_CL | [Recorded Future - Log Ingestion](/en-us/azure/sentinel/data-connectors-reference#recorded-future---log-ingestion) | Yes | Yes |
| RecordedFuturePlaybookAlerts\_V2\_CL | [Recorded Future - Log Ingestion](/en-us/azure/sentinel/data-connectors-reference#recorded-future---log-ingestion) | Yes | Yes |
| RecordedFutureSandboxResults\_V2\_CL | [Recorded Future - Log Ingestion](/en-us/azure/sentinel/data-connectors-reference#recorded-future---log-ingestion) | Yes | Yes |
| RecordedFutureThreatMap\_V2\_CL | [Recorded Future - Log Ingestion](/en-us/azure/sentinel/data-connectors-reference#recorded-future---log-ingestion) | Yes | Yes |
| RecordedFutureThreatMapMalware\_V2\_CL | [Recorded Future - Log Ingestion](/en-us/azure/sentinel/data-connectors-reference#recorded-future---log-ingestion) | Yes | Yes |
| RedCanaryDetections\_CL | [Red Canary Threat Detection (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#red-canary-threat-detection-via-codeless-connector-framework) | Yes | Yes |
| RedSiftAuth\_CL | [Red Sift Events (CCP Push)](/en-us/azure/sentinel/data-connectors-reference#red-sift-events-ccp-push) | No | No |
| RedSiftEmailForensics\_CL | [Red Sift Events (CCP Push)](/en-us/azure/sentinel/data-connectors-reference#red-sift-events-ccp-push) | No | No |
| RelevanceSystemAlerts\_CL | [Google Threat Intelligence Relevance System Alerts](/en-us/azure/sentinel/data-connectors-reference#google-threat-intelligence-relevance-system-alerts) | Yes | Yes |
| RFI\_PlaybookAlertResults\_V2\_CL | [Recorded Future Identity - Playbook Alert Importer](/en-us/azure/sentinel/data-connectors-reference#recorded-future-identity---playbook-alert-importer) | Yes | Yes |
| RSAIDPlus\_AdminLogs\_CL | [RSA ID Plus Admin Logs Connector](/en-us/azure/sentinel/data-connectors-reference#rsa-id-plus-admin-logs-connector) | No | No |
| Rubrik\_Anomaly\_Data\_CL | [Rubrik Security Cloud Security Events (Push)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-security-events-push)[Rubrik Security Cloud data connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-data-connector-using-azure-functions) | Yes | Yes |
| Rubrik\_Events\_Data\_CL | [Rubrik Security Cloud Security Events (Push)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-security-events-push)[Rubrik Security Cloud data connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-data-connector-using-azure-functions) | Yes | Yes |
| Rubrik\_Ransomware\_Data\_CL | [Rubrik Security Cloud Security Events (Push)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-security-events-push)[Rubrik Security Cloud data connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-data-connector-using-azure-functions) | Yes | Yes |
| Rubrik\_ThreatHunt\_Data\_CL | [Rubrik Security Cloud Security Events (Push)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-security-events-push)[Rubrik Security Cloud data connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-data-connector-using-azure-functions) | Yes | Yes |
| RubrikProtectionStatus\_CL | [Rubrik Security Cloud Protection Status (using Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#rubrik-security-cloud-protection-status-using-codeless-connector-framework) | Yes | Yes |
| SailPointISC\_Events\_CL | [SailPoint Identity Security Cloud (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sailpoint-identity-security-cloud-via-codeless-connector-framework) | Yes | Yes |
| SalesforceAuditTrailV2\_CL | [Salesforce Audit Logs (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#salesforce-audit-logs-via-codeless-connector-framework) | Yes | Yes |
| SalesforceMarketingCloudAuditEvents | [Salesforce Marketing Cloud (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#salesforce-marketing-cloud-via-codeless-connector-framework) | No | No |
| SalesForceRealTimeEventMonitoring\_CL | [SalesForce Real-Time Event Monitoring Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#salesforce-real-time-event-monitoring-connector-via-codeless-connector-framework) | Yes | Yes |
| SalesforceServiceCloudV3\_CL | [Salesforce Service Cloud (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#salesforce-service-cloud-via-codeless-connector-framework) | Yes | Yes |
| Samsung\_Knox\_Audit\_CL | [Samsung Knox Asset Intelligence](/en-us/azure/sentinel/data-connectors-reference#samsung-knox-asset-intelligence) | Yes | Yes |
| SAPBTPAuditLog\_CL | [SAP BTP](/en-us/azure/sentinel/data-connectors-reference#sap-btp) | Yes | Yes |
| SAPBTPAVL\_CL | [Application Vulnerability Report for SAP BTP](/en-us/azure/sentinel/data-connectors-reference#application-vulnerability-report-for-sap-btp) | No | No |
| SAPETDAlerts\_CL | [SAP Enterprise Threat Detection, cloud edition](/en-us/azure/sentinel/data-connectors-reference#sap-enterprise-threat-detection-cloud-edition) | Yes | Yes |
| SAPETDInvestigations\_CL | [SAP Enterprise Threat Detection, cloud edition](/en-us/azure/sentinel/data-connectors-reference#sap-enterprise-threat-detection-cloud-edition) | Yes | Yes |
| SAPLogServ\_CL | [SAP LogServ (RISE), S/4HANA Cloud private edition](/en-us/azure/sentinel/data-connectors-reference#sap-logserv-rise-s4hana-cloud-private-edition) | Yes | Yes |
| [SecurityAlert](/en-us/azure/azure-monitor/reference/tables/SecurityAlert) | [Microsoft 365 Insider Risk Management](/en-us/azure/sentinel/data-connectors-reference#microsoft-365-insider-risk-management)[Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr)[Microsoft Defender for Endpoint](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-endpoint)[Microsoft Defender for Identity](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-identity)[Microsoft Defender for IoT](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-iot)[Microsoft Defender for Office 365 (Preview)](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-office-365-preview)[Microsoft Entra ID Protection](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id-protection)[Subscription-based Microsoft Defender for Cloud (Legacy)](/en-us/azure/sentinel/data-connectors-reference#subscription-based-microsoft-defender-for-cloud-legacy)[Tenant-based Microsoft Defender for Cloud](/en-us/azure/sentinel/data-connectors-reference#tenant-based-microsoft-defender-for-cloud) | Yes | Yes |
| SecurityAlert​ | [Microsoft Defender for Cloud Apps](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-cloud-apps) | No | No |
| SecurityBridgeLogs\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| [SecurityEvent](/en-us/azure/azure-monitor/reference/tables/SecurityEvent) | [Cyborg Security HUNTER Hunt Packages](/en-us/azure/sentinel/data-connectors-reference#cyborg-security-hunter-hunt-packages)[Microsoft Active-Directory Domain Controllers Security Event Logs](/en-us/azure/sentinel/data-connectors-reference#microsoft-active-directory-domain-controllers-security-event-logs)[Security Events via Legacy Agent](/en-us/azure/sentinel/data-connectors-reference#security-events-via-legacy-agent)[Windows Security Events via AMA](/en-us/azure/sentinel/data-connectors-reference#windows-security-events-via-ama)[\[Deprecated\] Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#deprecated-microsoft-exchange-logs-and-events) | Yes | Yes |
| SecurityIncident | [Derdack SIGNL4](/en-us/azure/sentinel/data-connectors-reference#derdack-signl4)[Microsoft Defender XDR](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-xdr) | Yes | Yes |
| Seg\_Cg\_CL | [Mimecast Secure Email Gateway](/en-us/azure/sentinel/data-connectors-reference#mimecast-secure-email-gateway) | Yes | Yes |
| Seg\_Dlp\_CL | [Mimecast Secure Email Gateway](/en-us/azure/sentinel/data-connectors-reference#mimecast-secure-email-gateway) | Yes | Yes |
| SentinelOneActivities\_CL | [SentinelOne (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-via-codeless-connector-framework)[SentinelOne V2 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-v2-via-codeless-connector-framework) | Yes | Yes |
| SentinelOneAgents\_CL | [SentinelOne (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-via-codeless-connector-framework)[SentinelOne V2 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-v2-via-codeless-connector-framework) | Yes | Yes |
| SentinelOneAlerts\_CL | [SentinelOne (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-via-codeless-connector-framework) | Yes | Yes |
| SentinelOneAlertsV2\_CL | [SentinelOne V2 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-v2-via-codeless-connector-framework) | Yes | Yes |
| SentinelOneGroups\_CL | [SentinelOne (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-via-codeless-connector-framework)[SentinelOne V2 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-v2-via-codeless-connector-framework) | Yes | Yes |
| SentinelOneThreats\_CL | [SentinelOne (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-via-codeless-connector-framework)[SentinelOne V2 (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#sentinelone-v2-via-codeless-connector-framework) | Yes | Yes |
| SeraphicWebSecurity\_CL | [Seraphic Web Security](/en-us/azure/sentinel/data-connectors-reference#seraphic-web-security) | No | No |
| ServiceNowAlmAsset | [ServiceNow CMDB (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#servicenow-cmdb-via-codeless-connector-framework) | No | No |
| ServiceNowCmdbCi | [ServiceNow CMDB (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#servicenow-cmdb-via-codeless-connector-framework) | No | No |
| ServiceNowCmdbCiComputer | [ServiceNow CMDB (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#servicenow-cmdb-via-codeless-connector-framework) | No | No |
| ServiceNowCmdbCiServer | [ServiceNow CMDB (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#servicenow-cmdb-via-codeless-connector-framework) | No | No |
| ServiceNowCmdbRelCi | [ServiceNow CMDB (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#servicenow-cmdb-via-codeless-connector-framework) | No | No |
| [SigninLogs](/en-us/azure/azure-monitor/reference/tables/SigninLogs) | [Microsoft Entra ID](/en-us/azure/sentinel/data-connectors-reference#microsoft-entra-id) | Yes | Yes |
| SlackAuditV2\_CL | [SlackAudit (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#slackaudit-via-codeless-connector-framework) | Yes | Yes |
| SnowflakeLoadV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeLoginV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeMaterializedViewV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeQueryV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeRoleGrantV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeRolesV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeTableStorageMetricsV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeTablesV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeUserGrantV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SnowflakeUsersV3\_CL | [Snowflake (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#snowflake-via-codeless-connector-framework) | No | No |
| SOCPrimeAuditLogs\_CL | [SOC Prime Platform Audit Logs Data Connector](/en-us/azure/sentinel/data-connectors-reference#soc-prime-platform-audit-logs-data-connector) | Yes | Yes |
| Sonrai\_Tickets\_CL | [Sonrai Data Connector](/en-us/azure/sentinel/data-connectors-reference#sonrai-data-connector) | No | No |
| SophosEP\_CL | [\[DEPRECATED\] Sophos Endpoint Protection (using Azure Function) (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-sophos-endpoint-protection-using-azure-function-using-azure-functions) | Yes | Yes |
| SophosEPEvents\_CL | [Sophos Endpoint Protection (via Codeless Connector Platform)](/en-us/azure/sentinel/data-connectors-reference#sophos-endpoint-protection-via-codeless-connector-platform) | Yes | Yes |
| SquidProxy\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| StealthTalkAnomalousAuth\_CL | [StealthTalk Anomalous Authentication](/en-us/azure/sentinel/data-connectors-reference#stealthtalk-anomalous-authentication) | No | No |
| [StorageBlobLogs](/en-us/azure/azure-monitor/reference/tables/StorageBlobLogs) | [Azure Storage Account](/en-us/azure/sentinel/data-connectors-reference#azure-storage-account) | Yes | Yes |
| [StorageFileLogs](/en-us/azure/azure-monitor/reference/tables/StorageFileLogs) | [Azure Storage Account](/en-us/azure/sentinel/data-connectors-reference#azure-storage-account) | Yes | Yes |
| [StorageQueueLogs](/en-us/azure/azure-monitor/reference/tables/StorageQueueLogs) | [Azure Storage Account](/en-us/azure/sentinel/data-connectors-reference#azure-storage-account) | Yes | Yes |
| [StorageTableLogs](/en-us/azure/azure-monitor/reference/tables/StorageTableLogs) | [Azure Storage Account](/en-us/azure/sentinel/data-connectors-reference#azure-storage-account) | Yes | Yes |
| SymantecICDx\_CL | [Symantec Integrated Cyber Defense Exchange](/en-us/azure/sentinel/data-connectors-reference#symantec-integrated-cyber-defense-exchange) | No | No |
| [Syslog](/en-us/azure/azure-monitor/reference/tables/Syslog) | [CTERA Syslog](/en-us/azure/sentinel/data-connectors-reference#ctera-syslog)[Cisco Software Defined WAN](/en-us/azure/sentinel/data-connectors-reference#cisco-software-defined-wan)[Syslog via AMA](/en-us/azure/sentinel/data-connectors-reference#syslog-via-ama)[Syslog via Legacy Agent](/en-us/azure/sentinel/data-connectors-reference#syslog-via-legacy-agent) | Yes | Yes |
| TacitRed\_Findings\_CL | [TacitRed Compromised Credentials](/en-us/azure/sentinel/data-connectors-reference#tacitred-compromised-credentials) | No | No |
| Talon\_CL | [Talon Insights](/en-us/azure/sentinel/data-connectors-reference#talon-insights) | No | No |
| TaniumComplyCompliance\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumComplyVulnerabilities\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumDefenderHealth\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumDiscoverUnmanagedAssets\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumHighUptime\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumPatchCoverageStatus\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumPatchListApplicability\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumPatchListCompliance\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumSCCMClientHealth\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| TaniumThreatResponse\_CL | [Tanium's CCF Push Connector](/en-us/azure/sentinel/data-connectors-reference#taniums-ccf-push-connector) | Yes | Yes |
| Tenable\_IE\_CL | [Tenable Identity Exposure](/en-us/azure/sentinel/data-connectors-reference#tenable-identity-exposure) | Yes | Yes |
| Tenable\_VM\_Asset\_CL | [Tenable Vulnerability Management (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#tenable-vulnerability-management-using-azure-functions) | Yes | Yes |
| Tenable\_VM\_Compliance\_CL | [Tenable Vulnerability Management (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#tenable-vulnerability-management-using-azure-functions) | Yes | Yes |
| Tenable\_VM\_Vuln\_CL | [Tenable Vulnerability Management (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#tenable-vulnerability-management-using-azure-functions) | Yes | Yes |
| Tenable\_WAS\_Asset\_CL | [Tenable Vulnerability Management (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#tenable-vulnerability-management-using-azure-functions) | Yes | Yes |
| Tenable\_WAS\_Vuln\_CL | [Tenable Vulnerability Management (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#tenable-vulnerability-management-using-azure-functions) | Yes | Yes |
| TheHiveData | [TheHive (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#thehive-via-codeless-connector-framework) | No | No |
| ThinkstCanaryIncidents\_CL | [Thinkst Canary](/en-us/azure/sentinel/data-connectors-reference#thinkst-canary) | Yes | Yes |
| [ThreatIntelIndicators](/en-us/azure/azure-monitor/reference/tables/ThreatIntelIndicators) | [CrowdStrike Falcon Adversary Intelligence (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#crowdstrike-falcon-adversary-intelligence--using-azure-functions)[Cyjax Threat Intelligence IOC Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#cyjax-threat-intelligence-ioc-connector-using-azure-functions)[Feedly IoC](/en-us/azure/sentinel/data-connectors-reference#feedly-ioc)[GreyNoise Threat Intelligence](/en-us/azure/sentinel/data-connectors-reference#greynoise-threat-intelligence)[JoeSandboxThreatIntelligence (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#joesandboxthreatintelligence-using-azure-functions)[PRODAFT USTA - IoC Threat Intelligence](/en-us/azure/sentinel/data-connectors-reference#prodaft-usta---ioc-threat-intelligence) | Yes | No |
| [ThreatIntelligenceIndicator](/en-us/azure/azure-monitor/reference/tables/ThreatIntelligenceIndicator) | [Datalake2Sentinel](/en-us/azure/sentinel/data-connectors-reference#datalake2sentinel)[Luminar IOCs and Leaked Credentials (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#luminar-iocs-and-leaked-credentials-using-azure-functions)[MISP2Sentinel](/en-us/azure/sentinel/data-connectors-reference#misp2sentinel)[Microsoft Defender Threat Intelligence](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-threat-intelligence)[Mimecast Intelligence for Microsoft - Microsoft Sentinel (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#mimecast-intelligence-for-microsoft---microsoft-sentinel-using-azure-functions)[Premium Microsoft Defender Threat Intelligence](/en-us/azure/sentinel/data-connectors-reference#premium-microsoft-defender-threat-intelligence)[Threat Intelligence Platforms](/en-us/azure/sentinel/data-connectors-reference#threat-intelligence-platforms)[Threat Intelligence Upload API (Preview)](/en-us/azure/sentinel/data-connectors-reference#threat-intelligence-upload-api-preview)[Threat intelligence - TAXII](/en-us/azure/sentinel/data-connectors-reference#threat-intelligence---taxii)[VMRayThreatIntelligence (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#vmraythreatintelligence-using-azure-functions) | Yes | No |
| Tomcat\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| TransmitSecurityActivity\_V2\_CL | [Transmit Security Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#transmit-security-data-connector-via-codeless-connector-framework) | No | No |
| TrellixEvents | [Trellix Endpoint Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#trellix-endpoint-security-via-codeless-connector-framework) | No | No |
| TrendAI\_XDR\_OAT\_V2\_CL | [TrendAI Vision One™ - OAT Detections (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#trendai-vision-one---oat-detections-via-codeless-connector-framework) | Yes | Yes |
| TrendAI\_XDR\_WORKBENCH\_V2\_CL | [TrendAI Vision One™ - Workbench Alerts (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#trendai-vision-one---workbench-alerts-via-codeless-connector-framework) | Yes | Yes |
| TrendMicro\_XDR\_OAT\_CL | [Trend Vision One (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#trend-vision-one-using-azure-functions) | Yes | Yes |
| TrendMicro\_XDR\_RCA\_Result\_CL | [Trend Vision One (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#trend-vision-one-using-azure-functions) | No | No |
| TrendMicro\_XDR\_RCA\_Task\_CL | [Trend Vision One (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#trend-vision-one-using-azure-functions) | No | No |
| TrendMicro\_XDR\_WORKBENCH\_CL | [Trend Vision One (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#trend-vision-one-using-azure-functions) | Yes | Yes |
| TrendMicroCAS\_CL | [Trend Micro Cloud App Security (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#trend-micro-cloud-app-security-using-azure-functions) | Yes | Yes |
| TrendMicroCASV2\_CL | [Trend Micro Cloud App Security (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#trend-micro-cloud-app-security-via-codeless-connector-framework) | Yes | Yes |
| Ttp\_Attachment\_CL | [Mimecast Targeted Threat Protection](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection) | Yes | Yes |
| Ttp\_Impersonation\_CL | [Mimecast Targeted Threat Protection](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection) | Yes | Yes |
| Ttp\_Url\_CL | [Mimecast Targeted Threat Protection](/en-us/azure/sentinel/data-connectors-reference#mimecast-targeted-threat-protection) | Yes | Yes |
| Ubiquiti\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| union ASimAgentEventLogs, ASimAlertEventLogs, ASimAssetEntityLogs, ASimAuditEventLogs, ASimAuthenticationEventLogs, ASimDhcpEventLogs, ASimDnsActivityLogs, ASimFileEventLogs, ASimNetworkSessionLogs, ASimProcessEventLogs, ASimRegistryEventLogs, ASimUserManagementActivityLogs, ASimWebSessionLogs | [Synqly Integration Connector](/en-us/azure/sentinel/data-connectors-reference#synqly-integration-connector) | No | No |
| UniqkeyEvents\_CL | [Uniqkey Security Events](/en-us/azure/sentinel/data-connectors-reference#uniqkey-security-events) | Yes | Yes |
| UpwindCatalogAssets\_CL | [Upwind Catalog Loader (Ingestion API)](/en-us/azure/sentinel/data-connectors-reference#upwind-catalog-loader-ingestion-api) | Yes | Yes |
| UtimacoESKMKmipServerLogs\_CL | [Utimaco Enterprise Secure Key Manager (ESKM)](/en-us/azure/sentinel/data-connectors-reference#utimaco-enterprise-secure-key-manager-eskm) | No | No |
| Vaikora\_AgentSignals\_CL | [Vaikora AI Agent Behavioral Signals](/en-us/azure/sentinel/data-connectors-reference#vaikora-ai-agent-behavioral-signals) | Yes | Yes |
| ValenceAlert\_CL | [SaaS Security](/en-us/azure/sentinel/data-connectors-reference#saas-security) | No | No |
| ValimailEnforceEvents\_CL | [Valimail Enforce Configuration Events](/en-us/azure/sentinel/data-connectors-reference#valimail-enforce-configuration-events) | Yes | Yes |
| VaronisAlerts\_CL | [\[Deprecated\] Varonis SaaS](/en-us/azure/sentinel/data-connectors-reference#deprecated-varonis-saas) | Yes | Yes |
| VaronisAlertsV2\_CL | [Varonis SaaS (Push)](/en-us/azure/sentinel/data-connectors-reference#varonis-saas-push) | Yes | Yes |
| VaronisResources\_CL | [Varonis Purview Push Connector](/en-us/azure/sentinel/data-connectors-reference#varonis-purview-push-connector) | Yes | Yes |
| vcenter\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |
| VectraStream\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | No | No |
| VeeamAuthorizationEvents\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VeeamCovewareFindings\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VeeamMalwareEvents\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VeeamOneTriggeredAlarms\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VeeamSecurityComplianceAnalyzer\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VeeamSessions\_CL | [Veeam Data Connector (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#veeam-data-connector-using-azure-functions) | Yes | Yes |
| VersasecCmsErrorLogs\_CL | [VersasecCms](/en-us/azure/sentinel/data-connectors-reference#versaseccms) | No | No |
| VersasecCmsSysLogs\_CL | [VersasecCms](/en-us/azure/sentinel/data-connectors-reference#versaseccms) | No | No |
| VMwareWorkspaceOneDeviceApps | [VMware Workspace ONE (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#vmware-workspace-one-via-codeless-connector-framework) | No | No |
| VMwareWorkspaceOneDevices | [VMware Workspace ONE (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#vmware-workspace-one-via-codeless-connector-framework) | No | No |
| [W3CIISLog](/en-us/azure/azure-monitor/reference/tables/W3CIISLog) | [IIS Logs of Microsoft Exchange Servers](/en-us/azure/sentinel/data-connectors-reference#iis-logs-of-microsoft-exchange-servers)[\[Deprecated\] Microsoft Exchange Logs and Events](/en-us/azure/sentinel/data-connectors-reference#deprecated-microsoft-exchange-logs-and-events) | Yes | No |
| web\_assets\_CL | [Holm Security Data Connector](/en-us/azure/sentinel/data-connectors-reference#holm-security-data-connector) | No | No |
| [WindowsEvent](/en-us/azure/azure-monitor/reference/tables/WindowsEvent) | [Windows Forwarded Events](/en-us/azure/sentinel/data-connectors-reference#windows-forwarded-events) | Yes | Yes |
| WizAuditLogsV3\_CL | [Wiz for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#wiz-for-microsoft-sentinel) | No | No |
| WizDetectionsV3\_CL | [Wiz for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#wiz-for-microsoft-sentinel) | Yes | Yes |
| WizIssuesV3\_CL | [Wiz for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors-reference#wiz-for-microsoft-sentinel) | Yes | Yes |
| Workplace\_Facebook\_CL | [Workplace from Facebook (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#workplace-from-facebook-using-azure-functions) | No | No |
| WsSecurityEvents\_CL | [WithSecure Elements (CCF)](/en-us/azure/sentinel/data-connectors-reference#withsecure-elements-ccf)[WithSecure Elements API (Azure Function)](/en-us/azure/sentinel/data-connectors-reference#withsecure-elements-api-azure-function) | Yes | Yes |
| XbowAssessments\_CL | [XBOW Security Platform (via Azure Function)](/en-us/azure/sentinel/data-connectors-reference#xbow-security-platform-via-azure-function) | No | No |
| XbowAssets\_CL | [XBOW Security Platform (via Azure Function)](/en-us/azure/sentinel/data-connectors-reference#xbow-security-platform-via-azure-function) | No | No |
| XbowFindings\_CL | [XBOW Security Platform (via Azure Function)](/en-us/azure/sentinel/data-connectors-reference#xbow-security-platform-via-azure-function) | No | No |
| ZeroFox\_CTI\_advanced\_dark\_web\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_botnet\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_breaches\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_C2\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_compromised\_credentials\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_credit\_cards\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_dark\_web\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_discord\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_disruption\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_email\_addresses\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_exploits\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_irc\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_malware\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_national\_ids\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_phishing\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_phone\_numbers\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_ransomware\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_telegram\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_threat\_actors\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFox\_CTI\_vulnerabilities\_CL | [ZeroFox CTI](/en-us/azure/sentinel/data-connectors-reference#zerofox-cti) | No | No |
| ZeroFoxAdvancedDarkWeb\_CL | [ZeroFox Enterprise - Advanced Dark Web](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---advanced-dark-web) | Yes | Yes |
| ZeroFoxAlertPoller\_CL | [ZeroFox Alerts](/en-us/azure/sentinel/data-connectors-reference#zerofox-alerts)[ZeroFox Enterprise - Alerts (Polling CCF)](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---alerts-polling-ccf) | Yes | Yes |
| ZeroFoxBotnet\_CL | [ZeroFox Enterprise - Botnet](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---botnet) | Yes | Yes |
| ZeroFoxBotnetCC\_CL | [ZeroFox Enterprise - Botnet Compromised Credentials](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---botnet-compromised-credentials) | Yes | Yes |
| ZeroFoxBreaches\_CL | [ZeroFox Enterprise - Breaches](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---breaches) | Yes | Yes |
| ZeroFoxCompromisedCredentials\_CL | [ZeroFox Enterprise - Compromised Credentials](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---compromised-credentials) | Yes | Yes |
| ZeroFoxCreditCards\_CL | [ZeroFox Enterprise - Credit Cards](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---credit-cards) | Yes | Yes |
| ZeroFoxDarkWeb\_CL | [ZeroFox Enterprise - Dark Web](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---dark-web) | Yes | Yes |
| ZeroFoxDiscord\_CL | [ZeroFox Enterprise - Discord](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---discord) | Yes | Yes |
| ZeroFoxDisruption\_CL | [ZeroFox Enterprise - Disruption](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---disruption) | Yes | Yes |
| ZeroFoxEmailAddresses\_CL | [ZeroFox Enterprise - Email Addresses](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---email-addresses) | Yes | Yes |
| ZeroFoxExploits\_CL | [ZeroFox Enterprise - Exploits](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---exploits) | Yes | Yes |
| ZeroFoxIndicators\_CL | [ZeroFox Enterprise - Indicators](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---indicators) | Yes | Yes |
| ZeroFoxKeyIncidents\_CL | [ZeroFox Enterprise - Key Incidents](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---key-incidents) | Yes | Yes |
| ZeroFoxNationalIds\_CL | [ZeroFox Enterprise - National IDs](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---national-ids) | Yes | Yes |
| ZeroFoxPhysicalThreats\_CL | [ZeroFox Enterprise - Physical Threats](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---physical-threats) | Yes | Yes |
| ZeroFoxTelegram\_CL | [ZeroFox Enterprise - Telegram](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---telegram) | Yes | Yes |
| ZeroFoxVulnerabilities\_CL | [ZeroFox Enterprise - Vulnerabilities](/en-us/azure/sentinel/data-connectors-reference#zerofox-enterprise---vulnerabilities) | Yes | Yes |
| ZimperiumIncidentLog\_CL | [Zimperium Mobile Threat Defense CCF](/en-us/azure/sentinel/data-connectors-reference#zimperium-mobile-threat-defense-ccf) | Yes | Yes |
| ZimperiumIncidentMitigationLog\_CL | [Zimperium Mobile Threat Defense CCF](/en-us/azure/sentinel/data-connectors-reference#zimperium-mobile-threat-defense-ccf) | Yes | Yes |
| ZimperiumMitigationLogV2\_CL | [Zimperium Mobile Threat Defense CCF](/en-us/azure/sentinel/data-connectors-reference#zimperium-mobile-threat-defense-ccf) | Yes | Yes |
| ZimperiumThreatLogV2\_CL | [Zimperium Mobile Threat Defense CCF](/en-us/azure/sentinel/data-connectors-reference#zimperium-mobile-threat-defense-ccf) | Yes | Yes |
| ZNAudit\_CL | [Zero Networks Segment (Push)](/en-us/azure/sentinel/data-connectors-reference#zero-networks-segment-push) | Yes | Yes |
| ZNIdentityActivity\_CL | [Zero Networks Segment (Push)](/en-us/azure/sentinel/data-connectors-reference#zero-networks-segment-push) | Yes | Yes |
| ZNNetworkActivity\_CL | [Zero Networks Segment (Push)](/en-us/azure/sentinel/data-connectors-reference#zero-networks-segment-push) | Yes | Yes |
| ZNRPCActivity\_CL | [Zero Networks Segment (Push)](/en-us/azure/sentinel/data-connectors-reference#zero-networks-segment-push) | Yes | Yes |
| ZNSegmentAuditNativePoller\_CL | [Zero Networks Segment Audit](/en-us/azure/sentinel/data-connectors-reference#zero-networks-segment-audit) | Yes | Yes |
| Zoom\_CL | [\[DEPRECATED\] Zoom Reports (using Azure Functions)](/en-us/azure/sentinel/data-connectors-reference#deprecated-zoom-reports-using-azure-functions) | No | No |
| ZoomV2\_CL | [Zoom Reports Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#zoom-reports-connector-via-codeless-connector-framework) | Yes | Yes |
| ZPA\_CL | [Custom logs via AMA](/en-us/azure/sentinel/data-connectors-reference#custom-logs-via-ama) | Yes | Yes |