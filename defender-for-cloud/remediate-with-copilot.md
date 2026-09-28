---
layout: Conceptual
title: Remediate Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/remediate-with-copilot
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
description: Learn how to remediate recommendations with Copilot in Microsoft Defender for Cloud and improve your security posture.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 9b7d3e3f-59ac-fa25-5fee-a2d79009c5c6
document_version_independent_id: 33af7702-9a48-c3e0-f3cf-7ee51f264696
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/remediate-with-copilot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/remediate-with-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/remediate-with-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: e89652f3-1ec2-3e44-3426-9c07c55bdcac
---

# Remediate Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Microsoft Security Copilot so you can remediate recommendations by using natural language prompts. This workflow helps you reduce risk and improve your security posture.

After Security Copilot summarizes a recommendation in Defender for Cloud, you can choose how to handle it. You can then use prompts to guide the remediation process. Before you start, ensure you have Defender for Cloud enabled, access to Azure Copilot, and Security Compute Units assigned for Security Copilot.

## Prerequisites

Before you begin, ensure you complete the following steps:

- [Enable Microsoft Defender for Cloud](connect-azure-subscription)
- [Review Azure Copilot overview](/en-us/azure/copilot/overview)
- [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot)

## Remediate a recommendation

Copilot in Defender for Cloud can help you remediate recommendations.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Recommendations**.
4. Select a recommendation.
5. Select **Summarize with Copilot**.
6. Review the summary.
7. Select **Fix with Copilot**.
8. Follow the prompts to have Copilot fix the recommendation.
9. (Optional) If a script is presented, select **Run** to apply the remediation.

If you're unable or unsure how to remediate a recommendation, ask Copilot for more information. You can also delegate the recommendation to an appropriate person if needed.