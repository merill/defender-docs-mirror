---
layout: Conceptual
title: Prerequisites for Microsoft Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-storage
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
description: Learn about the prerequisites and permissions required to enable Microsoft Defender for Storage and its features of malware scanning and sensitive-data threat detection.
ms.topic: reference
ms.date: 2026-04-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 21c90f7e-103d-2444-4ff2-d7d7fa3bb5e1
document_version_independent_id: 1510f4b4-832a-1355-0b94-dabeced368f8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/support-matrix-defender-for-storage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/support-matrix-defender-for-storage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/support-matrix-defender-for-storage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: cf9af9d3-3d8a-8746-9fec-8dec738e525d
---

# Prerequisites for Microsoft Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn

This article lists the prerequisites and permissions required to [enable Microsoft Defender for Storage](tutorial-enable-storage-plan) and its features.

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- The following storage types are supported:

    | Capability | Azure Blob Standard | Azure Blob Premium v2 | Azure Page Blob | Azure Data Lake Storage Gen 2 | Azure Blob (Standard + Premium) + Network File System (NFS) 3.0 | Azure File Standard (SMB) | Azure File Premium Provisioned v1/v2 (SMB) |
    | --- | --- | --- | --- | --- | --- | --- | --- |
    | Activity Monitoring | Supported | Supported | Supported | Supported | Not supported | Supported | Supported |
    | Sensitive Data Discovery | Supported | Supported | Supported | Supported | Not supported | Supported | Not supported |
    | On-upload Malware Scanning | Supported only for blobs | Supported only for blobs | Not supported | Supported only for blobs | Supported only for blobs | Not supported | Not supported |
    | On-demand Malware Scanning | Supported | Supported | Not supported | Supported | Supported | Not supported | Not supported |
- Storage accounts that belong to a resource group with any of the following names aren't supported: `App_Browsers`, `App_Code`, `App_Data`, `App_GlobalResources`, `App_LocalResources`, `App_Themes`, `App_WebReferences`, `Bin`.

Note

Defender for Storage doesn't directly support Amazon Web Services (AWS) S3 buckets. You can use Microsoft Sentinel with the AWS S3 connector to consume AWS GuardDuty findings and display them within the Defender portal **Alerts** table. For more information, see [Microsoft Sentinel data connectors](/en-us/azure/sentinel/data-connectors-reference#sentinel-data-connectors/azure/sentinel/connect-aws?tabs=s3).

## Permissions

Depending on the scenario, you need different levels of permissions to enable Defender for Storage and its features. You can enable and configure Defender for Storage at the subscription level or at the storage account level. You can also use built-in Azure policies to enable Defender for Storage and enforce its enablement on a desired scope.

The following table summarizes the permissions that you need for each scenario. The permissions are either built-in Azure roles or action sets that you can assign to custom roles.

| Capability | Subscription level | Storage account level |
| --- | --- | --- |
| Activity monitoring | Security Admin or Pricings/read, Pricings/write | Security Admin or Microsoft.Security/defenderforstoragesettings/read, Microsoft.Security/defenderforstoragesettings/write |
| Malware scanning | Subscription Owner or action set 1 | Action set 2 |
| Sensitive-data threat detection | Subscription Owner or action set 1 | Action set 2 |

Note

Activity monitoring is always enabled when you enable Defender for Storage.

The action sets are collections of Azure resource provider operations that you can use to create custom roles. The action sets for enabling Defender for Storage and its features are as follows.

### Action set 1: Enablement and configuration at the subscription level

- Microsoft.Security/pricings/write
- Microsoft.Security/pricings/read
- Microsoft.Security/pricings/SecurityOperators/read
- Microsoft.Security/pricings/SecurityOperators/write
- Microsoft.Authorization/roleAssignments/read
- Microsoft.Authorization/roleAssignments/write
- Microsoft.Authorization/roleAssignments/delete

### Action set 2: Enablement and configuration at the storage account level

- Microsoft.Storage/storageAccounts/write
- Microsoft.Storage/storageAccounts/read
- Microsoft.Security/datascanners/read (must be granted at subscription level)
- Microsoft.Security/datascanners/write (must be granted at subscription level)
- Microsoft.Security/defenderforstoragesettings/read
- Microsoft.Security/defenderforstoragesettings/write
- Microsoft.EventGrid/eventSubscriptions/read
- Microsoft.EventGrid/eventSubscriptions/write
- Microsoft.EventGrid/eventSubscriptions/delete
- Microsoft.Authorization/roleAssignments/read
- Microsoft.Authorization/roleAssignments/write
- Microsoft.Authorization/roleAssignments/delete