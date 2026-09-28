---
layout: Conceptual
title: Remove blocked connectors from the Restricted entities page in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/connectors-remove-blocked
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
ms.assetid: 
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-nochange
description: Admins can learn how to remove connectors from the Restricted entities page in the Microsoft Defender portal. Connectors are added to the Restricted entities page after signs of compromise.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f79fa4d8-5d60-a49a-a0b0-ffb0f96d9a21
document_version_independent_id: f79fa4d8-5d60-a49a-a0b0-ffb0f96d9a21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/connectors-remove-blocked.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: connectors-remove-blocked
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/connectors-remove-blocked.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: e8fcade4-d9fc-a6e5-7379-22e9c08ab75e
---

# Remove blocked connectors from the Restricted entities page in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, several things happen if an [inbound connector](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/use-connectors-to-configure-mail-flow) is detected as potentially compromised:

- The connector is prevented from sending or relaying email.
- The connector is added to the **Restricted entities** page in the Microsoft Defender portal.

    A *restricted entity* is a **user account** or a **connector** that's blocked from sending email due to indications of compromise, which typically includes exceeding message receiving and sending limits.
- If the connector is used to send email, the message is returned in a non-delivery report (also known as an NDR or bounced message) with the error code `550;5.7.711` and the following text:

> 
> Your message couldn't be delivered. The most common reason for this is that your organization's email connector is suspected of sending spam or phish and it's no longer allowed to send email. Contact your email admin for assistance. Remote Server returned '550;5.7.711 Access denied, bad inbound connector. AS(2204).'

For more information about compromised connectors and how to regain control of those connectors, see [Respond to a compromised connector](connectors-detect-respond-to-compromise).

The following procedures explain how admins can remove connectors from the **Restricted entities** page in the Microsoft Defender portal or in Exchange Online PowerShell.

For more information about compromised *user accounts* and how to remove them from the **Restricted entities** page, see [Remove blocked users from the Restricted entities page](outbound-spam-restore-restricted-users).

## What do you need to know before you begin?

Before you begin, make sure you have access to the required tools and permissions:

- Open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Restricted entities** page, use https://security.microsoft.com/restrictedentities.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can remove connectors from the **Restricted entities** page. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Detection tuning (manage)** or **Authorization and settings/Security settings/Core security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Remove connectors from the Restricted entities page*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to the Restricted entities page*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- Before you remove a connector from the **Restricted entities** page, be sure to follow the required steps to regain control of the connector as described in [Respond to a compromised connector](connectors-detect-respond-to-compromise).

## Remove a connector from the Restricted entities page in the Microsoft Defender portal

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Restricted entities**. Or, to go directly to the **Restricted entities** page, use https://security.microsoft.com/restrictedentities.
2. On the **Restricted entities** page, identify the connector to unblock. The **Entity** value is **Connector**.

    Select a column header to sort by that column.

    To change the list of entities from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

    Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific connectors.
3. Select the connector to unblock by selecting the check box for the entity, and then selecting the **Unblock** action that appears on the page.
4. In the **Unblock entity** flyout that opens, read the details about the restricted connector. You should go through the recommendations to ensure you're taking the proper actions in case the connector is compromised.

    Note

    It might take up to 1 hour for all restrictions to be removed from the connector.

    When you're finished in the **Unblock entity** flyout, select **Unblock**.

## Verify the alert settings for restricted connectors

The default alert policy named **Suspicious connector activity** automatically notifies admins when connectors are blocked from relaying email. For more information about alert policies, see [Alert policies in the Microsoft Defender portal](alert-policies-defender-portal).

Important

For alerts to work, audit logging must be turned on (it's on by default). To verify that audit logging is turned on or to turn it on, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Alert policy**. Or, to go directly to the **Alert policy** page, use https://security.microsoft.com/alertpoliciesv2.
2. On the **Alert policy** page, find the alert named **Suspicious connector activity**. You can sort the alerts by name, or use the ![](media/defender-portal-icon-search.png)**Search** box to find the alert.

    Select the **Suspicious connector activity** alert by clicking anywhere in the row other than the check box next to the name.
3. In the **Suspicious connector activity** flyout that opens, verify or configure the following settings:

    - **Status**: Verify the alert is turned on ![](media/scc-toggle-on.png) .
    - Expand the **Set your recipients section** and verify the **Recipients** and **Daily notification limit** values.

        To change the values, select ![](media/defender-portal-icon-edit.png)**Edit recipient settings** in the section or select ![](media/defender-portal-icon-edit.png)**Edit policy** at the top of the flyout.

        - On the **Decide if you want to notify people when this alert is triggered** page of the wizard that opens, verify or change the following settings:

            - Verify **Opt-in for email notifications** is selected.
            - **Email recipients**: The default value is **TenantAdmins** (**Global Administrator** members). To add more recipients, click in the empty area of the box. A list of recipients appears, and you can start typing a name to filter and select a recipient. Remove an existing recipient from the box by selecting ![](media/defender-portal-icon-remove-selection.png) next to their name.
            - **Daily notification limit**: The default value is **No limit**.

            When you're finished on the **Decide if you want to notify people when this alert is triggered** page, select **Next**.
        - On the **Review your settings** page, select **Submit**, and then select **Done**.
4. Back in the **Suspicious connector activity** flyout, select ![](media/defender-portal-icon-remove.png) at the top of the flyout.

## Use Exchange Online PowerShell to view and remove connectors from the Restricted entities page

To view the list of connectors that are restricted from sending email, run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

```powershell
Get-BlockedConnector
```

To view details about a specific blocked connector, replace &lt;ConnectorID&gt; with the GUID value of the connector, and then run the following command:

```powershell
Get-BlockedConnector -ConnectorId <ConnectorID> | Format-List
```

For detailed syntax and parameter information, see [Get-BlockedConnector](/en-us/powershell/module/exchangepowershell/get-blockedconnector).

To remove a connector from the Restricted entities list, replace &lt;ConnectorID&gt; with the GUID value of the connector, and then run the following command:

```powershell
Remove-BlockedConnector -ConnectorId <ConnectorID>
```

For detailed syntax and parameter information, see [Remove-BlockedConnector](/en-us/powershell/module/exchangepowershell/remove-blockedconnector).