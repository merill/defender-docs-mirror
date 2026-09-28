---
layout: Conceptual
title: Advanced hunting example for Microsoft Defender for Office 365 - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-email-threats
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Get started searching for email threats using advanced hunting
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-03-28T00:00:00.0000000Z
locale: en-us
document_id: 438bab80-38c5-1eb5-d4e4-321697728d77
document_version_independent_id: 438bab80-38c5-1eb5-d4e4-321697728d77
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-email-threats.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-email-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-email-threats.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 55b78f16-2e10-bada-f121-ddc4e4a8afaf
---

# Advanced hunting example for Microsoft Defender for Office 365 - Microsoft Defender XDR | Microsoft Learn

Want to get started searching for email threats using advanced hunting? Try these steps:

The [Microsoft Defender for Office 365 deployment guide](/en-us/defender-office-365/mdo-deployment-guide) explains how to jump right in and get configuration going on Day 1.

Depending on your [preset security policy vs. custom policy choices](/en-us/defender-office-365/mdo-deployment-guide#determine-your-protection-policy-strategy), **Zero-Hour auto purge** (ZAP) settings are important to know if a malicious message was removed from a mailbox after delivery.

Quickly navigating to Kusto query language to hunt for issues is an advantage of converging these two security centers. Security teams can monitor ZAP misses by taking their next steps in the Microsoft Defender portal at https://security.microsoft.com &gt; **Hunting** &gt; **Advanced Hunting**.

1. On the **Advanced Hunting page** at https://security.microsoft.com/v2/advanced-hunting, verify the **New Query** tab is selected.
2. Copy the following query into the **Query** box:

    ```kusto
    EmailPostDeliveryEvents 
    | where Timestamp > ago(7d)
    //List malicious emails that were not zapped successfully
    | where ActionType has "ZAP" and ActionResult == "Error"
    | project ZapTime = Timestamp, ActionType, NetworkMessageId , RecipientEmailAddress 
    //Get logon activity of recipients using RecipientEmailAddress and AccountUpn
    | join kind=inner IdentityLogonEvents on $left.RecipientEmailAddress == $right.AccountUpn
    | where Timestamp between ((ZapTime-24h) .. (ZapTime+24h))
    //Show only pertinent info, such as account name, the app or service, protocol, the target device, and type of logon
    | project ZapTime, ActionType, NetworkMessageId , RecipientEmailAddress, AccountUpn, 
    LogonTime = Timestamp, AccountDisplayName, Application, Protocol, DeviceName, LogonType
    ```
3. Select **Run query**.

    [![The Advanced hunting page (under Hunting) with Query selected at the top of the query panel, and running a Kusto query to capture ZAP actions over the last seven days.](media/advanced-hunting-email-threats/ah-query-example-new.png)](/en-us/defender/media/ah-query-example-new.png#lightbox)

    The data from this query appears in the **Results** panel below the query itself. Results include information like `DeviceName`, `AccountDisplayName`, and `ZapTime` in a customizable result set. Results can also be exported for your records. To save the query for reuse, select **Save** &gt; **Save As** to add the query to your list of queries, shared, or community queries.

## Related information

- [Advanced hunting best practices](advanced-hunting-best-practices)
- [Overview - Advanced hunting](advanced-hunting-overview)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).