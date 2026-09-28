---
layout: Conceptual
title: Allow or block files using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/tenant-allow-block-list-files-configure
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
ms.collection:
- m365-security
- tier1
description: Admins can learn how to allow or block files in the Tenant Allow/Block List.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: df31abc9-0918-ea42-290a-063e3b9e9ab5
document_version_independent_id: df31abc9-0918-ea42-290a-063e3b9e9ab5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/tenant-allow-block-list-files-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tenant-allow-block-list-files-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/tenant-allow-block-list-files-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: cadd7d18-19d0-efd6-35e9-cd862d60cc0a
---

# Allow or block files using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, admins can create and manage entries for files in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about). Tenant Allow/Block List file hash matching applies to all files extracted during message analysis, including:

- Standard attachments.
- Inline or embedded content. For example:
    - Images in the message body.
    - Files contained within supported attachment types.

This article describes how admins can manage entries for files in the Microsoft Defender portal and in Exchange Online PowerShell.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList. To go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You specify files by using the SHA256 hash value of the file. To find the SHA256 hash value of a file in Windows, use the following PowerShell command to compute the SHA-256 hash of the file before adding it to the Tenant Allow/Block List:

    ```powershell
    Get-FileHash -Path "<Path>\<Filename>" -Algorithm SHA256
    ```

    An example value is `768a813668695ef2483b2bde7cf5d1b2db0423a0d3e63e498f3ab6f2eb13ea3a`. Perceptual hash (pHash) values aren't supported.
- Entry limits for files:

    - **Microsoft 365 organizations without Defender for Office 365**: A maximum of 1000 total file entries:
        - Allow entries: 500 maximum.
        - Block entries: 500 maximum
    - **Microsoft 365 organizations with Defender for Office 365 Plan 1 (included or in an add-on subscription)**: A maximum of 2000 total file entries:
        - Allow entries: 1000 maximum.
        - Block entries: 1000 maximum.
    - **Microsoft 365 organizations with Defender for Office 365 Plan 2 (included or in an add-on subscription)**: A maximum of 15000 total file entries:
        - Allow entries: 5000 maximum.
        - Block entries: 10000 maximum.
- You can enter a maximum of 64 characters in a file entry.
- An entry should be active within 5 minutes.
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):

        - *Add and remove entries from the Tenant Allow/Block List*: Membership assigned with the following permissions:
            - **Authorization and settings/Security settings/Detection tuning (manage)**
        - *Read-only access to the Tenant Allow/Block List*:
            - **Authorization and settings/Security settings/Read-only**.
            - **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Add and remove entries from the Tenant Allow/Block List*: Membership in one of the following role groups:
            - **Organization Management** or **Security Administrator** (Security admin role).
            - **Security Operator** (Tenant AllowBlockList Manager role): This permission works only when assigned directly in the **Exchange admin center** at https://admin.exchange.microsoft.com &gt; **Roles** &gt; **Admin Roles**.
        - *Read-only access to the Tenant Allow/Block List*: Membership in one of the following role groups:
            - **Global Reader**
            - **Security Reader**
            - **View-Only Configuration**
            - **View-Only Organization Management**
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- A **Files** tab is available on the **Submissions** page only in organizations with Microsoft Defender or Microsoft Defender for Endpoint Plan 2. For information and instructions to submit files from the **Files** tab, see [Submit files in Microsoft Defender for Endpoint](/en-us/defender-endpoint/admin-submissions-mde).

## Create allow entries for files

You can't create allow entries for files directly in the Tenant Allow/Block List. Unnecessary allow entries expose your organization to malicious email that the system would otherwise filter.

