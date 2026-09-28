---
layout: Conceptual
title: Migrate from Defender for Storage (classic) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-classic-migrate
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
description: Learn about how to migrate from Defender for Storage (classic) to the new Defender for Storage plan to take advantage of its enhanced capabilities and pricing.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 3527769c-bd8c-4fef-fd4f-2a263a845f10
document_version_independent_id: e4e7a3df-b6cf-885f-4007-6051e1f2a913
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-classic-migrate.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-classic-migrate
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-classic-migrate.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b396ef77-06f7-36c9-06f5-9727248b081e
---

# Migrate from Defender for Storage (classic) - Microsoft Defender for Cloud | Microsoft Learn

This article explains why you should migrate from Defender for Storage (classic) and how to prepare for migration.

It also explains what changes when you move to the new plan, how to identify your current plan configuration, and which migration methods to use at scale. Use this guidance to reduce migration risk and keep storage coverage consistent during the transition.

## Why migrate to the new Defender for Storage plan

On March 28, 2023, we introduced the new Defender for Storage plan. This plan offers several benefits not available in the Defender for Storage (classic) per-transaction or per-storage account pricing plans, such as:

- **Enhanced activity monitoring**: Continuous analysis of data plane and control plane activities for threat detection.
- **Detection of compromised or abused SAS tokens**: Continuous analysis of data plane and control plane activities for threat detection, including the detection of misconfigured and overly permissive Shared Access Signatures (SAS tokens) that might be leaked or compromised.
- **Option to enable sensitive data threat detection (add-on)**: Detection of potential exposure events and suspicious activities on resources containing sensitive data resulting in data exfiltration.
- **Option to enable malware scanning (paid add-on)**: Real-time detection of malicious files across all file types.
- **Predictable, per-storage account pricing**: A more foreseeable and flexible pricing structure for better control over coverage.
- **Granular controls at the resource level**: Enable at the subscription or resource level and exclude specific storage accounts from protected subscriptions, providing more granular control over your security coverage.

