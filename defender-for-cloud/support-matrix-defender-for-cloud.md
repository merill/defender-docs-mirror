---
layout: Conceptual
title: Interoperability with Azure services, Azure clouds, and client operating systems - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-cloud
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
description: Learn about the Azure cloud environments where Defender for Cloud can be used, the Azure services that Defender for Cloud protects, and the client operating systems that Defender for Cloud supports.
ms.topic: limits-and-quotas
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5c4ded7b-5ec3-4d9d-cead-048c20a56047
document_version_independent_id: 278fc90a-3961-03ad-cb47-9831202bd6e2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/support-matrix-defender-for-cloud.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/support-matrix-defender-for-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/support-matrix-defender-for-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b3ec076b-5a9d-87fe-4195-ef97be0db464
---

# Interoperability with Azure services, Azure clouds, and client operating systems - Microsoft Defender for Cloud | Microsoft Learn

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

This article indicates the Azure services, client operating systems, and which features are supported in Azure commercial and government clouds by Microsoft Defender for Cloud.

## Security benefits for Azure services

Defender for Cloud provides recommendations, security alerts, and vulnerability assessment for these Azure services:

| Service | [Recommendations](security-policy-concept)free with[Foundational CSPM](concept-cloud-security-posture-management) | [Security alerts](alerts-overview) | Vulnerability assessment |
| --- | --- | --- | --- |
| Azure App Service | ✔ | ✔ | - |
| Azure Automation account | ✔ | - | - |
| Azure Batch account | ✔ | - | - |
| Azure Blob Storage | ✔ | ✔ | - |
| Azure Cache for Redis | ✔ | - | - |
| Azure Cloud Services | ✔ | - | - |
| Azure AI Search | ✔ | - | - |
| Azure AI Service | ✔ | ✔ | - |
| Azure Container Registry | ✔ | ✔ | [Defender for Containers](defender-for-containers-introduction) |
| Azure Cosmos DB\* | ✔ | ✔ | - |
| Azure Data Lake Analytics | ✔ | - | - |
| Azure Data Lake Storage | ✔ | ✔ | - |
| Azure Database for MySQL\* | - | ✔ | - |
| Azure Database for PostgreSQL\* | - | ✔ | - |
| Azure Event Hubs namespace | ✔ | - | - |
| Azure Files | ✔ | ✔ | - |
| Azure Functions app | ✔ | - | - |
| Azure Key Vault | ✔ | ✔ | - |
| Azure Kubernetes Service | ✔ | ✔ | - |
| Azure Load Balancer | ✔ | - | - |
| Azure Logic Apps | ✔ | - | - |
| Azure SQL Database | ✔ | ✔ | [Defender for Azure SQL](defender-for-sql-introduction) |
| Azure SQL Managed Instance | ✔ | ✔ | [Defender for Azure SQL](defender-for-sql-introduction) |
| Azure Service Bus namespace | ✔ | - | - |
| Azure Service Fabric account | ✔ | - | - |
| Azure Stream Analytics | ✔ | - | - |
| Azure Subscription | ✔ \*\* | ✔ | - |
| Azure Virtual Network (incl. subnets, NICs, and network security groups) | ✔ | - | - |

\* These features are currently supported in preview.

\*\* Microsoft Entra recommendations are available only for subscriptions with [enhanced security features enabled](connect-azure-subscription).

## Cloud support

In the support table, **NA** indicates that the feature isn't available.

