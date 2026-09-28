---
layout: Conceptual
title: Allow or block IPv6 addresses using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/tenant-allow-block-list-ip-addresses-configure
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
description: Admins can learn how to allow or block IPv6 addresses in the Tenant Allow/Block List.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 5b87c557-222b-44b9-84dd-83af17d4cb0d
document_version_independent_id: 5b87c557-222b-44b9-84dd-83af17d4cb0d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/tenant-allow-block-list-ip-addresses-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tenant-allow-block-list-ip-addresses-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/tenant-allow-block-list-ip-addresses-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: fd2ebac7-2da2-6ca0-7b1a-e39bd1190dbf
---

# Allow or block IPv6 addresses using the Tenant Allow/Block List - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, admins can create and manage entries for IPv6 addresses in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about).

This article describes how admins can manage entries for IPv6 addresses in the Microsoft Defender portal and in Exchange Online PowerShell.

Note

IPv4 addresses (both single addresses and ranges) aren't supported in the Tenant Allow/Block List for this feature. Only IPv6 addresses are supported here. To allow or block IPv4 addresses, use the [default connection filter policy](connection-filter-policies-configure) instead.

## What do you need to know before you begin?

Before you work with IPv6 entries in the Tenant Allow/Block List, review the following requirements and limitations.

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList. To go directly to the **Submissions** page, use https://security.microsoft.com/reportsubmission.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- IPv6 addresses are supported only in the following formats:

    - Single addresses in colon-hexadecimal format. For example, 2001:0db8:85a3:0000:0000:8a2e:0370:7334.
    - Single addresses in zero-compression format. For example, 2001:db8::1 represents 2001:0db8:0000:0000:0000:0000:0000:0001.
    - CIDR IPv6 range. For example, 2001:0db8::/32. 1-128 range is supported.
- Entry limits for IP addresses:

    - **Microsoft 365 organizations without Defender for Office 365**: A maximum of 1000 total IP entries:
        - Allow entries: 500 maximum.
        - Block entries: 500 maximum.
    - **Microsoft 365 organizations with Defender for Office 365 Plan 1 (included or in an add-on subscription)**: A maximum of 2000 total IP entries:
        - Allow entries: 1000 maximum.
        - Block entries: 1000 maximum.
    - **Microsoft 365 organizations with Defender for Office 365 Plan 2 (included or in an add-on subscription)**: A maximum of 15000 total IP entries:
        - Allow entries: 5000 maximum.
        - Block entries: 10000 maximum.
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
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in one of the following roles gives users the required permissions *and* permissions for other features in Microsoft 365:

        - *Add and remove entries from the Tenant Allow/Block List*: Membership in one of the following roles:
            - **Global Administrator**^\*^
            - **Security Administrator**
        - *Read-only access to the Tenant Allow/Block List*: Membership in one of the following roles:
            - **Global Reader**
            - **Security Reader**

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Create allow entries for IPv6 addresses

The allow entry overrides only the IP filters for the specified sending IP address.

You can create allow entries for IPv6 addresses directly in the Tenant Allow/Block List by using the Microsoft Defender portal or PowerShell as described in the following procedures.

### Use the Microsoft Defender portal to create allow entries for IPv6 addresses in the Tenant Allow/Block List

Perform the following steps to create an allow entry for an IPv6 address in the Microsoft Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. On the **Tenant Allow/Block Lists** page, select the **IP addresses** tab.
3. On the **IP addresses** tab, select ![](media/defender-portal-icon-create.png)**Allow**.
4. In the **Allow IP addresses** flyout that opens, configure the following settings:

    - **Add IP address**: Enter one IP address per line, up to a maximum of 20.
    - **Remove allow entry after**: Select from the following values:

        - **1 day**
        - **7 days**
        - **30 days**
        - **Never expire** (default)
        - **Specific date**: The maximum value is 90 days from today.
    - **Optional note**: Enter descriptive text for why you're allowing the IP addresses.

    When you're finished in the **Allow IP addresses** flyout, select **Add**.

Back on the **IP addresses** tab, the entry is listed.

### Use PowerShell to create allow entries for IPv6 addresses in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
New-TenantAllowBlockListItems -ListType IP -Allow -Entries "IPAddress1","IPAddress2",..."IPAddressN" <-ExpirationDate Date | -NoExpiration> [-Notes <String>]
```

This example adds an allow entry for the specified IP address that never expires.

```powershell
New-TenantAllowBlockListItems -ListType IP -Allow -Entries "2001:db8:3333:4444:5555:6666:7777:8882" -NoExpiration
```

For detailed syntax and parameter information, see [New-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/new-tenantallowblocklistitems).

## Create block entries for IPv6 addresses

You can create block entries for IPv6 addresses directly in the Tenant Allow/Block List by using the Microsoft Defender portal or PowerShell as described in the following procedures.

Incoming email messages from IPv6 addresses in block entries are blocked at the edge of the service.

### Use the Microsoft Defender portal to create block entries for IPv6 addresses in the Tenant Allow/Block List

Perform the following steps to create a block entry for an IPv6 address in the Microsoft Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. On the **Tenant Allow/Block Lists** page, select the **IP addresses** tab.
3. On the **IP addresses** tab, select ![](media/defender-portal-icon-create.png)**Block**.
4. In the **Block IP addresses** flyout that opens, configure the following settings:

    - **Add IP address**: Enter one IP address per line, up to a maximum of 20.
    - **Remove block entry after**: Select from the following values:

        - **1 day**
        - **7 days**
        - **30 days**
        - **Never expire** (default)
        - **Specific date**: The maximum value is 90 days from today.
    - **Optional note**: Enter descriptive text for why you're blocking the IP addresses.

    When you're finished in the **Block IP addresses** flyout, select **Add**.

Back on the **IP addresses** tab, the entry is listed.

### Use PowerShell to create block entries for IPv6 addresses in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
New-TenantAllowBlockListItems -ListType IP -Block -Entries "IPAddress1","IPAddress2",..."IPAddressN" <-ExpirationDate Date | -NoExpiration> [-Notes <String>]
```

