---
layout: Conceptual
title: External Attack Surface Management Initiative in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/external-attack-surface-management-initiative
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to get MDEASM insights into your corporate attack surface with the initiative in Microsoft Security Exposure Management.
ms.topic: how-to
ms.date: 2025-05-27T00:00:00.0000000Z
ms.custom:
- msecd-doc-authoring-1014
- sfi-ga-nochange
- sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: b2b18026-d7f6-f852-43dd-dfe82f6a3686
document_version_independent_id: b2b18026-d7f6-f852-43dd-dfe82f6a3686
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/external-attack-surface-management-initiative.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-attack-surface-management-initiative
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/external-attack-surface-management-initiative.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0ea8e68c-f4ed-434c-9d19-be6d6d11d320
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c12d78a5-9897-4a37-b8c3-a69875f59a02
platformId: 85526194-9ec4-56ce-cc92-0f1ac029b8d5
---

# External Attack Surface Management Initiative in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

Explore how to integrate Microsoft Defender External Attack Surface Management (MDEASM) with Microsoft Security Exposure Management (MSEM) to enhance visibility and control over your organization's external exposures. By connecting MDEASM insights to MSEM using the External attack surface management initiative in Microsoft Security Exposure Management, you can assess the risk associated with your organization's or vendor's external attack surface and manage your security posture more effectively within the Exposure Management portal.

There are two ways to use the External Attack Surface Management initiative:

- **Pre-built footprint**: Provides high-level insights using a predefined set of external assets, without requiring a full MDEASM subscription.
- **Full integration with MDEASM**: Connects directly to your MDEASM subscription for comprehensive exposure analysis and asset-level details.

## Using the EASM initiative with pre-built footprint

The pre-built footprint option for the External Attack Surface Management initiative provides high-level insights without a full connection to an MDEASM subscription and doesn't require an active MDEASM subscription.

**Prerequisites**: To configure your External Attack Surface initiative, you need to have **Global Administrator** role, or **Core security settings (manage)** permissions.

1. Go to the **Initiatives** page, select the **External Attack Surface Protection**, then choose **Open initiative page**.
2. Go to the **Connect data source** to open the settings tab.

    Note

    If you previously configured the External Attack Surface Protection initiative, you can select **Switch data source** to reconfigure it with new data.
3. Choose **Search for your organization's pre-built footprint**.
4. Select the footprint you want to use from the list of available pre-built footprints and choose **Connect**.

    [![Screenshot of side panel for EASM pre-built footprint selection](media/easm/easm-pre-built-footprint.png)](media/easm/easm-pre-built-footprint.png#lightbox)
5. In up to 1 hour, the initiative is populated with high-level metrics and scores from the selected footprint.

    Note

    The pre-built footprint approach doesn't provide asset-level information or detailed exposure information.

## Using the EASM initiative with full MDEASM integration

### Prerequisites

Full integration with MDEASM requires a full MDEASM subscription (trial or paid) and provides comprehensive exposure analysis and asset-level details.

To configure your External Attack Surface initiative, you need to have **Global Administrator** role or **Core security settings (manage)** permissions.

Note

External attack surface assets do not support scoping, so all users with access can see all collected data.

### Set up the environment for full MDEASM integration

To deploy an MDEASM resource, follow these steps:

1. Log into the [Azure portal](https://portal.azure.com).
2. Create a Resource Group with the appropriate subscription and region.
3. Deploy an MDEASM Resource within that group; see [Create a Defender EASM Azure resource](/en-us/azure/external-attack-surface-management/deploying-the-defender-easm-azure-resource). Each new resource will automatically get a free 30 day trial.

### Discover the attack surface

You can discover your attack surface in two ways:

1. Use the **Get Started** option to search for your organization and build a preconfigured attack surface.
2. You can alternately create a custom discovery group by providing:

    - Domains
    - IP Blocks or Addresses (use example IPs such as 203.0.113.0 if needed)
    - Hosts
    - ASNs
    - Emails
    - WHOIS organization data

For more information, see [Discover your attack surface](/en-us/azure/external-attack-surface-management/discovering-your-attack-surface)

Tip

The easiest path is to provide a host, domain, and any known external IP addresses.

### Configure the initiative

Perform the following steps to connect the initiative to your MDEASM data source:

1. Go to the **Initiatives** page, select the **External Attack Surface Protection**, then choose **Open initiative page**.
2. Go to the **Connect data source** to open the settings tab.

    Note

    If you previously configured the External Attack Surface Protection initiative, you can select **Switch data source** to reconfigure it with new data.
3. Choose **Connect your MDEASM workspace**.
4. To enable the initiative to pull data from your Defender EASM resource, enter the values from your resource's **Essentials** section on the **Overview** pane found in Azure.

    - **Resource Name**
    - **Subscription ID**
    - **Resource Group Name**
    - **Region**

    ![Screenshot of side panel for EASM initiative](media/easm/easm-full_integration.png)
5. Select **Connect**. After validation, data will begin flowing into the graph, and metrics will calculate within 32 hours.

You can review your security initiative data through security metrics that reflect various exposure types as assessed by the External Attack Surface assessment engine. Select a metric to view additional information such as the exposed assets and their types.

You can also explore the data integrated from EASM using the [attack surface map](enterprise-exposure-map) to uncover insights related to your attack surface. You can search for various assets such as IP addresses, domains, hosts, and more, and review the findings on these assets.