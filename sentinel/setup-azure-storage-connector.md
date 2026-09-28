---
layout: Conceptual
title: Set up the Azure Storage connector to stream logs to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/setup-azure-storage-connector
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
description: Learn how to set up the Azure Storage Blob connector to ingest logs from Azure Storage into Microsoft Sentinel using the Codeless Connector Framework.
author: EdB-MSFT
ms.author: edbaynash
ms.date: 2026-07-01T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3b7f993a-1568-350d-8118-f57d510523ef
document_version_independent_id: 4594db94-3620-c637-41e1-0c7825d2a340
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/setup-azure-storage-connector.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/setup-azure-storage-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/setup-azure-storage-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/de8ce683-cbe1-461b-bae7-77db0888ec6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a06cf482-4ca9-4582-a142-bcf842258d42
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d91334b3-fd77-f867-182d-908c17185049
---

# Set up the Azure Storage connector to stream logs to Microsoft Sentinel | Microsoft Learn

The Azure Storage Blob connector simplifies collecting logs from Azure Storage. It lets ISVs and users build scalable connectors on top of Azure Storage integrations through the fully managed Codeless Connector Framework (CCF).

This article summarizes the connector resources and provides steps to create and validate your first Azure Storage connector.

## Prerequisites

Before you begin, ensure you have:

- An Azure Storage account with hierarchical namespace enabled (Azure Data Lake Storage Gen2) and a container that holds the log files.
- A Microsoft Sentinel workspace with a Microsoft Sentinel Contributor or higher role to create data connectors.
- Owner or EventGrid Contributor role permissions on the storage account to create Event Grid system topics and subscriptions.

Note

Make sure the **Microsoft.EventGrid** resource provider is registered in the subscription that contains the storage account.

## Connector resource overview

The Azure Storage Blob connector uses a queue-based blob-pointer model to subscribe to blob-created events in your storage account. An Event Grid system topic subscription listens for blob creation activity and pushes events, based on configurable filtering criteria, to an Azure Storage queue. Multiple connector instances can ingest from the same container while scoping files by folder and file pattern. You can control filtering through the portal or the connector Azure Resource Manager (ARM) template by setting blob prefix and suffix patterns.

[![A diagram showing the Azure Storage Blob connector architecture, including blob created events, Event Grid, storage queue, and Microsoft Sentinel ingestion flow.](media/setup-azure-storage-connector/overview-diagram.png)](media/setup-azure-storage-connector/overview-diagram.png#lightbox)

The Microsoft Sentinel connector:

- Polls the Azure Storage queue for blob-created messages.
- Fetches files from the Azure Storage Blob container based on the path in the queue message.
- Deletes the queue message after successful forwarding.

The connector authenticates to the Storage Account by using a service principal accessible to the connector application. For the application IDs per cloud and the full template schema, see the [Azure Storage Blob connectors API reference](data-connection-rules-reference-azure-storage). Use the ARM template automation to verify that the connector service principal exists and to apply the required role assignments on the storage account.

## Create an Azure Storage Blob connector

Perform the following steps to create an Azure Storage Blob connector:

1. Review and adapt the example ARM template in the [Azure Storage Blob connectors API reference](data-connection-rules-reference-azure-storage#build-the-azure-storage-blob-ccf-data-connector). Set the container name, queue name (if not auto-created), blob prefix/suffix filters, and destination table mapping.
2. Deploy the template by following [Create a codeless connector for Microsoft Sentinel](isv/create-codeless-connector#data-connection-rules). Ensure the deployment scope matches the storage account and Microsoft Sentinel workspace.
3. After deployment, confirm the connector instance is created in Microsoft Sentinel and that the Event Grid subscription status is **Healthy**.

## Validate the connector

Use the following checks to validate that the connector is working correctly:

- Upload a sample file that matches your prefix/suffix filter and confirm that queue messages are created and consumed.
- Verify ingestion in the target table in Microsoft Sentinel and check for errors in the connector health blade.
- If you use network restrictions, confirm that the connector-managed resources can reach the blob and queue endpoints.

## Troubleshooting

For troubleshooting steps, see [Troubleshoot Azure Storage Blob connector issues](azure-storage-blob-connector-troubleshoot).