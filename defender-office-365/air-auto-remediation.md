---
layout: Conceptual
title: Automated remediation in AIR - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-auto-remediation
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Learn about automated remediation in automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2.
ms.date: 2025-12-15T00:00:00.0000000Z
ms.custom:
- air
- sfi-image-nochange
ms.service: defender-office-365
locale: en-us
document_id: ada15b0f-c870-772c-14b7-297ed0939525
document_version_independent_id: ada15b0f-c870-772c-14b7-297ed0939525
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-auto-remediation.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-auto-remediation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-auto-remediation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 12a7619c-8592-c44b-9f93-2f5d055afdc0
---

# Automated remediation in AIR - Microsoft Defender for Office 365 | Microsoft Learn

By default, remediation actions identified by automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2 require approval by security operations (SecOps) teams. For more information about AIR, see [Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2](air-about)

Now, admins can also designate certain actions to automatically remediate. Automatically remediating messages identified as malicious in AIR investigations has the following benefits:

- Increases customer protection by expediting remediation of more threats.
- Saves time for SecOps teams by reducing the need for approval.

The rest of this article describes how to configure automated remediation in AIR and how to identify messages that were automatically remediated.

## Configure automated remediation

AIR creates a cluster around a detected malicious file or URL, and then the automated investigation checks the location of messages within the cluster. If the messages are in mailboxes, AIR produces a remediation action.

After you select the cluster types to automatically remediate, the selected remediation action occurs without the need for SecOps approval.

Tip

Clusters produced by AIR that don't automatically remediate still show as **Pending action** as they do today.

Clusters larger than 10,000 messages don't automatically remediate and show as **Pending action** for review.

Use the following steps to select the cluster types to automatically remediate:

In the Microsoft Defender portal at https://security.microsoft.com, go to **Settings** &gt; **Email & collaboration** &gt; **MDO automation settings**. Or, to go directly to the **Automation settings** page, use https://security.microsoft.com/securitysettings/mdoAutomationSettings.

The following settings are available on the **Automation settings** page:

- **Message clusters** section: Specifies the types of message clusters that are automatically remediated. Choose one or more of the following options:

    - **Similar files:** When the automated investigation recognizes a malicious file, it creates a cluster around the malicious file. The cluster groups all messages that contain the file into the cluster. Selecting this setting opts the organization in to automated remediation for these malicious file clusters.
    - **Similar URLs:** When the automated investigation recognizes a malicious URL, it creates a cluster around the malicious URL. The cluster groups all messages that contain the URL into the cluster. Selecting this setting opts the organization in to automated remediation for these malicious URL clusters.
    - **Multiple similar attributes**: Messages that share various attributes, such as subject or sender IP address. The automated investigation creates queries (clusters) of email using various attributes from the original email: sender values (IP address, sender domain) and contents (subject, cluster ID) to find email that might be related. he following similarity clusters that are created:

        - BodyFingerprintBin1/SenderIp
        - BodyFingerprintBin1/P2SenderDomain
        - Subject/P2SenderDomain
        - Subject/SenderIp

        Selecting this setting opts your organization into automated remediation if these clusters are found to be malicious.
- **Remediation action** section: Specifies the action to take on message cluster types specified in the **Message clusters** section.

    Currently, **Soft delete** is the only available action. For more information about soft deleted messages, see [Recoverable Items folder in Exchange Online](/en-us/exchange/security-and-compliance/recoverable-items-folder/recoverable-items-folder).

    Important

    The ability to recover soft deleted messages depends on the retention policy for soft deleted messages in each mailbox. Verify your legal obligations for email retention, including messages marked as malicious. For more information on the retention of soft deleted messages, see [Change how long permanently deleted items are kept for an Exchange Online mailbox in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention).

When you're finished on the **Automation settings** page, select **Save**.

[![Screenshot of automated remediation of malicious entity clusters configuration in the Defender portal at Settings \&gt; Email &amp; collaboration \&gt; MDO automation settings.](media/auto-air-mdo-automation-settings.png)](media/auto-air-mdo-automation-settings.png#lightbox)

## Review automatically remediated messages

The following subsection shows how to use the Defender portal to review automated remediation actions.

### Automated remediation results in the Action center

In the Action center at https://security.microsoft.com/action-center/, automatically remediated clusters appear on the **History** tab. Use the **Decided by** filter with the value **Automation** to return clusters that were automatically remediated.

For more information about the Action center, see [The Action center](/en-us/defender-xdr/m365d-action-center).

[![Screenshot of the History tab in the Action center with automatically remediated clusters filtered by the Decided by value Automation and the Action source value Automated email action.](media/auto-air-mdo-action-center.png)](media/auto-air-mdo-action-center.png#lightbox)

### Automated remediation results in investigations

Within an investigation in AIR, automatically remediated clusters appear on the **Pending action history** tab of the investigation with the **Handled by** value **Automation**.

For more information about AIR investigation results, see [Details and results of automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2](air-view-investigation-results).

[![Screenshot of the Pending actions history tab of an investigation with automatically remediated clusters with the Handled by value Automation.](media/auto-air-mdo-investigations.png)](media/auto-air-mdo-investigations.png#lightbox)

### Automated remediation results in Threat Explorer

In Threat Explorer (Explorer), automatically remediated messages have the **Additional action** value **Automated remediation:automated**.

For more information about Threat Explorer, see [About Threat Explorer and Real-time detections in Microsoft Defender for Office 365](threat-explorer-real-time-detections-about).

[![Screenshot of Threat Explorer showing messages that automated remediation deleted from the mailbox by automated remediation (filtered by the Additional action value Automated remediation).](media/auto-air-mdo-threat-explorer.png)](media/auto-air-mdo-threat-explorer.png#lightbox)

### Automated remediation results in Advanced hunting

In Advanced hunting, automatically remediated messages are in the `EmailPostDeliveryEvents` table with both of the following property values:

- `ActionType` equals **Automated Remediation**
- `ActionTrigger` equals **Automation**.

For more information about Advanced hunting, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-overview).

[![Screenshot of Advanced hunting for messages removed from mailboxes by automated remediation (EmailPostDeliveryEvents table where the ActionType value is Automated Remediation and the ActionTrigger value is Automation.)](media/auto-air-mdo-advanced-hunting.png)](media/auto-air-mdo-advanced-hunting.png#lightbox)

## Revert automated remediation actions on messages

Note

The ability to recover messages depends on the data still being available in Defender and the mailbox retention settings for soft deleted messages. For more information, see the following articles:

- [Data retention information for Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-data-retention)
- [Recoverable Items folder in Exchange Online](/en-us/exchange/security-and-compliance/recoverable-items-folder/recoverable-items-folder)
- [Change how long permanently deleted items are kept for an Exchange Online mailbox in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/change-deleted-item-retention)

The following methods are available to revert automated remediation actions and restore messages to mailboxes:

- ![](media/defender-portal-icon-take-actions.png)**Take action** on the message in Threat Explorer or Advanced Hunting. For information about the **Take action** wizard, see [The Take action wizard](threat-explorer-threat-hunting#the-take-action-wizard).
- The **Move to Inbox** or ![](media/defender-portal-icon-more-actions.png) &gt; **Move to Junk** actions in the cluster property details flyout on **History** tab of the Action center as shown in the following screenshot:

    [![Screenshot of the details flyout of an automatically remediated email cluster showing the available Move to Inbox action to undo the automated remediation action and restore messages to mailboxes.](media/auto-air-mdo-action-center-cluster-details.png)](media/auto-air-mdo-action-center-cluster-details.png#lightbox)