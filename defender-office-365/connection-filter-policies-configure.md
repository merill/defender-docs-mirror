---
layout: Conceptual
title: Configure the default connection filter policy - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/connection-filter-policies-configure
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
ms.assetid: 6ae78c12-7bbe-44fa-ab13-c3768387d0e3
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
description: Admins can learn how to configure connection filtering in Microsoft 365 to allow or block emails from email servers.
ms.service: defender-office-365
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 4c78fab7-4023-aa17-2f90-331e7a37dfab
document_version_independent_id: 4c78fab7-4023-aa17-2f90-331e7a37dfab
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/connection-filter-policies-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connection-filter-policies-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/connection-filter-policies-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: dcca7ccb-c0c3-b4e1-9adf-d01e4a33a927
---

# Configure the default connection filter policy - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, connection filtering via the default connection filter policy is available to allow or block inbound SMTP email connections (email delivery) from specified IP addresses. The key components of the default connection filter policy are:

- **IP Allow List**: Skip spam filtering for all incoming messages from the specified source IP addresses or IP address ranges. All incoming messages are still scanned for malware and high confidence phishing. For other scenarios where spam filtering still occurs, see Scenarios where messages from sources in the IP Allow List are still filtered. For more information about how the IP Allow List should fit into your overall allowlist strategy, see [Create sender allowlists](create-safe-sender-lists-in-office-365).
- **IP Block List**: Block all incoming messages from the specified source IP addresses or IP address ranges. The incoming messages are rejected, aren't marked as spam, and no other filtering occurs. For more information about how the IP Block List should fit into your overall blocked senders strategy, see [Create sender blocklists](create-block-sender-lists-in-office-365).
- **Safe list**: The *safe list* in the default connection filter policy is a dynamic allowlist that requires no customer configuration. Microsoft identifies these trusted email sources from subscriptions to various non-Microsoft lists. You enable or disable the use of the safe list; you can't configure the servers in the list. Spam filtering is skipped on incoming messages from the email servers on the safe list.

This article describes how to configure the default connection filter policy in the Microsoft 365 Microsoft Defender portal or in Exchange Online PowerShell. For more information about how connection filtering fits into your organization's overall anti-spam settings in Microsoft 365, see [Anti-spam protection](anti-spam-protection-about).

Note

The IP Allow List, safe list, and the IP Block List are one part of your overall strategy to allow or block email in your organization. For more information, see [Create sender allowlists](create-safe-sender-lists-in-office-365) and [Create sender blocklists](create-block-sender-lists-in-office-365).

IPv6 ranges aren't supported. You can create and manage entries for IPv6 addresses in the [Tenant Allow/Block List](tenant-allow-block-list-ip-addresses-configure).

Messages from blocked sources in the IP Block List aren't available in [message trace](/en-us/exchange/monitoring/trace-an-email-message/message-trace-modern-eac).

## What do you need to know before you begin?

Before you begin, review the following requirements and setup information.

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Anti-spam policies** page, use https://security.microsoft.com/antispam.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Modify policies*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to policies*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

    Tip

    If policy changes fail to save with a 403 or **CmdletAccessDeniedException** error and you verified that you have the required permissions, the issue might be related to an Exchange Online role-based access control (RBAC) configuration problem. Some organizations require a backend RBAC configuration refresh before policy changes succeed. If the issue persists, contact [Microsoft Support](/en-us/microsoft-365/admin/get-help-support) and reference "RBAC configuration refresh."
