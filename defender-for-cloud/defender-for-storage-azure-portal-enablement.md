---
layout: Conceptual
title: Enable Defender for Storage by Using the Azure Portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-azure-portal-enablement
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
description: Learn how to enable Microsoft Defender for Storage on your Azure subscription for Microsoft Defender for Cloud by using the Azure portal.
ms.topic: install-set-up-deploy
ms.date: 2025-06-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 07810985-c272-7d19-b8e5-882bdf1f3756
document_version_independent_id: e36d6d4f-d22a-50fa-c179-d45413d336e5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-azure-portal-enablement.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-azure-portal-enablement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-azure-portal-enablement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: dc7f95e0-69cb-e18d-52cb-3199b0a5aae8
---

# Enable Defender for Storage by Using the Azure Portal - Microsoft Defender for Cloud | Microsoft Learn

We recommend that you enable Microsoft Defender for Storage on the subscription level. Doing so helps ensure that all storage accounts currently in the subscription are protected. Protection for storage accounts that you create after enabling Defender for Storage on the subscription level starts up to 24 hours after creation.

Tip

You can always [configure specific storage accounts](advanced-configurations-for-malware-scanning#override-defender-for-storage-subscription-level-settings) with custom settings that differ from the settings configured at the subscription level. That is, you can override subscription-level settings.

# [Enable on a subscription (recommended)](#tab/enable-subscription)
To enable Defender for Storage at the subscription level by using the Azure portal:

1. Sign in to the Azure portal.
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the subscription for which you want to enable Defender for Storage.

    [![Screenshot that shows the selection of a subscription on the pane for environment settings.](media/defender-for-storage-malware-scan/azure-portal-enablement-subscription.png)](media/defender-for-storage-malware-scan/azure-portal-enablement-subscription.png#lightbox)
4. Select the three dots, and then select **Edit settings**.
5. On the **Defender plans** pane, locate **Storage** in the list. Then select **On** &gt; **Save**.

    [![Screenshot that shows the toggle for turning on a Defender for Storage plan.](media/defender-for-storage-malware-scan/azure-portal-enablement-turn-on.png)](media/defender-for-storage-malware-scan/azure-portal-enablement-turn-on.png#lightbox)

    If you currently have Defender for Storage enabled with per-transaction pricing, select the **New pricing plan available** link and confirm the pricing change.

Defender for Storage is now enabled for this subscription, including on-upload malware scanning and sensitive-data threat detection. Here are a few more options at this point:

- If you want to turn off on-upload malware scanning or sensitive-data threat detection, select **Settings** and change the status of the feature to **Off**. Then save the changes.
- If you want to change the size capping per storage account per month for malware scanning, or change the use of index tags for storing malware scan results, or enable soft deletion of malicious blobs, go to **Edit configuration**. Adjust the settings as needed, and then save your changes.
- If you want to disable the Defender for Storage plan, turn the status to **Off** for the plan on the **Defender plans** pane. Then save the changes.

# [Enable on a storage account](#tab/enable-storage-account)
To enable and configure Defender for Storage for a specific account by using the Azure portal:

1. Sign in to the Azure portal.
2. Go to your storage account. On the left menu, in the **Security + networking** section, select **Microsoft Defender for Cloud**.
3. **On-upload malware scanning** and **Sensitive data threat detection** are enabled by default. You can disable the features by clearing their checkboxes.
4. Select **Enable on storage account**.

[![Screenshot that shows the pane for enabling Defender for Storage.](media/defender-for-storage-malware-scan/azure-portal-enablement-on-storage-account.png)](media/defender-for-storage-malware-scan/azure-portal-enablement-on-storage-account.png#lightbox)

Defender for Storage is now enabled on this storage account. You can disable it or modify these features:

- On-upload malware scanning (such as monthly capping)
- Sensitive-data threat detection
- Limit of gigabytes scanned per month
- Filtering of on-upload scans
- Storage of scan results as blob index tags
- Soft deletion of malicious blobs
- Sending scan results to an Azure Event Grid topic
- Sending scan results to Log Analytics

Select **Settings**, edit the settings, and then select **Save**.

---

Tip

You can configure malware scanning to send scanning results to:

- [Event Grid custom topic](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-event-grid-for-malware-scanning): For near-real-time automatic response based on every scanning result.
- [Log Analytics workspace](/en-us/azure/defender-for-cloud/advanced-configurations-for-malware-scanning#set-up-logging-for-malware-scanning): For storing every scan result in a centralized log repository for compliance and audit.

[Learn more on how to set up a response for malware scanning results](defender-for-storage-configure-malware-scan).