| **Feature/Plan** | **Azure** | **Azure Government** | **Defender portal** | **Microsoft Azure operated by 21Vianet**^3^ |
| --- | --- | --- | --- | --- |
| **GENERAL FEATURES** |  |  |  |  |
| [Alert bi-directional synchronization with Microsoft Sentinel](/en-us/azure/sentinel/connect-azure-security-center) | GA | GA |  | NA |
| [Alert email notifications](configure-email-notifications) | GA | GA |  | NA |
| [Alert suppression rules](alerts-suppression-rules) | GA | GA |  | NA |
| [Automatic component/agent/extension provisioning](monitoring-components) | GA | GA | NA | GA |
| [Azure Workbooks integration for reporting](custom-dashboards-azure-workbooks) | GA | GA | NA | GA |
| [Continuous data export](continuous-export) | GA | GA | NA | NA |
| [Exempt resources from recommendations](exempt-resource) | Preview | NA | NA | NA |
| [Response automation with Azure Logic Apps](workflow-automations) | GA | GA | NA | NA |
| [Security alerts](alerts-overview) Generated when one or more Defender for Cloud plans is enabled. | GA | GA | GA | NA |
| **FOUNDATIONAL Cloud Security Posture Management (CSPM) FEATURES (FREE)** |  |  |  |  |
| [Copilot in Defender for Cloud](copilot-security-in-defender-for-cloud) | GA | NA | NA | NA |
| **FOUNDATIONAL CSPM FEATURES (FREE)** |  |  |  |  |
| [Asset inventory](asset-inventory) | GA | GA | GA | GA |
| [Security recommendations](security-policy-concept) based on the [Microsoft Cloud Security Benchmark](concept-regulatory-compliance) | GA | GA | GA | GA |
| [Secure score](secure-score-security-controls) | GA | GA | GA | GA |
| [DevOps security posture](concept-devops-environment-posture-management-overview) | Preview | NA |  | NA |
| **DEFENDER Cloud Security Posture Management (CSPM) FEATURES** |  |  |  |  |
| [Data and AI security dashboard](data-aware-security-dashboard-overview) | GA | NA | NA | NA |
| [Attack path](concept-attack-path) | GA | NA | GA | NA |
| [AI security posture management](ai-security-posture) | GA | GA |  | NA |
| [Active user](active-user) | Public preview | NA |  | NA |
| Security recommendations | GA | GA | GA | NA |
| Asset inventory | GA | GA | GA | NA |
| Secure score | GA | GA | GA | NA |
| [Workbooks](custom-dashboards-azure-workbooks) | GA | GA | NA | GA |
| Continues Export | GA | GA | NA | NA |
| Workflow automation | GA | GA | NA | NA |
| Quick Fix | GA | GA | NA | NA |
| Agentless Virtual Machine (VM) vulnerability scanning | GA | GA | NA | NA |
| Agentless VM secrets scanning | GA | GA | NA | NA |
| Attack path analysis | GA | GA | GA | NA |
| Risk prioritization | GA | GA | GA | NA |
| Security Explorer | GA | GA | NA | NA |
| Code-to-runtime mapping for containers | GA | NA | NA | NA |
| Code-to-runtime mapping for IaC | GA | NA | NA | NA |
| PR annotations | GA | NA |  | NA |
| Internet exposure analysis | GA | GA | NA | NA |
| External attack surface management | GA | NA | NA | NA |
| Cloud Infrastructure Entitlement Management (CIEM) | GA | NA |  | NA |
| Regulatory compliance | GA | GA | NA | NA |
| ServiceNow Integration | GA | NA | NA | NA |
| Critical assets protection | GA | GA | GA | NA |
| Governance | GA | GA | NA | NA |
| Sensitive data scanning (DSPM) | GA | GA | NA | NA |
| Agentless scanning for Kubernetes | GA | GA | NA | NA |
| Custom Recommendations (Preview) | Preview | NA | NA | NA |
| Agentless containers vulnerability assessment | GA | GA | NA | NA |
| API security posture management | GA | NA | NA | NA |
| [Serverless Containers](posture-for-serverless-containers) | GA | NA | GA | NA |
| [Serverless protection](serverless-protection)^4^ | GA | NA | NA | NA |
| **DEFENDER FOR CLOUD PLANS** |  |  |  |  |
| [Defender Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management) | GA | GA | NA | NA |
| [Defender for AI Services](ai-threat-protection) | GA | NA | NA | NA |
| [Defender for APIs](defender-for-apis-introduction) | GA | NA | NA | NA |
| [Defender for App Service](defender-for-app-service-introduction) | GA | NA | NA | GA |
| [Defender for Containers](defender-for-containers-introduction)[Review detailed feature support](support-matrix-defender-for-containers) | GA | GA | NA | GA |
| [DevOps Security](defender-for-devops-introduction) | GA | NA | NA | NA |
| [Defender for Domain Name System (DNS)](defender-for-dns-introduction) | GA | GA | NA | GA |
| [Defender for Key Vault](defender-for-key-vault-introduction) | GA | GA | NA | NA |
| [Defender for Resource Manager](defender-for-resource-manager-introduction) | GA | GA | NA | NA |
| [Defender for Servers](plan-defender-for-servers) Plan 1 (P1) and Plan 2 (P2) [Review detailed feature support](support-matrix-defender-for-servers) | GA | GA | NA | NA |
| [Defender for Storage](defender-for-storage-introduction) | GA | GA | NA | NA |
| **DEFENDER FOR STORAGE FEATURES** |  |  |  |  |
| Activity monitoring (security alerts) | GA | GA | NA | GA |
| [Malware scanning](defender-for-storage-malware-scan) | GA^1^ | GA | NA | NA |
| [Sensitive data threat detection (Sensitive Data Discovery)](defender-for-storage-data-sensitivity) | GA^1^ | NA | NA | NA |
| **DEFENDER FOR DATABASES FEATURES** |  |  |  |  |
| [Defender for Azure SQL database servers](defender-for-sql-introduction) | GA | GA | NA | GAA subset of alerts/vulnerability assessments is available.Behavioral threat protection isn't available. |
| [Defender for SQL servers on machines](defender-for-sql-servers-introduction) | GA | GA | NA | GA |
| [Defender for SQL Servers on Machines](defender-for-sql-introduction) | GA | GA | NA | GA |
| [Vulnerability assessment](sql-azure-vulnerability-assessment-overview) Express and Classic configurations | GA | GA | NA | GA |
| [Advanced threat protection](/en-us/azure/azure-sql/database/threat-detection-overview?view=azuresql&amp;preserve-view=true) | GA | GA | NA | GA |
| [Defender for Open-Source Relational Databases](defender-for-databases-introduction) | GA | GA | NA | GA |
| [Defender for Azure Cosmos DB](concept-defender-for-cosmos) | GA | GA | NA | NA |
| **DEFENDER FOR SERVERS FEATURES** |  |  |  |  |
| [File Integrity Monitoring](file-integrity-monitoring-overview) | GA | GA^2^ | NA | NA |
| **AI SERVICES FEATURES** |  |  |  |  |
| [Suspicious prompt evidence](ai-onboarding#enable-suspicious-prompt-evidence) | GA | NA | NA | NA |
| [Data security for AI interactions](ai-onboarding#enable-data-security-for-microsoft-with-microsoft-purview) | Preview | NA | NA | NA |
| [AI model security](ai-model-security) | Preview | NA | NA | NA |
| [Data and AI security dashboard](data-aware-security-dashboard-overview) | GA | NA | NA | NA |

^1^: Azure DNS Zone isn't supported for malware scanning and sensitive data threat detection. ^2^: GovCon Cloud Moderate (GCCM) doesn't support File Integrity Monitoring. ^3^: All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Learn more about the [retirement of Microsoft Defender for Cloud in Azure operated by 21Vianet](https://azure.microsoft.com/updates/?id=498749). ^4^: Vulnerability assessment is not supported for private network.

Important

- As of August 1, 2023, customers with an existing subscription to Defender for DNS can continue to use the service as a standalone plan.
- For new subscriptions, alerts about suspicious DNS activity are included as part of Defender for Servers Plan 2 (P2).
- There's no change to the protection scope: Defender for DNS continues to protect all Azure resources connected to Azure's default DNS resolvers. The change affects how DNS protection is billed and bundled, not what resources are covered.

## Supported operating systems

To learn more about the specific Defender for Cloud features available on Windows and Linux, review:

- [Defender for Servers support](support-matrix-defender-for-servers)
- [Defender for Containers support](support-matrix-defender-for-containers)

Note

Even though Microsoft Defender for Servers is designed to protect servers, some features are available on certain desktop operating systems. One feature that isn't currently supported for Windows desktop systems is [Defender for Cloud's integrated EDR solution: Microsoft Defender for Endpoint](integration-defender-for-endpoint).