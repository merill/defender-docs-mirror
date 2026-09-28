---
layout: Conceptual
title: Log and table reference for the Microsoft Sentinel solution for SAP applications | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-solution-log-reference
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
description: Learn about the SAP logs, tables, and functions available from the Microsoft Sentinel solution for SAP applications.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.custom: mvc
ms.date: 2026-08-04T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 153f9a52-f1b4-d3b4-600a-564ea273aef4
document_version_independent_id: 3d927686-8487-dbe0-750b-6b8d02d4fed0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-solution-log-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-solution-log-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-solution-log-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: ef532e6f-686f-f410-4282-0b7fc15b958d
---

# Log and table reference for the Microsoft Sentinel solution for SAP applications | Microsoft Learn

This article describes the logs and tables available as part of the Microsoft Sentinel solution for SAP applications and its data connector.

Content in this article is intended for your **SAP BASIS** teams.

## Use functions in your queries instead of underlying logs or tables

We *strongly recommend* that you use available functions as the subjects of their analysis whenever possible, instead of the underlying logs or tables.

[Functions](/en-us/azure/azure-monitor/logs/functions) provided with the Microsoft Sentinel solution for SAP applications are intended to serve as the principal user interface to the data. They form the basis for all the built-in analytics rules and workbooks available to you out of the box. Using functions allows for changes to be made to the data infrastructure beneath the functions, without breaking user-created content.

For more information, see [Microsoft Sentinel solution for SAP applications - functions reference](sap-solution-function-reference) and [Functions in Azure Monitor log queries](/en-us/azure/azure-monitor/logs/functions).

## Log coverage

The Microsoft Sentinel solution for SAP applications collects logs from the application, OS, and data layers, providing comprehensive protection for your SAP system:

- **Application layer**: Microsoft Sentinel monitors activities within the ABAP layer, which is the primary application layer in SAP systems, responsible for executing business logic and processing transactions. For example, Microsoft Sentinel collects logs that include user actions like sign-ins, password changes, and access to reports or files.

    In addition to security monitoring, logs collected at the application layer can also be used for compliance and auditing purposes.
- **OS layer**: Microsoft Sentinel gathers logs from the operating system to provide insights into OS-level activities, such as from the ABAP server and the virtual machines on which the SAP applications are running.

    Use the Microsoft Sentinel solution for SAP applications together with security content and data connectors for your other services for comprehensive and central monitoring, correlating information across all your systems and enhancing your overall security posture.
- **Database layer**: Ingest database logs into Microsoft Sentinel to monitor database activities, such as database administration activities and changes to table data. The Microsoft Sentinel solution for SAP applications is database-agnostic.

## Logs collected by the agentless data connector

The following built-in Log Analytics tables are collected by the agentless data connector:

- [ABAPAuditLog](/en-us/azure/azure-monitor/reference/tables/abapauditlog)
- [ABAPAuthorizationDetails](/en-us/azure/azure-monitor/reference/tables/abapauthorizationdetails)
- [ABAPChangeDocsLog](/en-us/azure/azure-monitor/reference/tables/abapchangedocslog)
- [ABAPUserDetails](/en-us/azure/azure-monitor/reference/tables/abapuserdetails)