---
layout: Conceptual
title: Transition from Report Message or the Report Phishing add-ins - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/submissions-users-report-message-add-in-configure
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.reviewer: dhagarwal
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.localizationpriority: medium
ms.assetid: 4250c4bc-6102-420b-9e0a-a95064837676
ms.collection:
- m365-security
- tier2
description: Migrate from the Report Message and Report Phishing add-ins to the built-in Report button in Outlook, including removal steps, user scoping, and deprecation guidance.
ms.service: defender-office-365
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 18a38582-55af-c1ad-a2d7-309165d0a460
document_version_independent_id: 18a38582-55af-c1ad-a2d7-309165d0a460
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/submissions-users-report-message-add-in-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: submissions-users-report-message-add-in-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/submissions-users-report-message-add-in-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 008add6b-5ee3-f44f-eb43-a66f01c7187c
---

# Transition from Report Message or the Report Phishing add-ins - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Important

The Microsoft Report Message and Report Phishing add-ins are now in maintenance mode and will eventually be deprecated. We recommend transitioning from the add-ins to the built-in **Report** button. The **Report** button is supported in virtually all consumer and enterprise Outlook clients. For more information, see the Frequently asked questions about the deprecation timeline, migration guidance, and the built-in **Report** button capabilities.

The built-in **Report** button in [supported versions of Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook) makes it easy for users to report false positives and false negatives to Microsoft for analysis. False positives are good email that was blocked or sent to the Junk Email folder. False negatives are unwanted email or phishing that was delivered to the Inbox.

Microsoft uses these user reported messages to improve the effectiveness of email protection technologies. For example, suppose people are reporting many messages as phishing using the **Report** button. These phishing reports surface in the Security Dashboard and other reports. A high volume of phishing reports probably indicates that the anti-phishing policies in your organization need to be updated.

Note

When reporting multiple messages or an email thread (conversation) using the built-in **Report** button, each message is submitted as a **separate, individual report** with its own sender, subject, and timestamp.

The following table describes the advantages of the built-in **Report** button over the Report Message and Report Phishing add-ins:

| Benefits | Built-in Report button | Report add-ins |
| --- | --- | --- |
| Works out of the box | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Consistent across consumer and enterprise accounts | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Easily discoverable across Outlook clients | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Front and center across Outlook clients | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Multi-message reporting from Inbox | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Message reporting from preview panel | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Message reporting from reading window | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Message reporting from context menu | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Supports shared and delegate mailboxes^\*^ | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Pre-reporting popup customization | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Pre-reporting popup localization | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Post-reporting popup customization | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Post-reporting popup localization | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |
| Works flawlessly with firewalls | ![](media/feature_present_icon.png) | ![](media/feature_absent_icon.png) |

^\*^User reporting from shared and delegate mailboxes is available in [select supported clients](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook).

To transition away from the add-ins, you can remove the Report Message or Report Phishing add-ins entirely, or scope the add-ins to a set of users during the migration.

## What do you need to know before you begin?

Verify the following permissions and prerequisites before you remove or scope the Report Message or Report Phishing add-ins.

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Security operations/Security data/Response (manage)** or **Security operations/Security data/Read-only**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions): Membership in the **Organization Management** role group.
    - [Exchange Online permissions](/en-us/Exchange/permissions-exo/permissions-exo): Membership in the **Organization Management** role group.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ role gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- The Report Message and Report Phishing add-ins now use Nested app authentication. For more information, see [Nested app auth requirement set](/en-us/javascript/api/requirement-sets/common/nested-app-auth-requirement-sets). If your Outlook client doesn't support the required NAA authentication, we suggest updating clients in the Microsoft admin center or advising users to use the built-in **Report** button.
- For organizational removals, the organization needs to be configured to use OAuth authentication. For more information, see [Determine if Centralized Deployment of add-ins works for your organization](/en-us/Microsoft-365/admin/manage/centralized-deployment-of-add-ins).
- For more information on how to report a message using reporting in Outlook, see [Report false positives and false negatives in Outlook](submissions-outlook-report-messages).

## Remove the Report Message or Report Phishing add-ins

Tip

If you delete the app registration for the add-in in Microsoft Entra ID (formerly Azure Active Directory), you also delete the add-in from the organization.

