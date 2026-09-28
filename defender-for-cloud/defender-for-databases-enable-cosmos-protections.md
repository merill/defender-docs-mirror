---
layout: Conceptual
title: Enable Microsoft Defender for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-databases-enable-cosmos-protections
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
description: Learn how to enable enhanced security features in Microsoft Defender for Azure Cosmos DB.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d8731ad9-75a9-b7ba-cdcf-2cdaa0848864
document_version_independent_id: 855f9a53-0373-e011-e2d5-6a1d39ce726b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-databases-enable-cosmos-protections.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-databases-enable-cosmos-protections
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-databases-enable-cosmos-protections.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd668c2f-f5b3-4573-8ad1-019570e3e2db
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cc82e69d-afbe-4554-9f4c-6705fc860c42
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 28adb262-4e3d-9b2c-b011-ac033867100d
---

# Enable Microsoft Defender for Azure Cosmos DB - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Azure Cosmos DB protection is available at both the subscription level and the resource level.

You can enable Microsoft Defender for Cloud on your subscription to protect all database types, including Microsoft Defender for Azure Cosmos DB. Enabling protection at the subscription level is the recommended approach.

You can also enable Microsoft Defender for Azure Cosmos DB at the resource level to protect a specific Azure Cosmos DB account.

## Prerequisites

Before you begin, make sure you have the following prerequisite:

- An Azure account. If you don't already have one, [create a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Enable database protection at the subscription level

Enable Microsoft Defender for Cloud at the subscription level to protect all database types in your subscription (recommended).

You can enable Microsoft Defender for Cloud protection on your subscription to protect database types such as Azure Cosmos DB, Azure SQL Database, Azure SQL servers on machines, and open-source relational databases.

You can also select specific resource types to protect when you configure your plan.

When you turn on enhanced security features for your subscription, Defender for Azure Cosmos DB is enabled for all your Azure Cosmos DB accounts.

