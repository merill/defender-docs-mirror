---
layout: Conceptual
title: Inventory delegated From addresses for outbound spam policies - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-delegated-from-addresses-inventory
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Exchange Online PowerShell to inventory Send As and Send on behalf permissions so you can map delegated From addresses to outbound spam policies.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-office-365
ms.date: 2026-07-27T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 1ff82200-21d9-dbc0-de4a-bf6ec4e585b2
document_version_independent_id: 1ff82200-21d9-dbc0-de4a-bf6ec4e585b2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-delegated-from-addresses-inventory.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-delegated-from-addresses-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-delegated-from-addresses-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: a5cdd8cf-bc2a-86ba-6d3b-3617d03c0b92
---

# Inventory delegated From addresses for outbound spam policies - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Outbound spam policy limits depend on the address in the **From** field (also known as the `5322.From` address or P2 sender) of each message, not just the authenticated sender. For details, see [How outbound spam policy limits apply to Send As and Send on behalf permissions](outbound-spam-policies-send-as-send-on-behalf).

An inventory of delegated sending permissions helps you:

- Identify who can send email from mailboxes and group addresses.
- Investigate unexpected outbound sending restrictions.
- Verify that delegated From addresses are covered by appropriate outbound spam policies.

Include the following delegated permissions in the inventory:

- **Send As** permissions assigned on mailboxes and groups.
- **Send on behalf** permissions assigned on mailboxes, distribution groups, dynamic distribution groups, mail-enabled security groups, and Microsoft 365 Groups.

Keep the following points in mind:

- **Full Access** permissions are excluded, because they don't grant the ability to send email from the mailbox.
- If a delegate has both **Send As** and **Send on behalf** permissions for the same target, **Send As** takes precedence.

## Before you begin

- Connect to Exchange Online PowerShell. For instructions, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can run the commands in this article. You have the following options:
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): Membership in a role group that has the **View-Only Recipients** role assigned. By default, that role is assigned to the **Organization Management**, **View-Only Organization Management**, **Compliance Management**, **Hygiene Management**, and **Help Desk** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Exchange Administrator**, **Exchange Recipient Administrator**, or **Global Reader** roles gives users read access to recipients *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Inventory Send As permissions

Send As assignments are stored as recipient permissions, so you can inventory them for the whole organization. The following Exchange Online PowerShell command returns Send As assignments, excludes the built-in `NT AUTHORITY\SELF` and `NT AUTHORITY\SYSTEM` trustees, and sorts the results:

```powershell
Get-EXORecipientPermission -AccessRights SendAs -ResultSize Unlimited | Where-Object { $_.Trustee -ne "NT AUTHORITY\SELF" -and $_.Trustee -ne "NT AUTHORITY\SYSTEM" } | Select-Object Identity, Trustee, AccessRights | Sort-Object Identity, Trustee
```

The output includes the following fields:

- *Identity* is the mailbox or group address that can be used as the delegated From address.
- *Trustee* is the user or mail-enabled security group granted Send As permission.

To export the results to a CSV file, replace &lt;PathAndFilename&gt; with the desired name and location of the CSV file, and then add ` | Export-Csv -Path "<PathAndFilename>.csv" -NoTypeInformation` to the end of the command.

For more information, see [Get-EXORecipientPermission](/en-us/powershell/module/exchangepowershell/get-exorecipientpermission).

## Inventory Send on behalf permissions

Send on behalf assignments are stored in the *GrantSendOnBehalfTo* property of recipient objects. Because the script that collects these assignments is long, save it as a script file and then run it in Exchange Online PowerShell:

1. Copy the code from the following code block into a plain-text editor like Notepad.
2. Save the file with a .ps1 extension (for example, `GetSendOnBehalf.ps1`) in a location that's easy to find (for example, `C:\Data\`).
3. In Exchange Online PowerShell, run the following command:

    ```powershell
    & "C:\Data\GetSendOnBehalf.ps1"
    ```

The script collects assignments from mailboxes, distribution groups, dynamic distribution groups, and Microsoft 365 Groups, and returns one row for each delegation.