Instead, you use the **Email attachments** tab on the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=emailAttachment. When you submit a blocked file as **I've confirmed it's clean**, you can select **Allow this file** to add an allow entry for the file on the **Files** tab on the **Tenant Allow/Block Lists** page. For instructions, see [Submit good email attachments to Microsoft](submissions-admin#report-good-email-attachments-to-microsoft).

Tip

Allow entries from submissions are added during mail flow based on the filters that determined the message was malicious. For example, if the sender email address and a URL in the message are determined to be malicious, an allow entry is created for the sender (email address or domain) and the URL.

During mail flow or time of click, if messages containing the entities in the allow entries pass other checks in the filtering stack, the messages are delivered (all filters associated with the allowed entities are skipped). For example, if a message passes [email authentication checks](email-authentication-about), URL filtering, and file filtering, a message from an allowed sender email address is delivered if it's also from an allowed sender.

By default, allow entries for [domains and email addresses](submissions-admin#report-good-email-to-microsoft), [files](submissions-admin#report-good-email-attachments-to-microsoft), and [URLs](submissions-admin#report-good-urls-to-microsoft) are kept for 45 days after the filtering system determines that the entity is clean, and then the allow entry is removed. Or you can set allow entries to expire up to 30 days after you create them. Allow entries for [spoofed senders](tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-spoofed-senders) never expire.

> 
> During time of click, the file allow entry overrides all filters associated with the file entity, which allows users to access the file.

## Create block entries for files

Email messages that contain these blocked files are blocked as *malware*. Messages that contain the blocked files are quarantined.

To create block entries for files, use either of the following methods:

- From the **Email attachments** tab on the **Submissions** page at https://security.microsoft.com/reportsubmission?viewid=emailAttachment. When you submit a file as **I've confirmed it's a threat**, you can select **Block this file** to add a block entry to the **Files** tab on the **Tenant Allow/Block Lists** page. For instructions, see [Report questionable email attachments to Microsoft](submissions-admin#report-questionable-email-attachments-to-microsoft).
- From the **Files** tab on the **Tenant Allow/Block Lists** page or in PowerShell as described in Use PowerShell to create block entries for files in the Tenant Allow/Block List.

### Use the Microsoft Defender portal to create block entries for files in the Tenant Allow/Block List

To create a block entry for files directly in the Microsoft Defender portal, perform the following steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. On the **Tenant Allow/Block Lists** page, select the **Files** tab.
3. On the **Files** tab, select ![](media/defender-portal-icon-create.png)**Add**, and then select **Block**.
4. In the **Block files** flyout that opens, configure the following settings:

    - **Add file hashes**: Enter one SHA256 hash value per line, up to a maximum of 20.
    - **Remove block entry after**: Select from the following values:

        - **1 day**
        - **7 days**
        - **30 days** (default)
        - **Never expire**
        - **Specific date**: The maximum value is 90 days from today.
    - **Optional note**: Enter descriptive text for why you're blocking the files.

    When you're finished in the **Block files** flyout, select **Add**.

Back on the **Files** tab, the entry is listed.

#### Use PowerShell to create block entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax to create block entries for file hashes in the Tenant Allow/Block List:

```powershell
New-TenantAllowBlockListItems -ListType FileHash -Block -Entries "HashValue1","HashValue2",..."HashValueN" <-ExpirationDate Date | -NoExpiration> [-Notes <String>]
```

This example adds block entries for two file hashes and configures them to never expire.

```powershell
New-TenantAllowBlockListItems -ListType FileHash -Block -Entries "768a813668695ef2483b2bde7cf5d1b2db0423a0d3e63e498f3ab6f2eb13ea3","2c0a35409ff0873cfa28b70b8224e9aca2362241c1f0ed6f622fef8d4722fd9a" -NoExpiration
```

For detailed syntax and parameter information, see [New-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/new-tenantallowblocklistitems).

## Use the Microsoft Defender portal to view entries for files in the Tenant Allow/Block List

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Tenant Allow/Block Lists** in the **Rules** section. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.

Select the **Files** tab.

On the **Files** tab, you can sort the entries by clicking on an available column header. The following columns are available:

- **Value**: The file hash.
- **Action**: The available values are **Allow** or **Block**.
- **Override verdicts**: The available values are **Up to malware** for both block and allow entries.
- **Modified by**
- **Last updated**
- **Last used date**: The date the entry was last used in the filtering system to override the verdict.
- **Remove on**: The expiration date.
- **Notes**

To filter the entries, select ![](media/defender-portal-icon-filter.png)**Filter**. The following filters are available in the **Filter** flyout that opens:

- **Action**: The available values are **Allow** and **Block**.
- **Never expire**: ![](media/scc-toggle-on.png) or ![](media/scc-toggle-off.png)
- **Last updated**: Select **From** and **To** dates.
- **Last used date**: Select **From** and **To** dates.
- **Remove on**: Select **From** and **To** dates.
- **Modified by**: Provide an incomplete or complete email address to search by it.

When you're finished in the **Filter** flyout, select **Apply**. To clear the filters, select ![](media/defender-portal-icon-clear-filters.png)**Clear filters**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific entries.

To group the entries, select ![](media/defender-portal-icon-group.png)**Group** and then select **Action**. To ungroup the entries, select **None**.

### Use PowerShell to view entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax to retrieve file hash entries from the Tenant Allow/Block List. You can filter the results by action (allow or block), specific hash value, or expiration status:

```powershell
Get-TenantAllowBlockListItems -ListType FileHash [-Allow] [-Block] [-Entry <FileHashValue>] [<-ExpirationDate Date | -NoExpiration>]
```

This example lists all file hash entries (both allow and block) in the Tenant Allow/Block List.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash
```

This example looks up a specific SHA-256 file hash in the Tenant Allow/Block List and returns its entry details.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash -Entry "9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08"
```

This example returns only the blocked file hash entries from the Tenant Allow/Block List.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash -Block
```

For detailed syntax and parameter information, see [Get-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/get-tenantallowblocklistitems).

## Use the Microsoft Defender portal to modify entries for files in the Tenant Allow/Block List

In existing file entries, you can change the expiration date and note.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **Files** tab
3. On the **Files** tab, select the entry from the list by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
4. In the **Edit file** flyout that opens, the following settings are available:

    - **Block entries**:
        - **Remove block entry after**: Select from the following values:
            - **1 day**
            - **7 days**
            - **30 days**
            - **Never expire**
            - **Specific date**: The maximum value is 90 days from today.
        - **Optional note**
    - **Allow entries**:
        - **Remove allow entry after**: Select from the following values:
            - **1 day**
            - **7 days**
            - **30 days**
            - **45 days after last used date**
            - **Specific date**: The maximum value is 30 days from today.
        - **Optional note**

    When you're finished in the **Edit file** flyout, select **Save**.

Tip

In the details flyout of an entry on the **Files** tab, use ![](media/defender-portal-icon-view-submission.png)**View submission** at the top of the flyout to go to the details of the corresponding entry on the **Submissions** page. This action is available if a submission was responsible for creating the entry in the Tenant Allow/Block List.

### Use PowerShell to modify existing allow or block entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax to update existing file hash entries in the Tenant Allow/Block List, such as changing the expiration date or notes:

```powershell
Set-TenantAllowBlockListItems -ListType FileHash <-Ids <Identity value> | -Entries <Value>> [<-ExpirationDate Date | -NoExpiration>] [-Notes <String>]
```

This example updates the expiration date of the specified file hash block entry to September 1, 2022.

```powershell
Set-TenantAllowBlockListItems -ListType FileHash -Entries "27c5973b2451db9deeb01114a0f39e2cbcd2f868d08cedb3e210ab3ece102214" -ExpirationDate "9/1/2022"
```

For detailed syntax and parameter information, see [Set-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/set-tenantallowblocklistitems).

## Use the Microsoft Defender portal to remove entries for files from the Tenant Allow/Block List

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **Files** tab.
3. On the **Files** tab, do one of the following steps:

    - Select the entry from the list by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.
    - Select the entry from the list by clicking anywhere in the row other than the check box. In the details flyout that opens, select ![](media/defender-portal-icon-delete.png)**Delete** at the top of the flyout.

        Tip

        To see details about other entries without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.
4. In the warning dialog that opens, select **Delete**.

Back on the **Files** tab, the entry is no longer listed.

Tip

You can select multiple entries by selecting each check box, or select all entries by selecting the check box next to the **Value** column header.

### Use PowerShell to remove entries for files from the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax to delete file hash entries from the Tenant Allow/Block List. You can specify entries by their identity value or hash value:

```powershell
Remove-TenantAllowBlockListItems -ListType FileHash <-Ids <Identity value> | -Entries <Value>>
```

This example removes the file hash entry with the specified SHA-256 value from the Tenant Allow/Block List.

```powershell
Remove-TenantAllowBlockListItems -ListType FileHash -Entries "27c5973b2451db9deeb01114a0f39e2cbcd2f868d08cedb3e210ab3ece102214"
```

For detailed syntax and parameter information, see [Remove-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/remove-tenantallowblocklistitems).