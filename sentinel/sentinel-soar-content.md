---
layout: Conceptual
title: Microsoft Sentinel SOAR content catalog | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-soar-content
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
description: This article displays and details the content provided by Microsoft Sentinel for security orchestration, automation, and response (SOAR), including playbooks and Logic Apps connectors.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2021-10-18T00:00:00.0000000Z
locale: en-us
document_id: 6773a2da-3c47-15aa-d72f-1c5db8d56962
document_version_independent_id: 03b701bc-0d25-095a-e933-8f4a4e466f34
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-soar-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-soar-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-soar-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 18b1db48-c857-71e1-31ab-21dd6d925232
---

# Microsoft Sentinel SOAR content catalog | Microsoft Learn

Microsoft Sentinel provides a wide variety of playbooks and connectors for security orchestration, automation, and response (SOAR), so that you can readily integrate Microsoft Sentinel with any product or service in your environment.

The integrations listed below may include some or all of the following components:

| Component type | Purpose | Use case and linked instructions |
| --- | --- | --- |
| **Playbook templates** | Automated workflow | Use playbook templates to deploy ready-made playbooks for responding to threats automatically.[Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks) |
| **Azure Logic Apps managed connector** | Building blocks for creating playbooks | Playbooks use managed connectors to communicate with hundreds of both Microsoft and non-Microsoft services.[List of Logic Apps connectors and their documentation](/en-us/connectors/connector-reference/) |
| **Azure Logic Apps custom connector** | Building blocks for creating playbooks | You may want to communicate with services that aren't available as prebuilt connectors. Custom connectors address this need by allowing you to create (and even share) a connector and define its own triggers and actions.<br>- [Custom connectors overview](/en-us/connectors/custom-connectors/)<br>- [Create your own custom Logic Apps connectors](/en-us/connectors/custom-connectors/create-logic-apps-connector) |
|  |  |  |

You can find SOAR integrations and their components in the following places:

- Microsoft Sentinel solutions
- Microsoft Sentinel Automation blade, playbook templates tab
- Logic Apps designer (for managed Logic Apps connectors)
- Microsoft Sentinel GitHub repository

Tip

- Many SOAR integrations can be deployed as part of a [Microsoft Sentinel solution](sentinel-solutions), together with related data connectors, analytics rules and workbooks. For more information, see the [Microsoft Sentinel solutions catalog](sentinel-solutions-catalog).
- More integrations are provided by the Microsoft Sentinel community and can be found in the GitHub repository.
- If you have a product or service that isn't listed or currently supported, please submit a Feature Request.You can also create your own, using the following tools:
    - Logic Apps custom connector
    - Azure functions
    - Logic Apps HTTP calls

## AbuseIPDB

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **AbuseIPDB**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Enrich incident by IP info, Report IP to Abuse IP DB, Deny list to Threat intelligence |
|  |  |  |  |

## Atlassian

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Jira** | [Managed Logic Apps connector](/en-us/connectors/jira/)Playbooks | MicrosoftCommunity | Sync incidents |
|  |  |  |  |

## AWS IAM

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **AWS IAM**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Add User Tags, Delete Access Keys, Enrich incidents |
|  |  |  |  |

## Checkphish by Bolster

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Checkphish by Bolster**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Get URL scan results |
|  |  |  |  |

## Check Point

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Check Point NGFW**(Available as solution) | Custom Logic Apps connectorPlaybooks | CheckPoint |  |
|  |  |  |  |

## Cisco

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Cisco ASA,Cisco Meraki** | Custom Logic Apps connectorPlaybooks | Community | Block IPs |
| **Cisco FirePower** | Custom Logic Apps connectorPlaybooks | Community | Block IPs and URLs |
| **Cisco ISE**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft |  |
| **Cisco Umbrella**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Block domains, policies management, destination lists management, enrichment, and investigation |
|  |  |  |  |

## Crowdstrike

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Falcon endpoint protection**(Available as solution) | Playbooks | Microsoft | Endpoints enrichment,isolate endpoints |
|  |  |  |  |

## Elastic Search

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Elastic search**(Available as solution) | Playbooks | Microsoft | Enrich incident |
|  |  |  |  |

## F5

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Big-IP** | Playbooks | Community | Block IPs and URLs |
|  |  |  |  |

## Forcepoint

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Forcepoint NGFW** | Custom Logic Apps connectorPlaybooks | Community | Block IPs and URLs |
|  |  |  |  |

## Fortinet

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **FortiGate**(Available as solution) | Custom Logic Apps connectorAzure FunctionPlaybooks | Microsoft | Block IPs and URLs |
| **Fortiweb Cloud**(Available as solution) | Custom Logic Apps connectorAzure FunctionPlaybooks | Microsoft | Block IPs and URLs , Incident enrichment |
|  |  |  |  |

## Freshdesk

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Freshdesk** | [Managed Logic Apps connector](/en-us/connectors/freshdesk/) |  | Sync incidents |
|  |  |  |  |

## GCP IAM

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **GCP IAM**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Disable service account, Disable service account key, Enrich Service account info |
|  |  |  |  |

## Have I Been Pwned

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Have I Been Pwned** | Custom Logic Apps connectorPlaybooks | Community |  |
|  |  |  |  |

## HYAS

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **HYAS Insight**(Available as solution) | [Managed Logic Apps connector](/en-us/connectors/hyasinsight/)Playbooks | HYAS |  |
|  |  |  |  |

## IBM

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Resilient** | Custom Logic Apps connectorPlaybooks | Community | Sync incidents |
|  |  |  |  |

