---
layout: Conceptual
title: Track and respond to emerging security threats with campaigns view in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/track-and-respond-to-emerging-threats-with-campaigns
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Walkthrough of threat campaigns within Microsoft Defender for Office 365 to demonstrate how they can be used to investigate a coordinated email attack against your organization.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: f1ba84e2-c745-88cb-99ab-bb9023022b96
document_version_independent_id: f1ba84e2-c745-88cb-99ab-bb9023022b96
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/track-and-respond-to-emerging-threats-with-campaigns.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/track-and-respond-to-emerging-threats-with-campaigns
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/track-and-respond-to-emerging-threats-with-campaigns.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 2bcf0d86-9fdb-8fd9-0235-8ed71753dd97
---

# Track and respond to emerging security threats with campaigns view in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

## Investigate coordinated email attacks using campaigns

Campaigns can be used to track and respond to emerging threats because campaigns allow you to investigate a coordinated email attack against your organization. As new threats target your organization, Microsoft Defender for Office 365 will automatically detect and correlate malicious messages.

## Prerequisites

- Microsoft Defender for Office 365 Plan 2 (included in E5 plans).
- Sufficient permissions (Security Reader role).
- Five to ten minutes to perform these steps.

## What is a campaign in Microsoft Defender for Office 365

A campaign is a coordinated email attack against one or many organizations. Email attacks that steal credentials and company data are a large and lucrative industry. As technologies to stop attacks grow and multiply, attackers modify their methods to continue their success.

Microsoft leverages vast amounts of anti-phishing, anti-spam, and anti-malware data across the entire service to help identify campaigns. We analyze and classify the attack information according to several factors, for example:

- **Attack source**: The source IP addresses and sender email domains.
- **Message properties**: The content, style, and tone of the messages.
- **Message recipients**: How recipients are related, for example, recipient domains, recipient job functions (such as admins and executives), company types (such as large, small, public, and private), and industries.
- **Attack payload**: Malicious links, attachments, or other payloads in the messages.

A campaign might be short-lived, or could span several days, weeks, or months with active and inactive periods. A campaign might be launched against your specific organization, or your organization might be part of a larger campaign across *multiple* companies.

Tip

To learn more about the data available within a campaign, read [Campaign Views in Microsoft Defender for Office 365](../campaigns).

## Watch the *Exploring campaign views* video

Watch the following video for an overview of campaign views in Microsoft Defender for Office 365.

## Download a campaign threat report

In the event that a campaign has targeted your organization and you'd like to learn more about the impact:

1. Navigate to the [Campaigns page in Microsoft Defender](https://security.microsoft.com/campaigns).
2. Select the campaign name that you would like to investigate.
3. Upon the flyout opening, select **Download threat report**.
4. Open the threat report and it will provide more information surrounding the campaign. The information in the report includes:
    - **Executive summary:** High-level summary of the type of campaign and the number of users targeted in your organization.
    - **Analysis:** Timeline chart of when the campaign started, the count of messages targeting your organization, and the destination and verdicts of the messages.
    - **Attack origin:** Top sending IP addresses and domains with a count of messages that were delivered to inboxes in your organization. This attack-origin data allows you to investigate who is targeting your organization.
    - **Email template and payload:** The subject line of the emails that were part of the campaign and URLs (and their frequency) present as part of the campaign.
    - **Recommendations:** Recommendations for next steps to remediate messages.

## Investigate inboxed messages that are part of an email threat campaign

1. Navigate to the [Campaigns page in Microsoft Defender](https://security.microsoft.com/campaigns).
2. Scroll through the list of campaigns in the **Details view**, below the graph.
3. Select the campaign name you want to investigate. If the campaign has a click count of more than zero, that indicates that a user in your organization clicked on a URL or downloaded a file from the email.
4. The campaign flyout displays more information about the campaign, the graph displays a timeline of the campaign from campaign start to end date, and the horizontal flow diagram displays the stages of the campaign from its origin, the verdict, and the current location of the messages.
5. Below the flow diagram, select the **URL clicks** tab to display information regarding the click. On the **URL clicks** tab, you can see the user that clicked on a URL, if the user is tagged as a priority account user, the URL itself, and the time of click.
6. If you want to learn more about the inboxed and clicked messages, select **Explore messages** &gt; **Inboxed messages**. A new tab will open and navigate to Threat Explorer.
7. In the **details view** of Explorer you can reference **Latest delivery** to determine if a message is still in the inbox or was moved into quarantine by system ZAP. *To get more details about the specific message, select the message. The flyout provides extra information. Upon selecting the **Open email entity page** on the top left of the flyout, a new tab will open and give you further information about the message.*
8. If you would like to take an action and move the messages out of the inbox, you can select the message and then select ![](../media/defender-portal-icon-take-actions.png)**Take action** &gt; **Move to junk folder**. Moving the message to the Junk Email folder helps ensure the user doesn't continue to interact with the malicious message, which could result in a potential breach.