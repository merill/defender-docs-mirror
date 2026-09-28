---
layout: Conceptual
title: Discover Sensitive Data in Cloud Resources - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/discover-sensitive-data
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
description: Learn how to discover resources with sensitive data types in the Data and AI security dashboard in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: e7f97069-f426-8aa0-a505-d9abc41d2683
document_version_independent_id: a6cad3a5-581a-5e4d-22ae-39a96332207b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/discover-sensitive-data.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/discover-sensitive-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/discover-sensitive-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1aef71c7-5ef5-d50a-d004-c7e32a6fed53
---

# Discover Sensitive Data in Cloud Resources - Microsoft Defender for Cloud | Microsoft Learn

Use sensitive data discovery in Microsoft Defender for Cloud to find cloud resources that expose sensitive information. This article shows you how to open sensitive data findings in the Data and AI security dashboard and investigate related recommendations and alerts.

## Prerequisites

Complete these steps before you start:

- [Enable Defender CSPM](tutorial-enable-cspm-plan).
- [Enable sensitive data discovery](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan).
- [Enable Defender for Storage](tutorial-enable-storage-plan).
- [Enable Defender for Databases](tutorial-enable-databases-plan).
- [Register each Azure subscription](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider) to the Microsoft.Security resource provider.

## View resources with sensitive data

Resources with sensitive data might be exposed to unwanted access. Use these steps to find those resources and review the results.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Data and AI security dashboard**.
3. In Data closer look, select **View all resources with sensitive info types**.

    [![Screenshot of the Data and AI security dashboard that shows where the view all resources with sensitive data type button is located.](media/discover-sensitive-data/view-all-resources.png)](media/discover-sensitive-data/view-all-resources.png#lightbox)
4. Select **Search**.

    [![Screenshot that shows where the search button is located on the Cloud Security Explorer page.](media/discover-sensitive-data/search-button.png)](media/discover-sensitive-data/search-button.png#lightbox)
5. Review each record found and select **View details** to see more information about the resource.
6. Select the resource name to see its recommendations and alerts.
7. Remediate recommendations. For guidance, see [Implement security recommendations](implement-security-recommendations).
8. Respond to the related alerts. For guidance, see [Respond to a security alert](manage-respond-alerts#respond-to-a-security-alert).