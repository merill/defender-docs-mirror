---
layout: Conceptual
title: Microsoft Security Copilot and Chat in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-copilot-in-microsoft-365-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about Microsoft Security Copilot capabilities in Microsoft Defender. Use natural language to investigate threats, analyze scripts, and get AI-powered incident summaries.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: article
ms.update-cycle: 180-days
ms.date: 2026-07-17T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: 1c1c91ae-be61-aaaf-5441-d4c98589356c
document_version_independent_id: 1c1c91ae-be61-aaaf-5441-d4c98589356c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-copilot-in-microsoft-365-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-in-microsoft-365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-copilot-in-microsoft-365-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 77aaf830-70e0-c946-d78c-093b2ef55f35
---

# Microsoft Security Copilot and Chat in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

This article provides an overview of Microsoft Security Copilot in Microsoft Defender, including key capabilities, access steps, and links to detailed guidance.

Note

Microsoft Defender XDR provides a unified XDR experience for Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, and Microsoft Defender for Vulnerability Management. Learn more about this pre- and post-breach defense suite in [What is Microsoft Defender XDR?](microsoft-365-defender)

## Security Copilot prerequisites

If you're new to Security Copilot, you should familiarize yourself with it by reading the following articles:

- [What is Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Security Copilot](/en-us/security-copilot/prompting-security-copilot)
- [Application card for Microsoft Copilot in Microsoft Defender](application-card-copilot-defender)

## Microsoft Security Copilot integration in Microsoft Defender

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) brings together the power of AI and human expertise to help security teams respond to attacks faster and more effectively. Copilot in Defender is available to users who have provisioned access to Security Copilot. You can access Copilot in two ways:

- Security Copilot is embedded in the Microsoft Defender portal to help provide security teams with enhanced capabilities to investigate and respond to incidents, hunt for threats, and protect their organization with relevant threat intelligence.
- Defender Chat experience (preview) is an open prompt chat assistant built into Microsoft Defender. It helps SOC analysts investigate threats, explore incidents, and answer security questions in plain language, without needing to navigate multiple screens or write complex queries.

