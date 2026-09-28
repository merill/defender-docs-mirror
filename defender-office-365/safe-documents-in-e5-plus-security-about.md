---
layout: Conceptual
title: Safe Documents in Microsoft 365 A5/E5/G5 or Microsoft Defender Suite - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/safe-documents-in-e5-plus-security-about
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
ms.custom:
- msecd-doc-authoring-1016
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
- sfi-ga-nochange
ms.assetid: 
ms.collection:
- m365-security
- tier1
description: Enable and configure Safe Documents to scan Office files opened in Protected View or Application Guard using the Microsoft Defender for Endpoint cloud backend. Includes licensing requirements for Microsoft 365 A5, E5, G5, and Microsoft Defender Suite.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7c9cf154-0f8b-1339-5723-1fd97681cf78
document_version_independent_id: 7c9cf154-0f8b-1339-5723-1fd97681cf78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/safe-documents-in-e5-plus-security-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: safe-documents-in-e5-plus-security-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/safe-documents-in-e5-plus-security-about.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 1208ecfa-9b91-e340-29e2-48e938d4247f
---

# Safe Documents in Microsoft 365 A5/E5/G5 or Microsoft Defender Suite - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Safe Documents is a premium feature that uses the cloud back end of [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) to scan opened Office documents in [Protected View](https://support.microsoft.com/office/d6f09ac7-e6b9-4495-8e43-2bbcdbcb6653) or [Application Guard for Office](app-guard-for-office-install).

Users don't need Defender for Endpoint installed on their local devices to get Safe Documents protection. Users get Safe Documents protection if all of the following requirements are met:

- Safe Documents is enabled in the organization using the Safe Documents configuration steps later in this article.
- Users are assigned licenses from a [licensing plan that includes the Office 365 SafeDocs service plan](/en-us/entra/identity/users/licensing-service-plan-reference).

    Safe Documents is controlled by the **Office 365 SafeDocs** (or **SAFEDOCS** or **bf6f5520-59e3-4f82-974b-7dbbc4fd27c7**) service plan. This service plan is available in the following products:

    - Microsoft 365 A5
    - Microsoft 365 E5
    - Microsoft 365 Government Community Cloud (GCC) G5
    - Microsoft 365 GCC High G5
    - Microsoft Defender Suite

    Safe Documents isn't included in Microsoft Defender for Office 365 Plan 1 or Plan 2.
- Users are using Microsoft 365 Apps for enterprise (formerly known as Office 365 ProPlus) version 2004 or later.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Configure Safe Documents settings*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to Safe Documents settings*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

### How does Microsoft handle your data?

To keep you protected, Safe Documents sends file information to the [Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) cloud for analysis. For details on how Microsoft Defender for Endpoint handles your data, see [Microsoft Defender for Endpoint data storage and privacy](/en-us/windows/security/threat-protection/microsoft-defender-atp/data-storage-privacy).

File information sent by Safe Documents isn't retained in Defender for Endpoint beyond the time needed for analysis (typically, less than 24 hours).

## Use the Microsoft Defender portal to configure Safe Documents

Use the following steps to configure Safe Documents in the Microsoft Defender portal:

