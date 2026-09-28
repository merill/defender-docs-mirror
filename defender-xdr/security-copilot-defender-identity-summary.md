---
layout: Conceptual
title: Summarize identity information with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-copilot-defender-identity-summary
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Summarize an identity information with Microsoft Copilot in Microsoft Defender to investigate identities.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: concept-article
ms.date: 2024-10-14T00:00:00.0000000Z
ms.update-cycle: 180-days
locale: en-us
document_id: dc40cda0-8f38-de9e-84c8-57310fce9ecd
document_version_independent_id: dc40cda0-8f38-de9e-84c8-57310fce9ecd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-copilot-defender-identity-summary.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-defender-identity-summary
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-copilot-defender-identity-summary.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: f0138946-adb4-93e1-be7c-4e49782b344e
---

# Summarize identity information with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Security operations teams investigating users can easily understand identity information with the identity summary capability in [Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) in Microsoft Defender. Through generative AI and harnessing the power of Microsoft Defender for Identity, Copilot creates contextual insights about an identity in an organization, helping analysts quickly understand important data to speed up their investigation.

With the identity summary capability, analysts can immediately identify suspicious or risky identity-related changes and actions that can negatively impact an organization. The summary also includes potential misconfigurations that affect an identity. Using natural language, Copilot delivers clear and actionable user information that analysts can use in their incident investigation activities. The capability currently focuses on users and will include service accounts in its next iteration.

This guide describes what the identity summary capability is and how it works, including how you can provide feedback on the results generated.

## Know before you begin

If you're new to Security Copilot, you should familiarize yourself with it by reading the following articles:

- [What is Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Security Copilot](/en-us/security-copilot/prompting-security-copilot)

With the identity summary capability, analysts can immediately identify suspicious or risky identity-related changes and actions that can negatively impact an organization. The summary also includes potential misconfigurations that affects an identity. Using natural language, Copilot delivers clear and actionable user information that analysts can use in their incident investigation activities. The capability currently focuses on users and will include service accounts in its next iteration.

## Security Copilot integration in Microsoft Defender

The identity summary capability is available in the Microsoft Defender portal for customers who have provisioned access to Security Copilot.

Users who access the Security Copilot standalone portal can use this capability through the Microsoft Defender XDR plugin. Know more about [preinstalled plugins in Security Copilot](/en-us/security-copilot/manage-plugins#preinstalled-plugins).

## Key features

The identity summary contains essential information about an identity, including:

- The date when a user account is created, and whether the user account is of high, medium, or low criticality
- Any unusual behavioral patterns related to sign in locations, sign in frequency, or frequency of failed sign in attempts
- A user's current role, including their department and position, and whether there are notable role changes compared to the user's job title and department to highlight inconsistencies
- Data about a user's last sign in to a device, whether or not the device is associated to the user, in the last 30 days
- Authentication methods and applications used
- Risks associated with a user based on Microsoft Entra ID
- General information like a user's professional title and contact information, department, and their manager's contact information

You can access the identity summary capability in the following ways:

- From an incident page, choose an identity on the incident graph and then (1) select **User details**. In the user details pane, (2) select **Summarize**. The results are displayed in the Copilot side panel.

    [![Screenshot showing the Summarize option in the user details pane.](media/security-copilot-defender-identity-summary/identity-summary-incident-small.png)](media/security-copilot-defender-identity-summary/identity-summary-incident.png#lightbox)
- Alternatively, you can select **Go to user page** on the bottom of the user details pane to open the user page. Copilot automatically generates the identity summary and displays the side panel upon opening the user page.
- You can also access the identity summary capability by choosing a user in the **Assets** tab of an incident. Select **Summarize** in the user details pane to generate the identity summary.

    [![Screenshot showing the Assets tab and a user account highlighted.](media/security-copilot-defender-identity-summary/identity-summary-assets-small.png)](media/security-copilot-defender-identity-summary/identity-summary-assets.png#lightbox)
- In an alert page, select a user then select **Summarize** in the user details pane to generate the identity summary.
- In the advanced hunting page, you can access the identity summary capability by selecting a user in the results table, then selecting the link to the user page. Copilot automatically generates the identity summary and displays the side panel upon opening the user page.
- From the main menu, navigate to **Assets &gt; Identities**. Select a username from the list, then select **View user page** to open the user page. Copilot automatically generates the identity summary and displays the side panel upon opening the user page.

    [![Screenshot highlighting the view user page option in a username search within Identities.](media/security-copilot-defender-identity-summary/identity-summary-viewuser-small.png)](media/security-copilot-defender-identity-summary/identity-summary-viewuser.png#lightbox)
- Type a username in the Microsoft Defender portal's **search box** then select the username from the search results. In the user details side panel, select **Summarize** to generate the identity summary.

Review the identity summary results. You can copy the results to clipboard, regenerate the results, or open Security Copilot by selecting the More actions ellipsis (...) on top of the identity summary card. You can extend your investigation of identity using prompts and other plugins in the Security Copilot portal.

## Sample identity summary prompt

In the Security Copilot standalone portal, you can use the following prompt to generate an identity summary:

- *Show the Defender summary of this user in the last {time frame}.*

Tip

When investigating users in the Security Copilot portal, Microsoft recommends including the word ***Defender*** in your prompts to ensure that the identity summary capability delivers the results. You can specify up to 120 days on the investigation time frame, with the default being 30 days when you don't indicate one.

## Provide feedback

Microsoft highly encourages you to provide feedback to Copilot, as it's crucial for a capability's continuous improvement. To provide feedback, navigate to the bottom of the Copilot side panel and select the feedback icon ![Screenshot of the feedback icon for Copilot in Defender cards](media/copilot-in-defender/create-report/copilot-defender-feedback.png).

![Screenshot that shows the Feedback text box where you can share your feedback.](media/security-copilot-defender-identity-summary/feedback-textbox.png)

Fill in the dedicated text box to share your thoughts, experiences, and requests. Microsoft values your feedback and takes it seriously in our commitment to enhance Copilot's performance and user experience.