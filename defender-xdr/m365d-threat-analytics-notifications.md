---
layout: Conceptual
title: Get email notifications for Threat analytics updates - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-threat-analytics-notifications
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Set up email notifications to get notified of new Threat analytics reports in Microsoft Defender XDR.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
ms.topic: how-to
ms.custom: seo-marvel-apr2020, msecd-doc-authoring-1014
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d6d6736b-4732-2f21-a6f9-edbb7da80167
document_version_independent_id: d6d6736b-4732-2f21-a6f9-edbb7da80167
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-threat-analytics-notifications.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-threat-analytics-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-threat-analytics-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 2ba7e37f-3c66-d924-f1e2-d6495cd9a960
---

# Get email notifications for Threat analytics updates - Microsoft Defender XDR | Microsoft Learn

You can set up email notifications that send you updates on [threat analytics](threat-analytics) reports. These notifications alert security administrators and analysts when new threat analytics reports are published or existing reports are updated in Microsoft Defender XDR. This article walks you through creating a notification rule, choosing which report types or tags to track, and adding recipients.

## Set up email notifications for report updates

To set up email notifications for threat analytics reports, perform the following steps:

1. In the navigation pane of the Microsoft Defender portal, select **Settings &gt; Microsoft Defender XDR**. Under **General**, select **Email notifications**.
2. In the **Threat analytics** tab, select **+ Create a notification rule**. A flyout appears.
3. Follow the steps listed in the flyout. First, give your new rule a name. The description field is optional, but a name is required. You can toggle the rule on or off using the checkbox under the description field.

    Note

    The name and description fields for a new notification rule only accept English letters and numbers. Punctuations like spaces, dashes, underscores, aren't supported.

    ![Screenshot of the notification rule naming step with rule details entered and the rule enabled](media/m365d-threat-analytics-notifications/ta_create_notification_2.png)
4. Choose the reports you want to be notified about. You can choose to be updated about all newly published or updated reports or only those reports of a certain type or with a specific tag.

    ![Screenshot of the notification configuration step with Ransomware tags selected and notification types available for selection](media/m365d-threat-analytics-notifications/ta_create_notification_3.png)
5. Add at least one recipient to receive the notification emails. You can also use this screen to send a test email to check the notification settings.

    ![Screenshot of the recipients step showing three recipients and confirmation that a test email was sent](media/m365d-threat-analytics-notifications/ta_create_notification_4.png)
6. Review your new rule. Select **Edit** at the end of each subsection to change any of the settings. Once your review is complete, select **Create rule**.

    ![Screenshot of the review step showing the option to edit the notification rule before creation](media/m365d-threat-analytics-notifications/ta_create_notification_5.png)
7. Select **Done** to complete the process and close the flyout.

    ![Screenshot of the rule created screen showing green checkmarks along the sidebar and a green check in the main area](media/m365d-threat-analytics-notifications/ta_create_notification_6.png)

Your new rule now appears in the list of Threat analytics email notifications.