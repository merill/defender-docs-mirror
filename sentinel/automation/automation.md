---
layout: Conceptual
title: Automation in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/automation
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: sshuster
description: Learn about Microsoft Sentinel security orchestration, automation, and response (SOAR) capabilities and components, including automation rules and playbooks.
ms.topic: concept-article
ms.author: monaberdugo
author: mberdugo
ms.date: 2025-07-16T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: b93c2416-fbf0-88c3-29f1-6abbf8c01c27
document_version_independent_id: bdec5701-71f1-8d25-d28e-3185d3d6b099
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/automation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/automation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/automation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: fb5e1b3e-58d3-cf52-6b6c-8df30a419863
---

# Automation in Microsoft Sentinel | Microsoft Learn

Security information and event management (SIEM) and security operations center (SOC) teams are typically inundated with security alerts and incidents on a regular basis, at volumes so large that available personnel are overwhelmed. This results all too often in situations where many alerts are ignored and many incidents aren't investigated, leaving the organization vulnerable to attacks that go unnoticed.

Microsoft Sentinel, in addition to being a SIEM system, is also a platform for security orchestration, automation, and response (SOAR). One of its primary purposes is to automate any recurring and predictable enrichment, response, and remediation tasks that are the responsibility of your security operations center and personnel (SOC/SecOps), freeing up time and resources for more in-depth investigation of, and hunting for, advanced threats.

This article describes Microsoft Sentinel's SOAR capabilities, and shows how using automation rules and playbooks in response to security threats increases your SOC's effectiveness and saves you time and resources.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Automation rules

Microsoft Sentinel uses automation rules to allow users to manage incident handling automation from a central location. Use automation rules to:

- Assign more advanced automation to incidents and alerts, using playbooks
- Automatically tag, assign, or close incidents without a playbook
- Automate responses for multiple [analytics rules](../detect-threats-built-in) at once
- Create lists of tasks for your analysts to perform when triaging, investigating, and remediating incidents
- Control the order of actions that are executed

We recommend that you apply automation rules when incidents are created or updated to further streamline the automation and simplify complex workflows for your incident orchestration processes.

For more information, see [Automate threat response in Microsoft Sentinel with automation rules](../automate-incident-handling-with-automation-rules).

## Playbooks

A playbook is a collection of response and remediation actions and logic that can be run from Microsoft Sentinel as a routine. A playbook can:

- Help automate and orchestrate your threat response
- Integrate with other systems, both internal and external
- Be configured to run automatically in response to specific alerts or incidents, or run manually on-demand, such as in response to new alerts

In Microsoft Sentinel, playbooks are based on workflows built in [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview), a cloud service that helps you schedule, automate, and orchestrate tasks and workflows across systems throughout the enterprise. This means that playbooks can take advantage of all the power and customizability of Logic Apps' integration and orchestration capabilities and easy-to-use design tools, and the scalability, reliability, and service level of a Tier 1 Azure service.

For more information, see [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks).

## Automation in the Microsoft Defender portal

Note the following details about how automation works for Microsoft Sentinel in the Defender portal. If you're an existing customer who's transitioning from the Azure portal to the Defender portal, you may note differences in the way automation functions in your workspace after onboarding to the Defender portal.

