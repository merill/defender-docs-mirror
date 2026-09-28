---
layout: Conceptual
title: Manage action accounts in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/manage-action-accounts
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to manage action accounts to work with Microsoft Defender for Identity. This step is optional.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e4c66893-3ea2-a47d-7ba0-6f5387d4c868
document_version_independent_id: e4c66893-3ea2-a47d-7ba0-6f5387d4c868
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/manage-action-accounts.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/manage-action-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/manage-action-accounts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 2eb17f4c-78b1-35e8-dbb5-bc334d6c412b
---

# Manage action accounts in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

Defender for Identity allows you to take [remediation actions](../remediation-actions) targeting on-premises Active Directory accounts in the event that an identity is compromised. To take these actions, Microsoft Defender for Identity needs to have the required permissions to do so. This action account configuration is separate from the [Directory Service Account](directory-service-accounts), which is for reading AD data.

Important

This configuration applies to the Defender for Identity sensor v2.x on domain controllers only. Remediation actions aren't performed by sensors on AD FS, AD CS, or Microsoft Entra Connect servers that aren't domain controllers. The sensor v3.x always uses the domain controller's local system account for remediation actions. If all your sensors are v3.x, no action account configuration is needed.

By default, the Microsoft Defender for Identity sensor impersonates the `LocalSystem` account of the domain controller and performs the actions, including [attack disrupting scenarios from Microsoft Defender](/en-us/microsoft-365/security/defender/automatic-attack-disruption).

If you need to change the default behavior of using the domain controller's `LocalSystem` account for remediation actions, set up a dedicated gMSA and scope the permissions that you need. For example:

Warning

The sensor v3.x does not use gMSA action accounts. It always uses the domain controller's local system account for remediation actions.

If any of your sensors are v3.x, select **Automatically use the sensor's local system account**. The v3.x sensors use the local system account regardless of gMSA configuration. The v3.x sensors don't use gMSA accounts configured for v2.x sensors.

For more information, see [Sensor v3.x service account requirements](deploy-sensor-v3#service-account-requirements).

[![Screenshot of the Manage action accounts tab.](../media/management-accounts.png)](../media/management-accounts.png#lightbox)

Note

Using a dedicated gMSA as an action account is optional. We recommend that you use the default settings for the `LocalSystem` account.

## Best practices for action accounts

We recommend that you avoid using the same gMSA account you configured for Defender for Identity managed actions on servers other than domain controllers. If you use the same account on another server and that server is compromised, an attacker could retrieve the password for the account and gain the ability to change passwords and disable accounts.

We also recommend that you avoid using the same account as both the Directory Service account and the Manage Action account. Separating these roles is important because the Directory Service account requires only read-only permissions to Active Directory, and the Manage Action account needs write permissions on user accounts.

If you have multiple forests, your gMSA managed action account must be trusted in all of your forests, or create a separate one for each forest. For more information, see [Microsoft Defender for Identity multi-forest support](multi-forest).

## Create and configure a specific action account

To create and configure a dedicated gMSA action account, perform the following steps:

1. Create a new gMSA account. For more information, see [Getting started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts).
2. Assign the **Log on as a service** right to the gMSA account on each domain controller running the Defender for Identity sensor.
3. Grant the required permissions to the gMSA account as follows:

    1. Open **Active Directory Users and Computers**.
    2. Right-click the relevant domain or OU and select **Properties**. For example:

        ![Screenshot of the domain Properties dialog open to the Security tab before adding gMSA permissions.](../media/domain-properties.png)
    3. Go the **Security** tab and select **Advanced**. For example:

        ![Screenshot of Advanced Security Settings where a new permission entry can be added for the gMSA account.](../media/advanced-security.png)
    4. Select **Add** &gt; **Select a principal**. For example:

        ![Screenshot of the Permission Entry dialog with the gMSA account selected as the security principal.](../media/select-principal.png)
    5. Make sure **Service accounts** is marked in **Object types**. For example:

        ![Screenshot of Object Types with Service Accounts enabled so the gMSA account can be found.](../media/object-types.png)
    6. In the **Enter the object name to select** box, enter the name of the gMSA account and select **OK**.
    7. In the **Applies to** field, select **Descendant User objects**, leave the existing settings, and add the permissions and properties shown in the following example:

        ![Screenshot of the Permission Entry dialog showing Descendant User objects scope with reset password and account control permissions.](../media/permission-entry.png)

        Required permissions include:

        | Action | Permissions | Properties |
        | --- | --- | --- |
        | **Enable force password reset** | Reset password | - `Read pwdLastSet`- `Write pwdLastSet` |
        | **To disable user** | - | - `Read userAccountControl`- `Write userAccountControl` |
    8. (Optional) In the **Applies to** field, select **Descendant Group objects** and set the following properties:

        - `Read members`
        - `Write members`
    9. Select **OK**.

## Add the gMSA account in the Microsoft Defender portal

Use the Microsoft Defender portal to add the gMSA action account:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and select **Settings** -&gt; **Identities** &gt; **Microsoft Defender for Identity** &gt; **Manage action accounts** &gt; **+Create new account**.

    For example:

    ![Screenshot of the Manage action accounts page in the Microsoft Defender portal showing the Create new account option.](../media/manage-action-accounts.png)
2. Enter the account name and domain and select **Save**.

Your action account is listed on the **Manage action accounts** page.