Copilot in Defender operates using [Microsoft's AI principles](https://www.microsoft.com/ai/responsible-ai). For more information, see the [Application card for Microsoft Copilot in Microsoft Defender](application-card-copilot-defender).

# [Defender Chat experience (preview)](#tab/defender-chat)
## Get started

To open the Defender chat experience from anywhere in the Defender portal, select the **Copilot** button in the top navigation bar. The chat panel slides open on the right side of the screen and stays in context while you continue working. A welcome screen appears with a greeting and an input field ready for your first question.

![Screenshot of the Defender Chat welcome screen and the Copilot icon selected in the top right corner.](media/security-copilot-in-microsoft-365-defender/open-chat.png)

To close the panel, select **Close** in the header or select the Copilot button again. Your conversation is preserved and you can reopen the panel and pick up where you left off.

## Page context awareness

Defender Chat responds based on the page you're currently viewing in the Defender portal and can answer questions based on that context.

If you ask a question such as "Which users are involved in *this* incident?", the chat understands which incident, alert, device, or entity you're referring to based on your current page without needing to provide IDs or names.

## Chat conversation capabilities

### Interactive conversations

The chat remembers the full context of your conversation, so you can ask follow-up questions naturally. For example, you can start with *Show me high-severity incidents from the past week*, then follow up with *Tell me more about the first one*, and the chat understands what you mean.

### Step-by-step plans

For complex or multi-step requests, the chat might first present a proposed plan outlining the steps it intends to take. You can Approve or Reject the plan before any actions are taken. This keeps you in control, especially for investigations that require multiple data lookups.

For example: If you ask *Investigate incident 12345 and summarize the key findings*, the chat might propose the following plan:

1. Retrieve incident details
2. Fetch associated alerts
3. Collect evidence and impacted entities
4. Summarize findings

After you approve the plan, the chat executes each step and shows its progress in real time.

### Clarifying questions

If your request is ambiguous, the chat might ask a clarifying question and offer quick-select options (up to four suggestions) to help you get to the right answer faster. Select an option or type your own response.

### Conversation history

Your conversations are saved automatically. Use the Conversations panel on the left side of the chat to:

- Resume a previous conversation
- Start a new session
- Delete a conversation
- Clear all conversations

Note

- Conversations aren't synced across devices or shared with other users. The last ten conversations are stored locally in your browser.

### Working with responses

Responses are formatted with structured tables, bullet points, and section headers for readability. You can:

- Copy a response: Select the *copy* icon on any message to copy it to your clipboard
- Export tables: Select *Export* on any table to export it to Excel for further analysis
- Stop generation: Select *Stop* to interrupt a response that's taking too long or heading in the wrong direction
- Retry: If something goes wrong, select *Retry* to attempt the response again

# [Copilot in Defender embedded skills](#tab/copilot-in-defender)
## Key features

- Embedded chat capability enabling conversation and steering
- Context-aware answers across incidents, alerts, identities, devices, IPs, and evidence
- Follow-up questions for clarification

### Investigate and respond to incidents like an expert

These AI tools enable security teams to tackle attack investigations in a timely manner with ease and precision. They can understand attacks immediately, quickly analyze suspicious files and scripts, and promptly assess and apply appropriate mitigation to stop and contain attacks.

#### Summarize incidents quickly

Investigating incidents with multiple alerts can be a daunting task. To immediately understand an incident, you can tap Copilot to [summarize an incident](security-copilot-m365d-incident-summary) for you. Copilot creates an overview of the attack. The overview contains essential information for you to understand what transpired in the attack, what assets are involved, and the timeline of the attack. Copilot automatically creates a summary when you navigate to an incident's page. It also helps you understand the assets involved and how to act by suggesting prompts about related identities, devices, IPs, and so on.

[![Screenshot of the incident summary card on the Copilot pane as seen in the Microsoft Defender incident page.](media/copilot-in-defender/incident-summary/copilot-defender-incident-summary.png)](media/copilot-in-defender/incident-summary/copilot-defender-incident-summary.png#lightbox)

#### Take action on incidents through guided responses

Resolving incidents requires analysts to understand an attack to know what solutions are appropriate. Copilot recommends solutions through [guided responses](security-copilot-m365d-guided-response) that are specific to each incident.

[![Screenshot highlighting the Copilot pane with the guided responses in the Microsoft Defender incident page.](media/copilot-in-defender/guided-response/copilot-defender-guided-response-small.png)](media/copilot-in-defender/guided-response/copilot-defender-guided-response.png#lightbox)

#### Run script analysis with ease

Most attackers rely on sophisticated malware when launching attacks to avoid detection and analysis. This malware is usually obfuscated and might be in the form of scripts or command lines in PowerShell. Copilot can quickly [analyze scripts](security-copilot-m365d-script-analysis), reducing the time for investigation.

[![Screenshot highlighting the script analysis button in the attack story view in the incident page.](media/copilot-in-defender/script-analyzer/copilot-defender-script-analysis-incident-small.png)](media/copilot-in-defender/script-analyzer/copilot-defender-script-analysis-incident.png#lightbox)

#### Generate device summaries

Investigating devices involved in incidents can be complicated. To quickly assess a device, Copilot can [summarize a device's information](copilot-in-defender-device-summary), including the device's security posture, any unusual behaviors, a list of vulnerable software, and relevant Microsoft Intune information.

[![Screenshot of the device summary results in Copilot in Defender.](media/copilot-in-defender/device-summary/copilot-defender-device-summary-device-page-small.png)](media/copilot-in-defender/device-summary/copilot-defender-device-summary-device-page.png#lightbox)

#### Analyze files promptly

Copilot helps security teams quickly assess and understand suspicious files with [file analysis](copilot-in-defender-file-analysis). Copilot provides a file's summary, including detection information, related file certificates, a list of API calls, and strings found in the file.

[![Screenshot of the file analysis results in Copilot in Defender with the Hide details option highlighted.](media/copilot-in-defender/file-analysis/copilot-defender-file-analysis-hide-small.png)](media/copilot-in-defender/file-analysis/copilot-defender-file-analysis-hide.png#lightbox)

#### Investigate identities immediately

Quickly assess a user's risk by generating an [identity summary](security-copilot-defender-identity-summary) with Copilot. Identify when an identity is at risk or suspicious with contextualized information about a user's role and role changes, sign in behaviors, devices signed in to, and relevant contact information.

[![Screenshot showing the Summarize option in the user details pane.](media/copilot-in-defender/identity-summary/identity-incident-graph-small.png)](media/copilot-in-defender/identity-summary/identity-incident-graph.png#lightbox)

#### Summarize emails in the Email entity page

For Defender for Office 365 email investigations, open the Security Copilot pane on the [Email entity page](/en-us/defender-office-365/mdo-email-entity-page) to generate an AI-authored summary of the selected message. The summary consolidates email metadata, timeline events, URLs, and attachments into an overview, event timeline, and indicators breakdown. The experience is user-triggered from the Copilot pane and available to users with Security Copilot access.

#### Write incident reports efficiently

Security operations teams usually write reports to record important information. These reports include response actions taken, their results, the team members involved, and other information to aid future security decisions. Documenting incidents can be time-consuming because an effective incident report must contain the incident summary, actions taken, and who took what actions and when. Copilot [generates an incident report](security-copilot-m365d-create-incident-report) by consolidating the incident summary, response actions, and team involvement.

[![Screenshot of the incident report card in the incident page showing the top half of the card.](media/copilot-in-defender/create-report/incident-report-main1-small.png)](media/copilot-in-defender/create-report/incident-report-main1.png#lightbox)

### Manage incidents in a unified experience

The Copilot tab consolidates incident-related actions into a single, unified chat experience, eliminating the need to switch between multiple panels or layers.

![Screenshot that shows the Copilot tab in the top right corner of the screen.](media/security-copilot-in-microsoft-365-defender/copilot-tab.png)

Select the **Copilot** tab on the incident page to view the incident summary, get recommendations, or generate a report.

![Screenshot that shows the available options in the Copilot tab, including incident summary, recommendations, and report generation.](media/security-copilot-in-microsoft-365-defender/copilot-tab-details.png)

Select **Summarize** to generate the incident summary or view it if it already exists. You can view summaries and interact with all your events and related prompts in the same panel.

You can run multiple summary requests in parallel for different entities (such as users and devices), and the results are cached unless regenerated.

[![Screenshot that shows the Copilot summary panel with multiple summary suggestions.](media/security-copilot-in-microsoft-365-defender/copilot-integrations.png)](media/security-copilot-in-microsoft-365-defender/copilot-integrations.png#lightbox)

![Screenshot that shows the Copilot panel generating a device summary in response to a summarize request in the device page.](media/security-copilot-in-microsoft-365-defender/summarize-device.png)

When you close a summary panel, the summary process stops.

Incident chats persist across incidents. When you switch to a different incident, the chat automatically closes, but when you reopen the Copilot panel you see the chat history. This lets you compare summaries of different incidents and navigate to relevant reports.

[![Screenshot that shows the Copilot chat history with summaries of different incidents.](media/security-copilot-in-microsoft-365-defender/multiple-summaries.png)](media/security-copilot-in-microsoft-365-defender/multiple-summaries.png#lightbox)

You can also select **Recommendations** to get AI-powered recommendations for next steps on how to investigate and remediate the incident, or select **Report** to generate a comprehensive report of the incident that includes the summary, timelines, involved entities, and more.

### Hunt like a pro

Copilot in Defender helps security teams proactively hunt for threats in their network by quickly building appropriate KQL queries.

Security teams who use advanced hunting can now use a query assistant that converts natural-language questions into ready-to-run KQL queries. The query assistant saves time by generating a KQL query that can be run immediately or tweaked to the analyst's needs. Read more about [Query assistant](advanced-hunting-security-copilot-query-assistant).

[![Screenshot of the Copilot pane in advanced hunting.](/en-us/defender/media/advanced-hunting-security-copilot-pane.png)](/en-us/defender/media/advanced-hunting-security-copilot-pane-big.png#lightbox)

### Protect your organization with relevant threat intelligence

Empower your security organization to make informed decisions with the latest threat intelligence. Copilot consolidates and summarizes threat intelligence to help security teams prioritize and respond to threats effectively.

#### Monitor threat intelligence

Ask Copilot to summarize the relevant threats impacting your environment, to prioritize resolving threats based on your exposure levels, or to find threat actors that might be targeting your industry. Read more about [Security Copilot in threat intelligence](defender-threat-intelligence#use-microsoft-copilot-in-defender-for-threat-intelligence).

[![Screenshot of the Copilot pane in threat intelligence in Defender.](media/security-copilot-in-microsoft-365-defender/copilot-defender-threat-intel-small.png)](media/security-copilot-in-microsoft-365-defender/copilot-defender-threat-intel-full.png#lightbox)

## Access Copilot in Defender

To ensure that you have access to Copilot in Defender, see the [Security Copilot purchase and licensing information](/en-us/security-copilot/faq-security-copilot). After you have access to Security Copilot, the key features become available in the Microsoft Defender portal.

## Sample prompts in Copilot

In the Microsoft Defender portal, you can find sample prompts to help you navigate and use some Copilot capabilities. The prompts are designed to help you understand these capabilities and how to use them effectively. Here are some examples of prompts you might see in the portal:

Advanced hunting prompts:

[![Screenshot highlighting the Copilot prompts in the advanced hunting page.](media/security-copilot-in-microsoft-365-defender/sample-prompt-adv-hunting-small.png)](media/security-copilot-in-microsoft-365-defender/sample-prompt-adv-hunting.png#lightbox)

Threat intelligence prompts:

[![Screenshot highlighting the Copilot prompts in the threat intelligence page.](media/security-copilot-in-microsoft-365-defender/sample-prompt-threat-intel-small.png)](media/security-copilot-in-microsoft-365-defender/sample-prompt-threat-intel.png#lightbox)

You can extend your investigation in the Security Copilot standalone portal using natural language prompts. The following are sample prompts that you can type in the prompt bar to help you summarize an incident with recommendations:

- Type **Summarize incident {incident number} and conclude with a set of recommendations** to generate the incident summary and recommendations.
- Type **What can you tell me about the reputation of the indicators in the script? Are they malicious? If so, why?** to analyze the script and generate details about the script.
- Type **Summarize this email and list its key indicators, including URLs, senders, and attachments** to generate a summary of the selected email entity.

Prompting in Copilot helps you navigate and use the capabilities effectively. You can also use the prompt bar to generate KQL queries, summarize incidents, and analyze files. See [tips for effective prompting](/en-us/copilot/security/prompting-tips). You can also use prebuilt promptbooks to get started with Copilot. To learn more, see [use prebuilt promptbooks in Copilot](/en-us/copilot/security/using-promptbooks).

---

## Provide feedback

All Copilot in Defender capabilities have an option for providing feedback. Reviewing and [providing feedback](/en-us/security-copilot/rai-faqs-security-copilot#what-are-the-limitations-of-security-copilot-how-can-users-minimize-the-impact-of-security-copilots-limitations-when-using-the-system) helps improve future responses. To provide feedback, use the 👍 / 👎 buttons on any response.

## Privacy and data security

Copilot continuously evolves using [data](/en-us/security-copilot/privacy-data-security#customer-data-and-system-generated-logs) that's [stored](/en-us/security-copilot/privacy-data-security#customer-data-storage-location), [processed](/en-us/security-copilot/privacy-data-security#location-for-prompt-evaluation), and [shared](/en-us/security-copilot/privacy-data-security#customer-data-sharing-preferences) depending on the settings defined by your administrator. Microsoft ensures that your data is always protected and secure when using Copilot. To learn more about data security and privacy in Copilot, see [Privacy and data security in Copilot](/en-us/security-copilot/privacy-data-security).

## Plugins in Security Copilot

Copilot uses [preinstalled Microsoft plugins](/en-us/security-copilot/manage-plugins#preinstalled-plugins) like Microsoft Defender, Defender Threat Intelligence, and Natural Language to KQL for Microsoft Sentinel and Defender plugins to generate relevant information, provide more context to incidents, and generate more accurate results. Ensure that [plugins are turned on in Copilot](/en-us/security-copilot/manage-plugins#managing-preinstalled-plugins) to allow access to relevant data and to generate requested content from other Microsoft services in your organization.