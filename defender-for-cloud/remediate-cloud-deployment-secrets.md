---
layout: Conceptual
title: Remediate cloud deployment secrets security issues in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/remediate-cloud-deployment-secrets
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
description: Learn how to remediate cloud deployment secrets security issues in Microsoft Defender for Cloud.
ms.topic: overview
ms.date: 2025-05-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 3812a61b-f3ff-39b6-1304-3e812aeddd02
document_version_independent_id: 340ee99c-14ec-92c4-4940-4101e073608c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/remediate-cloud-deployment-secrets.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/remediate-cloud-deployment-secrets
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/remediate-cloud-deployment-secrets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d2d1ffb8-febe-c2fd-7dac-a8a04a612524
---

# Remediate cloud deployment secrets security issues in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides secrets scanning for virtual machines, and for cloud deployments, to reduce lateral movement risk.

This article helps you to identify and remediate security risks with cloud deployment secrets.

## Prerequisites

- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Defender for Cloud](get-started) must be available in your Azure subscription.
- The [Defender Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management) plan.
- [Agentless machine scanning](concept-agentless-data-collection) must be enabled.

## Remediate secrets with attack paths

Attack path analysis is a graph-based algorithm that scans your [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph) to expose exploitable paths that attackers might use to reach high-impact assets.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations** &gt; **Attack path**.

    [![Screenshot that shows how to navigate to your attack path in Defender for Cloud.](media/secret-scanning/attack-path.png)](media/secret-scanning/attack-path.png#lightbox)
3. Select the relevant attack path.
4. Follow the remediation steps to remediate the attack path.

## Remediate secrets with recommendations

If a secret is found on your resource, that resource triggers an affiliated recommendation that is located under the **Remediate vulnerabilities** security control on the Defender for Cloud **Recommendations** page.

Defender for Cloud provides a [number of cloud deployment secrets security recommendations](secrets-scanning-cloud-deployment#security-recommendations).

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Expand the **Remediate vulnerabilities** security control.
4. Select one of the relevant recommendations.
5. Expand **Affected resources** to review the list of all resources that contain secrets.
6. In the Findings section, select a secret to view detailed information about the secret.
7. Expand **Remediation steps** and follow the listed steps.
8. Expand **Affected resources** to review the resources affected by this secret.
9. (Optional) You can select an affected resource to see that resource's information.

Secrets that don't have a known attack path are referred to as `secrets without an identified target resource`.

## Remediate secrets with cloud security explorer

The [cloud security explorer](concept-attack-path#what-is-cloud-security-explorer) enables you to proactively identify potential security risks within your cloud environment. It does so by querying the [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph).

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Create a query to look for secrets in your cloud deployments. To do this, select a resource type, and then select the types of secret you want to find. For example:

    [![Screenshot that shows a sample query for finding cloud deployment secrets in the cloud security graph.](media/remediate-cloud-deployment-secrets/query-example.png)](media/remediate-cloud-deployment-secrets/query-example.png#lightbox)

## Remediate secrets in the asset inventory

Your [asset inventory](asset-inventory) shows the [security posture](concept-cloud-security-posture-management) of the resources you've connected to Defender for Cloud. You can view the secrets discovered on a specific machine.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Inventory**.
3. Select the relevant VM.
4. Go to the **Secrets** tab.
5. Review each plaintext secret that appears with the relevant metadata.
6. Select a secret to view extra details of that secret.

Different types of secrets have different sets of additional information. For example, for plaintext SSH private keys, the information includes related public keys (mapping between the private key to the authorized keys’ file we discovered or mapping to a different virtual machine that contains the same SSH private key identifier).