1. In the Microsoft Defender portal, go to the **Safe Attachments** page at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Safe Attachments** in the **Policies** section. Or, to go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.
2. On the **Safe Attachments** page, select ![](media/defender-portal-icon-gear.png)**Global settings**.
3. In the **Global settings** flyout that opens, confirm or configure the following settings:

    - **Turn on Safe Documents for Office clients**: Move the toggle to the right to turn on the feature: ![](media/scc-toggle-on.png) .
    - **Allow people to click through Protected View even if Safe Documents identified the file as malicious**: We recommend that you leave this option turned off ![](media/scc-toggle-off.png) .

    When you're finished in the **Global settings** flyout, select **Save**.

    [![The Safe Documents settings after selecting Global settings on the Safe Attachments page](media/safe-docs-global-settings.png)](media/safe-docs-global-settings.png#lightbox)

### Use Exchange Online PowerShell to configure Safe Documents

If you'd rather user PowerShell to configure Safe Documents, use the following syntax in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

```powershell
Set-AtpPolicyForO365 -EnableSafeDocs <$true | $false> -AllowSafeDocsOpen <$true | $false>
```

- The *EnableSafeDocs* parameter enables or disables Safe Documents for the entire organization.
- The *AllowSafeDocsOpen* parameter allows or prevents users from leaving Protected View (that is, opening the document) if the document is identified as malicious.

This example enables Safe Documents for the entire organization, and prevents users from opening documents identified as malicious from Protected View.

```powershell
Set-AtpPolicyForO365 -EnableSafeDocs $true -AllowSafeDocsOpen $false
```

For detailed syntax and parameter information, see [Set-AtpPolicyForO365](/en-us/powershell/module/exchangepowershell/set-atppolicyforo365).

### Configure individual access to Safe Documents

If you want to selectively allow or block access to the Safe Documents feature, follow these steps:

1. Turn on Safe Documents in the Microsoft Defender portal (as described in Use the Microsoft Defender portal to configure Safe Documents) or Exchange Online PowerShell (as described in Use Exchange Online PowerShell to configure Safe Documents).
2. Use Microsoft Graph PowerShell to disable Safe Documents for specific users as described in [Disable specific Microsoft 365 services for specific users for a specific licensing plan](/en-us/microsoft-365/enterprise/disable-access-to-services-with-microsoft-365-powershell#disable-specific-microsoft-365-services-for-specific-users-for-a-specific-licensing-plan).

The name of the service plan to disable in PowerShell is **SAFEDOCS**.

For more information, see the following articles:

- [View Microsoft 365 licenses and services with PowerShell](/en-us/microsoft-365/enterprise/view-licenses-and-services-with-microsoft-365-powershell)
- [View Microsoft 365 account license and service details with PowerShell](/en-us/microsoft-365/enterprise/view-account-license-and-service-details-with-microsoft-365-powershell)
- [Product names and service plan identifiers for licensing](/en-us/entra/identity/users/licensing-service-plan-reference)

### Onboard to the Microsoft Defender for Endpoint service to enable auditing capabilities

To enable auditing capabilities, the local device needs to have Microsoft Defender for Endpoint installed. To deploy Microsoft Defender for Endpoint, you need to go through the various phases of deployment. After onboarding, you can configure auditing capabilities in the Microsoft Defender portal.

To learn more, see [Onboard to the Microsoft Defender for Endpoint service](/en-us/defender-endpoint/onboarding). If you need help, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](/en-us/defender-endpoint/troubleshoot-onboarding).

### How do I know this procedure worked?

To verify you successfully enabled and configured Safe Documents, do any of the following steps:

- In the Microsoft Defender portal, go to the **Safe Attachments** page at https://security.microsoft.com/safeattachmentv2, select ![](media/defender-portal-icon-gear.png)**Global settings**, and verify the **Turn on Safe Documents for Office clients** and **Allow people to click through Protected View even if Safe Documents identifies the file as malicious** settings.
- Run the following command in Exchange Online PowerShell and verify the property values:

    ```powershell
    Get-AtpPolicyForO365 | Format-List *SafeDocs*
    ```
- The following files are available to test Safe Documents protection. These files are similar to the EICAR.TXT file for testing anti-malware and anti-virus solutions. The files aren't harmful, but they trigger Safe Documents protection.

    - [SafeDocsDemo.docx](https://download.microsoft.com/download/1/9/7/19774467-5ff1-4c4d-9224-27b3751fa58f/SafeDocsDemo.docx)
    - [SafeDocsDemo.pptx](https://download.microsoft.com/download/b/e/f/bef1df26-2c91-45b3-b8d0-348c6fead4af/SafeDocsDemo.pptx)
    - [SafeDocsDemo.xlsx](https://download.microsoft.com/download/d/1/5/d1547fa8-575b-4ae0-969c-0d5265f6d985/SafeDocsDemo.xlsx)