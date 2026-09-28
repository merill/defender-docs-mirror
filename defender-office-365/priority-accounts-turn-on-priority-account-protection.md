---
layout: Conceptual
title: Configure and review priority account protection in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/priority-accounts-turn-on-priority-account-protection
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- sfi-ga-nochange
- msecd-doc-authoring-1016
description: Admins can learn how to turn on priority account protection in Microsoft Defender for Office 365 Plan 2 organizations.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: c35fa5e4-f323-be3d-7b8e-a116160abfde
document_version_independent_id: c35fa5e4-f323-be3d-7b8e-a116160abfde
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/priority-accounts-turn-on-priority-account-protection.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: priority-accounts-turn-on-priority-account-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/priority-accounts-turn-on-priority-account-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bd3bf6ca-b76c-a26a-6461-de01a610da42
---

# Configure and review priority account protection in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Microsoft 365 organizations with Microsoft Defender for Office 365 Plan 2, *priority account protection* is a differentiated level of protection applied to accounts that have the **Priority account** tag applied to them. For more information about the Priority account tag and how to apply it to users, see [Manage and monitor priority accounts](/en-us/microsoft-365/admin/setup/priority-accounts).

Priority account protection offers extra heuristics tailored to company executives that don't benefit regular users. Priority account protection is better suited to the mail flow patterns of company executives based on extensive data from the Microsoft datacenters.

By default, priority account protection is turned on in organizations with Defender for Office 365 Plan 2. This default behavior means an account tagged as a Priority account automatically receives priority account protection.

The following sections explain how to verify or enable priority account protection and where to view its results.

## What do you need to know before you begin?

Before you begin, make sure you have access to the Microsoft Defender portal and the required permissions.

- You open the Microsoft Defender portal at https://security.microsoft.com.
- You need to be assigned permissions before you can do the procedures in this section. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/System settings/Read and manage** or **Authorization and settings/System settings/Read-only**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): Membership in the **Organization Management** or **Security Administrator** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^ or **Security Administrator** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- Priority account protection is applied to accounts that have the **Priority account** tag applied to them. For instructions, see [Manage and monitor priority accounts](/en-us/microsoft-365/admin/setup/priority-accounts).
- The Priority account tag is a type of *user tag*. You can create custom user tags to differentiate specific groups of users in reporting and other features. For more information about user tags, see [User tags in Microsoft Defender for Office 365](user-tags-about).
- To use the PowerShell procedures in this section, connect to [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

## Review or turn on priority account protection in the Microsoft Defender portal

Note

We don't recommend turning off priority account protection.

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Settings** &gt; **Email & collaboration** &gt; **Priority account protection**. Or, to go directly to the **Priority account protection** page, use https://security.microsoft.com/securitysettings/priorityAccountProtection.
2. On the **Priority account protection** page, verify that **Priority account protection** is turned on (![](media/scc-toggle-on.png) ).

    [![Turn on Priority account protection.](media/mdo-priority-account-protection.png)](media/mdo-priority-account-protection.png#lightbox)

### Review or turn on priority account protection in Exchange Online PowerShell

If you'd rather use PowerShell to verify that priority account protection is turned on, run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

```powershell
Get-EmailTenantSettings | Format-List Identity,EnablePriorityAccountProtection
```

The value True for the EnablePriorityAccountProtection property means priority account protection is turned on. The value False means priority account protection is turned off.

To turn on priority account protection, run the following command:

```powershell
Set-EmailTenantSettings -EnablePriorityAccountProtection $true
```

For detailed syntax and parameter information, see [Get-EmailTenantSettings](/en-us/powershell/module/exchangepowershell/get-emailtenantsettings) and [Set-EmailTenantSettings](/en-us/powershell/module/exchangepowershell/set-emailtenantsettings).

## Review differentiated protection from priority account protection

The effects of priority account protection are visible in the following reporting features:

- [Threat protection status report](reports-email-security#threat-protection-status-report)
    - [View data by Email &gt; Phish and Chart breakdown by Detection Technology](reports-email-security#view-data-by-email--phish-and-chart-breakdown-by-detection-technology)
    - [View data by Email &gt; Spam and Chart breakdown by Detection Technology](reports-email-security#view-data-by-email--spam-and-chart-breakdown-by-detection-technology)
    - [View data by Email &gt; Malware and Chart breakdown by Detection Technology](reports-email-security#view-data-by-email--malware-and-chart-breakdown-by-detection-technology)
    - [Chart breakdown by Policy type](reports-email-security#chart-breakdown-by-policy-type)
    - [Chart breakdown by Delivery status](reports-email-security#chart-breakdown-by-delivery-status)
- [Threat Explorer and real-time detections](threat-explorer-real-time-detections-about)
- [Email entity page](mdo-email-entity-page)

For information about where the Priority account tag and other user tags are available as filters, see [User tags in reports and features](user-tags-about#user-tags-in-reports-and-features).

### Threat protection status report

The **Threat protection status** report brings together information about malicious content and malicious email detected and blocked by the built-in protections in Microsoft 365 and by Defender for Office 365. For more information, see [Threat protection status report](reports-email-security#threat-protection-status-report).

In the **Email &gt; Phish**, **Email &gt; Spam**, **Email &gt; Malware**, **Policy type**, and **Delivery status** views of the report, the option **Priority account protection** and the value **Yes** is available when you select ![](media/defender-portal-icon-filter.png)**Filter**. This option allows you to filter the data in the report by priority account protection detections.

### Threat Explorer

For more information about Threat Explorer, see [Threat Explorer and Real-time detections](threat-explorer-real-time-detections-about).

To view the results of priority account protection in Threat Explorer, do the following steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Explorer**. Or, to go directly to the **Explorer** page, use https://security.microsoft.com/threatexplorer.
2. On the **Explorer** page, on the **All email**, **Malware**, or **Phish** tabs, select **Context** &gt; **Equal any of** &gt; **Priority account protection**, and then select **Refresh**.

    [![Context filter within Threat Explorer.](media/threat-explorer-context-filter.png)](media/threat-explorer-context-filter.png#lightbox)

### Email entity page

The Email entity page is available from many locations in the Defender portal, including **Threat Explorer** (also known as **Explorer**). For more information, see [The Email entity page](mdo-email-entity-page).

On the Email entity page, select the **Analysis** tab. **Priority account protection** is listed in the **Threat detection details** section.

[![The Analysis tab of the Email entity page showing Priority account protection results.](media/email-entity-priority-account-protection.png)](media/email-entity-priority-account-protection.png#lightbox)