## InsightVM Cloud API

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **InsightVM Cloud API** | Custom Logic Apps connectorPlaybooks | Microsoft | Enrich incident with asset info, Enrich vulnerability info, Run VM scan |
|  |  |  |  |

## Microsoft

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Azure DevOps** | Managed Logic Apps connectorPlaybooks | MicrosoftCommunity | Sync incidents |
| **Azure Firewall**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Block IPs |
| **Microsoft Entra ID Protection** | [Managed Logic Apps connector](/en-us/connectors/azureadip/)Playbooks | MicrosoftCommunity | Users enrichment, Users remediation |
| **Microsoft Entra ID** | [Managed Logic Apps connector](/en-us/connectors/azuread/)Playbooks | MicrosoftCommunity | Users enrichment, Users remediation |
| **Azure Data Explorer** | [Managed Logic Apps connector](/en-us/connectors/kusto/) | Microsoft | Query and investigate |
| **Azure Log Analytics Data Collector** | [Managed Logic Apps connector](/en-us/connectors/azureloganalyticsdatacollector/) | MicrosoftCommunity | Query and investigate |
| **Microsoft Defender for Endpoint** | [Managed Logic Apps connector](/en-us/connectors/wdatp/)Playbooks | MicrosoftCommunity | Endpoints enrichment, isolate endpoints |
| **Microsoft Defender for IoT** | Playbooks | Microsoft | Orchestration and notification |
| **Microsoft Teams** | [Managed Logic Apps connector](/en-us/connectors/teams/)Playbooks | MicrosoftCommunity | Notifications, Collaboration, create human-involved responses |
|  |  |  |  |

## Minemeld

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Minemeld**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Create indicator, Enrich incident |
|  |  |  |  |

## Neustar IP GEO Point

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Neustar IP GEO Point**(Available as solution) | Playbooks | Microsoft | Get IP Geo Info |
|  |  |  |  |

## Okta

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Okta** | Managed Logic Apps connectorPlaybooks | Community | Users enrichment, Users remediation |
|  |  |  |  |

## OpenCTI

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **OpenCTI**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Create Indicator, Enrich incident, Get Indicator stream, Import to Sentinel |
|  |  |  |  |

## Palo Alto

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Palo Alto PAN-OS**(Available as solution) | Custom Logic Apps connectorPlaybooks | Community | Block IPs and URLs |
| **Wildfire** | Custom Logic Apps connectorPlaybooks | Community | Filehash enrichment and response |
|  |  |  |  |

## Proofpoint

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Proofpoint TAP**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Accounts enrichment |
|  |  |  |  |

## Qualys VM

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Qualys VM**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Get asset details, Get asset by CVEID, Get asset by Open port, Launch VM scan |
|  |  |  |  |

## Recorded Future

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Recorded Future Intelligence** | [Managed Logic Apps connector](/en-us/connectors/recordedfuture/)Playbooks | Recorded Future | Entities enrichment |
|  |  |  |  |

## ReversingLabs

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **TitaniumCloud File Enrichment**(Available as solution) | [Managed Logic Apps connector](/en-us/connectors/reversinglabstitaniu/)Playbooks | ReversingLabs | FileHash enrichment |
|  |  |  |  |

## RiskIQ

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **RiskIQ Digital Footprint**(Available as solution) | [Managed Logic Apps connector](/en-us/connectors/riskiqdigitalfootprint/)Playbooks | RiskIQ | Entities enrichment |
| **RiskIQ Passive Total** | [Managed Logic Apps connector](/en-us/connectors/riskiqpassivetotal/)Playbooks | RiskIQ | Entities enrichment |
| **RiskIQ Security Intelligence**(Available as solution) | [Managed Logic Apps connector](/en-us/connectors/riskiqintelligence/)Playbooks | RiskIQ | Entities enrichment |
|  |  |  |  |

## ServiceNow

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **ServiceNow** | [Managed Logic Apps connector](/en-us/connectors/service-now/)Playbooks | MicrosoftCommunity | Sync incidents |
|  |  |  |  |

## Slack

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Slack** | [Managed Logic Apps connector](/en-us/connectors/slack/)Playbooks | MicrosoftCommunity | Notification, Collaboration |
|  |  |  |  |

## TheHive

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **TheHive**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Create alert, Create Case, Lock User |
|  |  |  |  |

## ThreatX WAF

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **ThreatX WAF**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Block IP / URL, Incident enrichment |
|  |  |  |  |

## URLhaus

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **URLhaus**(Available as solution) | Custom Logic Apps connectorPlaybooks | Microsoft | Check host and enrich incident, Check hash and enrich incident, Check URL and enrich incident |
|  |  |  |  |

## Virus Total

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Virus Total** | [Managed Logic Apps connector](/en-us/connectors/virustotal/)Playbooks | MicrosoftCommunity | Entities enrichment |
|  |  |  |  |

## VMware

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Carbon Black Cloud**(Available as solution) | Custom Logic Apps connectorPlaybooks | Community | Endpoints enrichment, isolate endpoints |
|  |  |  |  |

## Zendesk

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Zendesk** | [Managed Logic Apps connector](/en-us/connectors/zendesk/)Playbooks | MicrosoftCommunity | Sync incidents |
|  |  |  |  |

## Zscaler

| Product | Integration components | Supported by | Scenarios |
| --- | --- | --- | --- |
| **Zscaler** | Playbooks | Microsoft | URL remediation, incident enrichment |
|  |  |  |  |