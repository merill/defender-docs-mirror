---
layout: Conceptual
title: Connect Microsoft Sentinel to other Microsoft services by using diagnostic settings-based connections | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-services-diagnostic-setting-based
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
description: Learn how to connect Microsoft Sentinel to Microsoft services with diagnostic settings-based connections.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7f727f1e-6299-640b-10fc-57f127f0047f
document_version_independent_id: 7f27b264-d5b7-fcdb-c10e-7f4f78b07659
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-services-diagnostic-setting-based.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-services-diagnostic-setting-based
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-services-diagnostic-setting-based.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: 16eb826c-8045-6ae6-e9fe-1ce8913cab9a
---

# Connect Microsoft Sentinel to other Microsoft services by using diagnostic settings-based connections | Microsoft Learn

This article describes how to connect to Microsoft Sentinel by using diagnostic settings connections. Microsoft Sentinel uses the Azure foundation to provide built-in, service-to-service support for data ingestion from many Azure and Microsoft 365 services, Amazon Web Services, and various Windows Server services. There are a few different methods through which these diagnostic settings-based connections are made.

This article presents information that is common to the Microsoft Sentinel data connectors that use diagnostic settings-based connections. Some diagnostic settings-based connectors are managed by using Azure Policy. For diagnostic settings-based connectors that aren't managed by Azure Policy, use the instructions in Connect via a standalone diagnostic settings-based connector.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

## Prerequisites

To ingest data into Microsoft Sentinel using a standalone, diagnostic settings-based connector, you must have read and write permissions on the Log Analytics workspace enabled for Microsoft Sentinel.

To ingest data into Microsoft Sentinel using diagnostic settings-based connectors managed by Azure Policy, you must also have the following prerequisites:

- To use Azure Policy to apply a log streaming policy to your resources, you must have the Owner role for the policy assignment scope.
- The following prerequisites, depending on which connector you're using:

    | Data connector | Licensing, costs, and other information |
    | --- | --- |
    | **Azure Activity** | This connector now uses the diagnostic settings pipeline. If you're using the legacy method, you must disconnect the existing subscriptions from the legacy method before setting up the new Azure Activity log connector.1. From the Microsoft Sentinel navigation menu, select **Data connectors**. From the list of connectors, select **Azure Activity**, and then select the **Open connector page** button on the lower right.2. Under the **Instructions** tab, in the **Configuration** section, in step 1, review the list of your existing subscriptions that are connected to the legacy method, and disconnect them all at once by clicking the **Disconnect All** button below.3. Continue setting up the new connector with the instructions in Connect via a standalone diagnostic settings-based connector. |
    | **Azure DDoS Protection** | - Configured [Azure DDoS Standard protection plan](/en-us/azure/ddos-protection/manage-ddos-protection#create-a-ddos-protection-plan).- Configured [virtual network with Azure DDoS Standard enabled](/en-us/azure/ddos-protection/manage-ddos-protection#enable-ddos-protection-for-a-virtual-network)- Other charges may apply- The **Status** for Azure DDoS Protection Data Connector changes to **Connected** only when the protected resources are under a DDoS attack. |
    | **Azure Storage Account** | The storage account (parent) resource has within it other (child) resources for each type of storage: files, tables, queues, and blobs. When configuring diagnostics for a storage account, you must select and configure: - The parent account resource, exporting the **Transaction** metric.- Each of the child storage-type resources, exporting all the logs and metrics.You'll only see the storage types that you actually have defined resources for. |

## Connect via a standalone diagnostic settings-based connector

This procedure describes how to connect to Microsoft Sentinel using data connectors that use standalone connections based on diagnostic settings.

1. From the Microsoft Sentinel navigation menu, select **Data connectors**.
2. Select your resource type from the data connectors gallery, and then select **Open Connector Page** on the preview pane.
3. In the **Configuration** section of the connector page, select the link to open the resource configuration page.

    If presented with a list of resources of the desired type, select the link for a resource whose logs you want to ingest.
4. From the resource navigation menu, select **Diagnostic settings**.
5. Select **+ Add diagnostic setting** at the bottom of the list.
6. In the **Diagnostics settings** screen, enter a name in the **Diagnostic settings name** field.

    Mark the **Send to Log Analytics** check box. Two new fields are displayed below the **Send to Log Analytics** check box. Choose the relevant **Subscription** and **Log Analytics Workspace** (where Microsoft Sentinel resides).
7. Mark the check boxes of the types of logs and metrics you want to collect. See our recommended choices for each resource type in the corresponding connector's section of the [Data connectors reference](data-connectors-reference) page.
8. Select **Save** at the top of the screen.

For more information, see also [Create diagnostic settings to send Azure Monitor platform logs and metrics to different destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings) in the Azure Monitor documentation.

## Connect via a diagnostic setting-based connector managed by Azure Policy

This procedure describes how to connect to Microsoft Sentinel using data connectors that use connections that are based on diagnostic settings and are managed by Azure Policy.

Connectors of this type use Azure Policy to apply a single diagnostic settings configuration to a collection of resources of a single type, defined as a scope. You can see the log types ingested from a given resource type on the left side of the connector page for that resource, under **Data types**.

1. From the Microsoft Sentinel navigation menu, select **Data connectors**.
2. Select your resource type from the data connectors gallery, and then select **Open Connector Page** on the preview pane.
3. In the **Configuration** section of the connector page, expand any expanders you see there and select the **Launch Azure Policy Assignment wizard** button.

    The policy assignment wizard opens, ready to create a new policy, with a policy name prepopulated.

    1. In the **Basics** tab, select the button with the three dots under **Scope** to choose your subscription (and, optionally, a resource group). You can also add a description.
    2. In the **Parameters** tab:

        - Clear the **Only show parameters that require input** check box.
        - If you see **Effect** and **Setting name** fields, leave them as is.
        - Choose your Microsoft Sentinel workspace from the **Log Analytics workspace** drop-down list.
        - The remaining drop-down fields represent the available diagnostic log types. Leave marked as *True* all the log types you want to ingest.
    3. The policy will be applied to resources added in the future. To apply the policy on your existing resources as well, select the **Remediation** tab and mark the **Create a remediation task** check box.
    4. In the **Review + create** tab, click **Create**. Your policy is now assigned to the scope you chose.

With this type of data connector, the connectivity status indicators (a color stripe in the data connectors gallery and connection icons next to the data type names) shows as *connected* (green) only if data has been ingested at some point in the past 14 days. Once 14 days have passed with no data ingestion, the connector shows as being disconnected. The moment more data comes through, the *connected* status returns.

You can find and query the data for each resource type using the table name that appears in the corresponding connector's section of the [Data connectors reference](data-connectors-reference) page. For more information, see [Create diagnostic settings to send Azure Monitor platform logs and metrics to different destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings?tabs=CMD) in the Azure Monitor documentation.