1. In the Microsoft 365 admin center at https://admin.microsoft.com, expand **Show all** if necessary, and then go to **Settings** &gt; **Integrated apps**. You can also go directly to the **Integrated apps** page via https://admin.microsoft.com/Adminportal/Home#/Settings/IntegratedApps.

    Tip

    Admins in Microsoft 365 GCC High or DoD need to use the Microsoft 365 admin center at https://portal.office365.us/adminportal/home#/Settings/AddIns and then select **Settings** &gt; **Add-ins**.

    Although the screenshots in this procedure show the **Report Phishing** add-in, the steps are identical for the **Report Message** add-in.
2. On the **Deployed apps** tab of the **Integrated apps** page, select the **Report Message** add-in or the **Report Phishing** add-in by clicking anywhere in the row.

[![Screenshot of selecting the Report Phishing add-in on the Integrated apps page in the Microsoft 365 admin center.](media/microsoft-365-admin-center-select-report-phish-add-in.png)](media/microsoft-365-admin-center-select-report-phish-add-in.png#lightbox)
3. On the **Overview** tab of the details flyout that opens, select **Remove app** from the **Actions** section.

[![Screenshot of the Overview tab on the details flyout of the Report Phishing add-in in the Microsoft 365 admin center.](media/microsoft-365-admin-center-report-phish-add-in-details-overview-tab.png)](media/microsoft-365-admin-center-report-phish-add-in-details-overview-tab.png#lightbox)
4. In the **Remove apps** confirmation flyout that opens, select **Yes, I'm sure I want to remove the app and associated data**, and then select **Remove**.

[![Screenshot of the tab on the removal flyout of the Report Phishing add-in in the Microsoft 365 admin center.](media/microsoft-365-admin-center-report-phish-add-in-remove-overview-tab.png)](media/microsoft-365-admin-center-report-phish-add-in-remove-overview-tab.png#lightbox)
5. After a few moments, **Successfully removed** flyout appears. It might take up to 24 hours for the add-in to disappear from your organization.

[![Screenshot of the flyout showing the removal of the Report Phishing add-in in the Microsoft 365 admin center.](media/microsoft-365-admin-center-report-phish-addin-remove-complete-tab.png)](media/microsoft-365-admin-center-report-phish-addin-remove-complete-tab.png#lightbox)

    Select **Done** to return to the **Integrated apps** page where the add-in is no longer listed.

## Scope the Report Message or Report Phishing add-ins to a set of users

Instead of removing the add-ins entirely, you can limit them to specific users or groups during the transition to the built-in **Report** button.

1. In the Microsoft 365 admin center at https://admin.microsoft.com, expand **Show all** if necessary, and then go to **Settings** &gt; **Integrated apps**. Or, to go directly to the **Integrated apps** page, use https://admin.microsoft.com/Adminportal/Home#/Settings/IntegratedApps.

    Tip

    Admins in Microsoft 365 GCC High, or DoD need to use the Microsoft 365 admin center at https://portal.office365.us/adminportal/home#/Settings/AddIns and then select **Settings** &gt; **Add-ins**.

    Although the screenshots in this procedure show the **Report Phishing** add-in, the steps are identical for the **Report Message** add-in.
2. On the **Deployed apps** tab of the **Integrated apps** page, select the **Report Message** add-in or the **Report Phishing** add-in by doing one of the following steps:

    - Select the add-in by clicking anywhere in the row. In the details flyout that opens, select the **Users** tab.
    - In the **Name** column, select **⋮** &gt; **Edit users**.

[![Screenshot of selecting the Report Phishing add-in on the Integrated apps page in the Microsoft 365 admin center.](media/microsoft-365-admin-center-select-report-phish-add-in.png)](media/microsoft-365-admin-center-select-report-phish-add-in.png#lightbox)
3. On the **Users** tab of the details flyout, verify **Specific users/groups** is selected in the **Assign users** section.

    Any existing users or groups are shown in the **Added users** section.

    Click in the search box to find and select users or groups. New selections are added to the **To be added** section that appears.

    To remove a user or group, select ![](media/defender-portal-icon-remove.png) on the entry:

    - From the **Added users** section: The user or group is added to the **To be removed** section that appears.
    - From the **To be added** section: The user or group is removed from this section and won't be added.
    - From the **To be removed** section: The user or group is removed from this section and won't be removed.

    When you're finished on the **Users** tab of the details flyout, select **Update** to save your changes.

[![Screenshot of the Users tab on the details flyout of the Report Message add-in in the Microsoft 365 admin center.](media/microsoft-365-admin-center-report-phish-add-in-details-users-tab.png)](media/microsoft-365-admin-center-report-phish-add-in-details-users-tab.png#lightbox)

    After a few moments, the **Updating users completed** flyout appears. Select **Done** to return to the **Users** tab of the add-in details flyout where your updates are shown in the **Added users** section.

    Select ![](media/defender-portal-icon-remove.png)**Close flyout** to return to the **Integrated apps** page.

## Frequently asked questions

The following questions address common concerns about the add-in deprecation, migration to the built-in **Report** button, and rollout considerations.

### Q: Why are the add-ins being deprecated?

**A**: The add-ins are being deprecated for the following reasons:

- There are security issues with the add-ins that make them unsafe for the organization. Given Microsoft's commitment to safety, they need to be deprecated.
- The add-ins can't architecturally support functionality that customers keep asking for.

Therefore, we decided to move to the built-in **Report** button to better serve your requirements.

### Q: What do we mean by the add-ins are in maintenance mode?

**A**: It means that no improvement will be made to the add-ins. The add-ins will remain functional until they're deprecated. Naturally, any new improvement requests for the add-ins will be rejected.

### Q: Will there be further communication before the add-in are deprecated?

**A**: Yes. There will be further communication as we progress towards the deprecation.

### Q: Some users in my organization are on an older client, which prevents us from migrating. What can I do?

**A**: We recommend you update clients in the Microsoft admin center or ask users to update their clients. Reach out to Microsoft Support if you have issues updating clients for users.

### Q: The Report phishing add-in offers a single report option but the built-in Report button has more options. What can I do?

**A**: This design was finalized after partnership with more than 50 customers and a Private Preview of approximately two and half years. Many customers who had this question are actually much more comfortable with the built-in **Report** button and have transitioned completely to it.

The built-in **Report** button is a split button. Clicking on the button without using the dropdown list reports the message as phishing. Use the dropdown list to report messages as junk or not junk.

We recommend that you try the built-in **Report** button. If you're still facing issues, you can always reach out to us via Microsoft Support.

### Q: I can't scope the built-in Report button, which prevents me from rolling it out. What can I do?

**A**: This behavior is by design. We think the built-in **Report** button provides a base level of protection for all users, including shared and delegate mailboxes. Scoping the built-in **Report** button to a limited number of users can result in forgetting about those users, which leaves a security gap that can be exploited by attackers. Many customers totaling more than a million users migrated smoothly to the built-in **Report** button without scoping ability. Instead, those customers scoped non-Microsoft add-in buttons or the Microsoft add-ins as they rolled out the built-in **Report** button across the organization.

If you're looking to scope the functionality for experimentation, we recommend using a test environment.

### Q: I want to see further improvements in the inbuild report button. What can I do?

**A**: Raise a design change request (DCR) via Microsoft support.

### Q: Is there a way to keep the add-in but remove the built-in Report button?

**A**: No. Because of the security issues and architectural limitations described in Why are the add-ins being deprecated?, the add-ins will be deprecated. There's no way to keep the add-in and remove the built-in **Report** button. To remove the add-in, go to **Settings** &gt; **Integrated apps** in the Microsoft 365 admin center, select the add-in on the **Deployed apps** tab, and then select **Remove app**.

### Q: What is the recommendation for moving from the add-ins to a non-Microsoft reporting add-in?

**A**: After you remove the add-in from the **Deployed apps** tab of the **Integrated apps** page, install the non-Microsoft add-in according to their instructions.

On the [User reported settings page](submissions-user-reported-messages-custom-mailbox) in the Defender portal, you need to do the following steps:

1. Select **Monitor reported messages in Outlook**.
2. Select **Use a non-Microsoft add-in button**.
3. In the **Reported message destination**section, configure the following options:
    - **Send reported messages to**: Select one of the following values:
        - **My reporting mailbox only**
        - **Microsoft and My reporting mailbox**
    - **Add an Exchange Online mailbox to send reported messages to**: Specify an existing internal reporting mailbox to hold user reported messages from the non-Microsoft service.

### Q: I still have questions that aren't answered here. What can I do?

**A**: No worries. Just raise a support ticket via Microsoft support and we'll get right back to you.