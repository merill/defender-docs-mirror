---
layout: Conceptual
title: Reference table for all Keyvault security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/recommendations-reference-keyvault
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
description: This article lists all Microsoft Defender for Cloud Keyvault security recommendations that help you harden and protect your resources.
ms.topic: reference
ms.date: 2025-04-29T00:00:00.0000000Z
ms.custom: generated
ai-usage: ai-assisted
locale: en-us
document_id: 88bc0ef1-25b3-3764-b256-64d56bb48a80
document_version_independent_id: c1b8e157-0f72-60ce-4266-7081010b7708
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/recommendations-reference-keyvault.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/recommendations-reference-keyvault
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/recommendations-reference-keyvault.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: 86d5d35b-7eb2-3a8c-5eca-fd0ce4b8f332
---

# Reference table for all Keyvault security recommendations in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article lists all the Keyvault security recommendations you might see in Microsoft Defender for Cloud.

The recommendations that appear in your environment are based on the resources that you're protecting and on your customized configuration. You can [see the recommendations in the portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5) that apply to your resources.

To learn about actions that you can take in response to these recommendations, see [Remediate recommendations in Defender for Cloud](implement-security-recommendations).

Tip

If a recommendation description says *No related policy*, usually it's because that recommendation is dependent on a different recommendation.

For example, the recommendation *Endpoint protection health failures should be remediated* relies on the recommendation that checks whether an endpoint protection solution is installed (*Endpoint protection solution should be installed*). The underlying recommendation *does* have a policy. Limiting policies to only foundational recommendations simplifies policy management.

Read this blog to learn how to [protect Your Azure Key Vault and why Azure role based access control is critical for security](https://techcommunity.microsoft.com/blog/microsoftdefendercloudblog/protecting-your-azure-key-vault-why-azure-rbac-is-critical-for-security/4407848).

## Azure Keyvault recommendations

### Role-Based Access Control should be used on Keyvault Services

**Description**: To provide granular filtering on the actions that users can perform, use [Role-Based Access Control (RBAC)](/en-us/azure/key-vault/general/rbac-guide?branch=main&amp;tabs=azure-cli) to manage permissions in Keyvault Service and configure relevant authorization policies. (Related policy: [Azure Key Vault should use RBAC permission model - Microsoft Azure](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F12d4fa5e-1f9f-4c21-97a9-b99b3c6611b5)).

**Severity**: High

**Type**: Control plane

### Key Vault secrets should have an expiration date

**Description**: Secrets should have a defined expiration date and not be permanent. Secrets that are valid forever provide a potential attacker with more time to compromise them. It is a recommended security practice to set expiration dates on secrets. (Related policy: [Key Vault secrets should have an expiration date](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F98728c90-32c7-4049-8429-847dc0f4fe37)).

**Severity**: High

**Type**: Control plane

### Key Vault keys should have an expiration date

**Description**: Cryptographic keys should have a defined expiration date and not be permanent. Keys that are valid forever provide a potential attacker with more time to compromise the key. It is a recommended security practice to set expiration dates on cryptographic keys. (Related policy: [Key Vault keys should have an expiration date](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F152b15f7-8e1f-4c1f-ab71-8c010ba5dbc0)).

**Severity**: High

**Type**: Control plane

### Key vaults should have soft delete enabled

**Description**: Deleting a key vault without soft delete enabled permanently deletes all secrets, keys, and certificates stored in the key vault. Accidental deletion of a key vault can lead to permanent data loss. Soft delete allows you to recover an accidentally deleted key vault for a configurable retention period. (Related policy: [Key vaults should have soft delete enabled](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1e66c121-a66a-4b1f-9b83-0fd99bf0fc2d)).

**Severity**: High

**Type**: Control plane

### Azure Key Vault should have firewall enabled or public network access disabled

**Description**: Enable the key vault firewall so that the key vault is not accessible by default to any public IPs or disable public network access for your key vault so that it's not accessible over the public internet. Optionally, you can configure specific IP ranges to limit access to those networks.

Learn more at: [Network security for Azure Key Vault](/en-us/azure/key-vault/general/network-security) and https://aka.ms/akvprivatelink. (Related policy: [Azure Key Vault should have firewall enabled or public network access disabled](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F55615ac9-af46-4a59-874e-391cc3dfb490)).

**Severity**: Medium

**Type**: Control plane

### Azure Key Vaults should use private link

**Description**: Azure Private Link lets you connect your virtual networks to Azure services without a public IP address at the source or destination. The Private Link platform handles the connectivity between the consumer and services over the Azure backbone network. By mapping private endpoints to key vault, you can reduce data leakage risks. Learn more about private links at: [https://aka.ms/akvprivatelink.] (Related policy: [Azure Key Vaults should use private link](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailAdaptor.ReactView/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa6abeaec-4d90-4a02-805f-6b26c4d3fbe9)).

**Severity**: Medium

**Type**: Control plane