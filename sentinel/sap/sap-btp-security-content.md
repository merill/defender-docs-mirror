---
layout: Conceptual
title: Microsoft Sentinel Solution for SAP BTP - security content reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-btp-security-content
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
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: mapankra
description: Learn about the built-in security content provided by the  Microsoft Sentinel Solution for SAP BTP.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.date: 2024-07-17T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 850d5195-1370-4d33-214e-e4b3b30f3be8
document_version_independent_id: 9c85e476-f1d7-009f-c358-2dc1a8e06a9a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-btp-security-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-btp-security-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-btp-security-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 5f1d8e74-3419-69c6-3a1b-bf3324d46308
---

# Microsoft Sentinel Solution for SAP BTP - security content reference | Microsoft Learn

This article details the security content available for the Microsoft Sentinel Solution for SAP BTP.

Available security content currently includes a built-in workbook and analytics rules. You can also add SAP-related [watchlists](../watchlists) to use in your search, detection rules, threat hunting, and response playbooks.

[Learn more about the solution](sap-btp-solution-overview).

## SAP BTP workbook

The BTP Activity Workbook provides a dashboard overview of BTP activity.

[![Screenshot of the Overview tab of the SAP BTP workbook.](media/sap-btp-security-content/sap-btp-workbook-btp-overview.png)](media/sap-btp-security-content/sap-btp-workbook-btp-overview.png#lightbox)

The **Overview** tab shows:

- An overview of BTP subaccounts, helping analysts identify the most active accounts and the type of ingested data.
- Subaccount sign-in activity, helping analysts identify spikes and trends that might be associated with sign-in failures in SAP Business Application Studio (BAS).
- Timeline of BTP activity and number of BTP security alerts, helping analysts search for any correlation between the two.

The **Identity Management** tab shows a grid of identity management events, such as user and security role changes, in a human-readable format. The search bar lets you quickly find specific changes.

[![Screenshot of the Identity Management tab of the SAP BTP workbook.](media/sap-btp-security-content/sap-btp-workbook-identity-management.png)](media/sap-btp-security-content/sap-btp-workbook-identity-management.png#lightbox)

For more information, see [Tutorial: Visualize and monitor your data](../monitor-your-data) and [Deploy Microsoft Sentinel Solution for SAP BTP](deploy-sap-btp-solution).

## Built-in analytics rules

These analytics rules detect suspicious activity using SAP BTP audit logs. The rules are organized by SAP service or product area. For more information see SAP's official documentation about [Security Events Logged by Cloud Foundry Services](https://help.sap.com/docs/btp/sap-business-technology-platform/security-events-logged-by-cf-services?version=Cloud) on SAP BTP.

**Data sources**: SAPBTPAuditLog\_CL

### SAP Cloud Integration - Integration Suite

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **BTP - Cloud Integration access policy tampering** | Detects unauthorized modification of access policies that could allow attackers to gain access to sensitive integration artifacts or evade security controls. | Create, change, or delete access policies or artifact references in SAP Cloud Integration. | Defense Evasion, Privilege Escalation |
| **BTP - Cloud Integration artifact deployment** | Detects deployment of potentially malicious integration flows that could be used for data exfiltration, persistence, or executing unauthorized code in the integration environment. | Deploy or undeploy integration artifacts in SAP Cloud Integration. | Execution, Persistence |
| **BTP - Cloud Integration JDBC data source changes** | Detects manipulation of database connections that could enable unauthorized access to backend systems or credential theft from stored connection strings. | Deploy or undeploy JDBC data sources in SAP Cloud Integration. | Credential Access, Lateral Movement |
| **BTP - Cloud Integration package import or transport** | Detects potentially malicious package imports that could introduce backdoors, supply chain compromises, or unauthorized code into the integration environment. | Import or transport integration packages/artifacts in SAP Cloud Integration. | Initial Access, Persistence |
| **BTP - Cloud Integration tampering with security material** | Detects unauthorized access to credentials, certificates, and encryption keys that could enable attackers to compromise external systems or intercept encrypted communications. | Create, update, or delete credentials, X.509 certificates, or PGP keys in SAP Cloud Integration. | Credential Access, Defense Evasion |

### SAP Cloud Identity Service - Identity Authentication

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **BTP - Cloud Identity Service application configuration monitor** | Detects creation or modification of federated applications (SAML/OIDC) that could allow attackers to establish persistent backdoor access through rogue SSO configurations. | Create, update, or delete SSO domain/service provider configurations in SAP Cloud Identity Service. | Credential Access, Privilege Escalation |
| **BTP - Mass user deletion in Cloud Identity Service** | Detects large-scale user account deletion that could indicate a destructive attack, attempted cover-up of unauthorized activity, or denial of service against legitimate users.Default threshold: 10 | Delete count of user accounts over the defined threshold in SAP Cloud Identity Service. | Impact |
| **BTP - User added to privileged Administrators list** | Detects privilege escalation through assignment of powerful identity management permissions that could enable attackers to create backdoor accounts or modify authentication controls. | Grant privileged administrator permissions to a user in SAP Cloud Identity Service. | Lateral Movement, Privilege Escalation |

### SAP Business Application Studio (BAS)

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **BTP - Failed access attempts across multiple BAS subaccounts** | Detects reconnaissance activity or credential spray attacks targeting development environments across multiple subaccounts, indicating potential preparation for a broader compromise.Default threshold: 3 | Run failed sign-in attempts to BAS over the defined threshold number of subaccounts. | Discovery, Reconnaissance |
| **BTP - Malware detected in BAS dev space** | Detects malicious code in development workspaces that could be used to compromise the software supply chain, inject backdoors into applications, or establish persistence in the development environment. | Copy or create a malware file in a BAS developer space. | Execution, Persistence, Resource Development |

### SAP Build Work Zone

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **BTP - Build Work Zone unauthorized access and role tampering** | Detects attempts to access restricted portal resources or mass deletion of access controls that could indicate an attacker removing security boundaries or covering tracks after unauthorized activity. | Detect unauthorized OData service access or mass deletion of roles/users in SAP Build Work Zone. | Initial Access, Persistence, Defense Evasion |

### SAP BTP platform and subaccounts

| Rule name | Description | Source action | Tactics |
| --- | --- | --- | --- |
| **BTP - Audit log service unavailable** | Detects potential tampering with audit logging that could indicate an attacker attempting to operate without detection by disabling security monitoring or hiding malicious activity. | Subaccount fails to report audit logs exceeding configured threshold (default: 60 minutes). | Defense Evasion |
| **BTP - Mass user deletion in a subaccount** | Detects large-scale user deletion that could indicate a destructive attack, sabotage attempt, or effort to disrupt business operations by removing user access.Default threshold: 10 | Delete count of user accounts over the defined threshold. | Impact |
| **BTP - Trust and authorization Identity Provider monitor** | Detects modifications to federation and authentication settings that could enable attackers to establish alternate authentication paths, bypass security controls, or gain unauthorized access through identity provider manipulation. | Change, read, update, or delete any of the identity provider settings within a subaccount. | Credential Access, Privilege Escalation |
| **BTP - User added to sensitive privileged role collection** | Detects privilege escalation attempts through assignment of powerful administrative roles that could enable full control over subaccounts, connectivity, and security configurations. | Assign one of the following role collections to a user: - `Subaccount Service Administrator`- `Subaccount Administrator`- `Connectivity and Destination Administrator`- `Destination Administrator`- `Cloud Connector Administrator` | Lateral Movement, Privilege Escalation |