**To enable database protection at the subscription level**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Locate Databases and toggle the switch to **On**.

    [![Screenshot showing the available protections you can enable.](media/quickstart-enable-defender-for-cosmos/protection-type.png)](media/quickstart-enable-defender-for-cosmos/protection-type-expanded.png#lightbox)
5. Select **Save**.

**To select specific resource types to protect when you configure your plan**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Locate Databases and toggle the switch to **On**.
5. Select **Select types**

    ![Screenshot showing where the option to select the type is located.](media/quickstart-enable-defender-for-cosmos/select-type.png)
6. Toggle the desired resource type switches to **On**.

    ![Screenshot showing the available resources you can enable.](media/quickstart-enable-defender-for-cosmos/resource-type.png)
7. Select **Confirm**.

## Enable Microsoft Defender for Azure Cosmos DB at the resource level

You can enable Defender for Azure Cosmos DB on a specific account by using the Azure portal, PowerShell, Azure CLI, an ARM template, or Azure Policy.

**To enable Microsoft Defender for Cloud for a specific Azure Cosmos DB account**:

Use one of the following methods: Azure portal, PowerShell, ARM template, Azure CLI, or Azure Policy.

# [Azure portal](#tab/azure-portal)
To enable Defender for Azure Cosmos DB from the Azure portal, perform the following steps:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **your Azure Cosmos DB account** &gt; **Settings**.
3. Select **Microsoft Defender for Cloud**.
4. Select **Enable Microsoft Defender for Azure Cosmos DB**.

    [![Screenshot of the option to enable Microsoft Defender for Azure Cosmos DB on your specified Azure Cosmos DB account.](media/quickstart-enable-defender-for-cosmos/enable-storage.png)](media/quickstart-enable-defender-for-cosmos/enable-storage.png#lightbox)

# [PowerShell](#tab/azure-powershell)
To enable Defender for Azure Cosmos DB by using PowerShell, run the following steps:

1. Install the [Az.Security](https://www.powershellgallery.com/packages/Az.Security/1.1.1) module.
2. Call the [Enable-AzSecurityAdvancedThreatProtection](/en-us/powershell/module/az.security/enable-azsecurityadvancedthreatprotection) command.

    ```powershell
    Enable-AzSecurityAdvancedThreatProtection -ResourceId "/subscriptions/<Your subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.DocumentDb/databaseAccounts/myCosmosDBAccount/" 
    ```
3. Verify the setting for your account by calling the [Get-AzSecurityAdvancedThreatProtection](/en-us/powershell/module/az.security/get-azsecurityadvancedthreatprotection) command.

    ```powershell
    Get-AzSecurityAdvancedThreatProtection -ResourceId "/subscriptions/<Your subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.DocumentDb/databaseAccounts/myCosmosDBAccount/" 
    ```

# [ARM template](#tab/arm-template)
Use an Azure Resource Manager template to deploy an Azure Cosmos DB account with Microsoft Defender for Azure Cosmos DB enabled. For deployment details and a sample ARM template, see [Create an Azure Cosmos DB account with Microsoft Defender for Azure Cosmos DB enabled](https://github.com/azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.documentdb/microsoft-defender-cosmosdb-create-account).

# [Azure CLI](#tab/azure-cli)
To enable Microsoft Defender for Azure Cosmos DB on a single account via Azure CLI, call the [az security atp cosmosdb update](/en-us/cli/azure/security/atp/cosmosdb) command. Remember to replace values in angle brackets with your own values:

```azurecli
az security atp cosmosdb update \
    --resource-group <resource-group> \
    --cosmosdb-account <cosmosdb-account> \
    --is-enabled true
```

To verify that Defender for Azure Cosmos DB is enabled on your account, call the [az security atp cosmosdb show](/en-us/cli/azure/security/atp/cosmosdb) command. This command displays the current protection state so you can confirm the feature is active. Remember to replace values in angle brackets with your own values:

```azurecli
az security atp cosmosdb show \
    --resource-group <resource-group> \
    --cosmosdb-account <cosmosdb-account>
```

# [Azure Policy](#tab/azure-policy)
Use Azure Policy to enable Microsoft Defender for Cloud across Azure Cosmos DB accounts under a specific subscription or resource group.

1. Launch the Azure Policy &gt; Definitions page.
2. Search for the **Configure Microsoft Defender for Azure Cosmos DB to be enabled** policy, then select the policy to view the policy definition page.

    ![Screenshot of selecting the policy.](media/defender-for-databases-enable-cosmos-protections/select-policy.png)
3. Select the **Assign button** for the built-in policy.

    ![Screenshot of selecting the assign button.](media/defender-for-databases-enable-cosmos-protections/select-assign-button.png)
4. Specify an Azure subscription.

    ![Screenshot of choosing Azure subscription.](media/defender-for-databases-enable-cosmos-protections/choose-subscription.png)
5. Select **Review + create** to review the policy assignment and complete it.

---

## Simulate security alerts from Microsoft Defender for Azure Cosmos DB

For a full list, see [supported alerts](alerts-azure-cosmos-db) in the Defender for Cloud alert reference.

You can use sample alerts to check alert quality and behavior.

Sample alerts also help you test alert settings, such as SIEM links, workflow automation, and email notifications.

Create sample alerts to verify that your alerting, automation, and notification pipelines work as expected.

**To create sample alerts from Microsoft Defender for Azure Cosmos DB**:

1. Sign in to the [Azure portal](https://portal.azure.com/) as a Subscription Contributor user.
2. Navigate to the security alerts page.
3. Select **Sample alerts**.
4. Select the subscription.
5. Select the relevant Microsoft Defender for Cloud plan(s).
6. Select **Create sample alerts**.

    ![Screenshot showing the order needed to create an alert.](media/quickstart-enable-defender-for-cosmos/sample-alerts.png)

After a few minutes, alerts appear on the security alerts page.

Alerts also appear in other configured destinations, such as connected SIEM systems and email notifications.