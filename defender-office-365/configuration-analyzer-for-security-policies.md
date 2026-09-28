---
layout: Conceptual
title: Configuration analyzer for threat policies - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/configuration-analyzer-for-security-policies
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.reviewer: 
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-nochange
- sfi-image-nochange
description: Admins can learn how to use the configuration analyzer to find and fix threat policies that are less secure than Standard protection and Strict protections in preset security policies.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9ede4e3e-20a8-9ed3-a28d-ef0f0b7cfd68
document_version_independent_id: 9ede4e3e-20a8-9ed3-a28d-ef0f0b7cfd68
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/configuration-analyzer-for-security-policies.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configuration-analyzer-for-security-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/configuration-analyzer-for-security-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: c68c553d-6345-4a57-c146-98dda76bf6c6
---

# Configuration analyzer for threat policies - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Configuration analyzer in the Microsoft Defender portal provides a central location to find and fix threat policies where the settings are less secure than the Standard protection and Strict protection profile settings in [preset security policies](preset-security-policies).

The following types of policies are analyzed by the configuration analyzer:

- **Threat policies for default protections for cloud mailboxes**: All organizations with cloud mailboxes:

    - [Anti-spam policies](anti-spam-policies-configure).
    - [Anti-malware policies](anti-malware-policies-configure).
    - [Anti-phishing policies for all cloud mailboxes](anti-phishing-policies-about#spoof-settings).
- **Threat policies in Microsoft Defender for Office 365**: Defender for Office 365 is included or in an add-on subscription:

    - Anti-phishing policies in Microsoft Defender for Office 365, which include:
        - The same [spoof settings](anti-phishing-policies-about#spoof-settings) available in anti-phishing policies for all cloud mailboxes.
        - [Impersonation settings](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365)
        - [Phishing email thresholds](anti-phishing-policies-about#phishing-email-thresholds-in-anti-phishing-policies-in-microsoft-defender-for-office-365)
    - [Safe Links policies](safe-links-policies-configure).
    - [Safe Attachments policies](safe-attachments-policies-configure).

The Standard and Strict policy setting values used as baselines are described in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365).

The configuration analyzer also checks the following non-policy settings:

- **DKIM**: Whether [SPF](email-authentication-spf-configure) and [DKIM](email-authentication-dkim-configure) records for the specified domain are detected in DNS.
- **Outlook**: Whether native Outlook external sender identifiers are [configured by using the Set-ExternalInOutlook cmdlet](/en-us/powershell/module/exchangepowershell/set-externalinoutlook) in the organization.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Configuration analyzer** page, use https://security.microsoft.com/configurationAnalyzer.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):

        - *Use the configuration analyzer and update the affected threat policies*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to the configuration analyzer*: Membership in the **Global Reader** or **Security Reader** role groups.
    - [Exchange Online permissions](/en-us/Exchange/permissions-exo/permissions-exo): Membership in the **View-Only Organization Management** role group gives read-only access to the configuration analyzer.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Use the configuration analyzer in the Microsoft Defender portal

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Configuration analyzer** in the **Templated policies** section. To go directly to the **Configuration analyzer** page, use https://security.microsoft.com/configurationAnalyzer.

The **Configuration analyzer** page has three main tabs:

- **Standard recommendations**: Compare your existing threat policies to the Standard recommendations. You can adjust your settings values to bring them up to the same level as Standard.
- **Strict recommendations**: Compare your existing threat policies to the Strict recommendations. You can adjust your settings values to bring them up to the same level as Strict.
- **Configuration drift analysis and history**: Audit and track policy changes over time.

### Standard recommendations and Strict recommendations tabs in the configuration analyzer

By default, the configuration analyzer opens on the **Standard recommendations** tab. You can switch to the **Strict recommendations** tab. The settings, layout, and actions are the same on the **Standard recommendations** and **Strict recommendations** tabs.

[![The Settings and recommendations view in the Configuration analyzer](media/configuration-analyzer-settings-and-recommendations-view.png)](media/configuration-analyzer-settings-and-recommendations-view.png#lightbox)

The first section of the **Standard recommendations** or **Strict recommendations** tab displays the number of settings in each type of policy that need improvement as compared to Standard or Strict protection. The types of policies are:

- **Anti-spam**
- **Anti-phishing**
- **Anti-malware**
- **Safe Attachments** (if your subscription includes Microsoft Defender for Office 365)
- **Safe Links** (if your subscription includes Microsoft Defender for Office 365)
- **DKIM**
- **Built-in Protection** (if your subscription includes Microsoft Defender for Office 365)
- **Outlook**

If a policy type and number isn't shown, then all of your policies of that type meet the recommended settings of Standard or Strict protection.

The rest of the **Standard recommendations** or **Strict recommendations** tab is the table of settings that need to be brought up to the level Standard or Strict protection. The table contains the following columns^\*^:

- **Recommendations**: The value of the setting in the Standard or Strict protection profile.
- **Policy**: The name of the affected policy that contains the setting.
- **Policy group/setting name**: The name of the setting that requires your attention.
- **Policy type**: Anti-spam, Anti-phishing, Anti-malware, Safe Links, or Safe Attachments.
- **Current configuration**: The current value of the setting.
- **Last modified**: The date that the policy was last modified.
- **Status**: Typically, this value is **Not started**.

^\*^ To see all columns, you likely need to do one or more of the following steps:

- Horizontally scroll in your web browser.
- Narrow the width of appropriate columns.
- Zoom out in your web browser.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filters** flyout that opens:

- **Anti-spam**
- **Anti-phishing**
- **Anti-malware**
- **Safe Attachments**
- **Safe Links**
- **ATP Built-in Protection rule**
- **DKIM**
- **Outlook**

When you're finished in the **Filters** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific entries.

#### View details about a recommended policy setting

On the **Standard protection** or **Strict protection** tab of the configuration analyzer, select an entry by clicking anywhere in the row other than the check box next to the recommendation name. In the details flyout that opens, the following information is available:

- **Policy**: The name of the affected policy.
- **Why?**: Information about why we recommend the value for the setting.
- The specific setting to change and the value to change it to.
- **View policy**: The link takes you to the details flyout of the affected policy in the Microsoft Defender portal where you can manually update the setting.
- A link to [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365).

Tip

To see details about other recommendations without leaving the details flyout, use ![](media/updownarrows.png)**Previous** and **Next** at the top of the flyout.

When you're finished in the details flyout, select **Close**.

[![Flyout experience in the Configuration analyzer](media/configuration-analyzer-details-flyout.png)](media/configuration-analyzer-details-flyout.png#lightbox)

#### Take action on a recommended policy setting

On the **Standard protection** or **Strict protection** tab of the configuration analyzer, select an entry by selecting the check box next to the recommendation name. The following actions appear on the page:

- ![](media/defender-portal-icon-edit.png)**Apply recommendation**: If the recommendation requires multiple steps, this action is grayed out.

    When you select this action, a confirmation dialog (with the option to not show the dialog again) opens. When you select **OK**, the following things happen:

    - The setting is updated to the recommended value.
    - The recommendation is still selected, but the only available action is ![](media/defender-portal-icon-refresh.png)**Refresh**.
    - The **Status** value for the row changes to **Complete**.
- ![](media/defender-portal-icon-view-policy.png)**View policy**: You're taken to the details flyout of the affected policy in the Microsoft Defender portal where you can manually update the setting.
- ![](media/defender-portal-icon-download.png)**Export**: Exports the selected recommendation to a .csv file, select ![](media/defender-portal-icon-download.png)**Export**.

    You can also export recommendations after you select multiple recommendations or after you select all recommendations by selecting the check box next to the **Recommendations** column header.

After you automatically or manually update the setting, select ![](media/defender-portal-icon-refresh.png)**Refresh** to see the reduced number of recommendations and the removal of the updated row from the results.

### Configuration drift analysis and history tab in the configuration analyzer

Note

[Unified Auditing](/en-us/purview/audit-log-enable-disable) needs to be enabled for drift analysis.

The **Configuration drift analysis and history** tab allows you to track the changes to your threat policies and how those changes compare to the Standard or Strict settings. By default, the following information is displayed:

- **Last modified**
- **Modified by**
- **Setting Name**
- **Policy**: The name of the affected policy.
- **Type**: Anti-spam, Anti-phishing, Anti-malware, Safe Links, or Safe Attachments.
- **Configuration change**: The old value and the new value of the setting
- **Configuration drift**: The value **Increase** or **Decrease** that indicates the setting increased or decreased security compared to the recommended Standard or Strict setting.

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filters** flyout that opens:

- **Date**: **Start time** and **End time**. You can go back as far as 90 days from today.
- **Type**: **Standard protection** or **Strict protection**.

When you're finished in the **Filters** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box to filter the entries by a specific **Modified by**, **Setting name**, or **Type** value.

To export the entries shown on the **Configuration drift analysis and history** tab to a .csv file, select ![](media/defender-portal-icon-download.png)**Export**.

[![The Configuration drift analysis and history view in the Configuration analyzer](media/configuration-analyzer-configuration-drift-analysis-view.png)](media/configuration-analyzer-configuration-drift-analysis-view.png#lightbox)