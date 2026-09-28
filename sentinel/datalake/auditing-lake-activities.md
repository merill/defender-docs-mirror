---
layout: Conceptual
title: Audit Log for Microsoft Sentinel Data Lake and Graph in Microsoft Purview Portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/auditing-lake-activities
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
description: Use the audit log to search for Microsoft Sentinel data lake and graph activities to help with investigation.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: amyhari
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ea1a59df-8fe9-9062-1134-08d122257848
document_version_independent_id: a258195b-8ab5-acda-36f4-bc4c5190cbf1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/auditing-lake-activities.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/auditing-lake-activities
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/auditing-lake-activities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 775121b1-299a-937b-fa28-762d75810093
---

# Audit Log for Microsoft Sentinel Data Lake and Graph in Microsoft Purview Portal | Microsoft Learn

This article explains how to access, search, and interpret audit logs for Microsoft Sentinel data lake and graph activities in the Microsoft Purview portal.

The audit log helps you investigate specific activities across Microsoft services. Microsoft Sentinel data lake and graph activities are audited and can be searched in the audit log. The audit log provides a record of activities that are performed by users and administrators in Microsoft Sentinel data lake and graph, such as:

- Accessing data in lake via KQL queries
- Running notebooks on data lake
- Create/ edit/ run/ delete jobs
- Run graph query
- Create and run MCP tools

Auditing is automatically turned on for Microsoft Sentinel data lake and graph. All Microsoft Sentinel data lake and graph activities are logged in the audit log automatically.

## Prerequisites

Microsoft Sentinel data lake and graph uses the [Microsoft Purview auditing solution](/en-us/purview/audit-solutions-overview). Before you can look at the audit data, you need to turn on auditing in the Microsoft Purview portal. For more information, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).

To access the audit log, you need to have the **View-Only Audit Logs** or **Audit Logs** role in Exchange Online. By default, those roles are assigned to the Compliance Management and Organization Management role groups.

Note

Global administrators in Office 365 and Microsoft 365 are automatically added as members of the Organization Management role group in Exchange Online.

Important

Global Administrator is a highly privileged role that should be limited to scenarios when you can't use an existing role. Microsoft recommends that you use roles with the fewest permissions. Using accounts with lower permissions helps improve security for your organization.

## Microsoft Sentinel data lake and graph activities

The following linked articles list the audited events for Microsoft Sentinel data lake and graph activities:

- [Microsoft Sentinel data lake onboarding activities](/en-us/purview/audit-log-activities#microsoft-sentinel-data-lake-onboarding-activities)
- [Microsoft Sentinel data lake notebook activities](/en-us/purview/audit-log-activities#microsoft-sentinel-data-lake-notebook-activities)
- [Microsoft Sentinel data lake job activities](/en-us/purview/audit-log-activities#microsoft-sentinel-data-lake-job-activities)
- [Microsoft Sentinel data lake KQL activities](/en-us/purview/audit-log-activities#microsoft-sentinel-data-lake-kql-activities)
- [Microsoft Sentinel AI tool activities](https://aka.ms/sentinel-ai-tool-activities)
- [Microsoft Sentinel graph activities](https://aka.ms/sentinel-graph-activities)

For detailed audit log schema information, see [Microsoft Sentinel data lake and graph schema](https://aka.ms/sentinel-lake-audit-schema).

## Search the audit log

Follow these steps to search the audit log:

1. Navigate to the [Microsoft Purview portal](https://purview.microsoft.com) and select **Audit**.
2. On the **New Search** page, filter the activities, dates, and users you want to audit.
3. Select **Search**

    [![Screenshot of the unified audit log page.](media/auditing-lake-activities/unified-audit-log.png)](media/auditing-lake-activities/unified-audit-log.png#lightbox)
4. Export your results to Excel for further analysis.

For step-by-step instructions, see [Search the audit sign in the Microsoft Purview portal](/en-us/purview/audit-new-search).

Audit log record retention is based on Microsoft Purview retention policies. For more information, see [Manage audit log retention policies](/en-us/purview/audit-log-retention-policies).

## Search for events using a PowerShell script

Before you run this script, make sure you have the **View-Only Audit Logs** or **Audit Logs** role in Exchange Online and that you can connect to Exchange Online via remote PowerShell.

You can use the following PowerShell code snippet to query the Office 365 Management API to retrieve information about Microsoft Sentinel data lake and graph audit events. This script opens a remote Exchange Online session, imports the session cmdlets, and then runs `Search-UnifiedAuditLog` to search for audit log entries within a specified date range and record type.

```PowerShell
$cred = Get-Credential
$s = New-PSSession -ConfigurationName microsoft.exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $cred -Authentication Basic -AllowRedirection 
Import-PSSession $s
Search-UnifiedAuditLog -StartDate 2023/03/12 -EndDate 2023/03/20 -RecordType <ID>
```

Note

See the API column in [Audit activities](/en-us/purview/audit-log-activities) for the record type values.

For instructions on using PowerShell to search the audit log, see [Use a PowerShell script to search the audit log](/en-us/purview/audit-log-search-script)