```powershell
$sendOnBehalfPermissions = @()

# Mailboxes
Get-EXOMailbox -ResultSize Unlimited -Properties GrantSendOnBehalfTo |
    Where-Object { $_.GrantSendOnBehalfTo.Count -gt 0 } |
    ForEach-Object {
        $target = $_
        foreach ($delegate in $target.GrantSendOnBehalfTo) {
            $sendOnBehalfPermissions += [PSCustomObject]@{
                Permission        = "Send on behalf"
                FromAddress       = $target.PrimarySmtpAddress
                FromDisplayName   = $target.DisplayName
                FromRecipientType = $target.RecipientTypeDetails
                Delegate          = $delegate
            }
        }
    }

# Distribution groups
Get-DistributionGroup -ResultSize Unlimited |
    Where-Object { $_.GrantSendOnBehalfTo.Count -gt 0 } |
    ForEach-Object {
        $target = $_
        foreach ($delegate in $target.GrantSendOnBehalfTo) {
            $sendOnBehalfPermissions += [PSCustomObject]@{
                Permission        = "Send on behalf"
                FromAddress       = $target.PrimarySmtpAddress
                FromDisplayName   = $target.DisplayName
                FromRecipientType = $target.RecipientTypeDetails
                Delegate          = $delegate
            }
        }
    }

# Dynamic distribution groups
Get-DynamicDistributionGroup -ResultSize Unlimited |
    Where-Object { $_.GrantSendOnBehalfTo.Count -gt 0 } |
    ForEach-Object {
        $target = $_
        foreach ($delegate in $target.GrantSendOnBehalfTo) {
            $sendOnBehalfPermissions += [PSCustomObject]@{
                Permission        = "Send on behalf"
                FromAddress       = $target.PrimarySmtpAddress
                FromDisplayName   = $target.DisplayName
                FromRecipientType = $target.RecipientTypeDetails
                Delegate          = $delegate
            }
        }
    }

# Microsoft 365 Groups
Get-UnifiedGroup -ResultSize Unlimited |
    Where-Object { $_.GrantSendOnBehalfTo.Count -gt 0 } |
    ForEach-Object {
        $target = $_
        foreach ($delegate in $target.GrantSendOnBehalfTo) {
            $sendOnBehalfPermissions += [PSCustomObject]@{
                Permission        = "Send on behalf"
                FromAddress       = $target.PrimarySmtpAddress
                FromDisplayName   = $target.DisplayName
                FromRecipientType = "Microsoft 365 Group"
                Delegate          = $delegate
            }
        }
    }

$sendOnBehalfPermissions |
    Sort-Object FromAddress, Delegate |
    Format-Table -AutoSize
```

To export the results to a CSV file, replace the final `Format-Table -AutoSize` command with `Export-Csv -Path "<PathAndFilename>.csv" -NoTypeInformation`, where &lt;PathAndFilename&gt; is the desired name and location of the CSV file.

Note

For dynamic distribution groups, the *GrantSendOnBehalfTo* property returns directory identities. To return friendly display names instead, run **Get-DynamicDistributionGroup** with the *IncludeGrantSendOnBehalfToWithDisplayNames* switch.

## Review permissions assigned through groups

The inventory reports only the trustee that received the permission directly. Because a trustee can be a group, users can inherit delegated sending rights through membership even when their names don't appear in the results.

For each group trustee:

- Determine whether the group-based permission assignment is still needed.
- Review the current membership of the group. The command in this section expands nested groups automatically, so members of nested groups are included in the results.
- Document the effective users that can send email from the delegated address.

To list all members of a group, including members of any nested groups, replace &lt;GroupName&gt; with the name, alias, or email address of the group, and then run the following command:

```powershell
function Get-AllGroupMembers ($GroupIdentity) {$members = Get-DistributionGroupMember -Identity $GroupIdentity -ResultSize Unlimited; foreach ($member in $members) {if ($member.RecipientType -like "*Group*") { Get-AllGroupMembers $member.PrimarySmtpAddress} else {$member}}}; Get-AllGroupMembers "<GroupName>" | Select-Object DisplayName, PrimarySmtpAddress, RecipientType -Unique
```

## Map delegated permissions to outbound spam policies

Use the inventory results to build a mapping between the effective delegate, the delegated From address, the delegated permission type, and the outbound spam policy that applies to that From address. For example:

| Effective delegate | Delegated From address | Permission | Outbound spam policy for the From address |
| --- | --- | --- | --- |
| `sender@contoso.com` | `shared@contoso.com` | Send As | Default outbound spam policy |
| `sender@contoso.com` | `sales@contoso.com` | Send on behalf | High-volume senders |

For each user, compare:

- The user's own From address.
- Every delegated From address the user routinely uses.
- Delegated permissions obtained through group membership.
- Delegated permissions obtained through nested groups.

If different policies have different limits or restriction actions, users can encounter unexpected restrictions when they send email from delegated addresses. To adjust policy coverage, see [Configure outbound spam policies](outbound-spam-policies-configure).