| Functionality | Description |
| --- | --- |
| **Automation rules with alert triggers** | In the Defender portal, automation rules with alert triggers act only on Microsoft Sentinel alerts. To automate responses to Defender XDR alerts as well, use the **[Enhanced Alert Trigger](generate-playbook#enhanced-alert-trigger)**. For more information, see [Alert create trigger](../automate-incident-handling-with-automation-rules#alert-create-trigger). |
| **Automation rules with incident triggers** | In both the Azure portal and the Defender portal, the **Incident provider** condition property is removed, as all incidents have *Microsoft XDR* as the incident provider (the value in the *ProviderName* field). At that point, any existing automation rules run on both Microsoft Sentinel and Microsoft Defender XDR incidents, including those where the **Incident provider** condition is set to only *Microsoft Sentinel* or *Microsoft 365 Defender*. However, automation rules that specify a specific analytics rule name run only on incidents that contain alerts that were created by the specified analytics rule. This means that you can define the **Analytic rule name** condition property to an analytics rule that exists only in Microsoft Sentinel to limit your rule to run on incidents only in Microsoft Sentinel. Also, after onboarding to the Defender portal, the **SecurityIncident** table no longer includes a **Description** field. Therefore: - If you're using this **Description** field as a condition for an automation rule with an incident creation trigger, that automation rule won't work after onboarding to the Defender portal. In such cases, make sure to update the configuration appropriately. For more information, see [Incident trigger conditions](../automate-incident-handling-with-automation-rules#conditions). - If you have an integration configured with an external ticketing system, like ServiceNow, the incident description will be missing. |
| **Latency in playbook triggers** | [It might take up to 5 minutes](../move-to-defender#5min) for Microsoft Defender incidents to appear in Microsoft Sentinel. If this delay is present, playbook triggering is delayed too. |
| **Automation batching window** | If multiple changes are made to the same incident within 5-10 minutes, a single update is sent to Microsoft Sentinel, with only the most recent change. Intermediate updates are lost, which can impact workflows that depend on processing sequential incident state changes. For more information, see [Incident update trigger](../automate-incident-handling-with-automation-rules#incident-update-trigger). |
| **Changes to existing incident names** | The Defender portal uses a unique engine to correlate incidents and alerts. When onboarding your workspace to the Defender portal, existing incident names might be changed if the correlation is applied. To ensure that your automation rules always run correctly, we therefore recommend that you avoid using incident titles as condition criteria in your automation rules, and suggest instead to use the name of any analytics rule that created alerts included in the incident, and tags if more specificity is required. |
| ***Updated by* field** | After onboarding your workspace, the **Updated by** field has a [new set of supported values](../automate-incident-handling-with-automation-rules#incident-update-trigger), which no longer include *Microsoft 365 Defender*. In existing automation rules, *Microsoft 365 Defender* is replaced by a value of *Other* after onboarding your workspace. |
| **Creating automation rules directly from an incident** | [Creating automation rules directly from an incident](../false-positives#add-exceptions-with-automation-rules-azure-portal-only) is supported only in the Azure portal. If you're working in the Defender portal, create your automation rules from scratch from the **Automation** page. |
| **Microsoft incident creation rules** | Microsoft incident creation rules aren't supported in the Defender portal. For more information, see [Microsoft Defender XDR incidents and Microsoft incident creation rules](../microsoft-365-defender-sentinel-integration#microsoft-defender-xdr-incidents-and-microsoft-incident-creation-rules). |
| **Running automation rules from the Defender portal** | It might take up to 10 minutes from the time that an alert is triggered and an incident is created or updated in the Defender portal to when an automation rule is run. This time lag is because the incident is created in the Defender portal and then forwarded to Microsoft Sentinel for the automation rule. |
| **Active playbooks tab** | After onboarding to the Defender portal, by default the **Active playbooks** tab shows a predefined filter with onboarded workspace's subscription. In the Azure portal, add data for other subscriptions using the subscription filter. For more information, see [Create and customize Microsoft Sentinel playbooks from templates](use-playbook-templates). |
| **Running playbooks manually on demand** | The following procedures aren't currently supported in the Defender portal: - [Run a playbook manually on an alert](run-playbooks#run-a-playbook-manually-on-an-alert)- [Run a playbook manually on an entity](run-playbooks#run-a-playbook-manually-on-an-entity) |
| **Running playbooks on incidents requires Microsoft Sentinel sync** | If you try to run a playbook on an incident from the Defender portal and see the message *"Can't access data related to this action. Refresh the screen in a few minutes."*, this means that the incident isn't yet synchronized to Microsoft Sentinel. Refresh the incident page after the incident is synchronized to run the playbook successfully. |
| **Incidents: Adding alerts to incidents / Removing alerts from incidents** | Since adding or removing alerts from incidents isn't supported after onboarding your workspace to the Defender portal, these actions are also not supported from within playbooks. For more information, see [Understand how alerts are correlated and incidents are merged in the Defender portal](../move-to-defender#understand-how-alerts-are-correlated-and-incidents-are-merged-in-the-defender-portal). |
| **Microsoft Defender XDR integration in multiple workspaces** | If you've integrated XDR data with more than one workspace in a single tenant, the data will now only be ingested into the primary workspace in the Defender portal. Transfer automation rules to the relevant workspace to keep them running. |
| **Automation and the Correlation engine** | The correlation engine may combine alerts from multiple signals into a single incident, which could result in automation receiving data you didn’t anticipate. We recommend reviewing your automation rules to ensure you're seeing the expected results. |