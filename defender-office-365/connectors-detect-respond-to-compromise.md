---
layout: Conceptual
title: Respond to a compromised connector in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/connectors-detect-respond-to-compromise
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- sfi-image-nochange
description: Learn how to recognize and respond to a compromised connector in Microsoft 365.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 547c3de3-989b-67bb-25d2-40e6a75fc5d9
document_version_independent_id: 547c3de3-989b-67bb-25d2-40e6a75fc5d9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/connectors-detect-respond-to-compromise.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connectors-detect-respond-to-compromise
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/connectors-detect-respond-to-compromise.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: afcc2a02-30e3-44ad-e88e-a89f133d3323
---

# Respond to a compromised connector in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Connectors are used for enabling mail flow between Microsoft 365 and email servers that you have in your on-premises environment. For more information, see [Configure mail flow using connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow).

An inbound connector with the **Type** value `OnPremises` is considered compromised when an attacker creates a new connector or modifies and existing connector to send spam or phishing email.

This article explains the symptoms of a compromised connector and how to regain control of the connector.

## Symptoms of a compromised connector

A compromised connector exhibits one or more of the following characteristics:

- A sudden spike in outbound mail volume.
- A mismatch between the `5321.MailFrom` address (also known as the **MAIL FROM** address, P1 sender, or envelope sender) and the `5322.From` address (also known as the From address or P2 sender) in outbound email. For more information about these senders, see [How Microsoft 365 validates the From address to prevent phishing](anti-phishing-from-email-address-validation#an-overview-of-email-message-standards).
- Outbound mail sent from a domain that isn't provisioned or registered.
- The connector is blocked from sending or relaying mail.
- The presence of an inbound connector that wasn't created by an admin.
- Unauthorized changes in the configuration of an existing connector (for example, the name, domain name, and IP address).
- A recently compromised admin account. Creating or editing connectors requires admin access.

If you see any of the preceding signs of connector compromise or other unusual symptoms, you should investigate.

## Secure and restore email function to a suspected compromised connector

Do **all** of the following steps to regain control of a compromised inbound connector. Go through the steps as soon as you suspect a problem and as quickly as possible to make sure that the attacker doesn't resume control of the connector. These steps also help you remove any back-door entries that the attacker might have added to the connector.

### Step 1: Identify if an inbound connector has been compromised

To confirm whether a connector is compromised, review recent suspicious connector traffic or related messages and investigate and validate connector-related activity.

#### Review recent suspicious connector traffic or related messages

Tip

The Explorer view in the following procedure requires [Microsoft Defender for Office 365 Plan 2](mdo-about). If you don't have Plan 2, skip to the **Alerts** and **Message trace** procedure later in this section.

In [Microsoft Defender for Office 365 Plan 2](mdo-about), open the Microsoft Defender portal at https://security.microsoft.com and go to **Explorer**. Or, to go directly to the **Explorer** page, use https://security.microsoft.com/threatexplorer.

1. On the **Explorer** page, verify that the **All email** tab is selected and then configure the following options:

    - Select the date/time range.
    - Select **Connector**.
    - Enter the connector name in the ![](media/defender-portal-icon-search.png)**Search** box.
    - Select **Refresh**.

    [![Inbound connector explorer view](media/connector-compromise-explorer.png)](media/connector-compromise-explorer.png#lightbox)
2. Look for abnormal spikes or dips in email traffic.

    [![Number of emails delivered to junk folder](media/connector-compromise-abnormal-spike.png)](media/connector-compromise-abnormal-spike.png#lightbox)
3. Answer the following questions:

    - Does the **Sender IP** match your organization's on-premises IP address?
    - Were a significant number of recent messages sent to the **Junk Email** folder? This result clearly indicates that a compromised connector was used to send spam.
    - Is it reasonable for the message recipients to receive email from senders in your organization?

    [![Sender IP and your organization's on-prem IP address](media/connector-compromise-sender-ip.png)](media/connector-compromise-sender-ip.png#lightbox)

In [Microsoft Defender for Office 365](mdo-about) or [the built-in security features for all cloud mailboxes](eop-about), use **Alerts** and **Message trace** to look for the symptoms of connector compromise:

1. Open the Defender portal at https://security.microsoft.com and go to **Incidents & alerts** &gt; **Alerts**. Or, to go directly to the **Alerts** page, use https://security.microsoft.com/alerts.
2. On the **Alerts** page, use the ![](media/defender-portal-icon-filter.png)**Filter** &gt; **Policy** &gt; **Suspicious connector activity** to find any alerts related to suspicious connector activity.
3. Select a suspicious connector activity alert by clicking anywhere in the row other than the check box next to the name. On the details page that opens, select an activity under **Activity list**, and copy the **Connector domain** and **IP address** values from the alert.

    [![Connector compromise outbound email details](media/connector-compromise-outbound-email-details.png)](media/connector-compromise-outbound-email-details.png#lightbox)
4. Open the Exchange admin center at https://admin.exchange.microsoft.com and go to **Mail flow** &gt; **Message trace**. Or, to go directly to the **Message trace** page, use https://admin.exchange.microsoft.com/#/messagetrace.

    On the **Message trace** page, select the **Custom queries** tab, select ![](media/defender-portal-icon-create.png)**Start a trace**, and use the **Connector domain** and **IP address** values from the previous step.

    For more information about message trace, see [Message trace in the modern Exchange admin center in Exchange Online](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac).

    [![New message trace flyout](media/connector-compromise-new-message-trace.png)](media/connector-compromise-new-message-trace.png#lightbox)
5. In the message trace results, look for the following information:

    - A significant number of messages were recently marked as **FilteredAsSpam**. This result clearly indicates that a compromised connector was used to send spam.
    - Whether it's reasonable for the message recipients to receive email from senders in your organization

    [![New message trace search results](media/connector-compromise-message-trace-results.png)](media/connector-compromise-message-trace-results.png#lightbox)

#### Investigate and validate connector-related activity

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), replace &lt;StartDate&gt; and &lt;EndDate&gt; with your values, and then run the following command to search the audit log for inbound connector creation, modification, and removal events. For more information, see [Use a PowerShell script to search the audit log](/en-us/purview/audit-log-search-script).

```powershell
Search-UnifiedAuditLog -StartDate "<StartDate>" -EndDate "<EndDate>" -Operations "New-InboundConnector","Set-InboundConnector","Remove-InboundConnector"
```

For detailed syntax and parameter information, see [Search-UnifiedAuditLog](/en-us/powershell/module/exchangepowershell/search-unifiedauditlog).

### Step 2: Review and revert unauthorized change(s) in a connector

Open the Exchange admin center at https://admin.exchange.microsoft.com and go to **Mail flow** &gt; **Connectors**. Or, to go directly to the **Connectors** page, use https://admin.exchange.microsoft.com/#/connectors.

On the **Connectors** page, review the list of connectors. Remove or turn off any unknown connectors, and check each connector for unauthorized configuration changes.

### Step 3: Unblock the connector to re-enable mail flow

After you've regained control of the compromised connector, unblock the connector on the **Restricted entities** page in the Defender portal. For instructions, see [Remove blocked connectors from the Restricted entities page](connectors-remove-blocked).

### Step 4: Investigate and remediate potentially compromised admin accounts

After you identify the admin account that was responsible for the unauthorized connector configuration activity, investigate the admin account for compromise. For instructions, see [Responding to a Compromised Email Account](responding-to-a-compromised-email-account).