---
layout: Conceptual
title: Troubleshooting data encryption with your own key - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ems-cloud-app-security-govt-service-byok-troubleshoot
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
description: This article provides a list of problems that can prevent Defender for Cloud Apps from accessing your Azure Key Vault key used to encrypt collected data at rest.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: troubleshooting-general
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9c9de421-611e-ee11-e5e0-3b5323ed95ab
document_version_independent_id: 9c9de421-611e-ee11-e5e0-3b5323ed95ab
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ems-cloud-app-security-govt-service-byok-troubleshoot.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ems-cloud-app-security-govt-service-byok-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ems-cloud-app-security-govt-service-byok-troubleshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 1d4d3c54-7726-441b-87ce-72e2082da1ed
---

# Troubleshooting data encryption with your own key - Microsoft Defender for Cloud Apps | Microsoft Learn

This article provides a list of problems that can prevent Defender for Cloud Apps from accessing your Azure Key Vault key used to encrypt collected data at rest.

Important

If there's a problem accessing your Azure Key Vault key, Defender for Cloud Apps will fail to encrypt your data, and your tenant will be locked down within an hour. When your tenant is locked down, all access to it will be blocked until the cause has been resolved. Once your key is accessible again, full access to your tenant will be restored

## Troubleshooting

The following table lists the possible scenarios that can cause data encryption to fail and the actions you can take to resolve them:

| Scenario | Actions |
| --- | --- |
| **Missing Key Vault or key permissions** | In the selected Key Vault, under access policy, make sure that the following key permissions are selected:Under **Key management operations**- ListUnder **Cryptographic operations**- Wrap key- Unwrap keyFor the selected key, make sure you're using an RSA encryption and that the following operations are permitted:- Wrap key- Unwrap key |
| **Azure Key Vault firewall blocking access to key** | In the selected Key Vault, make sure that the firewall is configured with the following IP addresses:- 13.66.200.132- 23.100.71.251- 40.78.82.214- 51.105.4.145- 52.166.166.111 |
| **Encryption key is not enabled** | In the selected key's settings, make sure that the key is enabled.![Screenshot showing key enable option.](media/cloud-app-security-byok/byok-kv-key-enabled.png) |
| **Encryption key is not active** | In the selected key's settings, make sure that the activation date and time is before the current date and time.![Screenshot showing key activation date.](media/cloud-app-security-byok/byok-kv-key-activation-date.png) |
| **Encryption key has expired** | In the selected key's settings, make sure that the expiration date and time hasn't passed.![Screenshot showing key expiration date.](media/cloud-app-security-byok/byok-kv-key-expiration-date.png) |
| **Encryption key not found or deleted** | Verify that the selected key exists in your Key Vault. If key was deleted, recover and enable it again. If the key was moved to another Key Vault, move it back to the selected Key Vault. |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).