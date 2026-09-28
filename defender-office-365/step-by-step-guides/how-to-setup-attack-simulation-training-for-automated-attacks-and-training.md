---
layout: Conceptual
title: Set up automated attacks and training in Attack Simulation Training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-setup-attack-simulation-training-for-automated-attacks-and-training
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Automate Attack Simulation Training campaigns and send payloads to target users. Learn how to create automated simulation flows with specific techniques and payloads that run when defined conditions are met.
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
document_id: d6de3b45-2139-55a3-15b1-8272410ce124
document_version_independent_id: d6de3b45-2139-55a3-15b1-8272410ce124
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-setup-attack-simulation-training-for-automated-attacks-and-training.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-setup-attack-simulation-training-for-automated-attacks-and-training
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-setup-attack-simulation-training-for-automated-attacks-and-training.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: d5a2214c-26ef-5b86-356d-5590cc25f9d4
---

# Set up automated attacks and training in Attack Simulation Training - Microsoft Defender for Office 365 | Microsoft Learn

Attack simulation training lets you run safe attack simulations to test your organization's phishing risk. It also helps teach users how to spot and avoid phishing attacks. This guide shows you how to set up automated flows with specific techniques and payloads that launch when your chosen conditions are met. Before you start, review the prerequisites to confirm you have the required licensing and permissions.

## Prerequisites

Before you begin, make sure you have:

- Microsoft Defender for Office 365 Plan 2 (included as part of E5).
- Sufficient permissions (Security Administrator role).
- 5-10 minutes to perform the following procedures.

## Send a payload to target users

Use the following steps to create a simulation automation and send a payload to target users:

1. Navigate to [Attack simulation training](https://security.microsoft.com/attacksimulator).
2. Choose **Simulation automations** from the top navigation bar.
3. Press **Create automation**.
4. Name the Simulation automation with something relevant and memorable. *Next*.
5. Pick the techniques you'd like to use from the flyout. *Next*.
6. Manually select up to 20 payloads you'd like to use for this automation, or alternatively select Randomize. *Next*.
7. If you picked OAuth as a Payload, you need to enter the name, logo, and scope (permissions) you'd like the app to have when it's used in a simulation. *Next*.
8. Choose who to target with the payload, if choosing the entire organization highlight the radio button. *Next*.
9. If you don't want to target the entire organization, select **Add Users**. Then search for or filter users in the wizard, and select **Add Users**. *Next*.
10. Customize the training if appropriate, otherwise leave Assign training for me (recommended) selected. *Next*.
11. Customize the landing page displayed when a user is phished if appropriate, otherwise leave as the Microsoft Default. *Next*.
12. Choose if you'd like end user notifications, if so select the delivery preferences and customize where appropriate. *Next*.
13. For Simulation schedule, you can either select **Randomized** or **Fixed**, the recommended option is Randomized, once selected, select *Next*.
14. Depending on your choice of Randomized or Fixed, the schedule details can differ, but select preferences for the selected schedule type, including the start and end dates of the automation. *Next*.
15. For **Launch Details**, select any final options you want, such as using unique payloads, or targeting repeat offenders and then select *Next*.
16. **Submit** and the Simulation automation is set up.