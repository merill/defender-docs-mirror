---
layout: Conceptual
title: Microsoft Security Copilot in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/copilot-security-in-defender-for-cloud
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
description: Learn about the benefits of copilot in Microsoft Defender for Cloud and how it applies to analyzing your security posture.
ms.date: 2025-09-25T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: fe4e12cd-0379-84d5-c8d0-a972f5de0daa
document_version_independent_id: 87670968-67a2-a3a2-7045-0216ec0cc124
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/copilot-security-in-defender-for-cloud.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/copilot-security-in-defender-for-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/copilot-security-in-defender-for-cloud.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 303fbbca-1887-2e50-9a07-eb71c5c9181c
---

# Microsoft Security Copilot in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates Microsoft Security Copilot and Microsoft Copilot for Azure into its experience. These integrations let you ask security-related questions, receive responses, and automatically trigger the necessary skills to analyze, summarize, remediate, and delegate recommendations by using natural language prompts.

Both [Security Copilot](/en-us/copilot/security/microsoft-security-copilot) and [Copilot for Azure](/en-us/azure/copilot/overview?wt.mc_id=copilot_1a_webpage_gdc) are cloud-based AI platforms that provide a natural language copilot experience. These platforms help security professionals understand the context and effect of recommendations, remediate or delegate tasks, and address misconfigurations in code.

Defender for Cloud's integration with Security Copilot and Copilot for Azure on the recommendations page lets you enhance your security posture and mitigate risks in your environments. It streamlines the process of understanding and implementing recommendations, making your security management more efficient and effective.

## Learn more about Security Copilot

If you're new to Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Microsoft Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Microsoft Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Microsoft Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Microsoft Security Copilot](/en-us/security-copilot/prompting-security-copilot)

## Security Copilot integration in Defender for Cloud

Defender for Cloud integrates Copilot directly into the Defender for Cloud experience. With this integration, you can analyze, summarize, remediate, and delegate your recommendations by using natural language prompts.

[![Screenshot showing the location of the 'Analyze with Copilot' button on the recommendations page.](media/copilot-security-in-defender-for-cloud/analyze-copilot.png)](media/copilot-security-in-defender-for-cloud/analyze-copilot.png#lightbox)

When you open Copilot, you can use natural language prompts to ask questions about the recommendations. Copilot provides responses in natural language, helping you understand the context of the recommendation. It explains the effect of implementing the recommendation and provides steps for implementation.

Some sample prompts include:

- Show critical risks for publicly exposed resources
- Show critical risks to sensitive data
- Show resources with high severity vulnerabilities

Copilot can assist with refining recommendations, providing summaries, remediation steps, and delegation. It enhances your ability to analyze and act on recommendations.

[![Screenshot showing the location of the 'Summarize with Copilot' button on a recommendation.](media/copilot-security-in-defender-for-cloud/summarize-copilot.png)](media/copilot-security-in-defender-for-cloud/summarize-copilot.png#lightbox)

## Key features

The following section provides information about the available features in Security Copilot in Defender for Cloud.

### Data processing workflow

When you use Security Copilot in Defender for Cloud, the following data processing workflow takes place:

1. A user enters a prompt in the Copilot interface.
2. Copilot for Azure receives the prompt.
3. Copilot for Azure evaluates the prompt and the active page to determine the skills needed to resolve the prompt.
4. If the prompt is security related and the skill is available, Security Copilot executes the skills and sends back a response to Copilot in Azure for presentation.
5. If a security-related prompt is received but the skill is unavailable, Azure Copilot searches all of its available skills to find the most relevant skills to resolve the prompt. It then sends a response to the user.

    [![Diagram showing the data processing workflow of the Copilot experience in Defender for Cloud.](media/copilot-security-in-defender-for-cloud/data-process-workflow.png)](media/copilot-security-in-defender-for-cloud/data-process-workflow.png#lightbox)

Check out the [Security Copilot FAQs](faq-copilot).

## Enable the Security Copilot integration in Defender for Cloud

Security Copilot in Defender for Cloud doesn't rely on any of the available plans in Defender for Cloud. Security Copilot is available for all users when you:

1. [Enable Defender for Cloud on your environment](connect-azure-subscription).
2. [Have access to Azure Copilot](/en-us/azure/copilot/overview).
3. [Have Security Compute Units assigned for Security Copilot](/en-us/copilot/security/get-started-security-copilot).

To enjoy the full range of Security Copilot's capabilities in Defender for Cloud, enable the [Defender for Cloud Security Posture Management (DCSPM) plan](concept-cloud-security-posture-management#plan-availability) on your environments. The DCSPM plan includes extra security. These features include [Attack path analysis](how-to-manage-attack-path), [Risk prioritization](risk-prioritization), and others. You can use Security Copilot to navigate and manage each feature. Without the DCSPM plan, you can still use Security Copilot in Defender for Cloud, but with limited capacity.

## Monitor your usage

Security Copilot has a usage limit. When the usage in your organization nears its limit, you're notified when you submit a prompt. To avoid a disruption of service, contact the Azure capacity owner or contributor to increase the Security Compute Units (SCU) or limit the number of prompts.

Learn more about [usage limits](/en-us/copilot/security/manage-usage).

## Provide feedback

Your feedback on the Defender for Cloud integration with Security Copilot helps with development. Provide feedback in Copilot, with the **How's this response** after each completed prompt, and select any of the following options:

- **Looks right** - Select this option if the results are accurate, based on your assessment.
- **Needs improvement** - Select this option if any detail in the results is incorrect or incomplete, based on your assessment.
- **Inappropriate** - Select this option if the results contain questionable, ambiguous, or potentially harmful information.

For each feedback option, you can provide more information in the next dialog box that appears. Whenever possible, and when the result is **Needs improvement**, write a few words explaining what can be done to improve the outcome. If you entered prompts specific to Defender for Cloud and the results aren't related, include that information.

## Privacy and data security in Security Copilot

When you interact with Security Copilot to get Defender TI data, Copilot pulls that data from Defender for Cloud. The prompts, the data retrieved, and the output shown in the prompt results are processed and stored within the Copilot service.

[Learn more about privacy and data security in Microsoft Security Copilot](/en-us/security-copilot/privacy-data-security).