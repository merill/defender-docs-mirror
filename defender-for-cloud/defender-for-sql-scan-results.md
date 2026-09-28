---
layout: Conceptual
title: How to consume and export scan results - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-scan-results
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
description: Access vulnerability assessment findings in Azure Resource Graph and use multiple methods to query, view, and export scan results for reporting and remediation.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 3aa948a2-2fe7-b84a-8e30-2ac5cdd06d2b
document_version_independent_id: b4d43865-8abe-4c6a-a202-9c54a7225d63
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-scan-results.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-scan-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-scan-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3928677-9b71-43a6-875f-004dc4f98b65
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6bbc70ca-58b2-4c69-8249-28ec92c08029
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 5b9deb08-4fa6-a1d8-dcfa-2457afdebeb6
---

# How to consume and export scan results - Microsoft Defender for Cloud | Microsoft Learn

Use this article to query vulnerability assessment findings and export SQL scan results for investigation, reporting, and remediation workflows.

## Query and export vulnerability assessment scan results

Defender for SQL's vulnerability assessment (VA) scans your databases every week and reports identified misconfigurations.

All findings are stored in Azure Resource Graph (ARG), which is the source for most of the Defender for SQL user interface experience. When findings are written to ARG, Defender for Cloud enriches them with related settings, such as disabled rules or exempt recommendations. As a result, ARG reflects the effective status of findings and recommendations.

This article describes several ways to consume and export your scan results.

## Query and export findings in ARG with Defender for Cloud

Use the Defender for Cloud Recommendations page to query findings in Azure Resource Graph (ARG) and export results for reporting.

**To query and export your findings with ARG with Defender for Cloud**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Set the **Scanner** filter to **SQL Vulnerability Assessment**.
4. Select **Open Query**.
5. Select **Run query**.
6. Select **Download as CSV**.

The query changes based on the recommendations view you've selected.

[![Screenshot of the recommendation view options with By Title selected.](media/defender-for-sql-scan-results/select-recommendations-view.png)](media/defender-for-sql-scan-results/select-recommendations-view.png#lightbox)

These queries are editable. You can customize them for a specific resource, a set of findings, or a finding status.

## Query findings directly in Resource Graph Explorer

Use Resource Graph Explorer to query findings directly when you need advanced query customization.

**To query and export your findings with ARG**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Resource Graph Explorer**.
3. Edit and enter the following query. Replace the placeholders in the `resourceId` filter with the resource ID of your SQL database:

    ```kusto
    securityresources
    | where type =~ "microsoft.security/assessments"
    | extend assessmentKey=extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id), parentResourceId= extract("(.+)/providers/Microsoft.Security", 1, id)
    | extend resourceIdTemp = iff(properties.resourceDetails.id != "", properties.resourceDetails.id, extract("(.+)/providers/Microsoft.Security", 1, id))
    | extend scanner = (// AssessmentsQueryBuilder.columnDefinitions.scanner
    (tostring(
    coalesce(bag_keys(parse_json(tostring(properties.additionalData.ScannersDetails)))[0], bag_keys(parse_json(tostring(properties.additionalData.ScannersDetails)))[0],
    properties.additionalData.scanner, properties.additionalData.scanner, 
    properties.additionalData.Scanner, properties.additionalData.Scanner, 
    properties.additionalData.SecretScannerName, properties.additionalData.SecretScannerName,
    properties.additionalData.ToolName, properties.additionalData.ToolName,
    properties.additionalData.ScannerName, properties.additionalData.ScannerName,
    todynamic("N/A")))))
    | where scanner in~ ("SQL Vulnerability Assessment")
    | extend resourceId = iff(properties.resourceDetails.source =~ "OnPremiseSql", strcat(resourceIdTemp, "/servers/", properties.resourceDetails.serverName, "/databases/" , properties.resourceDetails.databaseName), resourceIdTemp)
    | where resourceId =~ "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Sql/servers/<server-name>/databases/<database-name>"
    | project resourceId,
    subscriptionId,
    assessmentKey,
    RuleId=properties.additionalData.ruleId,
    name=properties.displayName,
    description=properties.metadata.description,
    severity=properties.additionalData.severity,
    status=properties.status.code,
    cause=properties.status.cause,
    category=properties.additionalData.category,
    impact=properties.additionalData.impact,
    remediation=properties.metadata.remediationDescription,
    benchmarks=properties.additionalData.benchmarks,
    scanner,
    HasBaseline=properties.additionalData.hasBaseline
    ```
4. Select **Run query**.
5. Select **Download as CSV**.

    [![Screenshot of Resource Graph Explorer page with Run query and Download as CSV controls highlighted.](media/defender-for-sql-scan-results/run-and-download.png)](media/defender-for-sql-scan-results/run-and-download.png#lightbox)

The Resource Graph Explorer query is editable. You can customize it for a specific resource, a set of findings, or a finding status.

## Open a query from your SQL database

Use the SQL database resource page to query vulnerability findings for a specific SQL database.

**To open a query from your SQL database**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to the relevant SQL database.
3. Go to **Security** &gt; **Microsoft Defender for Cloud**.
4. Select the relevant recommendation finding.
5. Select **Open Query**.

    [![Screenshot of SQL database recommendation page with the Open query button selected.](media/defender-for-sql-scan-results/open-query.png)](media/defender-for-sql-scan-results/open-query.png#lightbox)
6. Select **Run query**.
7. Select **Download as CSV**.

    [![Screenshot of Resource Graph Explorer page with Run query and Download as CSV controls highlighted.](media/defender-for-sql-scan-results/run-and-download.png)](media/defender-for-sql-scan-results/run-and-download.png#lightbox)

The query opened from the SQL database resource page is editable. You can customize it for a specific resource, a set of findings, or a finding status.

## Automate email notifications with Logic Apps

Azure Logic Apps is a low-code and no-code cloud service that automates workflows and integrates data and services across cloud and on-premises systems. You can use Logic Apps to automate reports for vulnerability assessment findings across supported SQL versions and send weekly report summaries for scanned servers. You can also customize schedules, such as daily, weekly, or monthly, and report scopes, such as database, server, or resource group.

To automate notifications by using the sample template, follow the [Logic Apps email notification template for SQL vulnerability reports](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Workflow%20automation/Notify-SQLVulnerabilityReport).

This example Logic App template automates a weekly email report that summarizes the vulnerability scan results for every database from a selected list of servers. After you deploy the template, you must authorize the Microsoft 365 connector to generate a valid access token to authenticate your credentials.

The recipients receive emails with the findings of the scan results.

Sample email Azure SQL server:

[![Screenshot of a sample email vulnerability assessment report from a server.](media/defender-for-sql-scan-results/sample-va-email.png)](media/defender-for-sql-scan-results/sample-va-email.png#lightbox)

Sample email SQL VM:

[![Screenshot of a sample SQL virtual machine results email.](media/defender-for-sql-scan-results/sample-email-sql-vm.png)](media/defender-for-sql-scan-results/sample-email-sql-vm.png#lightbox)

## Other methods for exporting scan results

You can use [workflow automations](workflow-automations) to trigger actions based on changes to the recommendation's status.

You can also use the [Vulnerability Assessments workbook](defender-for-sql-on-machines-vulnerability-assessment#view-vulnerabilities-in-graphical-interactive-reports) to view an interactive report of your findings. The data from the workbook can be exported, and a copy of the workbook can be customized and stored. Learn how to [create rich, interactive reports of Defender for Cloud data](custom-dashboards-azure-workbooks).

You can also enable [Continuous export](continuous-export) to stream alerts and recommendations as they're generated or to define a schedule to send periodic snapshots of all of the new data.