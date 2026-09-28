---
layout: Conceptual
title: Discover generative AI workloads - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/identify-ai-workload-model
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
description: Learn how to use the cloud security explorer to determine which AI workloads and models are running in your environment.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 3bbadbbf-b591-5874-87b9-ad4699737256
document_version_independent_id: 29ef2648-cd5d-2f25-94f0-dc104d2fadac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/identify-ai-workload-model.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/identify-ai-workload-model
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/identify-ai-workload-model.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: b6fb4cef-12fc-2580-5e00-62bc12ac4e95
---

# Discover generative AI workloads - Microsoft Defender for Cloud | Microsoft Learn

The Defender Cloud Security Posture Management (CSPM) plan in Microsoft Defender for Cloud provides a comprehensive view of your organization's AI Bill of Materials (AI BOM). The instructions in this article explain how to use the cloud security explorer to identify the AI workloads and models that are running in your environment. With the cloud security explorer query results, you can assess the security posture of the scanned AI workloads.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Read about [AI security posture management](ai-security-posture).
- Learn more about [investigating risks with the cloud security explorer and attack paths](concept-attack-path).
- You need a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Enable [Defender for Cloud on your Azure subscription](connect-azure-subscription).
- Enable [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) on your Azure subscription.
- Have at least one environment with AI supported workloads (Azure OpenAI, AWS account).

## Discover AI workloads and models in use

The cloud security explorer can be used to identify generative AI workloads and models running in your environment.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Select the **AI workloads and models in use** query template.

    [![Screenshot that shows where to locate the AI workloads and models in use query template in the Cloud Security Explorer page.](media/identify-ai-workload-model/ai-workload-query.png)](media/identify-ai-workload-model/ai-workload-query.png#lightbox)
4. Select **Search**.
5. Select a result to review its details.

    [![Screenshot of the results of the query with one of the results selected and the results detail pane open.](media/identify-ai-workload-model/result-details.png)](media/identify-ai-workload-model/result-details.png#lightbox)
6. Select a node to review the findings.

    The node findings show the deployed models that are running on your resources and specific model metadata for those deployments.