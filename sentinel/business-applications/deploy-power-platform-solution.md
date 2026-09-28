---
layout: Conceptual
title: Connect Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/business-applications/deploy-power-platform-solution
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
description: Deploy the Microsoft Sentinel solution for Microsoft Business Apps to collect audit and activity logs from Power Platform and Dynamics 365 Customer Engagement for threat detection.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 716fabe4-3b4f-4a5a-4628-a01a51f0f825
document_version_independent_id: df84ffc9-66cc-eb0a-5909-ecce45593ed4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/business-applications/deploy-power-platform-solution.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/business-applications/deploy-power-platform-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/business-applications/deploy-power-platform-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e6f942e8-55a7-4c86-b8e3-7456508ea850
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0ceb3227-2ff7-4d97-8e75-3d7b9ccc937a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/f1834696-48d6-470d-966b-6ee418881596
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/4d680e1a-c470-4772-a236-5c714bd09be0
platformId: a1435dc3-9d5f-d96c-8a73-ea9731f02868
---

# Connect Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement to Microsoft Sentinel | Microsoft Learn

This article describes how to deploy the [Microsoft Sentinel solution for Microsoft Business Apps](solution-overview) to connect your Microsoft Power Platform and Microsoft Dynamics 365 Customer Engagement system to Microsoft Sentinel. The solution collects audit and activity logs to detect threats, suspicious activities, illegitimate activities, and more. Before you begin, make sure you meet the prerequisites for this solution.

## Prerequisites

Before deploying the Microsoft Sentinel solution for Microsoft Business Apps, ensure that you meet the following prerequisites:

- Your Log Analytics workspace must be enabled for Microsoft Sentinel
- You must have read and write access to the workspace. You must be able to create:

    - [Data Collection Rules/Endpoints](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview), with the `Microsoft.Insights/DataCollectionEndpoints`, and `Microsoft.Insights/DataCollectionRules`
- Your organization must use Dynamics 365 Customer Engagement and/or one or more of the Power Platform workloads.
- Audit logging must also be enabled in [Microsoft Purview](/en-us/purview/purview). For more information, see [Turn auditing on or off for Microsoft Purview](/en-us/microsoft-365/compliance/audit-log-enable-disable)
- If you're working with Microsoft Dataverse, audit logging is supported only for production environments. For more information, see [Microsoft Dataverse and model-driven apps activity logging requirements](/en-us/power-platform/admin/enable-use-comprehensive-auditing#requirements).

## Install the solution and deploy your data connectors

Complete the following steps to install the solution and set up data connectors in Microsoft Sentinel.

1. Install the Microsoft Sentinel solution for Microsoft Business Applications from the Microsoft Sentinel **Content hub**.

    For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy).
2. Select **Configuration &gt; Data connectors**, and locate any of the following data connectors you want to deploy:

    - Microsoft Dataverse
    - Microsoft Power Platform Admin Activity
    - Microsoft Power Automate

    Note

    The Dynamics 365 Finance and Operations connector is also included as part of the solution. For more information, see [Deploy for Dynamics 365 Finance and Operations](../dynamics-365/deploy-dynamics-365-finance-operations-solution).
3. For each data connector, on the side pane, select **Open connector page &gt; Connect**.

## Configure data collection for Dataverse

When working with Microsoft Dataverse, Dataverse activity logging is available only for production environments, and isn't enabled by default. Enable auditing at both the [global level for Dataverse](/en-us/power-platform/admin/manage-dataverse-auditing#startstop-auditing-for-an-environment-and-set-retention-policy), and for each Dataverse entity:

- To enable auditing on default entities, import one of the following Power Platform managed solutions:

    - For use with Dynamics 365 CE Apps, import the [Audit Settings solution for Dynamics 365 CE Apps](https://aka.ms/AuditSettings/Dynamics).
    - Otherwise, import the [Audit Settings solution for Dataverse only](https://aka.ms/AuditSettings/DataverseOnly).

    The solution enables detailed auditing for each of the default entities listed in [Audit Settings for Dataverse](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/Microsoft%20Business%20Applications/Audit%20Settings/README.md).
- To enable auditing on custom entities, you must manually enable detailed auditing on each of the custom entities. For more information, see [Manage Dataverse auditing](/en-us/power-platform/admin/manage-dataverse-auditing#turn-on-or-off-auditing-for-specific-fields-on-an-entity).

    To get the full incident detection value of the solution, we recommend that you enable, for each Dataverse entity you want to audit, the following options in the **General** tab of the Dataverse entity settings page:

    - Under the **Data Services** section, select **Auditing**.
    - Under the **Auditing** section, select **Single record auditing** and **Multiple record auditing**.

    Make sure to save and publish your customizations.

## Verify log ingestion to Microsoft Sentinel

Use the following steps to confirm that logs are being ingested into Microsoft Sentinel.

1. After deploying your data connectors and configuring data collection, run activities like create, update, and delete to generate logs for data that you enabled for monitoring.
2. For Power Platform activity logs, wait 60 minutes for Microsoft Sentinel to ingest the data.
3. To verify that Microsoft Sentinel is getting the data you expect, run KQL queries against the data tables that collect logs from your data connectors.

    For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), run KQL queries on the **General** &gt; **Logs** page. In the [Defender portal](https://security.microsoft.com/), run KQL queries in the **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.

    For example, to verify your Power Platform log ingestion, run the following query to return 50 rows from the table with the Power Apps activity logs.

    ```kusto
    PowerPlatformAdminActivity
    | take 50
    ```

The following table lists the Log Analytics tables to query.

| Log Analytics tables | Data collected |
| --- | --- |
| PowerPlatformAdminActivity | Power Platform administrative logs |
| PowerAutomateActivity | Power Automate activity logs |
| DataverseActivity | Dataverse and model-driven apps activity logging |