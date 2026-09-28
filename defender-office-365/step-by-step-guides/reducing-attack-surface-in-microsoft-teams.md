---
layout: Conceptual
title: Reduce the Attack Surface for Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/reducing-attack-surface-in-microsoft-teams
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configuration to reduce the attack surface in Microsoft Teams, including enabling Microsoft Defender for Office 365.
ms.service: defender-office-365
author: MSFTBen
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 59e6efdd-d4d7-01a8-2fb4-23876feb2dcf
document_version_independent_id: 59e6efdd-d4d7-01a8-2fb4-23876feb2dcf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/reducing-attack-surface-in-microsoft-teams.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/reducing-attack-surface-in-microsoft-teams
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/reducing-attack-surface-in-microsoft-teams.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 2373668b-f0b7-1110-8980-01cf0df8daee
---

# Reduce the Attack Surface for Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Teams is a widely used collaboration tool, where many users are now spending their time. Attackers know this and are pivoting. The following steps help you reduce the attack surface in Teams and keep your organization more secure.

Important

There is a balance to strike between security and productivity, and not all these steps may be relevant for your organizational risk profile.

## Prerequisites

Make sure you have the following before you begin:

- Microsoft Teams
- Microsoft Defender for Office 365 Plan 1 (for some features)
- Teams admin or Security admin role
- 5-10 minutes to do these steps.

Note

Not all these options will be available for government specific clouds such as Microsoft 365 GCC.

## Turn on Microsoft Defender for Office 365 in Teams

If your organization is licensed for Microsoft Defender for Office 365 (free 90-day evaluation available at aka.ms/trymdo), you can ensure seamless protection from zero-day malware and time-of-click protection within Microsoft Teams.

[Safe Links settings for Microsoft Teams](../safe-links-about#safe-links-settings-for-microsoft-teams) & [Configure Safe Attachments for SharePoint, OneDrive, and Teams](../safe-attachments-for-spo-odfb-teams-configure) (Detailed Documentation)

1. **Login** to the security center's safe attachments configuration page at https://security.microsoft.com/safeattachmentv2.
2. Press **Global settings**.
3. Ensure **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** is set to on.
4. Navigate to the security center's Safe links configuration page at: https://security.microsoft.com/safelinksv2.
5. If you have multiple policies, you'll need to complete this step for each policy (excluding built-in, standard and strict preset policies).
6. **Select** a policy, a flyout appears on the left-hand side.
7. Press **Edit protection settings**.
8. Ensure **Safe Links checks a list of known, malicious links when users click links in Microsoft Teams** is checked.
9. Press **Save**.
10. In organizations with Microsoft Defender for Office 365 Plan 1 or Plan 2, or Microsoft Defender XDR, admins can decide whether users can report malicious messages in Microsoft Teams. For more information, see [User reported settings in Microsoft Teams](../submissions-teams).

## Restrict channel email messages to approved domains

An attacker could email channels directly if they discover the channel email address. The best practice is to have this only setup for known trusted domains rather than open to all (default).

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Teams** and then choose **Teams settings**.
3. Under the **Email integration** heading, choose to allow or disallow users to send emails to a channel email address by toggling **Users can send emails to a channel email address**.
4. If you have allowed users to send emails to a channel email address in the previous step, enter the specific domains you wish to accept mail from in the **Accept channel email from these SMTP domains** box. (for example, an alert provider, or trusted supplier).
5. Press **Save** at the bottom of the page.

## Manage non-Microsoft storage options

Users can store their files in potentially unsupported non-Microsoft storage providers. If you don't use these providers, you can disable this setting to reduce data leakage risk.

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Teams** and then choose **Teams settings**.
3. Under the **Files** heading, choose which storage providers you want to be available for use within the files tab.
4. Press **Save** at the bottom of the page.

## Disable non-Microsoft and custom apps

Applications are a very useful part of Microsoft Teams, but it's recommended to maintain a list of allowed apps rather than allowing all apps by default.

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Teams apps** and then choose **Permission Policies**.
3. If you have custom permission policies, you'll need to complete this procedure for each of them if appropriate, otherwise select **Global (Org-wide default)**.
4. Select the appropriate settings for your organization, a recommended starting point is:
    - Microsoft apps – set to **Allow all apps** (default).
    - Non-Microsoft apps – set to **Allow specific apps and block all others** (if you already have non-Microsoft apps to then select for allowing) otherwise select **Block all apps**.
    - Custom apps – set to **Allow specific apps and block all others** (if you already have custom apps to then select for allowing) otherwise select **Block all apps**.
5. Press **Save**.
6. Repeat these steps for each custom permission policy you've created.

## Configure meeting settings

You can reduce the attack surface by ensuring people outside your organization can't request access to control presenter's screens and require dial in and all external people to be authenticated & admitted from a meeting lobby. [Manage meeting policies for participants and guests](/en-us/microsoftteams/meeting-policies-participants-and-guests).

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Meetings** and then choose **Meeting Policies**.
3. If you've assigned any custom or built-in policies to users, you'll need to complete this meeting policy procedure for each of them if appropriate, otherwise select **Global (Org-wide default)**.
4. Under the **Content sharing** heading, ensure **External participants can give or request control** is set to **off**.
5. Under the **Meeting join & lobby** heading, ensure **People dialing in can bypass the lobby** is set to **off**.
6. Ensure **Anonymous users can join a meeting** is set to **off**.
7. Under the **Meeting engagement** heading, Set **Meeting chat** to **"On for everyone but anonymous users"**.
8. Select **Save**.
9. Repeat this procedure for each policy to apply the external participant, lobby, anonymous join, and meeting chat settings.

## Restrict presenters in Teams meetings

You can reduce the risk of unwanted or inappropriate content being shared during meetings by restricting who can present to Organizers (everyone is allowed to present by default).

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Meetings** and then choose **Meeting Policies**.
3. If you've assigned any custom or built-in policies to users, you'll need to complete this presenter restriction procedure for each of them if appropriate, otherwise select **Global (Org-wide default)**.
4. Under the **Content sharing** heading, set **Who can present** to **Only organizers and co-organizers**.
5. Select **Save**.
6. Repeat this procedure for each policy to set **Who can present**.

## Limit domains for external access

External access lets your users chat with people outside your organization in Teams. This is useful for collaboration, but attackers can also use it to contact your users directly if they know an email address. [Manage external access in Microsoft Teams](/en-us/microsoftteams/manage-external-access)

1. **Login** to the Teams admin center at: https://admin.teams.microsoft.com/.
2. On the left-hand navigation, expand **Users** and then choose **External access**.
3. Under the **Teams and Skype for Business users in external organizations** heading, select the **Choose which external domains your users have access to** dropdown and set this to **Allow only specific external domains**.
4. Enter any external domains users should be able to communicate with by selecting **Allow domains**, using the flyout, and selecting **Done** when finished.
5. Select **Save**.

Note that external organizations must also allow your organization's domain for external access to work.

Tip

You can also create external access policies with domain allow/deny lists and assign them to specific users or groups for more granular control. For more information, see [Manage external access](/en-us/microsoftteams/manage-external-access).