---
layout: Conceptual
title: Enable Defender for Storage by Using Infrastructure as Code - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-infrastructure-as-code-enablement
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
description: Learn how to enable and configure Microsoft Defender for Storage by using infrastructure as code (IaC) templates, PowerShell, or Azure Policy.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: be3bf927-0804-450a-1ee3-208cec8a2c91
document_version_independent_id: e6d36ec8-8183-2a88-20f2-e21d20449c07
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-infrastructure-as-code-enablement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-infrastructure-as-code-enablement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-infrastructure-as-code-enablement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 16510164-ab67-ddc6-b2ba-367dbf6489c6
---

# Enable Defender for Storage by Using Infrastructure as Code - Microsoft Defender for Cloud | Microsoft Learn

Use this article to enable and configure Microsoft Defender for Storage by using infrastructure as code (IaC) templates, PowerShell, or Azure Policy. You can enable at either the subscription level or the storage account level. For an overview of Defender for Storage and its features, see [What is Microsoft Defender for Storage](defender-for-storage-introduction).

## Enable Defender for Storage by using infrastructure as code

We recommend that you enable Microsoft Defender for Storage on the subscription level. Doing so helps ensure that all storage accounts currently in the subscription are protected. Protection for storage accounts that you create after enabling Defender for Storage on the subscription level starts up to 24 hours after creation.

Tip

You can always [configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings) with custom settings that differ from the settings configured at the subscription level. That is, you can override subscription-level settings.

# [Enable on a subscription](#tab/enable-subscription)
### Terraform template

To enable and configure Defender for Storage at the subscription level by using Terraform, you can use the following code snippet:

```terraform
resource "azurerm_security_center_subscription_pricing" "DefenderForStorage" {
  tier          = "Standard"
  resource_type = "StorageAccounts"
  subplan       = "DefenderForStorageV2"
 
  extension {
    name = "OnUploadMalwareScanning"
    additional_extension_properties = {
      CapGBPerMonthPerStorageAccount = "10000"
      BlobScanResultsOptions = "BlobIndexTags"
    }
  }
 
  extension {
    name = "SensitiveDataDiscovery"
  }
}
```

By customizing this code, you can:

- **Modify the monthly cap for malware scanning**: Adjust the `CapGBPerMonthPerStorageAccount` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Remove the corresponding extension block from the Terraform code.
- **Disable the entire Defender for Storage plan**: Set the `tier` property value to `"Free"`, and remove the `subPlan` and `extension` properties.

To learn more about the `azurerm_security_center_subscription_pricing` resource, refer to the [Terraform documentation for `azurerm_security_center_subscription_pricing`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/security_center_subscription_pricing). You can also find comprehensive details on the Terraform provider for Azure in the [Terraform AzureRM documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs).

### Bicep template

