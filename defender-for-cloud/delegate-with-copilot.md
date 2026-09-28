---
layout: Conceptual
title: Delegate Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/delegate-with-copilot
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
description: Learn how to delegate recommendations with Copilot in Microsoft Defender for Cloud and improve your security posture.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: bb36f78a-4fc0-663a-2f46-81954019fc99
document_version_independent_id: e5551cbe-82ac-037d-b385-1a7a86c055d3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/delegate-with-copilot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/delegate-with-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/delegate-with-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: ccaad95b-c8ce-b670-fd9d-f05e930d4f6e
---

# Delegate Recommendations with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn

Use Microsoft Security Copilot prompts to delegate recommendations in Defender for Cloud. Assign a recommendation to a person or team. The right people can then handle risks in your environment. This article walks you through how to use Copilot to summarize a recommendation, generate a delegation message, and track remediation progress.

## Prerequisites

Before you start, ensure you meet these requirements:

- [Enable Defender for Cloud on your environment](connect-azure-subscription)
- [Access to Azure Copilot](/en-us/azure/copilot/overview)
- [Security Compute Units (SCUs) assigned for Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot)

## Delegate a recommendation

To assign a recommendation to the right person or team for remediation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Recommendations**.
4. Select a recommendation.
5. Select **Summarize with Copilot**.
6. Review the summary.
7. Select **Generate message with Copilot**.
8. Delegate the recommendation with the provided prompts.

After you delegate the recommendation, monitor remediation progress on the Recommendations page. Copilot stays open, so you can enter more prompts as needed.