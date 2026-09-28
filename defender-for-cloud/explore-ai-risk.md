---
layout: Conceptual
title: Explore risks to pre-deployment generative AI artifacts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/explore-ai-risk
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
description: Learn how to discover potential security risks for your generative AI applications in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 9da092e8-4b4e-da44-ae75-b8b9c49b1b8e
document_version_independent_id: 3434262f-dac3-9dcf-adee-27e82cbd4441
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/explore-ai-risk.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/explore-ai-risk
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/explore-ai-risk.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b1ad67d0-188b-a985-a96d-8255e916f075
---

# Explore risks to pre-deployment generative AI artifacts - Microsoft Defender for Cloud | Microsoft Learn

The Defender Cloud Security Posture Management (CSPM) plan in Microsoft Defender for Cloud helps you secure your generative AI apps. It scans AI artifacts, such as container images and code repositories, to find known vulnerabilities in AI libraries.

In this article, you use the cloud security explorer in Defender for Cloud to find containers running vulnerable generative AI images and to identify vulnerable code repositories that provision Azure OpenAI. After you complete these steps, you can review findings and remediate recommendations.

## Prerequisites

Before you begin, make sure you meet the following prerequisites:

- Read about [AI security posture management](ai-security-posture).
- Learn more about [investigating risks with the cloud security explorer and attack paths](concept-attack-path).
- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Enable [Defender for Cloud on your Azure subscription](connect-azure-subscription).
- Enable [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) on your Azure subscription.
- Have at least one [Azure OpenAI resource](/en-us/azure/ai-studio/how-to/create-azure-ai-resource), with at least one [model deployment](/en-us/azure/ai-studio/how-to/deploy-models-openai) connected to it via Azure AI Foundry portal.

## Identify containers running on vulnerable generative AI container images

Use the cloud security explorer to find containers that run generative AI images with known vulnerabilities.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Select the **Container running container images with known Generative AI vulnerabilities** query template.

    [![Screenshot that shows where to locate the generative AI vulnerable container images query.](media/explore-ai-risk/gen-ai-vulnerable-images-query.png)](media/explore-ai-risk/gen-ai-vulnerable-images-query.png#lightbox)
4. Select **Search**.
5. Select a result to review its details.

    [![Screenshot that shows a sample of results for the vulnerable image query.](media/explore-ai-risk/vulnerable-images-results.png)](media/explore-ai-risk/vulnerable-images-results.png#lightbox)
6. Select a node to review the findings.

    [![Screenshot that shows the details of the selected containers node.](media/explore-ai-risk/vulnerable-images-results-details.png)](media/explore-ai-risk/vulnerable-images-results-details.png#lightbox)
7. In the insights section, select a CVE ID from the drop-down menu.
8. Select **Open the vulnerability page**.
9. [Remediate the recommendation](implement-security-recommendations#remediate-a-recommendation).

## Identify vulnerable generative AI code repositories

Use the cloud security explorer to find vulnerable generative AI code repositories that provision Azure OpenAI.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Select the **Generative AI vulnerable code repositories that provision Azure OpenAI** query template.

    [![Screenshot that shows where to locate the generative AI vulnerable code repositories query.](media/explore-ai-risk/gen-ai-vulnerable-code-query.png)](media/explore-ai-risk/gen-ai-vulnerable-code-query.png#lightbox)
4. Select **Search**.
5. Select a result to review its details.

    [![Screenshot that shows a sample of results for the vulnerable code query.](media/explore-ai-risk/vulnerable-results.png)](media/explore-ai-risk/vulnerable-results.png#lightbox)
6. Select a node to review the findings.

    [![Screenshot that shows the details of the selected vulnerable code node.](media/explore-ai-risk/vulnerable-results-details.png)](media/explore-ai-risk/vulnerable-results-details.png#lightbox)
7. In the insights section, select a CVE ID from the drop-down menu.
8. Select **Open the vulnerability page**.
9. [Remediate the recommendation](implement-security-recommendations#remediate-a-recommendation).