To enable and configure Defender for Storage at the subscription level by using [Bicep](/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep), make sure your [target scope is set to `subscription`](/en-us/azure/azure-resource-manager/bicep/deploy-to-subscription?tabs=azure-cli#scope-to-subscription). Add the following code to your Bicep template:

```bicep
targetScope = 'subscription'

resource StorageAccounts 'Microsoft.Security/pricings@2023-01-01' = {
  name: 'StorageAccounts'
  properties: {
    pricingTier: 'Standard'
    subPlan: 'DefenderForStorageV2'
    extensions: [
      {
        name: 'OnUploadMalwareScanning'
        isEnabled: 'True'
        additionalExtensionProperties: {
          CapGBPerMonthPerStorageAccount: '10000'
          BlobScanResultsOptions: 'BlobIndexTags'
        }
      }
      {
        name: 'SensitiveDataDiscovery'
        isEnabled: 'True'
      }
    ]
  }
}
```

By customizing this code, you can:

- **Modify the monthly cap for malware scanning**: Adjust the `CapGBPerMonthPerStorageAccount` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` under `SensitiveDataDiscovery`.
- **Disable the entire Defender for Storage plan**: Set the `pricingTier` property value to `Free`, and remove the `subPlan` and `extensions` properties.

Learn more about the Bicep template in the [Microsoft.Security pricing documentation](/en-us/azure/templates/microsoft.security/pricings?pivots=deployment-language-bicep&amp;source=docs).

### Azure Resource Manager template

To enable and configure Defender for Storage at the subscription level by using an Azure Resource Manager template (ARM template), add this JSON snippet to the `resources` section of your ARM template:

```json
{
    "type": "Microsoft.Security/pricings",
    "apiVersion": "2023-01-01",
    "name": "StorageAccounts",
    "properties": {
        "pricingTier": "Standard",
        "subPlan": "DefenderForStorageV2",
        "extensions": [
            {
                "name": "OnUploadMalwareScanning",
                "isEnabled": "True",
                "additionalExtensionProperties": {
                    "CapGBPerMonthPerStorageAccount": "10000",
                    "BlobScanResultsOptions": "BlobIndexTags"
                }
            },
            {
                "name": "SensitiveDataDiscovery",
                "isEnabled": "True"
            }
        ]
    }
}
```

By customizing this code, you can:

- **Modify the monthly cap for malware scanning**: Adjust the `CapGBPerMonthPerStorageAccount` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` under `SensitiveDataDiscovery`.
- **Disable the entire Defender for Storage plan**: Set the `pricingTier` property value to `Free`, and remove the `subPlan` and `extension` properties.

Learn more about the ARM template in the [Microsoft.Security pricing documentation](/en-us/azure/templates/microsoft.security/pricings?pivots=deployment-language-arm-template&amp;source=docs).

# [Enable on a storage account](#tab/enable-storage-account)
### Terraform template

To enable and configure Defender for Storage at the storage account level by using Terraform, import the [AzAPI provider](https://registry.terraform.io/providers/Azure/azapi/latest/docs) and use the following code snippet:

```terraform
resource "azurerm_storage_account" "example" { ... }

resource "azapi_resource_action" "enable_defender_for_Storage" {
  type        = "Microsoft.Security/defenderForStorageSettings@2022-12-01-preview"
  resource_id = "${azurerm_storage_account.example.id}/providers/Microsoft.Security/defenderForStorageSettings/current"
  method      = "PUT"

  body = jsonencode({
    properties = {
      isEnabled = true
      malwareScanning = {
        onUpload = {
          isEnabled     = true
          capGBPerMonth = 10000
          blobScanResultsOptions = BlobIndexTags
        }
      }
      sensitiveDataDiscovery = {
        isEnabled = true
      }
      overrideSubscriptionLevelSettings = true
    }
  })
}
```

In this code, `azapi_resource_action` is an action that's specific to the configuration of Defender for Storage. It's different from the typical resource declarations in Terraform. It's used to perform specific actions on the resource, such as enabling or disabling features.

By customizing this code, you can:

- **Modify the monthly cap for malware scanning**: Adjust the `capGBPerMonth` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` in the section for the `malwareScanning` or `sensitiveDataDiscovery` property.
- **Disable the entire Defender for Storage plan**: Use the following code snippet:

    ```terraform
    resource "azurerm_storage_account" "example" { ... }
    
    resource "azapi_resource_action" "disable_defender_for_Storage" {
      type        = "Microsoft.Security/defenderForStorageSettings@2022-12-01-preview"
      resource_id = "${azurerm_storage_account.example.id}/providers/Microsoft.Security/defenderForStorageSettings/current"
      method      = "PUT"
    
      body = jsonencode({
        properties = {
          isEnabled = false
          overrideSubscriptionLevelSettings = false
        }
      })
    }
    ```

    If you want to disable the Defender for Storage plan for the storage account under subscriptions with Defender for Storage enabled at the subscription level, you can change the value of `overrideSubscriptionLevelSettings` to `True`. If you want to keep some features enabled, you can modify the properties accordingly.

For further customization and control over your storage account's security settings, see the [Microsoft.Security/defenderForStorageSettings API documentation](/en-us/rest/api/defenderforcloud-composite/defender-for-storage/create?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true). You can also find comprehensive details on the Terraform provider for Azure in the [Terraform AzureRM documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs).

### Bicep template

To enable and configure Defender for Storage at the storage account level by using Bicep, add the following code to your Bicep template:

```bicep
resource storageAccount 'Microsoft.Storage/storageAccounts@2021-04-01' ...

resource defenderForStorageSettings 'Microsoft.Security/DefenderForStorageSettings@2022-12-01-preview' = {
  name: 'current'
  scope: storageAccount
  properties: {
    isEnabled: true
    malwareScanning: {
      onUpload: {
        isEnabled: true
        capGBPerMonth: 10000
        blobScanResultsOptions: BlobIndexTags
      }
    }
    sensitiveDataDiscovery: {
      isEnabled: true
    }
    overrideSubscriptionLevelSettings: true
  }
}
```

By customizing this code, you can:

- **Modify the monthly cap for malware scanning**: Adjust the `capGBPerMonth` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` in the section for the `malwareScanning` or `sensitiveDataDiscovery` property.
- **Disable the entire Defender for Storage plan**: Set the `isEnabled` property value to `False`, and remove the `malwareScanning` and `sensitiveDataDiscovery` sections from the properties.

For more information, see the [Microsoft.Security/DefenderForStorageSettings API documentation](/en-us/rest/api/defenderforcloud-composite/defender-for-storage/create?view=rest-defenderforcloud-composite-latest&amp;tabs=HTTP&amp;preserve-view=true).

### ARM template

To enable and configure Defender for Storage at the storage account level by using an Azure Resource Manager template (ARM template), add this JSON snippet to the `resources` section of your ARM template:

```json
{
    "type": "Microsoft.Security/DefenderForStorageSettings",
    "apiVersion": "2022-12-01-preview",
    "name": "current",
    "properties": {
        "isEnabled": true,
        "malwareScanning": {
            "onUpload": {
                "isEnabled": true,
                "capGBPerMonth": 10000,
                "blobScanResultsOptions": BlobIndexTags
            }
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

- **Modify the monthly cap for malware scanning**: Adjust the `capGBPerMonth` parameter to your preferred value. This parameter sets a cap on the maximum data that can be scanned for malware each month, per storage account. If you want to permit unlimited scanning, assign the value `-1`. The default value is -1.
- **Turn off the on-upload malware scanning or sensitive-data threat detection feature**: Change the `isEnabled` value to `False` in the section for the `malwareScanning` or `sensitiveDataDiscovery` property.
- **Disable the entire Defender for Storage plan**: Set the `isEnabled` property value to `False`, and remove the `malwareScanning` and `sensitiveDataDiscovery` sections from the properties.

---

Tip

You can configure malware scanning to send scanning results to:

- [Azure Event Grid custom topic](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-event-grid-for-malware-scanning): For near-real-time automatic response based on every scanning result.
- [Log Analytics workspace](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-logging-for-malware-scanning): For storing every scan result in a centralized log repository for compliance and audit.

[Learn more on how to set up a response for malware scanning results](defender-for-storage-configure-malware-scan).

## Enable at scale with PowerShell

Use PowerShell when you need to enable Defender for Storage for multiple subscriptions.

Before you begin, install the `Az.Security` module:

```powershell
Install-Module -Name Az.Security
```

Use the following command to enable Defender for Storage on a single subscription:

```powershell
Set-AzSecurityPricing -Name "StorageAccounts" -PricingTier "Standard" -SubPlan "DefenderForStorageV2"
```

Use the following script to enable Defender for Storage on all subscriptions in a tenant:

```powershell
$subscriptions = Get-AzSubscription
foreach ($sub in $subscriptions) {
    Set-AzContext -SubscriptionId $sub.Id
    Write-Host "Enabling Defender for Storage on subscription: $($sub.Name)"
    Set-AzSecurityPricing -Name "StorageAccounts" -PricingTier "Standard" -SubPlan "DefenderForStorageV2"
}
```

Note

You need the Security Admin or Owner role on each subscription that you update.

To verify the configuration, run:

```powershell
Get-AzSecurityPricing -Name "StorageAccounts"
```

## Enable automatically with Azure Policy

Use Azure Policy to help ensure new subscriptions are automatically covered and to help prevent configuration drift.

Use the built-in policy definition **Configure Microsoft Defender for Storage to be enabled**.

To assign the policy in the Azure portal:

1. Go to **Policy**.
2. Select **Definitions**.
3. Search for **Defender for Storage**.
4. Select **Configure Microsoft Defender for Storage to be enabled**.
5. Select **Assign**.

Use the `DeployIfNotExists` effect to remediate supported resources automatically.

You can create policy exemptions for specific storage accounts or subscriptions that shouldn't be covered.

Note

Azure Policy assignments can take up to 30 minutes to take effect. Existing non-compliant resources require a remediation task.

For more information, see [Azure Policy documentation](/en-us/azure/governance/policy/overview).

## Validate your deployment

After you deploy Defender for Storage, use the following checklist to validate the configuration:

1. In the Azure portal, go to **Microsoft Defender for Cloud** &gt; **Environment settings** &gt; select your subscription &gt; confirm **Defender for Storage** shows as **On**.
2. Verify storage accounts are listed as protected under **Inventory**.
3. Run a test upload to confirm malware scanning is active. Upload an [EICAR test file](https://www.eicar.org/download-anti-malware-testfile/) to a blob container.
4. Check role assignments. Defender for Storage requires the `StorageBlobDataReader` role on the storage account for the Defender for Cloud service principal.
5. For IaC deployments, confirm no configuration drift by rerunning your template and verifying idempotency.

## Troubleshoot common issues

The following table lists common deployment issues, likely causes, and recommended resolutions.

| Issue | Likely cause | Resolution |
| --- | --- | --- |
| Plan activation fails at subscription level | Insufficient permissions | Ensure you have the Security Admin or Owner role on the subscription. |
| Storage account not protected after subscription-level enablement | Propagation delay | Protection can take up to 24 hours to apply to existing accounts. |
| Configuration drift after ARM/Bicep deployment | Conflicting resource-level settings | Check for resource-level overrides by using `overrideSubscriptionLevelSettings`. Set it to `false` at the storage account level to inherit subscription settings. |
| Auto-provisioning not enabling on new subscriptions | Azure Policy not assigned | Assign the **Configure Microsoft Defender for Storage to be enabled** built-in policy to your management group. |
| Malware scanning not triggering | Plan enabled but extension disabled | Verify the `OnUploadMalwareScanning` extension has `isEnabled: True` in your template. |