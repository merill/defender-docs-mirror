---
layout: Conceptual
title: Manage licenses for Microsoft Defender for IoT in the Microsoft Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/manage-license
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to size, purchase, and update Defender for IoT licenses in the Microsoft Defender portal, including upgrading from a trial to a permanent license.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7ee3642a-bb10-46c4-736d-679cf6a75d19
document_version_independent_id: 7ee3642a-bb10-46c4-736d-679cf6a75d19
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/manage-license.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-license
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/manage-license.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0ae8296f-c0ad-a888-4d20-067804bd286e
---

# Manage licenses for Microsoft Defender for IoT in the Microsoft Defender portal - Microsoft Defender for IoT | Microsoft Learn

After setting up a license for Microsoft Defender for IoT, you can manage and update it as needed. To purchase the correct license, you need to know the total number of devices within your network so that you can choose the correct sized license for your network.

This article shows how to make changes to your license, including the steps to choose the best size license to purchase.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Calculate the number of IoT devices for licensing

To calculate the number of devices in your network:

1. In the [Microsoft Defender portal](https://security.microsoft.com/machines) menu, select **Assets &gt; Devices**. The device inventory opens.
2. Select the **IoT/OT devices** tab. Note down the total number of devices listed. In this example there are 816 IoT/OT devices detected.

    [![Screenshot showing the list of OT devices in the device inventory for caluculating the total number of devices at the site.](media/manage-licenses/calculate-ot-devices.png)](media/manage-licenses/calculate-ot-devices.png#lightbox)

## Select a Defender for IoT license size in the Microsoft 365 admin center

Purchase the license for your network from the [Microsoft 365 admin center](/en-us/microsoft-365/commerce/licenses/buy-licenses), ensuring it covers enough devices for your site needs.

1. Go to the Microsoft 365 admin center **Billing &gt; Purchase services**. If **Purchase services** isn't available, select **Marketplace** instead.
2. Search for Defender for IoT.
3. Choose the license appropriate for the size of your site. There are five different sized licenses ranging from Extra-large for up to 5,000 devices, to extra-small covering a maximum of 100 devices.

    Make sure to select the number of licenses you want to purchase based on the number of sites you're monitoring. You might need to select licenses of different sizes if the number of devices at each site is different.
4. Complete the purchasing instructions.