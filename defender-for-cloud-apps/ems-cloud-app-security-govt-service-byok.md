---
layout: Conceptual
title: Encrypt Defender for Cloud Apps data at rest with your own key - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ems-cloud-app-security-govt-service-byok
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides instructions for using your own key to encrypt data at rest stored in Defender for Cloud Apps.
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1016
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
- sfi-image-nochange
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f9e74fcb-5a44-f581-d60f-ac525602256a
document_version_independent_id: f9e74fcb-5a44-f581-d60f-ac525602256a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ems-cloud-app-security-govt-service-byok.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ems-cloud-app-security-govt-service-byok
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ems-cloud-app-security-govt-service-byok.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: 0e8f3c51-9297-30c6-81cf-ad498c230895
---

# Encrypt Defender for Cloud Apps data at rest with your own key - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes how to configure Defender for Cloud Apps to use your own key to encrypt the data it collects, while it's at rest. If you're looking for documentation about applying encryption to data stored in cloud apps, see [Microsoft Purview integration](azip-integration).

Defender for Cloud Apps takes your security and privacy seriously. Therefore, once Defender for Cloud Apps starts collecting data, it uses its own managed keys to protect your data in accordance with our [data security and privacy](cas-compliance-trust) policy. Additionally, Defender for Cloud Apps allows you to further protect your data at rest by encrypting it with your own Azure Key Vault key.

Important

If there's a problem accessing your Azure Key Vault key, Defender for Cloud Apps will fail to encrypt your data, and your tenant will be locked down within an hour. When your tenant is locked down, all access to it will be blocked until the cause has been resolved. Once your key is accessible again, full access to your tenant will be restored.

The procedure to enable customer-managed data encryption is available only on the Microsoft Defender portal, and can't be performed on the classic Microsoft Defender for Cloud Apps.

## Prerequisites

You must register the **Microsoft Defender for Cloud Apps - BYOK** app in your tenant's Microsoft Entra ID associated with your Defender for Cloud Apps tenant.

### To register the app

Perform the following steps to register the Microsoft Defender for Cloud Apps - BYOK app in Microsoft Entra ID.

1. Install [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation).
2. Open a PowerShell terminal and run the following commands:

    ```Powershell
    Connect-MgGraph -Scopes "Application.ReadWrite.All"
    
    # Create a new service principal
    New-MgServicePrincipal -AppId 6a12de16-95c8-4e42-a451-7dbbc34634cd
    
    # Update Service Principal
    $servicePrincipalId = Get-MgServicePrincipal -Filter "AppId eq '6a12de16-95c8-4e42-a451-7dbbc34634cd'" | Select Id
    $params = @{accountEnabled = $true
    }
    
    Update-MgServicePrincipal -ServicePrincipalId $servicePrincipalId.Id -BodyParameter $params
    ```

    Where *ServicePrincipalId* is the ID returned by the previous command (`New-MgServicePrincipal`).

Note

- Defender for Cloud Apps encrypts data at rest for all new tenants.
- Any data that resides in Defender for Cloud Apps for more than 48 hours will be encrypted.

## Deploy your Azure Key Vault key

Use the following steps to create and configure the Azure Key Vault key that Defender for Cloud Apps uses for encryption.

1. Create a [new Key Vault](/en-us/azure/key-vault/general/quick-create-portal#create-a-vault) with the **Soft-delete** and **Purge protection** options enabled.
2. In the new generated Key Vault, open the **Access policies** pane and then select **+Add Access Policy**.

    1. Select **Key permissions** and choose the following permissions from the dropdown menu:

        | Section | Required permissions |
        | --- | --- |
        | Key Management Operations | - List |
        | Cryptographic Operations | - Wrap key- Unwrap key |

        ![Screenshot of Key Vault access policy with List, Wrap key, and Unwrap key permissions selected for Defender for Cloud Apps.](media/cloud-app-security-byok/byok-kv-access-policy-key-perms.png)
    2. Under **Select principal**, choose **Microsoft Defender for Cloud Apps - BYOK** or **Microsoft Cloud App Security - BYOK**.

        ![Screenshot of the Azure Key Vault Add access policy page with Microsoft Defender for Cloud Apps - BYOK selected as the principal.](media/cloud-app-security-byok/byok-kv-add-access-policy.png)
    3. Select **Save**.
3. Create a [new RSA key](/en-us/azure-stack/user/azure-stack-key-vault-manage-portal#create-a-key) and do the following:

    Note

    Only RSA keys are supported.

    1. After creating the key, select the new generated key, select the current version and then you'll see **Permitted operations**.
    2. Under **Permitted operations**, make sure the following options are enabled:

        - Wrap key
        - Unwrap key
    3. Copy the **Key Identifier** URI. You'll need it later.

    ![Screenshot of Azure Key Vault key settings page with Wrap key and Unwrap key permitted operations enabled.](media/cloud-app-security-byok/byok-kv-key-perms.png)
4. Optionally, if using a firewall for a selected network, configure the following firewall settings to give Defender for Cloud Apps access to the specified key, and then click **Save**:

    1. Make sure no virtual networks are selected.
    2. Add the following IP addresses:
        - 13.66.200.132
        - 23.100.71.251
        - 40.78.82.214
        - 51.105.4.145
        - 52.166.166.111
        - 13.72.32.204
        - 52.244.79.38
        - 52.227.8.45
    3. Select **Allow trusted Microsoft services to bypass this firewall**.

    ![Screenshot of Azure Key Vault firewall settings showing allowed IP addresses and trusted Microsoft services option for Defender for Cloud Apps access.](media/cloud-app-security-byok/byok-kv-firewall.png)

## Enable data encryption in Defender for Cloud Apps

When you enable data encryption, Defender for Cloud Apps immediately uses your Azure Key Vault key to encrypt data at rest. Since your key is essential to the encryption process, it's important to ensure that your designated Key Vault and key are accessible at all times.

### To enable data encryption

Perform the following steps to enable customer-managed data encryption in Defender for Cloud Apps.

1. In the Microsoft Defender portal, select **Settings &gt; Cloud Apps &gt; Data encryption &gt; Enable data encryption**.
2. In the **Azure Key Vault key URI** box, paste the **Key Identifier** URI value you copied from the key in Azure Key Vault. Defender for Cloud Apps always uses the latest key version, regardless of the key version specified by the URI.
3. Once the URI validation has completed, select **Enable**.

Warning

Disabling data encryption removes encryption with your own key from data at rest. However, your data remains encrypted by Defender for Cloud Apps managed keys.

**To disable data encryption:** Go to the **Data encryption** tab and click **Disable data encryption**.

## Handle key rotation

Whenever you create new versions of the key configured for data encryption, Defender for Cloud Apps automatically rolls to the latest version of the key.

## How to handle data encryption failures

If there is a problem accessing your Azure Key Vault key, Defender for Cloud Apps will fail to encrypt your data and your tenant will be locked down within an hour. When your tenant is locked down, all access to it will be blocked until the cause has been resolved. Once your key is accessible again, full access to your tenant will be restored. For information about handling data encryption failures, see [Troubleshooting data encryption with your own key](ems-cloud-app-security-govt-service-byok-troubleshoot).