---
layout: Conceptual
title: Overview of API security testing integrations (preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-partner-applications
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
description: Learn about security testing scan results from partner applications within Microsoft Defender for Cloud.
ms.topic: concept-article
ms.date: 2024-11-26T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 703d538d-19a2-0ee8-e2b3-4f51adff58c2
document_version_independent_id: 2bd4a435-53a0-d46f-a62a-e9dcbe013eac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-partner-applications.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-partner-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-partner-applications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 257c4087-c57f-b61e-8480-7a3b29cbc50b
---

# Overview of API security testing integrations (preview) - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud supports partner tools to help enhance the existing runtime security capabilities that are provided by Defender for APIs. Defender for Cloud supports proactive API security testing capabilities in early stages of the development lifecycle (including source code repositories & CI/CD pipelines).

The support for partner solutions helps to further streamline, integrate, and orchestrate security findings from partner solutions with Microsoft Defender for Cloud. This support enables full lifecycle API security, and the ability for security teams to effectively discover and remediate API security vulnerabilities before they're deployed in production.

The security scan results from partner applications are available within Defender for Cloud. The ability to view the results in Defender for Cloud ensures that central security teams have visibility into the health of APIs within the Defender for Cloud recommendation experience. These security teams can now take governance steps that are natively available through Defender for Cloud recommendations, and extensibility to export scan results from the Azure Resource Graph into management tools of their choice.

[![Screenshot of a sample security analysis recommendation page.](media/defender-partner-applications/api-security.png)](media/defender-partner-applications/api-security.png#lightbox)

## Prerequisites

This feature requires a DevOps connector in Defender for Cloud. See [how to onboard DevOps environments](devops-support).

| Aspect | Details |
| --- | --- |
| Release state | Preview  The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability. |
| Required/preferred environmental requirements | APIs within source code repository, including API specification files such as OpenAPI, Swagger. |
| Clouds | Available in commercial clouds. Not available in national/sovereign clouds (Azure Government, Microsoft Azure operated by 21Vianet). |
| Source code management systems | [GitHub Enterprise Cloud](https://docs.github.com/enterprise-cloud@latest/admin/overview/about-github-enterprise-cloud). This also requires a license for GitHub Advanced Security (GHAS). [Azure DevOps Services](https://azure.microsoft.com/products/devops/) |

## Supported applications

| Logo | Partner name | Description | Enablement Guide |
| --- | --- | --- | --- |
| ![](media/defender-partner-applications/42crunch-logo.png) | [42Crunch onboarding guide](https://aka.ms/APISecurityTestingPartnershipIgnite2023) | Developers can proactively test and harden APIs within their CI/CD pipelines through static and dynamic testing of APIs against the top OWASP API risks and OpenAPI specification best practices. | [42Crunch technical onboarding guide](onboarding-guide-42crunch) |
| ![](media/defender-partner-applications/stackhawk-logo.png) | [StackHawk](https://aka.ms/APISecurityTestingPRStackHawk) | StackHawk is the only modern DAST and API security testing tool that runs in CI/CD, enabling developers to quickly find and fix security issues before they hit production. | [StackHawk onboarding guide](https://aka.ms/APISecurityTestingOnboardingGuideStackHawk) |
| ![](media/defender-partner-applications/bright-security-logo.png) | [Bright Security](https://brightsec.com/news/bright-securitys-enterprise-grade-dev-centric-dast-integrates-with-microsoft-defender-for-cloud/) | Bright Security’s dev-centric DAST platform empowers both developers and AppSec professionals with enterprise grade security testing capabilities for web applications, APIs, and GenAI and LLM applications. Bright knows how to deliver the right tests, at the right time in the SDLC, in developers and AppSec tools and stacks of choice with minimal false positives and alert fatigue. | [Bright Security onboarding guide](https://aka.ms/APISecurityTestingOnboardingGuideBrightSecurity) |