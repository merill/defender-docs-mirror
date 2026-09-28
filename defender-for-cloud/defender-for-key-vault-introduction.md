---
layout: Conceptual
title: Microsoft Defender for Key Vault - the benefits and features - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-key-vault-introduction
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about the benefits and features of Microsoft Defender for Key Vault.
ms.date: 2025-08-20T00:00:00.0000000Z
ms.topic: overview
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 67260cbb-36e2-c0b6-b19c-943531c307bd
document_version_independent_id: 9cc8930e-3efe-4dda-2f93-c2812836810f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-key-vault-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-key-vault-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-key-vault-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 3c8e36c6-15f3-c151-3ce0-61b259fef3fe
---

# Microsoft Defender for Key Vault - the benefits and features - Microsoft Defender for Cloud | Microsoft Learn

Azure Key Vault is a cloud service that safeguards encryption keys and secrets like certificates, connection strings, and passwords.

Enable **Microsoft Defender for Key Vault** for Azure-native, advanced threat protection for Azure Key Vault, providing another layer of security intelligence.

## Availability

| Aspect | Details |
| --- | --- |
| Release state: | General availability (GA) |
| Pricing: | **Microsoft Defender for Key Vault** is billed as shown on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). |

For cloud availability, see the [Defender for Cloud support matrices for Azure commercial/other clouds](support-matrix-defender-for-cloud).

## What are the benefits of Microsoft Defender for Key Vault?

Microsoft Defender for Key Vault detects unusual and potentially harmful attempts to access or exploit Key Vault accounts. This layer of protection helps you address threats even if you're not a security expert, and without the need to manage third-party security monitoring systems.

When anomalous activities occur, Defender for Key Vault shows alerts, and optionally sends them via email to relevant members of your organization. These alerts include the details of the suspicious activity and recommendations on how to investigate and remediate threats.

## Microsoft Defender for Key Vault alerts

When you get an alert from Microsoft Defender for Key Vault, we recommend you investigate and respond to the alert as described in [Respond to Microsoft Defender for Key Vault](defender-for-key-vault-usage). Microsoft Defender for Key Vault protects applications and credentials, so even if you're familiar with the application or user that triggered the alert, it's important to check the situation surrounding every alert.

The alerts appear in Key Vault's **Security** page, the Workload protections, and Defender for Cloud's security alerts page.

[![Screenshot that shows the Azure Key Vault's security page](media/defender-for-key-vault-intro/key-vault-security-page.png)](media/defender-for-key-vault-intro/key-vault-security-page.png#lightbox)

Tip

You can simulate Microsoft Defender for Key Vault alerts by following the instructions in [Validating Azure Key Vault threat detection in Microsoft Defender for Cloud](https://techcommunity.microsoft.com/t5/azure-security-center/validating-azure-key-vault-threat-detection-in-azure-security/ba-p/1220336).

## Respond to Microsoft Defender for Key Vault alerts

When you receive an alert from Microsoft Defender for Key Vault, we recommend you investigate and respond to the alert as described below. Microsoft Defender for Key Vault protects applications and credentials, so even if you're familiar with the application or user that triggered the alert, it's important to verify the situation surrounding every alert.

Alerts from Microsoft Defender for Key Vault include these elements:

- Object ID
- User Principal Name or IP address of the suspicious resource

Depending on the *type* of access that occurred, some fields might not be available. For example, if your key vault was accessed by an application, you won't see an associated User Principal Name. If the traffic originated from outside of Azure, you won't see an Object ID.

Tip

Azure virtual machines are assigned Microsoft IPs. This means that an alert might contain a Microsoft IP even though it relates to activity performed from outside of Microsoft. So even if an alert has a Microsoft IP, you should still investigate as described on this page.

### Step 1: Identify the source

1. Verify whether the traffic originated from within your Azure tenant. If the key vault firewall is enabled, it's likely that you've provided access to the user or application that triggered this alert.
2. If you can't verify the source of the traffic, continue to Step 2. Respond accordingly.
3. If you can identify the source of the traffic in your tenant, contact the user or owner of the application.

Caution

Microsoft Defender for Key Vault is designed to help identify suspicious activity caused by stolen credentials. **Don't** dismiss the alert simply because you recognize the user or application. Contact the owner of the application or the user and verify the activity was legitimate. You can create a suppression rule to eliminate noise if necessary. Learn more in [Suppress security alerts](alerts-suppression-rules).

### Step 2: Respond accordingly

If you don't recognize the user or application, or if you think the access shouldn't have been authorized:

- If the traffic came from an unrecognized IP Address:

    1. Enable the Azure Key Vault firewall as described in [Configure Azure Key Vault firewalls and virtual networks](/en-us/azure/key-vault/general/network-security).
    2. Configure the firewall with trusted resources and virtual networks.
- If the source of the alert was an unauthorized application or suspicious user:

    1. Open the key vault's access policy settings.
    2. Remove the corresponding security principal, or restrict the operations the security principal can perform.
- If the source of the alert has a Microsoft Entra role in your tenant:

    1. Contact your administrator.
    2. Determine whether there's a need to reduce or revoke Microsoft Entra permissions.

### Step 3: Measure the impact

When the event has been mitigated, investigate the secrets in your key vault that were affected:

1. Open the **Security** page on your Azure key vault and view the triggered alert.
2. Select the specific alert that was triggered and review the list of the secrets that were accessed and the timestamp.
3. Optionally, if you have key vault diagnostic logs enabled, review the previous operations for the corresponding caller IP, user principal, or object ID.

### Step 4: Take action

When you've compiled your list of the secrets, keys, and certificates that were accessed by the suspicious user or application, you should rotate those objects immediately.

1. Affected secrets should be disabled or deleted from your key vault.
2. If the credentials were used for a specific application:
    1. Contact the administrator of the application and ask them to audit their environment for any uses of the compromised credentials since they were compromised.
    2. If the compromised credentials were used, the application owner should identify the information that was accessed and mitigate the impact.