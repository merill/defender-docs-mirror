---
layout: Conceptual
title: Summarize incidents with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-copilot-m365d-incident-summary
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Generate incident summaries with Microsoft Copilot embedded in Microsoft Defender.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ms.update-cycle: 180-days
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 47b1b67c-1739-8ba1-4bea-34652d23e368
document_version_independent_id: 47b1b67c-1739-8ba1-4bea-34652d23e368
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-copilot-m365d-incident-summary.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-m365d-incident-summary
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-copilot-m365d-incident-summary.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 0f85d502-867d-0ab4-5283-5d6c457aab2c
---

# Summarize incidents with Microsoft Copilot in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender applies the capabilities of [Security Copilot](/en-us/security-copilot/microsoft-security-copilot) to summarize incidents. Incident summaries provide impactful information and insights to simplify investigation tasks. Investigations are often time-consuming and involve numerous steps.

This guide outlines how to access the summarizing capability of Copilot in Defender and what information is included in the summary, including information on providing feedback.

## Prerequisites

If you're new to Security Copilot, familiarize yourself with it by reading the following articles:

- [What is Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Security Copilot](/en-us/security-copilot/prompting-security-copilot)

Incident responders can access the right context to investigate and remediate incidents through Defender's correlation capabilities and Security Copilot's AI-powered data processing and contextualization. With an incident summary, responders get important information quickly to help in their investigation.

## Security Copilot integration in Microsoft Defender

The incident summary capability is available in the Microsoft Defender portal for customers with provisioned access to Security Copilot.

The incident summary capability is also available in the Security Copilot standalone experience through the Microsoft Defender XDR plugin. For more information about the Microsoft Defender XDR plugin, see [preinstalled plugins in Security Copilot](/en-us/security-copilot/manage-plugins#preinstalled-plugins).

## Incident summary content

Incidents containing up to 100 alerts can be summarized into one incident summary. An incident summary, depending on the availability of the data, includes the following information:

- The time and date when an attack started.
- The entity or asset where the attack started.
- A summary of timelines of how the attack unfolded.
- The assets involved in the attack.
- Indicators of compromise (IoCs).
- Names of [threat actors](/en-us/defender-xdr/microsoft-threat-actor-naming) involved.
- Suggested Security Copilot prompts, which guide you to focus on the most relevant next steps, gain deeper insights, and simplify investigations.

### Summarize an incident

To view an incident summary in Microsoft Defender, perform the following steps:

1. Open an incident page. Copilot automatically creates an incident summary in the **Tasks** pane. You can stop the summary creation by selecting **Cancel** or restart creation by selecting **Regenerate**.
2. The incident summary card loads on the Copilot pane. Review the generated summary on the card. Review the summary and use the information to guide your investigation and response to the incident.

    [![Screenshot that shows the incident summary card on the Copilot pane as seen in the Microsoft Defender incident page.](media/copilot-in-defender/incident-summary/copilot-defender-incident-summary.png)](media/copilot-in-defender/incident-summary/copilot-defender-incident-summary.png#lightbox)

    Tip

    You can navigate to a file, IP, or URL page from the Copilot results pane by clicking on the evidence in the results.
3. Select **See prompts** to view suggested prompts. Suggested prompts surface relevant follow-up questions based on the most crucial information in the given incident.

    Select a suggested prompt to get more insights about the specific assets involved in the incident, such as device summaries, identity summaries, and related threat intelligence.

    [![Screenshot that shows the Copilot suggested prompts on the incident summary card.](media/security-copilot-m365d-incident-summary/copilot-defender-incident-summary-see-prompts.png)](media/security-copilot-m365d-incident-summary/copilot-defender-incident-summary-see-prompts-large.png#lightbox)
4. Select the **More actions** ellipsis (...) at the top of the incident summary card to copy or regenerate the summary, or view the summary in the Security Copilot portal. Selecting **Open in Security Copilot** opens a new tab to the Security Copilot standalone portal where you can input prompts and access other plugins.

    ![Screenshot that shows the actions available on the incident summary card.](media/security-copilot-m365d-incident-summary/incident-summary-options.png)

### Manage Copilot incident summaries settings (preview)

By default, Copilot generates a summary for each incident the user opens, but you can change this setting to display incident summaries only in specific instances. You can choose to have summaries generated:

- Always (for every incident opened)
- Based on the severity level of the incident
- On demand only

To change the settings for Copilot incident summaries in Microsoft Sentinel, follow these steps:

1. Go to **Setup & configuration** &gt; **Settings** &gt; **Copilot in Defender** in the Microsoft Sentinel navigation pane.

    ![Screenshot that shows the Copilot settings page in Microsoft Sentinel.](media/security-copilot-m365d-incident-summary/copilot-settings.png)
2. Under **Preferences**, select **Incident Summary generation**.
3. Select either **Auto-generate** or **Generate on demand**, depending on your preference.
4. If you select **Auto-generate**, choose between **Always** or **Incident severity**. If you select **Incident severity**, choose the *minimum* severity level for which you want Copilot to generate incident summaries automatically.

    ![Screenshot that shows the Copilot settings preferences page in Microsoft Sentinel.](media/security-copilot-m365d-incident-summary/copilot-settings-preferences.png)
5. Select **Save**.

- When you select **Incident severity**, an estimate of the number of incidents of each severity level reviewed per day is displayed, along with the estimated SCU consumption.

    ![Screenshot that shows the approximate number of incidents of each severity level.](media/security-copilot-m365d-incident-summary/incident-severity.png)
- Copilot saves generated incident summaries for a week. If the incident you select has a summary already in the cache, and the incident didn't change significantly, the summary is automatically redisplayed at no cost regardless of the setting.
- To generate a summary on demand for an incident that doesn't automatically generate, select the **Generate** button.

    ![Screenshot that shows the Generate summary button on the incident page.](media/security-copilot-m365d-incident-summary/generate-summary.png)

## Sample incident summary prompt

In the Security Copilot standalone portal, you can use the following prompt to generate incident summaries:

- *Provide a summary for Defender incident {incident ID}.*

Tip

When you generate an incident summary in the Security Copilot portal, include the word ***Defender*** in your prompts to ensure that the incident summary capability delivers the results.

## Provide feedback on incident summaries

Microsoft highly encourages you to provide feedback to Copilot, as it's crucial for continuous improvement of the incident summary capability. You can provide feedback on the summary by selecting the feedback icon ![Screenshot of the feedback button in Copilot in Defender cards](media/copilot-in-defender/copilot-defender-feedback.png) found on the bottom of the Copilot pane.