- To find the source IP addresses of the email servers (senders) that you want to allow or block, you can check the connecting IP (**CIP**) header field in the message header. To view a message header in various email clients, see [View internet message headers in Outlook](https://support.microsoft.com/office/cd039382-dc6e-4264-ac74-c048563d212c).
- The IP Allow List takes precedence over the IP Block List (an address on both lists isn't blocked).
- The IP Allow List and the IP Block List each support a maximum of 1,273 entries, where an entry is a single IP address, an IP address range, or a Classless InterDomain Routing (CIDR) IP.

## Use the Microsoft Defender portal to modify the default connection filter policy

Use the following steps to modify the default connection filter policy in the Microsoft Defender portal.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-spam** in the **Policies** section. Or, to go directly to the **Anti-spam policies** page, use https://security.microsoft.com/antispam.
2. On the **Anti-spam policies** page, select **Connection filter policy (Default)** from the list by clicking anywhere in the row other than the check box next to the name.
3. In the policy details flyout that opens, use the **Edit** links to modify the policy settings:

    - **Description** section: Select **Edit description** to enter a description for the policy in the **Description** box of the **Edit name and description** flyout that opens. You can't modify the name of the policy.

        When you're finished in the **Edit name and description** flyout, select **Save**.
    - **Connection filtering** section: Select **Edit connection filter policy**. In the flyout that opens, configure the following settings:

        - **Always allow messages from the following IP addresses or address range**: This setting is the IP Allow List. In the IP Allow List box, enter the IP address or address range and press **Enter**. The entry is added as a separate item (displayed as a gray box with an **X** icon). After confirming the entry appears, select **Save**. Valid values are:

            - Single IP: For example, 192.168.1.1.
            - IP range: For example, 192.168.0.1-192.168.0.254.
            - CIDR IP: For example, 192.168.0.1/25. Valid subnet mask values are /24 through /32. To skip spam filtering for /1 to /23, see Skip spam filtering for a CIDR IP outside of the available range.

            Repeat this step as many times as necessary. To remove an existing entry, select ![](media/defender-portal-icon-remove-selection.png) next to the entry.
    - **Always block messages from the following IP addresses or address range**: This setting is the IP Block List. Enter a single IP (for example, 192.168.1.1), IP range (for example, 192.168.0.1-192.168.0.254), or CIDR IP (for example, 192.168.0.1/25) in the box and press **Enter**. The entry is added as a separate item (displayed as a gray box with an **X** icon). After confirming the entry appears, select **Save**.
    - **Turn on safe list**: Enable or disable the use of the safe list that specifies known, good senders to skip spam filtering. To use the safe list, select the check box.

    When you're finished in the flyout, select **Save**.
4. Back on the policy details flyout, select **Close**.

Tip

If the IP address ranges you added don't immediately appear in the connection filter policy, do the following steps:

- Try refreshing the portal or verify the changes in Exchange Online PowerShell:

    ```powershell
    Get-HostedConnectionFilterPolicy -Identity Default
    ```
- Verify you have the required Microsoft Entra ID permissions as described in the What do you need to know before you begin? section.

If the issue persists, it might indicate a synchronization delay or a service issue.

## Use the Microsoft Defender portal to view the default connection filter policy

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-spam** in the **Policies** section. Or, to go directly to the **Anti-spam policies** page, use https://security.microsoft.com/antispam.

On the **Anti-spam policies** page, the following properties are displayed in the list of policies:

- **Name**: The default connection filter policy is named **Connection filter policy (Default)**.
- **Status**: The value is **Always on** for the default connection filter policy.
- **Priority**: The value is **Lowest** for the default connection filter policy.
- **Type**: The value is blank for the default connection filter policy.

To change the list of policies from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific policies.

Select the default connection filter policy by clicking anywhere in the row other than the check box next to the name to open the details flyout for the policy.

## Use PowerShell to modify the default connection filter policy

In [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell), use the **Set-HostedConnectionFilterPolicy** cmdlet to configure the default connection filter policy, including IP allow and block lists:

```powershell
Set-HostedConnectionFilterPolicy -Identity Default [-AdminDisplayName <"Optional Comment">] [-EnableSafeList <$true | $false>] [-IPAllowList <IPAddressOrRange1,IPAddressOrRange2...>] [-IPBlockList <IPAddressOrRange1,IPAddressOrRange2...>]
```

- Valid IP address or address range values are:
    - Single IP: For example, 192.168.1.1.
    - IP range: For example, 192.168.0.1-192.168.0.254.
    - CIDR IP: For example, 192.168.0.1/25. Valid network mask values are /24 through /32.
- To *overwrite* any existing entries with the values you specify, use the following syntax: `IPAddressOrRange1,IPAddressOrRange2,...,IPAddressOrRangeN`.
- To *add or remove* IP addresses or address ranges without affecting other existing entries, use the following syntax: `@{Add="IPAddressOrRange1","IPAddressOrRange2",...,"IPAddressOrRangeN";Remove="IPAddressOrRange3","IPAddressOrRange4",...,"IPAddressOrRangeN"}`.
- To empty the IP Allow List or IP Block List, use the value `$null`.

The following example overwrites the IP Allow List and the IP Block List in the default connection filter policy with the specified IP addresses and address ranges.

```powershell
Set-HostedConnectionFilterPolicy -Identity Default -IPAllowList 192.168.1.10,192.168.1.23 -IPBlockList 10.10.10.0/25,172.17.17.0/24
```

The following example adds new IP addresses and address ranges to the existing IP Allow List and removes an old entry, without replacing the entire list.

```powershell
Set-HostedConnectionFilterPolicy -Identity Default -IPAllowList @{Add="192.168.2.10","192.169.3.0/24","192.168.4.1-192.168.4.5";Remove="192.168.1.10"}
```

For detailed syntax and parameter information, see [Set-HostedConnectionFilterPolicy](/en-us/powershell/module/exchangepowershell/set-hostedconnectionfilterpolicy).

## How do you know these procedures worked?

To verify you successfully modified the default connection filter policy, do any of the following steps:

- On the **Anti-spam policies** page in the Microsoft Defender portal at https://security.microsoft.com/antispam, select **Connection filter policy (Default)** from the list by clicking anywhere in the row other than the check box next to the name, and verify the policy settings in the details flyout that opens.
- In Exchange Online PowerShell, run the following command to review the current settings of the default connection filter policy and verify your changes:

    ```powershell
    Get-HostedConnectionFilterPolicy -Identity Default
    ```
- Send a test message from an entry on the IP Allow List.

## Other considerations for the IP Allow List

This section covers CIDR IP limitations, selective domain filtering, and scenarios where IP Allow List messages are still filtered.

Note

All incoming messages are scanned for malware and high confidence phishing, regardless of whether the message source is in the IP Allow List.

### Skip spam filtering for a CIDR IP outside of the available range

The IP Allow List supports only CIDR IPs with a network mask of /24 to /32.

To skip spam filtering on messages from source email servers in the /1 to /23 range, you can [use Exchange mail flow rules (transport rules)](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl). However, we don't recommend using mail flow rules. Messages are blocked if an IP address in the /1 to /23 CIDR IP range appears on any of Microsoft's proprietary blocklists or non-Microsoft blocklists.

Now that you're fully aware of the potential issues, you can create a mail flow rule with the following settings (at a minimum) to ensure that messages from these IP addresses skip spam filtering:

- Rule condition: **Apply this rule if** &gt; **The sender** &gt; **IP address is in any of these ranges or exactly matches** &gt; (enter your CIDR IP with a /1 to /23 network mask).
- Rule action: **Modify the message properties** &gt; **Set the spam confidence level (SCL)** &gt; **Bypass spam filtering**.

You can audit the rule, test the rule, activate the rule during a specific time period, and other selections. We recommend testing the rule for a period before you enforce it. For more information, see [Manage mail flow rules in Exchange Online](/en-us/Exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

### Skip spam filtering on selective email domains from the same source

Typically, adding an IP address or address range to the IP Allow List means you trust all incoming messages from that email source. What if that source sends email from multiple domains, and you want to skip spam filtering for some of those domains, but not others? You can use the IP Allow List in combination with a mail flow rule.

For example, the source email server 192.168.1.25 sends email from the domains contoso.com, fabrikam.com, and tailspintoys.com, but you only want to skip spam filtering for messages from senders in fabrikam.com:

1. Add 192.168.1.25 to the IP Allow List.
2. Configure a mail flow rule with the following settings (at a minimum):

    - Rule condition: **Apply this rule if** &gt; **The sender** &gt; **IP address is in any of these ranges or exactly matches** &gt; 192.168.1.25 (the same IP address or address range that you added to the IP Allow List in the previous step).
    - Rule action: **Modify the message properties** &gt; **Set the spam confidence level (SCL)** &gt; **0**.
    - Rule exception: **The sender** &gt; **domain is** &gt; fabrikam.com (only the domain or domains that you want to skip spam filtering).

Adding the source IP address to the IP Allow List is supposed to skip spam filtering for all domains from that source. However, this bypass is an input, not a final decision. Like the **Bypass spam filtering** (SCL -1) action in a mail flow rule, the IP Allow List bypass is subject to [Secure by default](secure-by-default), which evaluates the request and might not honor it. Some messages from the source can still be filtered.

The **Set the spam confidence level (SCL)** to **0** might no longer reliably return those domains to filtering, because the requested SCL value is an input, not a decision.

### Scenarios where messages from sources in the IP Allow List are still filtered

Note

These scenarios apply to all environments: standalone, hybrid, multi-geo, and cross-forest. Filtering behavior is based on security checks (for example, malware detection, phishing protection, or mail flow rules, not on the deployment model).

Messages from an email server in your IP Allow List are still subject to spam filtering in the following scenarios:

- An IP address in your IP Allow List is also configured in an on-premises, IP-based inbound connector in *any* Microsoft 365 organization, **and** that Microsoft 365 organization and the first Microsoft 365 server that encounters the message both happen to be in *the same* forest in the Microsoft datacenters. In this scenario, **IPV:CAL***is* added to the message's [anti-spam message headers](message-headers-eop-mdo) (indicating the message bypassed spam filtering), but the message is still subject to spam filtering.
- Your organization that contains the IP Allow List and the Microsoft 365 server that first encounters the message both happen to be in *different* forests in the Microsoft datacenters. In this scenario, **IPV:CAL***isn't* added to the message headers, so the message is still subject to spam filtering.

If you encounter either of these scenarios, you can create a mail flow rule with the following settings (at a minimum) to ensure that messages from the problematic IP addresses skip spam filtering:

- Rule condition: **Apply this rule if** &gt; **The sender** &gt; **IP address is in any of these ranges or exactly matches** &gt; (your IP address or addresses).
- Rule action: **Modify the message properties** &gt; **Set the spam confidence level (SCL)** &gt; **Bypass spam filtering**.