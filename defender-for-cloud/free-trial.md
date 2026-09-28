---
layout: Conceptual
title: Check the Status of Your Free Trial - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/free-trial
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
description: Learn how to check the status of your 30 day free trial of Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 573d5192-d1f9-e11a-b01e-7b953b93e59c
document_version_independent_id: 409384de-ebd8-f630-cc4f-5d3663efaf0e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/free-trial.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/free-trial
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/free-trial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 9e50cde7-5880-e8a7-cdb2-4b62cf591821
---

# Check the Status of Your Free Trial - Microsoft Defender for Cloud | Microsoft Learn

When you enable Microsoft Defender for Cloud for the first time on your Azure subscription, you automatically start a 30-day free trial. During this trial period, you can explore the capabilities of Defender for Cloud, foundational Cloud Security Posture Management (CSPM), and access to [Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-defender).

The free trial lasts for 30 days, or until you reach the usage limit for certain plans, whichever comes first.

When the usage limit is met or the 30-day trial ends, charges begin based on the plans enabled in your environment. To learn more about these plans, their usage limits, and associated costs, see the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

If you have multiple subscriptions, each subscription has its own free trial period. You need to check the status of each subscription's free trial individually.

Azure gives you a 30-day free trial every time you activate a new plan. For example, if you activate Defender for Servers, you get 30 days free. If at a later time you activate Defender for Cloud Security Posture Management (DCSPM), you get another 30 days for that plan. Amazon Web Service (AWS) gets one trial per AWS account, and Google Cloud Project gets one trial per GCP project, regardless of which plan is enabled or when.

## Prerequisites

Before you check your free trial status, make sure you meet the following requirements:

- You have a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You [enabled Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- To check the status of a free trial, you must have a role of Reader or higher on the subscription.
- To enable a plan on your subscription, you must have the **Security Admin** or **Owner** role.

## Check your free trial status with Azure CLI

You can check the status of your free trial by using the built-in Azure Command-Line Interface (CLI).

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud**.
3. Select **CLI**.

    [![Screenshot that shows where the button is located on the Defender for Cloud overview screen to open the Azure CLI.](media/free-trial/select-cli.png)](media/free-trial/select-cli.png#lightbox)
4. Select **PowerShell**.
5. Run the following command to list the Defender for Cloud pricing configurations for your subscription, including the free trial status of each plan:

    ```powershell
    Get-AzSecurityPricing
    ```

The `FreeTrialRemainingTime` field shows the remaining time, if any, of the free trial. If the field shows `00:00:00`, it means that the free trial is complete.

## Check your free trial status with Azure Resource Graph Explorer

You can check the status of your free trial by using the Resource Graph Explorer in the Azure portal.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Resource Graph Explorer**.
3. Run the following query:

    ```kusto
     // Total volume
     securityresources
     | where type == "microsoft.security/pricings"
     | extend iso = tostring(properties.freeTrialRemainingTime)
     | extend
     days = extract(@"P(\d+)D", 1, iso),
     hours = extract(@"T(\d+)H", 1, iso),
     minutes = extract(@"H(\d+)M", 1, iso)
     | extend enablementDate = format_datetime(todatetime(properties.enablementTime), "yyyy-MM-dd HH:mm:ss")
     | project
     subscriptionId,
     name,
     pricingTier = properties.pricingTier,
     FreeTrialRemainingTime = strcat(
         coalesce(days, "0"), " days, ",
         coalesce(hours, "0"), " hours, ",
         coalesce(minutes, "0"), " minutes"
     ),
     resourcesCoverageStatus = properties.resourcesCoverageStatus,
     enablementDate
     | sort by subscriptionId asc
    ```

The `FreeTrialRemainingTime` column shows the remaining time, if any, of the free trial. If the column shows `0 days, 0 hours, 0 minutes`, it means that the free trial is complete.

## Check your free trial status with Defender for Cloud

You can check the status of your free trial directly in the Defender for Cloud portal.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Locate the icon that applies to your subscription:

    [![Screenshot that shows where the icon is located on the plans page.](media/free-trial/icon-location.png)](media/free-trial/icon-location.png#lightbox)

    | Icon | Description |
    | --- | --- |
    | ![](media/free-trial/full-trial.png) | The full trial is still available. |
    | ![](media/free-trial/trial-started.png) | The free trial is active. Hover over the icon to see the remaining time. |
    | No icon | The free trial is over. |

## Disable the free trial

If you decide not to continue using Defender for Cloud during your free trial, you can disable it.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Disable the relevant plan.
5. Select **Save**.