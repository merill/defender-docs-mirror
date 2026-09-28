---
layout: Conceptual
title: Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/safe-attachments-for-spo-odfb-teams-configure
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
ms.assetid: 07e76024-0c80-40dc-8c48-1dd0d0f863cb
ms.collection:
- m365-security
- SPO_Content
- tier2
description: Admins can learn how to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams, including how to set alerts for detected files.
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 94b4ee3b-d1a9-9d2b-458b-9325c12836b6
document_version_independent_id: 94b4ee3b-d1a9-9d2b-458b-9325c12836b6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/safe-attachments-for-spo-odfb-teams-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: safe-attachments-for-spo-odfb-teams-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/safe-attachments-for-spo-odfb-teams-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
platformId: 1cfaa947-d1a0-f69d-d346-f68bb17cf4e3
---

# Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft Defender for Office 365, Safe Attachments for Office 365 for SharePoint, OneDrive, and Microsoft Teams protects your organization from inadvertently sharing malicious files. For more information, see [Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-about).

You turn on or turn off Safe Attachments for Office 365 for SharePoint, OneDrive, and Microsoft Teams in the Microsoft Defender portal or in Exchange Online PowerShell.

## What do you need to know before you begin?

Before you begin, make sure you have the following access, permissions, and setup in place:

- You open the Microsoft Defender portal at [Microsoft Defender portal](https://security.microsoft.com). To go directly to the **Safe Attachments** page, use [Safe Attachments](https://security.microsoft.com/safeattachmentv2).
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):

        - *Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams*: **Authorization and settings/Security settings/Core Security settings (manage)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):

        - *Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams*: Membership in the **Organization Management** or **Security Administrator** role groups.
    - [Microsoft Entra permissions](/en-us/microsoft-365/admin/add-users/about-admin-roles): Membership in the the following roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        - *Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams*: **Global Administrator**^\*^ or **Security Administrator**.
        - *Use SharePoint Online PowerShell to prevent people from downloading malicious files*: **Global Administrator**^\*^ or **SharePoint Administrator**.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- Verify that audit logging is enabled for your organization (it's on by default). For instructions, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).
- Allow up to 30 minutes for the settings to take effect.

## Step 1: Use the Microsoft Defender portal to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams

Perform the following steps to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams in the Microsoft Defender portal:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Safe Attachments** in the **Policies** section. Or, to go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.
2. On the **Safe Attachments** page, select ![](media/defender-portal-icon-gear.png)**Global settings**.
3. In the **Global settings** flyout that opens, go to the **Protect files in SharePoint, OneDrive, and Microsoft Teams** section.

    Move the **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** toggle to the right ![](media/scc-toggle-on.png) to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams.

    When you're finished in the **Global settings** flyout, select **Save**.

### Use Exchange Online PowerShell to turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams

If you'd rather use PowerShell to enable Defender for Office 365 protection for SharePoint, OneDrive, and Microsoft Teams so that malicious files in those services can be detected and acted on, [connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell) and run the following command:

```powershell
Set-AtpPolicyForO365 -EnableATPForSPOTeamsODB $true
```

For detailed syntax and parameter information, see [Set-AtpPolicyForO365](/en-us/powershell/module/exchangepowershell/set-atppolicyforo365).

## Step 2: (Recommended) Use SharePoint Online PowerShell to prevent users from downloading malicious files

By default, users can't open, move, copy, or share^\*^ malicious files that are detected by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams. However, they can delete and download malicious files.

^\*^ If users go to **Manage access**, the **Share** option is still available.

To configure the SharePoint tenant to block users from downloading files that have been identified as malicious, [connect to SharePoint Online PowerShell](/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online) and run the following command:

```powershell
Set-SPOTenant -DisallowInfectedFileDownload $true
```

**Notes**:

- This setting affects both users and admins.
- People can still delete malicious files.

For detailed syntax and parameter information, see [Set-SPOTenant](/en-us/powershell/module/microsoft.online.sharepoint.powershell/set-spotenant).

## Step 3 (Recommended) Use the Microsoft Defender portal to create an alert policy for detected files

You can create an alert policy that notifies admins when Safe Attachments for SharePoint, OneDrive, and Microsoft Teams detects a malicious file. To learn more about alert policies, see [Alert policies in the Microsoft Defender portal](alert-policies-defender-portal).

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Alert policy**. To go directly to the **Alert policy** page, use https://security.microsoft.com/alertpolicies.
2. On the **Alert policy** page, select ![](media/defender-portal-icon-create.png)**New alert policy** to start the new alert policy wizard.
3. On the **Name your alert, categorize it, and choose a severity** page, configure the following settings:

    - **Name**: Type a unique and descriptive name. For example, **Malicious Files in Libraries**.
    - **Description**: Type an optional description. For example, **Notifies admins when malicious files are detected in SharePoint, OneDrive, or Microsoft Teams**.
    - **Severity**: Select **Low**, **Medium**, or **High** from the dropdown list.
    - **Category**: Select **Threat management** from the dropdown list.

    When you're finished on the **Name your alert, categorize it, and choose a severity** page, select **Next**.
4. On the **Choose an activity, conditions and when to trigger the alert** page, configure the following settings:

    - **What do you want to alert on?** section &gt; **Activity is** &gt; **Common user activities** section &gt; Select **Detected malware in file** from the dropdown list.
    - **How do you want the alert to be triggered?** section: Select **Every time an activity matches the rule**.

    When you're finished on the **Choose an activity, conditions and when to trigger the alert** page, select **Next**.
5. On the **Decide if you want to notify people when this alert is triggered** page, configure the following settings:

    - Verify **Opt-in for email notifications** is selected. In the **Email recipients** box, select one or more admins who should receive notification when a malicious file is detected.
    - **Daily notification limit**: Leave the default value **No limit** selected.

    When you're finished on the **Decide if you want to notify people when this alert is triggered** page, select **Next**.
6. On the **Review your settings** page, review your settings. You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    In the **Do you want to turn the policy on right away?** section, select **Yes, turn it on right away**.

    When you're finished n the **Review your settings** page, select **Submit**.
7. On the confirmation page, you can review the alert policy in read-only mode.

    When you're finished, select **Done**.

    Back on the **Alert policy** page, the new policy is listed.

### Use Security & Compliance PowerShell to create an alert policy for detected files

If you'd rather use PowerShell to create an alert policy that notifies administrators whenever malware is detected in SharePoint, OneDrive, or Microsoft Teams libraries, [connect to Security & Compliance PowerShell](/en-us/powershell/exchange/connect-to-scc-powershell) and run the following command:

```powershell
New-ProtectionAlert -Name "Malicious Files in Libraries" -Description "Notifies admins when malicious files are detected in SharePoint, OneDrive, or Microsoft Teams" -AggregationType None -Category ThreatManagement -ThreatType Activity -Operation FileMalwareDetected -NotifyUser "admin1@contoso.com","admin2@contoso.com"
```

The default *Severity* value is Low. To specify Medium or High, include the *Severity* parameter and value in the command.

For detailed syntax and parameter information, see [New-ProtectionAlert](/en-us/powershell/module/exchangepowershell/new-protectionalert).

### How do you know these procedures worked?

Use the following methods to confirm that each procedure completed successfully:

- To verify you successfully turned on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams, use either of the following steps:

    - In the Microsoft Defender portal, go to **Policies & rules** &gt; **Threat policies** &gt; **Policies** section &gt; **Safe Attachments**, select **Global settings**, and verify the value of the **Turn on Defender for Office 365 for SharePoint, OneDrive, and Microsoft Teams** setting.
    - In Exchange Online PowerShell, run the following command to verify the property setting:

        ```powershell
        Get-AtpPolicyForO365 | Format-List EnableATPForSPOTeamsODB
        ```

        For detailed syntax and parameter information, see [Get-AtpPolicyForO365](/en-us/powershell/module/exchangepowershell/get-atppolicyforo365).
- To verify you successfully blocked people from downloading malicious files, open SharePoint Online PowerShell, and run the following command to check whether downloads of infected files are blocked:

    ```powershell
    Get-SPOTenant | Format-List DisallowInfectedFileDownload
    ```

    For detailed syntax and parameter information, see [Get-SPOTenant](/en-us/powershell/module/microsoft.online.sharepoint.powershell/get-spotenant).
- To verify you successfully configured an alert policy for detected files, use either of the following methods:

    - In the Microsoft Defender portal at https://security.microsoft.com/alertpolicies, select the alert policy, and verify the settings.
    - In Security & Compliance PowerShell, replace &lt;AlertPolicyName&gt; with the name of the alert policy, run the following command, and verify the property values:

        ```powershell
        Get-ProtectionAlert -Identity "<AlertPolicyName>"
        ```

        For detailed syntax and parameter information, see [Get-ProtectionAlert](/en-us/powershell/module/exchangepowershell/get-protectionalert).
- Use the [Threat protection status report](reports-email-security#threat-protection-status-report) to view information about detected files in SharePoint, OneDrive, and Microsoft Teams. Specifically, you can use the **View data by: Content &gt; Malware** view.