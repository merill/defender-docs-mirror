---
layout: Conceptual
title: Protect your key vaults with the Defender for Key Vault plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/tutorial-enable-key-vault-plan
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
description: Learn how to enable the Defender for Key Vault plan on your Azure subscription for Microsoft Defender for Cloud.
ms.topic: install-set-up-deploy
ms.date: 2025-05-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 00f9233a-c82e-f315-ba5a-c082fc9fb47c
document_version_independent_id: 52801b12-cd8a-966f-161a-ea1bf391dd04
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/tutorial-enable-key-vault-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/tutorial-enable-key-vault-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/tutorial-enable-key-vault-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b92233c4-418a-1192-dcce-5bf6f7075858
---

# Protect your key vaults with the Defender for Key Vault plan - Microsoft Defender for Cloud | Microsoft Learn

Azure Key Vault is a cloud service that safeguards encryption keys and secrets like certificates, connection strings, and passwords.

Enable Microsoft Defender for Key Vault for Azure-native, advanced threat protection for Azure Key Vault, providing an additional layer of security intelligence.

Learn more about [Microsoft Defender for Key Vault](defender-for-key-vault-introduction).

You can learn more about Defender for Key Vault's pricing on [the pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Prerequisites

- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must [enable Microsoft Defender for Cloud](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.

## Enable the Key Vault plan

Microsoft Defender for Key Vault detects unusual and potentially harmful attempts to access or exploit Key Vault accounts. This layer of protection helps you address threats even if you're not a security expert, and without the need to manage third-party security monitoring systems.

**To enable Defender for Key Vault plan on your subscription**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. In the Defender for Cloud menu, select **Environment settings**.
4. Select the relevant subscription.
5. On the Defender plans page, toggle the Key Vault plan to **On**.

    [![Screenshot of the Defender for Cloud plans that shows where to enable the key vault plan toggle.](media/tutorial-enable-key-vault-plan/enable-key-vault.png)](media/tutorial-enable-key-vault-plan/enable-key-vault.png#lightbox)
6. Select **Save**.

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that provide insights into your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) helps you understand your current coverage by showing which plans are enabled on your subscriptions and resources.