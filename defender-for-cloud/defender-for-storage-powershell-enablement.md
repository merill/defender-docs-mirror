---
layout: Conceptual
title: Enable Microsoft Defender for Storage with Azure PowerShell - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-powershell-enablement
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
description: Learn how to enable Microsoft Defender for Storage on your Azure subscription for Microsoft Defender for Cloud by using Azure PowerShell.
ms.topic: install-set-up-deploy
ms.date: 2025-06-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e3897f87-5358-4efd-9a02-c800014a4571
document_version_independent_id: a5887733-c103-3149-5a0b-4b4a86adaf66
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-powershell-enablement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-powershell-enablement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-powershell-enablement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/f7db5823-dfbf-4e94-9016-c24311b90d7e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/a5ab72d9-1367-4994-84a6-d9964cd9936d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 791ecf88-2cfe-6da7-0651-2a1d24f85832
---

# Enable Microsoft Defender for Storage with Azure PowerShell - Microsoft Defender for Cloud | Microsoft Learn

We recommend that you enable Microsoft Defender for Storage on the subscription level. Doing so helps ensure that all storage accounts currently in the subscription are protected. Protection for storage accounts that you create after enabling Defender for Storage on the subscription level starts up to 24 hours after creation.

Tip

You can always [configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings) with custom settings that differ from the settings configured at the subscription level. That is, you can override subscription-level settings.

## Set up Azure PowerShell

Before you work with Azure PowerShell, perform the following steps:

1. If you don't have it already, [install the Az PowerShell module](/en-us/powershell/azure/install-azure-powershell).
2. Use the `Connect-AzAccount` cmdlet to sign in to your Azure account. [Learn more about signing in to Azure by using Azure PowerShell](/en-us/powershell/azure/authenticate-azureps).
3. Use the following commands to register your subscription to the Microsoft Defender for Cloud resource provider. Replace `<subscriptionId>` with your subscription ID.

    ```powershell
    Set-AzContext -Subscription <subscriptionId>
    Register-AzResourceProvider -ProviderNamespace 'Microsoft.Security'
    ```

## Enable and configure Defender for Storage

# [Enable on a subscription](#tab/enable-subscription)
Enable Defender for Storage at the subscription level with per-transaction pricing by using the `Set-AzSecurityPricing` cmdlet:

```powershell
Set-AzSecurityPricing -Name "StorageAccounts" -PricingTier "Standard" -SubPlan "DefenderForStorageV2" -Extension '[
    {
        "name": "OnUploadMalwareScanning",
            "isEnabled": "True",
        "additionalExtensionProperties": {
            "CapGBPerMonthPerStorageAccount": "10000"
        }
    },
    {
        "name": "SensitiveDataDiscovery",
        "isEnabled": "True"
    }]'
```

If you don't provide extension properties for the cmdlet, both malware scanning and sensitive data discovery are enabled by default.

By customizing this code, you can:

- **Modify the monthly threshold for on-upload malware scanning**: Adjust the `CapGBPerMonthPerStorageAccount` property to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default limit is 10,000 GB.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` on the `OnUploadMalwareScanning` and `SensitiveDataDiscovery` extension properties.
- **Disable the entire Defender for Storage plan**: Set the `-PricingTier` property value to `Free`, and remove the `-SubPlan` and `-Extension` properties.

Tip

You can use the [GetAzSecurityPricing](/en-us/powershell/module/az.security/get-azsecuritypricing) cmdlet to see all of the Defender for Cloud plans that are enabled for the subscription.

For more information about the `Set-AzSecurityPricing` cmdlet, see the [Azure PowerShell reference](/en-us/powershell/module/az.security/set-azsecuritypricing).

# [Enable on a storage account](#tab/enable-storage-account)
Enable and configure Defender for Storage at the storage account level by using the `Update-AzSecurityDefenderForStorage` cmdlet. In the following example, replace the `<SubscriptionId>`, `<ResourceGroupName>`, and `<StorageAccountName>` values with your own Azure subscription ID, resource group, and storage account name.

```powershell
Update-AzSecurityDefenderForStorage -ResourceId "/subscriptions/<SubscriptionId>/resourcegroups/<ResourceGroupName>/providers/Microsoft.Storage/storageAccounts/<StorageAccountName>" -IsEnabled -OverrideSubscriptionLevelSetting -OnUploadIsEnabled -OnUploadCapGbPerMonth 7000 -SensitiveDataDiscoveryIsEnabled
```

With Defender for Storage enabled at the subscription level, the `-OverrideSubscriptionLevelSetting` parameter is necessary to override the settings at the subscription level. If you don't use the override parameter, the extensions are set according to the subscription-level settings, regardless of the parameter values that you supply in the cmdlet.

By customizing this code, you can:

- **Modify the monthly threshold for malware scanning**: Adjust the `-OnUploadCapGBPerMonth` parameter to your preferred value. This parameter sets a cap on the maximum data to be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default limit is 10,000 GB.
- **Send malware scan results to Azure Event Grid**: Supply the Event Grid topic's resource ID in the parameter `-MalwareScanningScanResultsEventGridTopicResourceId "<resourceId>"`.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Set `-OnUploadIsEnabled:$false` or `-SensitiveDataDiscoveryIsEnabled:$false`, respectively.
- **Disable the entire Defender for Storage plan**: Set `IsEnabled:$false`, `-OnUploadIsEnabled:$false`, and `-SensitiveDataDiscoveryIsEnabled:$false`.

Tip

You can use the [`Get-AzSecurityDefenderForStorage`](/en-us/powershell/module/az.security/get-azsecuritydefenderforstorage) cmdlet to see the Defender for Storage settings for a storage account.

For more information about the `Update-AzSecurityDefenderForStorageRefer` cmdlet, see the [Azure PowerShell reference](/en-us/powershell/module/az.security/update-azsecuritydefenderforstorage).

---

Tip

You can configure malware scanning to send scanning results to:

- [Event Grid custom topic](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-event-grid-for-malware-scanning): For near-real-time automatic response based on every scanning result.
- [Log Analytics workspace](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-logging-for-malware-scanning): For storing every scan result in a centralized log repository for compliance and audit.

[Learn more on how to set up a response for malware scanning results](defender-for-storage-configure-malware-scan).