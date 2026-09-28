---
layout: Conceptual
title: Remediate machine secrets in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/remediate-server-secrets
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
description: Learn how to remediate security issues with machine secrets in Microsoft Defender for Cloud.
ms.topic: overview
ms.date: 2026-04-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 923785e4-ca77-335a-ad28-2d006d427b45
document_version_independent_id: 2c41620d-b961-0150-301a-c8bab127b123
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/remediate-server-secrets.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/remediate-server-secrets
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/remediate-server-secrets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: f4bca702-cb0c-2947-d800-57d1a7a056a6
---

# Remediate machine secrets in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud can [scan machines and cloud deployments](secrets-scanning) for [supported secrets](secrets-scanning#secrets-support), to reduce lateral movement risk.

This article helps you to identify and remediate [machine secrets scan](secrets-scanning-servers) findings.

Note

This page describes the classic Recommendations view in Defender for Cloud. For the latest experience in the Depender portal, see [Review security recommendations](review-security-recommendations).

- You can review and remediate findings using [machine secrets recommendations](secrets-scanning-servers#machine-secrets-recommendations).
- View secrets discovered on a specific machine in the [Defender for Cloud inventory](asset-inventory)
- Drill down into machine secrets findings using [cloud security explorer queries](secrets-scanning-servers#predefined-cloud-security-explorer-queries) and [machine secrets attack paths](secrets-scanning-servers#machine-secrets-attack-paths)
- Not every method is supported for every secret. Review the [supported methods](secrets-scanning#reviewing-secrets-findings) for different types of secrets.

It’s important to be able to prioritize secrets and identify which ones need immediate attention. To help you do this, Defender for Cloud provides:

- Providing rich metadata for every secret, such as last access time for a file, a token expiration date, an indication whether the target resource that the secrets provide access to exists, and more.
- Combining secrets metadata with cloud assets context. This helps you to start with assets that are exposed to the internet, or contain secrets that might compromise other sensitive assets. Secrets scanning findings are incorporated into risk-based recommendation prioritization.
- Providing multiple views to help you pinpoint the mostly commonly found secrets, or assets containing secrets.

## Prerequisites

- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Defender for Cloud](get-started) must be available in your Azure subscription.
- At least one of these plans [must be enabled](connect-azure-subscription#enable-all-paid-plans-on-your-subscription):
    - [Defender for Servers Plan 2](defender-for-servers-overview)
    - [Defender CSPM](concept-cloud-security-posture-management)
- [Agentless machine scanning](concept-agentless-data-collection) must be enabled.

## Remediate secrets with recommendations

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Expand the **Remediate vulnerabilities** security control.
4. Select one of the relevant recommendations:

    - **Azure resources**: `Machines should have secrets findings resolved`
    - **AWS resources**: `EC2 instances should have secrets findings resolved`
    - **GCP resources**: `VM instances should have secrets findings resolved`

        [![Screenshot that shows either of the two results under the Remediate vulnerabilities security control.](media/secret-scanning/recommendation-findings.png)](media/secret-scanning/recommendation-findings.png#lightbox)
5. Expand **Affected resources** to review the list of all resources that contain secrets.
6. In the Findings section, select a secret to view detailed information about the secret.

    [![Screenshot that shows the detailed information of a secret after you selected the secret in the findings section.](media/secret-scanning/select-findings.png)](media/secret-scanning/select-findings.png#lightbox)
7. Expand **Remediation steps** and follow the listed steps.
8. Expand **Affected resources** to review the resources affected by this secret.
9. (Optional) You can select an affected resource to see the resource's information.

Secrets that don't have a known attack path are referred to as `secrets without an identified target resource`.

## Remediate secrets for a machine in the inventory

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Inventory**.
3. Select the relevant VM.
4. Go to the **Secrets** tab.
5. Review each plaintext secret that appears with the relevant metadata.
6. Select a secret to view extra details of that secret.

    Different types of secrets have different sets of additional information. For example, for plaintext SSH private keys, the information includes related public keys (mapping between the private key to the authorized keys’ file we discovered or mapping to a different virtual machine that contains the same SSH private key identifier).

## Remediate secrets with attack paths

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations** &gt; **Attack path**.

    [![Screenshot that shows how to navigate to your attack path in Defender for Cloud.](media/secret-scanning/attack-path.png)](media/secret-scanning/attack-path.png#lightbox)
3. Select the relevant attack path.
4. Follow the remediation steps to remediate the attack path.

## Remediate secrets with cloud security explorer

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Select one of the following templates:

    - **VM with plaintext secret that can authenticate to another VM** - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access other VMs or EC2s.
    - **VM with plaintext secret that can authenticate to a storage account** - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access storage accounts.
    - **VM with plaintext secret that can authenticate to an SQL database** - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access SQL databases.

If you don't want to use any of the available templates, you can also [build your own query](how-to-manage-cloud-security-explorer) in the cloud security explorer.