---
layout: Conceptual
title: Enable Defender for Storage by Using the REST API - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-rest-api-enablement
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
description: Learn how to enable Microsoft Defender for Storage on your Azure subscription for Microsoft Defender for Cloud by using the REST API.
ms.topic: install-set-up-deploy
ms.date: 2025-06-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3d9d10a9-f646-4de9-f97d-19ea9e91180a
document_version_independent_id: 83be2945-a57b-f3b9-08ff-a6d461ed88ba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-rest-api-enablement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-rest-api-enablement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-rest-api-enablement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 886a196f-7868-59d8-edb5-638a2c14be85
---

# Enable Defender for Storage by Using the REST API - Microsoft Defender for Cloud | Microsoft Learn

We recommend that you enable Microsoft Defender for Storage on the subscription level. Doing so helps ensure that all storage accounts currently in the subscription are protected. Protection for storage accounts that you create after enabling Defender for Storage on the subscription level starts up to 24 hours after creation.

Tip

You can always [configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings) with custom settings that differ from the settings configured at the subscription level. That is, you can override subscription-level settings.

# [Enable on a subscription](#tab/enable-subscription)
To enable and configure Defender for Storage at the subscription level by using the REST API, create a `PUT` request with the following endpoint. Replace the `subscriptionId` value in the endpoint URL with your own Azure subscription ID.

```rest
PUT
https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings/StorageAccounts?api-version=2024-01-01

```

Add the following request body:

```json
{
    "properties": {
        "extensions": [
            {
                "name": "OnUploadMalwareScanning",
                "isEnabled": "True",
                "additionalExtensionProperties": {
                    "CapGBPerMonthPerStorageAccount": "10000",
          "BlobScanResultsOptions": "BlobIndexTags"/"None"
          "AutomatedResponse": "BlobSoftDelete"/"None"
                }
            },
            {
                "name": "SensitiveDataDiscovery",
                "isEnabled": "True"
            }
        ],
        "subPlan": "DefenderForStorageV2",
        "pricingTier": "Standard"
    }
}
```

By customizing this code, you can:

- **Modify the monthly threshold for malware scanning**: Adjust the `CapGBPerMonthPerStorageAccount` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default limit is 10,000 GB.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` under `SensitiveDataDiscovery`.
- **Turn off the use of blob index tags**: Change the `BlobScanResultsOptions` value to `None`. If you don't set this value, all scan results are published to blob index tags.
- **Disable the entire Defender for Storage plan**: Set the `pricingTier` property value to `Free`, and remove the `subPlan` and `extensions` properties.

[Learn more about updating Defender plans with the REST API in HTTP, Java, Go, and JavaScript](/en-us/rest/api/defenderforcloud-composite/pricings/update?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true).

# [Enable on a storage account](#tab/enable-storage-account)
To enable and configure Defender for Storage at the storage account level by using the REST API, create a `PUT` request with the following endpoint. Replace the `subscriptionId`, `resourceGroupName`, and `accountName` values in the endpoint URL with your own Azure subscription ID, resource group, and storage account name.

```rest
PUT
https://management.azure.com/{resourceId}/providers/Microsoft.Security/defenderForStorageSettings/current?api-version=2025-07-01-preview

```

Add the following request body:

```json
{
   "properties": {
        "isEnabled": true,
        "malwareScanning": {
            "onUpload": {
                "isEnabled": true,
                "capGBPerMonth": 10000,
                "filters": {
                    "excludeBlobsWithPrefix": [
                        "<excluded-container>/",
                        "<container>/<excluded-blob-prefix>"
                        "<excluded-containers-prefix>"
                    ],
                    "excludeBlobsWithSuffix": [
                        ".parquet",
                        ".tmp",
                        "<excluded-blob-name-suffix>.json"
                    ],
                    "excludeBlobsLargerThan": 2147483648
        }
            },
            
      "automatedResponse": "BlobSoftDelete",
      "scanResultsEventGridTopicResourceId": "/subscriptions/<Subscription>/resourceGroups/<resourceGroup>/providers/Microsoft.EventGrid/topics/<topicName>"
        },
        "sensitiveDataDiscovery": {
            "isEnabled": true
        },
        "overrideSubscriptionLevelSettings": true
    },
    "scope": "[resourceId('Microsoft.Storage/storageAccounts', parameters('StorageAccountName'))]"
}
```

By customizing this code, you can:

- **Modify the monthly threshold for malware scanning**: Adjust the `capGBPerMonth` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default limit is 10,000 GB.
- **Have more granular control over on-upload malware scanning and exclude specific containers, blob types, or sizes**: Use the `filters` property. [Learn more about on-upload malware scanning filters](on-upload-malware-scanning).
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` in the section for the `malwareScanning` or `sensitiveDataDiscovery` property.
- **Turn off the use of blob index tags**: Change the `BlobScanResultsOptions` value to `None`. If you don't set this value, all scan results are published to blob index tags.
- **Disable the entire Defender for Storage plan**: Set the `isEnabled` property value to `False`, and remove the `malwareScanning` and `sensitiveDataDiscovery` sections from the properties.

For more information, see the [Microsoft.Security/DefenderForStorageSettings API documentation](/en-us/rest/api/defenderforcloud-composite/defender-for-storage/create?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true).

---

Tip

You can configure malware scanning to send scanning results to:

- [Azure Event Grid custom topic](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-event-grid-for-malware-scanning): For near-real-time automatic response based on every scanning result.
- [Log Analytics workspace](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-logging-for-malware-scanning): For storing every scan result in a centralized log repository for compliance and audit.

[Learn more on how to set up a response for malware scanning results](defender-for-storage-configure-malware-scan).