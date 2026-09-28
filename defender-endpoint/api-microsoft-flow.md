---
layout: Conceptual
title: Use the Microsoft Defender for Endpoint Power Automate connector to create event-triggered flows - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api-microsoft-flow
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Create Power Automate flows with the Microsoft Defender for Endpoint connector to trigger automated security workflows when events or alerts occur in your tenant.
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7a920b29-0e75-8435-540a-e17c5113d138
document_version_independent_id: 7a920b29-0e75-8435-540a-e17c5113d138
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api-microsoft-flow.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-microsoft-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api-microsoft-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 698dc812-bfa9-9717-da4d-704b8acc955b
---

# Use the Microsoft Defender for Endpoint Power Automate connector to create event-triggered flows - Microsoft Defender for Endpoint | Microsoft Learn

Automating security procedures is a standard requirement for every modern Security Operations Center (SOC). For SOC teams to operate in the most efficient way, automation is a must. Use Microsoft Power Automate to help you create automated workflows and build an end-to-end procedure automation within a few minutes. Microsoft Power Automate supports different connectors that were built exactly for automating security workflows.

Use this guide to create event-triggered automations in Power Automate, such as workflows that run when a new alert is created in your tenant. Microsoft Defender API has an official Power Automate Connector with many capabilities.

[![The Actions page in the Microsoft Defender 365 portal](media/api-flow-0.png)](media/api-flow-0.png#lightbox)

Note

For more information about premium connectors licensing prerequisites, see [Licensing for premium connectors](/en-us/power-automate/triggers-introduction#licensing-for-premium-connectors).

## Example: Create an event-triggered flow

This example demonstrates how to create a flow that is triggered whenever a new alert occurs on your tenant. You'll define what event starts the flow and which follow-up action the flow takes when the trigger occurs.

1. Log in to [Microsoft Power Automate](https://make.powerautomate.com).
2. Go to **My flows** &gt; **New** &gt; **Automated-from blank**.

    a. [![The New flow pane under My flows menu item in the Microsoft Defender 365 portal](media/api-flow-1.png)](media/api-flow-1.png#lightbox)
3. Choose a name for your Flow, search for "Microsoft Defender ATP Triggers" as the trigger, and then select the new Alerts trigger.

    [![ The Choose your flow's trigger section in the Microsoft Defender 365 portal](media/api-flow-2.png)](media/api-flow-2.png#lightbox)

    Now you have a Flow that is triggered every time a new Alert occurs.

    [![A trigger description](media/api-flow-3.png)](media/api-flow-3.png#lightbox)

    Next, add actions to retrieve alert details and define the automated response. For example, you can isolate the device if the Severity of the Alert is High and send an email about the alert. The Alert trigger provides only the Alert ID and the Machine ID. You can use the Microsoft Defender ATP connector to expand these entities.

### Get the Alert entity using the connector

Perform the following steps to retrieve the full Alert entity by using the connector:

1. Choose **Microsoft Defender ATP** for the new step.
2. Choose **Alerts - Get single alert API**.
3. Set the **Alert ID** from the last step as **Input**.

    [![The Alerts pane](media/api-flow-4.png)](media/api-flow-4.png#lightbox)

### Isolate the device if the Alert's severity is High

Use the following steps to isolate the device when the alert severity is High:

1. Add **Condition** as a new step.
2. Check if the Alert severity **is equal to** High.

    If yes, add the **Microsoft Defender ATP - Isolate machine** action with the Machine ID and a comment.

    [![The Actions pane](media/api-flow-5.png)](media/api-flow-5.png#lightbox)
3. Add a new step for emailing about the Alert and the Isolation. There are multiple email connectors that are easy to use, such as Outlook or Gmail.
4. Save your flow.

    You can also create a **scheduled** flow that runs Advanced Hunting queries and much more!