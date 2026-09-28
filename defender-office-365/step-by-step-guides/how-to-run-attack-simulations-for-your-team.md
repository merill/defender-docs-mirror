---
layout: Conceptual
title: How to run attack simulations for your team - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-run-attack-simulations-for-your-team
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Send an Attack Simulation Training payload to users in your team or organization. Use simulated attacks to identify vulnerable users, policies, and practices before a real attack occurs.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 0be3243d-6d88-6335-41b1-a61525d1a46c
document_version_independent_id: 0be3243d-6d88-6335-41b1-a61525d1a46c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-run-attack-simulations-for-your-team.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-run-attack-simulations-for-your-team
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-run-attack-simulations-for-your-team.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 0cbe2a75-4fac-47ed-8f6b-904091f2d007
---

# How to run attack simulations for your team - Microsoft Defender for Office 365 | Microsoft Learn

## Overview

Attack simulation training lets you run safe, realistic cyber attack scenarios in your organization. These simulations help you find vulnerable users, policies, and practices before a real attack hits. You can use built-in or custom training to reduce risk and help end users learn about threats. This article walks you through creating and launching a simulated phishing attack, choosing target users, and configuring training assignments. Before you start, you need Microsoft Defender for Office 365 Plan 2 and the Security Administrator role.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

- Microsoft Defender for Office 365 Plan 2 (included as part of E5)
- Sufficient permissions (Security Administrator role)
- 5-10 minutes to perform the following procedures.

## Send a payload to target users

Perform the following steps to send a simulation payload to your target users:

1. Navigate to [Attack Simulation Training](https://security.microsoft.com/attacksimulator) in your subscription.
2. Choose **Simulations** from the top navigation bar.
3. Select **Launch a simulation**.
4. Pick the technique you'd like to use from the flyout, and select **Next**.
5. Name the Simulation with something relevant / memorable and select **Next**.
6. Pick a relevant payload from the wizard, review the details and customize if appropriate, when you're happy with the choice, select **Next**.
7. Choose who to target with the payload. If you're choosing the entire organization, select that option and then select **Next**.
8. Otherwise, select **Add Users** and then search or filter the users with the wizard. Select Add Users and then **Next**.
9. Under **Select training content preference**, leave the default *Microsoft training experience (Recommended)* or select *Redirect to a custom URL* if you want to use the custom URL. If you don't want to assign any training, then select *No training*.
    - You can either let Microsoft assign training courses by selecting *Assign training for me* or you can choose specific modules with *Select training courses and modules myself*
    - Select a Due Date (30, 15, or 7 days) from the drop-down menu.
    - Select **Next** to continue.
10. Customize the landing page displayed when a user is phished if appropriate, or otherwise leave the Microsoft Default.
    1. Under **Payload indicators**, check the box to add payload indicators to email. Adding payloads helps users to learn how to identify the phishing email. Select *Open preview panel* to view the message.
    2. Select **Next** to continue.
11. Choose if you'd like end user notifications, and if so, select the delivery preferences and customize where needed.
    1. Notice that you can also select *default language* for the notification under the **Select default language** drop-down menu.
12. Select when to launch the simulation, and how long it should be valid for. You can also enable *region aware time zone delivery*. This option delivers simulated attack messages to your employees during *their working hours* based on their region. Select **Next**.
13. Send a test if you're ready. Review the summary of choices. Select **Submit**.

### Further reading

To learn how attack simulation training works, see [Simulate a phishing attack with Attack simulation training](../attack-simulation-training-simulations).