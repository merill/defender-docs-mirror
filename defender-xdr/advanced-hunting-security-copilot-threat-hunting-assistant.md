---
layout: Conceptual
title: Microsoft Security Copilot Threat Hunting Assistant in advanced hunting - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-security-copilot-threat-hunting-assistant
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft Security Copilot Threat Hunting Assistant can help you investigate threats using natural language.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 751f384a-af5f-5062-b2eb-855ce08875f0
document_version_independent_id: 751f384a-af5f-5062-b2eb-855ce08875f0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-security-copilot-threat-hunting-assistant.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-security-copilot-threat-hunting-assistant
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-security-copilot-threat-hunting-assistant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 87bf0a67-7b09-ff71-5cd1-271a05f12b7e
---

# Microsoft Security Copilot Threat Hunting Assistant in advanced hunting - Microsoft Defender XDR | Microsoft Learn

The Microsoft Security Copilot Threat Hunting Assistant is an AI-powered experience that revolutionizes threat hunting by enabling you to investigate threats using natural language from start to finish. Unlike traditional hunting methods that rely heavily on Kusto query language (KQL) expertise, the Threat Hunting Assistant transforms complex data into actionable insights quickly and intuitively, helping you drive the investigation into actions.

The Threat Hunting Assistant goes beyond query generation by delivering a complete, conversational threat hunting experience. It not only generates queries but also interprets results, surfaces insights, and guides you through full hunting sessions. These capabilities empower analysts of all levels to hunt threats faster, more accurately, and with greater confidence.

Watch this video to get an overview of the Threat Hunting Assistant:

## Key capabilities of the Threat Hunting Assistant

The Threat Hunting Assistant provides the following key capabilities:

- **Natural language question to natural language answer.** Ask any data-related question in natural language (for example, *Which devices communicated with IPs in France in the last 24 hours?*) and receive direct conversational answers backed by KQL queries and tabular results.
- **Conversational flow.** The assistant keeps track of context throughout your hunting session, enabling you to ask follow-up questions that build on previous ones and ensuring continuity across the entire session.
- **Schema-aware data discovery.** The assistant checks which tables are available to you and reads their schemas before it writes a query, so queries are grounded in your environment's actual data rather than assumed table names. This includes custom tables in your Microsoft Sentinel workspace.
- **Iterative refinement.** The assistant evaluates the results it gets back and adjusts its approach if they don't answer your question, for example by bringing in an additional table. You can follow its progress in the Copilot side pane as it works.
- **Observations.** The assistant provides natural language observations and charts (pie, timeline, or vertical bar) to simplify result analysis. It selects relevant chart fields automatically, but you can change the chart type or grouping afterward.
- **Insight generation.** The assistant surfaces additional contextual insights from related data sources to enrich your investigation, helping you discover connections and patterns that might otherwise be missed.
- **Smart suggestions.** The assistant suggests follow-up questions and remediation actions based on your investigation. These suggestions appear only after a response is generated. These suggestions reset when you ask a new question.
- **Integrated experience.** The assistant's outputs are directly added to Advanced hunting components, with generated KQL placed in the editor and results displayed as usual. This integration gives users full access to all advanced hunting features during investigations, ensuring maximum flexibility.

## Try your first request

To start using the Threat Hunting Assistant, follow these steps:

Note

Make sure that the Threat Hunting Assistant mode is active. [Get access to Security Copilot in advanced hunting](advanced-hunting-security-copilot#get-access)

1. Open the **Advanced hunting** page from the navigation bar in the Microsoft Defender portal. The Copilot side pane appears on the right.

    [![Screenshot of the Copilot pane in advanced hunting.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-pane-big.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-pane-big.png#lightbox)

    You can also reopen Copilot by selecting **Copilot** at the top of the query editor.
2. Start your hunting session by selecting a suggested prompt or typing a question in natural language in the prompt bar and pressing ![](media/advanced-hunting-security-copilot/send.png) or Enter.

**Sample questions you can ask the assistant:**

- Give me the list of users who sent more than 100 emails in the last 30 days.
- Show me all failed sign-in attempts for admin accounts this week.
- Which devices communicated with suspicious domains today?

The assistant supports all types of hunting scenarios, including:

- Investigating an alert or incident
- Investigating a suspicious indicator of compromise (IOC)
- Reviewing the impact of an attack from a threat intelligence report
- Testing a security hypothesis

## Understand the response

When the Threat Hunting Assistant responds to your question, you get a comprehensive answer that includes:

- **Direct conversational answer:** A natural language response to your question is displayed in the Copilot side pane.

    [![Screenshot of the Copilot pane in advanced hunting with the answer highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-answer.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-answer.png#lightbox)
- **KQL query and results:** The underlying KQL query is generated and run automatically, with the results displayed in the advanced hunting results pane and seamlessly integrated into the experience.

    [![Screenshot of the advanced hunting page with query and results highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-query.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-query.png#lightbox)
- **Explanation of how the query was built:** To check how Copilot came up with the query, select **See the logic behind the query** below the query.

    [![Screenshot of the Copilot pane in advanced hunting with the logic behind the query highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-logic.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-logic.png#lightbox)
- **Observations:** Data highlights and a chart are displayed above the results, simplifying results analysis. You can change the chart type or field grouping.

    [![Screenshot of the advanced hunting page with Copilot-generated chart highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-chart.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-chart.png#lightbox)
- **Contextual insights:** Additional insights derived from various appropriate resources are displayed in the Copilot side pane as part of the natural language response.

    [![Screenshot of the Copilot pane in advanced hunting with insights highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-insights.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-insights.png#lightbox)
- **Smart follow-up suggestions:** Recommended next questions or actions are displayed at the bottom of the Copilot side pane to help drive your hunt in the right direction:

    - **Follow-up question suggestions** appear and the bottom of the side pane, above the prompt. Select one of the questions to run it automatically.

        [![Screenshot of the Copilot pane in advanced hunting with follow-up suggestions highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-suggestions.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-suggestions.png#lightbox)
    - You might also get **Action suggestions** in case a remediation action is recommended and needed in the context of your investigation. When you select an action suggestion, the **Take actions** wizard opens with the action type and targeted entities already filled out. Complete the wizard to apply the suggested action.

        [![Screenshot of the Copilot pane in advanced hunting with action suggestion highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-take-action.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-take-action.png#lightbox)

        Note

        You can only select the action suggestions for the last response in the conversation. If you send another question, the previous action suggestions are disabled.

## Continue your investigation

After receiving a response, you can continue your hunting session in several ways:

- **Ask follow-up questions:** The assistant maintains context from your session history.
- **Request query modifications:** Ask the assistant to modify the generated query.
- **Select suggested actions:** Choose from the follow-up questions or actions suggested by the assistant.
- **Use advanced hunting features:** Save your query, export results, create a detection rule, or use any of the other advanced hunting features for the KQL query displayed in the editor and the generated results.

## Start a new session

Warning

Starting a new session deletes all chat history, which isn't saved.

To start a new hunting session, select the **New chat (+)** icon at the top of the Copilot side pane.

## Provide feedback

You can provide feedback directly in the portal by selecting the feedback icon and choosing your response. Your feedback helps improve the Threat Hunting Assistant's capabilities and accuracy.

[![Screenshot of the advanced hunting page with Copilot feedback buttons highlighted.](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-feedback.png)](media/advanced-hunting-security-copilot/advanced-hunting-security-copilot-agent-feedback.png#lightbox)

Tip

Providing detailed feedback about what worked well or what could be improved helps us continuously enhance the Threat Hunting Assistant experience.