---
layout: Conceptual
title: Respond to and mitigate threats in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-respond-mitigate-threats
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to investigate, respond to, and mitigate detected threats in Microsoft Defender for Business through an example workflow in the Defender portal.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b1a6ce9c-7cdf-f5fb-df13-674aea178fa8
document_version_independent_id: b1a6ce9c-7cdf-f5fb-df13-674aea178fa8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-respond-mitigate-threats.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-respond-mitigate-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-respond-mitigate-threats.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 889ce437-a165-cbce-2df0-3f0096fb9266
---

# Respond to and mitigate threats in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

The Microsoft Defender portal enables your security team to respond to and mitigate detected threats. This article walks you through an example of how you can use Defender for Business to review threat indicators on the Home page, investigate at-risk devices in the device inventory, and take response actions such as running an antivirus scan or initiating an automated investigation.

## View detected threats

Use the following steps to view detected threats in the Microsoft Defender portal and take response actions.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Notice the cards on the Home page. These cards show how many threats were found, how many user accounts were affected, and which devices or other assets are at risk. The following image is an example:

    ![Screenshot of cards in the Microsoft Defender portal](media/mdb-examplecards.png)
3. Select a button or link on a card to view more details. For example, the **Devices at risk** card has a **View details** button. Select the **View details** button to open the **Devices** list, as shown in the following image:

    ![Screenshot of device inventory](media/mdb-device-inventory.png)

    The **Devices** page lists company devices with their risk level and exposure level.
4. Select an item, such as a device. A flyout pane opens with more details about alerts and incidents for the selected device, as shown in the following image:

    ![Screenshot of the flyout pane for a selected device](media/mdb-deviceinventory-selecteddeviceflyout.png)
5. On the flyout, review the details. Select the ellipsis (...) to open a menu of available actions, as shown in the following image:

    ![Screenshot of available actions for a selected device](media/mdb-deviceinventory-selecteddeviceflyout-menu.png)
6. Select an available action. For example, you might choose **Run antivirus scan**, which starts a quick scan with Microsoft Defender Antivirus on the device. Or, you could select **Initiate Automated Investigation** to trigger an automated investigation on the device.