---
layout: FAQ
title: Common questions - Copilot in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-copilot
summary: >
  <p>Microsoft Defender for Cloud's integration with Microsoft Security Copilot brings the benefits of AI and automation to your security operations. Copilot helps you prioritize and respond to security incidents faster and more effectively.</p>
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
description: Frequently asked questions about Copilot for Microsoft Defender for Cloud.
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: bb104b12-e754-7c92-c706-139e542dbb2c
document_version_independent_id: e539e628-02db-b313-e529-a5623cadb0d9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-copilot.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-copilot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-copilot.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 1ba43c30-396c-5e9a-9044-34856a2b602a
---

# Common questions - Copilot in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's integration with Microsoft Security Copilot brings the benefits of AI and automation to your security operations. Copilot helps you prioritize and respond to security incidents faster and more effectively.

## What can go wrong when I enter a prompt into Copilot for Azure?

When you enter a prompt into Copilot for Azure, you might encounter the following issues:

- Copilot for Azure might fail to choose a skill.
- Copilot for Azure might not select the Defender for Cloud skill.
- Copilot for Azure might select its own skill instead of a Defender for Cloud skill. For example, a skill belonging to Azure documentation, a skill focused on Azure alerts.
- A Microsoft Security Copilot skill might be selected. For example, CVS related prompts can sometimes be answered by [Microsoft Defender External Attack Surface Management](https://azure.microsoft.com/products/defender-external-attack-surface-management/) skills.
- A Defender for Cloud skills is selected but the user doesn't have Microsoft Security Copilot security compute units (SCUs). Learn more about [managing the usage of SCUs in Microsoft Security Copilot](/en-us/copilot/security/manage-usage).
- A Defender for Cloud skill is selected but the response can be blocked by security measures.

## Is it possible for a user to submit a prompt with the intentions of Microsoft Security Copilot of answering it and Azure Copilot answering it instead?

Yes. If you ask a question that doesn't relate to a skill that Defender for Cloud currently supports, Azure Copilot attempts to answer the question based on the skills and data available to it.

## How can I know which skills are currently supported?

To get a better understanding of the skills that Defender for Cloud currently supports, check out [Analyze recommendations with Microsoft Security Copilot](analyze-with-copilot).

## Is there a way to determine which Copilot is responding to a user’s prompt?

Yes. When you submit a prompt, a progress screen appears. If the message `Using Microsoft Security Copilot` appears, then Azure Copilot passed along the prompt to Microsoft Security Copilot to respond.

[![Screenshot that shows the copilot window showing the words Using Microsoft Security Copilot.](media/faq-copilot/using-copilot.png)](media/faq-copilot/using-copilot.png#lightbox)

## What happens when Azure Copilot or Microsoft Security Copilot can't handle a user prompt?

If a prompt can't be answered by either Azure Copilot or Microsoft Security Copilot, a response stating "Sorry, I can't assist with that" will be displayed.

## I got a response from one of the Copilots that is inaccurate, what should I do?

For any responses that somehow deviate from your expectations, we recommend using the feedback option that appears after the prompt by selecting up the thumbs-up or thumbs-down buttons.

## Is there a way to force Azure Copilot to use Microsoft Security Copilot for all prompts?

No.

## Will I be charged for using Azure Copilot if my skill is executed by Microsoft Security Copilot?

No.