The new pricing plan charges based on the number of storage accounts you protect, simplifying calculations and allowing for easy scaling as your needs change. For detailed pricing information, see [the pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

To take advantage of the enhanced monitoring, malware scanning, sensitive data detection, and predictable pricing in the new plan, we recommend moving to the new Defender for Storage plan by February 5, 2025.

Note

After February 5, 2025, you can no longer enable Defender for Storage (classic), the legacy per-transaction pricing plan, in most scenarios. The only exception is for subscriptions that already have the per-transaction pricing **enabled**.

## Important changes in Defender for Storage (classic)

Defender for Storage (Classic) offers two pricing structures: per-transaction and per-storage account.

### Impact on the Defender for Storage (classic) per-transaction plan

Important

Switching to the new Defender for Storage plan is irreversible. After you switch, you can no longer revert to the Defender for Storage (classic) per-transaction or per-storage account plans at either the subscription or storage account level.

The classic per-transaction plan will no longer be available for new storage accounts and subscriptions. Existing accounts will retain the plan without future features and updates, so we encourage you to move to the new plan for the enhanced features and simplified pricing. If your subscription or storage account already has the classic per-transaction plan enabled, it will remain active, but enabling this plan at the resource level will only be possible for these existing subscriptions.

If you have policies that enforce the classic per-transaction plan without specifying the per-transaction subplan, existing subscriptions will retain the classic per-transaction plan already enabled on those subscriptions, while new subscriptions will default to the new plan. However, if you specify the per-transaction subplan, the policy assignment will fail for new subscriptions. Once you switch to the new plan, you can no longer revert to the Defender for Storage (classic) per-transaction or per-storage account plans at either the subscription or storage account level.

## Identify active Defender for Storage plans

We provide three options to find out your Defender for Storage plans enablement and configuration:

- **KQL query in Resource Graph Explorer**: Use this KQL query in the Azure portal's [Resource Graph Explorer](https://ms.portal.azure.com/#view/HubsExtension/ArgQueryBlade) to view which plans are enabled at the subscription level:

    ```kusto
    // DF-Storage Plans
    securityresources
    | where type == "microsoft.security/pricings"
    | where name == "StorageAccounts"
    | extend pricingTier = properties.pricingTier
    | extend DefenderForStoragePlan = properties.subPlan
    | extend IsInTrialPeriod = properties.freeTrialRemainingTime
    | extend MalwareScanningEnabled = properties.extensions[0].isEnabled
    | extend MalwareScanningCapping = properties.extensions[0].additionalExtensionProperties["CapGBPerMonthPerStorageAccount"]
    | extend SensitiveDataDiscoveryEnabled = properties.extensions[1].isEnabled
    | extend IsEnabled = iff(pricingTier == "Free", "Disabled", "Enabled"), 
        DefenderForStoragePlan  = iff(isnull(DefenderForStoragePlan ), "", DefenderForStoragePlan ), 
        MalwareScanningEnabled = iff(isnull(MalwareScanningEnabled), "", MalwareScanningEnabled), 
        MalwareScanningCapping = iff(isnull(MalwareScanningCapping), "", MalwareScanningCapping), 
        SensitiveDataDiscoveryEnabled = iff(isnull(SensitiveDataDiscoveryEnabled), "", SensitiveDataDiscoveryEnabled),
        IsInTrialPeriod = iff(IsInTrialPeriod == "PT0S", "", "Yes")
    | project properties, tenantId, subscriptionId, IsInTrialPeriod, IsEnabled, DefenderForStoragePlan, MalwareScanningEnabled, MalwareScanningCapping, SensitiveDataDiscoveryEnabled
    ```
- **Detailed analysis with PowerShell script**: For a more detailed investigation, including information at both the subscription and resource levels (with add-ons configuration), run the [Analyze-DefenderForStorageConfig.ps1 PowerShell script](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Powershell%20scripts/Analyze%20Defender%20For%20Storage%20Configuration/Analyze-DefenderForStorageConfig.ps1).
- **Workbook for subscription-level coverage details**: Use the provided workbook to see which plans are enabled at the subscription level and their configuration details. To access the workbook, see [Microsoft Defender for Storage - Price Estimation Dashboard](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Workbooks/Microsoft%20Defender%20for%20Storage%20Price%20Estimation).

## Choose a migration method for Defender for Storage (classic)

To enable and configure the new Microsoft Defender for Storage plan, you have several options:

- **Azure built-in policy (recommended)**: Apply [built-in policies](defender-for-storage-policy-enablement) to uniformly secure all existing and future storage accounts at scale within a defined scope, such as management groups.
- **Infrastructure as Code (IaC) templates**: Use [Terraform](defender-for-storage-infrastructure-as-code-enablement#terraform-template), [Bicep](defender-for-storage-infrastructure-as-code-enablement#bicep-template), or [Azure Resource Manager](defender-for-storage-infrastructure-as-code-enablement#azure-resource-manager-template) templates for automated deployment and configuration.
- **Azure portal**: Migrate to the new plan [through the Azure portal](defender-for-storage-azure-portal-enablement).
    1. Navigate to **Environment settings** in Defender for Cloud or the Defender for Cloud pane in one of the storage accounts.
    2. Under **Storage**, select **New plan available**.
    3. In the **Upgrade Defender for Storage plan** pane, choose your configuration options and then select **Upgrade subscription**.
- **REST API**: Use the [REST API](defender-for-storage-rest-api-enablement) to enable the new plan programmatically.

## Identify active policies

To enable the new plan, make sure to disable the old Defender for Storage policies:

- "Configure Azure Defender for Storage to be enabled"
- "Azure Defender for Storage should be enabled"
- "Configure Microsoft Defender for Storage to be enabled (per-storage account plan)"
- "Configure Microsoft Defender for Storage (Classic) to be enabled"
- "Deploy Defender for Storage (Classic) on storage accounts"

You can use the following methods to identify the active policies:

### Azure Resource Graph Explorer

To identify active policies in your subscription using [Azure Resource Graph Explorer](https://ms.portal.azure.com/#view/HubsExtension/ArgQueryBlade), run the following query. This query searches Azure Resource Graph for policy assignments scoped to the specified subscription that match the old Defender for Storage policy names. If you have custom policies, modify the query accordingly:

```kusto
policyresources
| where type == "microsoft.authorization/policyassignments"
| where subscriptionId == "{subscriptionId}"
| where properties['displayName'] in ("Configure Azure Defender for Storage to be enabled", "Azure Defender for Storage should be enabled", "Configure Microsoft Defender for Storage to be enabled (per-storage account plan)", "Configure Microsoft Defender for Storage (Classic) to be enabled", "Deploy Defender for Storage (Classic) on storage accounts")
```

### PowerShell

To identify active policies in your subscription using PowerShell, run the following command. This command lists all Azure Policy assignments at the subscription scope so you can verify which Defender for Storage policies are applied:

```powershell
Get-AzPolicyAssignment -Scope "/subscriptions/{subscriptionId}"
```