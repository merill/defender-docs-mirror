---
layout: Conceptual
title: Quickly configure Microsoft Teams protection in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-support-teams-quick-configure
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
description: Admins who aren't using Microsoft Defender for Office 365 can learn how to quickly set up protection in Microsoft Teams.
ms.service: defender-office-365
ms.date: 2026-04-07T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 0bb7413c-fe3f-8584-049e-2d240f7c6862
document_version_independent_id: 0bb7413c-fe3f-8584-049e-2d240f7c6862
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-support-teams-quick-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-support-teams-quick-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-support-teams-quick-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 86d834c1-00a6-a8d8-77b2-46d58a18ad94
---

# Quickly configure Microsoft Teams protection in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Even if you aren't using Microsoft Defender for Office 365 for email protection, you can still use it for Microsoft Teams protection.

This article contains the quick steps to turn on and configure Defender for Office 365 protection for Microsoft Teams.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions) and [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - Membership in the **Organization Management** or **Security Administrator** role groups in Email & collaboration permissions and membership in the **Organization Management** role group in Exchange Online permissions.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ or **Security Administrator** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- Allow up to 30 minutes for a new or updated policy to be applied.
- For more information about licensing requirements, see [Licensing terms](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description#licensing-terms).
- Teams integration deployment is part of the overall deployment process of Defender for Office 365. For more information, see [Pilot and deploy Defender for Office 365](/en-us/defender-xdr/pilot-deploy-defender-office-365?toc=%2Fdefender-office-365%2FTOC.json&amp;bc=%2Fdefender-office-365%2Fbreadcrumb%2Ftoc.json).
- Users are also protected with near real-time warnings for known bad links in Microsoft Teams messages, which is on by default. For more information, see [Microsoft Defender for Office 365 support for Microsoft Teams](mdo-support-teams-about).

## Step 1: Verify Safe Attachments integration for Microsoft Teams

For complete instructions, see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure).

1. In the Microsoft Defender portal, go to the **Safe Attachments** page at https://security.microsoft.com/safeattachmentv2.
2. On the **Safe Attachments** page, select ![](media/defender-portal-icon-gear.png)**Global settings**.
3. In the **Global settings** flyout that opens, go to the **Protect files in SharePoint, OneDrive, and Microsoft Teams** section to verify **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

Tip

- You can't restrict Safe Attachments for SharePoint, OneDrive, and Microsoft Teams to Microsoft Teams only.
- You can't scope Safe Attachments for SharePoint, OneDrive, and Microsoft Teams to specific users. It's on or off for everyone.

## Step 2: Verify Safe Links integration for Microsoft Teams

For complete instructions, see [Use the Microsoft Defender portal to modify custom Safe Links policies](safe-links-policies-configure#use-the-microsoft-defender-portal-to-modify-custom-safe-links-policies).

1. In the Microsoft Defender portal, go to the **Safe Links** page at https://security.microsoft.com/safelinksv2.
2. On the **Safe Links** page, verify Teams integration is turned on in any custom policies (policies with a numerical **Priority** value) by doing the following steps:

    1. Select the policy by clicking anywhere in the row other than the check box next to the first column.
    2. In the **Teams** section of the **Protection settings** section in the details flyout that opens, verify the value is **On: Safe Links checks a list of known, malicious links when users click links in Microsoft Teams. URLs are not rewritten**.

        If the value is **Off**, select **Edit protection settings** at the bottom of the **Protection settings** section. In the **URL & click protection settings** flyout that opens, select the check box in the **Teams** section, select **Save**, and then select **Close**.

    Repeat these steps on every custom Safe Links policy.

Important

Teams integration is on in the [Built-in protection preset security policy](preset-security-policies), but any other Safe Links policies [take precedence](preset-security-policies#order-of-precedence-for-preset-security-policies-and-other-threat-policies) over the Built-in protection preset security policy (as shown in the order they're listed on the **Safe Links** page). So, ensure that Teams protection is enabled in these policies.

## Step 3: Defender for Office 365: Verify Zero-hour auto purge (ZAP) for Microsoft Teams

For complete instructions, see [Configure ZAP for Teams protection in Defender for Office 365](mdo-support-teams-about#configure-zap-for-teams-protection-in-defender-for-office-365).

1. In the Microsoft Defender portal, go to the **Microsoft Teams protection** page at https://security.microsoft.com/securitysettings/teamsProtectionPolicy.
2. On the **Microsoft Teams protection** page, verify the toggle in the **Zero-hour auto purge (ZAP)** section is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

Tip

When ZAP for Microsoft Teams is turned on, you can use **Exclude these participants** on the **Microsoft Teams protection** page to exclude users from Teams protection. For more information, see [Configure ZAP for Teams protection in Defender for Office 365](mdo-support-teams-about#configure-zap-for-teams-protection-in-defender-for-office-365).

## Step 4: Defender for Office 365: Configure user reported settings for Microsoft Teams

For complete instructions, see [User reported settings in Microsoft Teams](submissions-teams).

1. In the Teams admin center, go to the **Settings & policies** page at https://admin.teams.microsoft.com/one-policy/settings.
2. On the **Settings & policies** page, select either the **Global (Org-wide) default settings** tab for all users or **Custom policies for users & groups** for specific users.
3. On the tab, go to the **Messaging** section and select **Messaging**. If you selected the **Custom policies for users & groups** tab in the previous step, do one of the following steps to edit the specific policy:

    - Click on the policy name in the **Name** column.
    - Click anywhere in the row other than the **Name** column, and then select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
4. In the policy details page that opens, find the **Report a security concern** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the 'Report a security concern' toggle in Messaging policies in the Teams admin center.](media/submissions-teams-turn-on-off-tac-security-risk.png)](media/submissions-teams-turn-on-off-tac-security-risk.png#lightbox)
5. In the Teams admin center, go to the **Messaging settings** page at https://admin.teams.microsoft.com/messaging/settings.
6. On the **Messaging settings** page, go to the **Messaging safety** section, find the **Report incorrect security detections** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the Report incorrect security detections toggle on the Messaging settings page in the Microsoft Teams admin center.](media/submissions-teams-turn-on-off-tac-not-security-risk.png)](media/submissions-teams-turn-on-off-tac-not-security-risk.png#lightbox)
7. In the Teams admin center, go to the **Calling settings** page at https://admin.teams.microsoft.com/one-policy/settings/calling.
8. On the **Calling settings** page, go to the **General** section, find the **Report a call** toggle, and verify the value is ![](media/scc-toggle-on.png)**On**.

    If the value is ![](media/scc-toggle-off.png)**Off**, move the toggle to ![](media/scc-toggle-on.png)**On**, and then select **Save**.

    [![Screenshot of the 'Report a call toggle on the Call settings page in the Microsoft Teams admin center.](media/submissions-teams-turn-on-off-tac-security-risk-call.png)](media/submissions-teams-turn-on-off-tac-security-risk-call.png#lightbox)
9. In the Microsoft Defender portal, go to the **User reported settings** page at https://security.microsoft.com/securitysettings/userSubmission.
10. On the **User reported settings** page, go to the **Microsoft Teams** section, and verify **Monitor reported items in Microsoft Teams** is selected.

If it's not selected, select the check box, and then select **Save**.