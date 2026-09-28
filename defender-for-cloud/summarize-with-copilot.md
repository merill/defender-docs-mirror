---
layout: Conceptual
title: Summarize Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/summarize-with-copilot
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
description: Learn how to summarize recommendations with Microsoft Security Copilot in Microsoft Defender for Cloud and improve your security posture.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 0d69b492-52d0-1873-8f7d-25a717ed12fa
document_version_independent_id: b0f422ae-32d3-d883-3f67-f9380e5dc1a9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/summarize-with-copilot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/summarize-with-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/summarize-with-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 6fd1b2cf-2c56-5a71-909d-18121dddea64
---

# Summarize Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud works with Microsoft Security Copilot. You can use this feature to summarize recommendations and better understand risks in your environment.

When you summarize a recommendation, you get a quick overview in plain language. The summary helps you learn what the recommendation means and decide what to fix first.

## Prerequisites

- [Enable Defender for Cloud on your environment](connect-azure-subscription).
- [Have access to Azure Copilot](/en-us/azure/copilot/overview).
- [Have Security Compute Units assigned for Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot).

## Summarize with Copilot

Select a recommendation, and then use Copilot to summarize it. Enter prompts to learn more and decide what to do next.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Recommendations**.
4. Select a recommendation.
5. Select **Summarize with Copilot**.

    [![Screenshot of a recommendation that shows where the Summarize with Copilot button is located.](media/summarize-with-copilot/summarize-with-copilot.png)](media/summarize-with-copilot/summarize-with-copilot.png#lightbox)
6. Review the provided summary.
7. Enter more prompts as needed.

    [![Screenshot of the Copilot window that shows the summary of the recommendation.](media/summarize-with-copilot/summarize-with-copilot-results.png)](media/summarize-with-copilot/summarize-with-copilot-results.png#lightbox)

When you understand the recommendation, decide how to handle it. Copilot stays open so you can enter other prompts as needed.