This example adds a block entry for the specified IP address that never expires.

```powershell
New-TenantAllowBlockListItems -ListType IP -Block -Entries "2001:db8:3333:4444:5555:6666:7777:8882" -NoExpiration
```

For detailed syntax and parameter information, see [New-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/new-tenantallowblocklistitems).

## View entries for IPv6 addresses in the Tenant Allow/Block List

You can view existing IPv6 allow and block entries by using the Microsoft Defender portal or Exchange Online PowerShell.

### Use the Microsoft Defender portal to view entries for IPv6 addresses in the Tenant Allow/Block List

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Tenant Allow/Block Lists** in the **Rules** section. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.

Select the **IP addresses** tab.

On the **IP addresses** tab, you can sort the entries by clicking on an available column header. The following columns are available:

- **Value**: The IP address.
- **Action**: The available values are **Allow** or **Block**.
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

### Use PowerShell to view entries for IPv6 addresses in the Tenant Allow/Block List

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Get-TenantAllowBlockListItems -ListType IP [-Allow] [-Block] [-Entry <IPaddress>] [<-ExpirationDate Date | -NoExpiration>]
```

This example returns all allowed and blocked IP addresses.

```powershell
Get-TenantAllowBlockListItems -ListType IP
```

This example returns information for the specified IP address.

```powershell
Get-TenantAllowBlockListItems -ListType IP -Entry "2001:db8:3333:4444:5555:6666:7777:8882"
```

This example filters the results to show only blocked IP addresses.

```powershell
Get-TenantAllowBlockListItems -ListType IP -Block
```

For detailed syntax and parameter information, see [Get-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/get-tenantallowblocklistitems).

## Modify entries for IPv6 addresses in the Tenant Allow/Block List

For existing IP addresses entries, you can change the expiration date and note.

### Use the Microsoft Defender portal to modify entries for IPv6 addresses in the Tenant Allow/Block List

Perform the following steps to modify an existing IPv6 address entry in the Microsoft Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **IP addresses** tab
3. On the **IP addresses** tab, select the entry from the list by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
4. In the **Edit IP addresses** flyout that opens, the following settings are available:

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
            - **Never expire**
            - **Specific date**: The maximum value is 30 days from today.
        - **Optional note**

    When you're finished in the **Edit IP addresses** flyout, select **Save**.

## Use PowerShell to modify existing allow or block entries for IPv6 addresses in the Tenant Allow/Block List

To update an existing IP address entry in the Tenant Allow/Block List, in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Set-TenantAllowBlockListItems -ListType IP <-Ids <Identity value> | -Entries <Value> [<-ExpirationDate Date | -NoExpiration>] [-Notes <String>]
```

The following example changes the expiration date of the specified blocked IP address entry:

```powershell
Set-TenantAllowBlockListItems -ListType IP -Entries "2001:db8:3333:4444:5555:6666:7777:8882" -ExpirationDate "9/1/2024"
```

For detailed syntax and parameter information, see [Set-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/set-tenantallowblocklistitems).

## Remove entries for IPv6 addresses from the Tenant Allow/Block List

You can remove IPv6 address entries from the Tenant Allow/Block List by using the Microsoft Defender portal or Exchange Online PowerShell.

### Use the Microsoft Defender portal to remove entries for IPv6 addresses from the Tenant Allow/Block List

Perform the following steps to remove IPv6 address entries from the Tenant Allow/Block List in the Microsoft Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Rules** section &gt; **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use https://security.microsoft.com/tenantAllowBlockList.
2. Select the **IP addresses** tab.
3. On the **IP addresses** tab, do one of the following steps:

    - Select the entry from the list by selecting the check box next to the first column, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.
    - Select the entry from the list by clicking anywhere in the row other than the check box. In the details flyout that opens, select ![](media/defender-portal-icon-delete.png)**Delete** at the top of the flyout.

        Tip

        To see details about other entries without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.
4. In the warning dialog that opens, select **Delete**.

Back on the **IP addresses** tab, the entry is no longer listed.

Tip

You can select multiple entries by selecting each check box, or select all entries by selecting the check box next to the **Value** column header.

## Use PowerShell to remove entries for IPv6 addresses from the Tenant Allow/Block List

To remove an IP address entry from the Tenant Allow/Block List, in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Remove-TenantAllowBlockListItems -ListType IP <-Ids <Identity value> | -Entries <Value>>
```

The following example removes the specified IP address entry from the Tenant Allow/Block List:

```powershell
Remove-TenantAllowBlockListItems -ListType IP -Entries "2001:db8:3333:4444:5555:6666:7777:8882"
```

For detailed syntax and parameter information, see [Remove-TenantAllowBlockListItems](/en-us/powershell/module/exchangepowershell/remove-tenantallowblocklistitems).