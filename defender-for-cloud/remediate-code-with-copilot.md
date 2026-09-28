---
layout: Conceptual
title: Remediate Code with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/remediate-code-with-copilot
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
description: Learn how Microsoft Security Copilot in Defender for Cloud helps fix Infrastructure as Code misconfigurations by generating pull requests.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d636a360-08e4-507c-742e-71bfb7af0fd2
document_version_independent_id: 30ecd595-7111-e667-8611-cec204209e53
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/remediate-code-with-copilot.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/remediate-code-with-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/remediate-code-with-copilot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: f8492fe9-5b28-e75f-852f-fd20c1013f07
---

# Remediate Code with Microsoft Security Copilot - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with Microsoft Security Copilot to help you fix Infrastructure as Code (IaC) issues in your code repositories. By using Copilot, you can catch and fix security issues early in the development cycle. Copilot creates pull requests (PRs) that correct the problems it finds. Automatically generated PRs help ensure that code issues are fixed quickly and correctly.

Before you get started, make sure you meet the prerequisites for Defender for Cloud, Security Copilot, and repository integration.

## Prerequisites

Before you begin, make sure the following prerequisites are in place:

- [Enable Defender for Cloud on your environment](connect-azure-subscription)
- [Connect your Azure DevOps environment to Defender for Cloud](quickstart-onboard-devops)
- [Configure the Microsoft Security DevOps Azure DevOps extension](azure-devops-extension)
- [Review and ensure you meet the DevOps security support and prerequisites requirements](devops-support)
- [Have access to Azure Copilot](/en-us/azure/copilot/overview).
- [Have Security Compute Units assigned for Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot)

## Remediate an Infrastructure as Code scanning finding

You can use Copilot in Defender for Cloud to fix flagged issues. Follow these steps to resolve a finding:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Go to **Recommendations**.
4. Search for and select the **Azure DevOps repositories should have infrastructure as code scanning findings resolved** recommendation.

    [![Screenshot that shows the recommendation that you searched for.](media/remediate-code-with-copilot/search-recommendation.png)](media/remediate-code-with-copilot/search-recommendation.png#lightbox)
5. Select **Reduce risk with Copilot**.

    [![Screenshot that shows where the Summarize with copilot button is located.](media/remediate-code-with-copilot/copilot-summarize.png)](media/remediate-code-with-copilot/copilot-summarize.png#lightbox)
6. Select **Help me remediate this recommendation**.
7. Select **security check**.
8. Select the description that matches the security check finding.
9. Select **Select**.

    [![Screenshot that shows where the select button is located.](media/remediate-code-with-copilot/select-select.png)](media/remediate-code-with-copilot/select-select.png#lightbox)
10. Review the summary of the code fix.
11. Select **Submit**.
12. Select the pull request link shown in the Copilot results.
13. Review the pull request.

After Copilot creates the pull request in your code repository, a developer should review and approve it before merging.