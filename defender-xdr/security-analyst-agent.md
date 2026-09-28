---
layout: Conceptual
title: Microsoft Security Copilot Security Analyst Agent - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-analyst-agent
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft Security Copilot Security Analyst Agent can identify, assess, and prioritize risks in the Microsoft Defender portal.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ca50ad80-eb02-99c2-93ac-dae9e3d471e5
document_version_independent_id: ca50ad80-eb02-99c2-93ac-dae9e3d471e5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-analyst-agent.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-analyst-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-analyst-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 44d5d628-09f2-8a75-36b6-9f947d70aa20
---

# Microsoft Security Copilot Security Analyst Agent - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Security Analyst Agent in Defender helps security analysts quickly identify, assess, and prioritize risks by providing:

- **Flexible Analysis:** Perform ready-to-use or custom analyses on security data. Get actionable and prioritized insights, recommendations, and reports to uncover top vulnerabilities and risks.
- **Data Integration:** Analyse data from Microsoft Defender XDR, Sentinel Log Analytics or Sentinel Data Lake, based on your instructions. You can also upload CSV files for custom dataset analysis (Available currently in Standalone experience, but will be shortly available in Defender)
- **Interactive Exploration:** Visualize data to spot anomalies and risks faster.
- **Conversation Assistance:** Chat with the agent, ask follow-up questions, and perform related analyses to deepen your understanding

Use Security Analyst Agent, if you want to perform basic analysis tasks such pattern analysis, trend analysis, time series and visualization and more complex analysis tasks such as anomaly detection, clustering, ranking, risk scoring and prioritization, forecasting and predictive modelling to uncover hidden risks. The agent generates prioritized insights with full evidence for defensibility. This is python-powered advanced analysis in a chat first experience, without need for writing any code or queries.

The agent can perform single or multi-step analysis on large volumes of data and iteratively reasons and uncovers hidden risks, prioritizes these risks with detailed evidence trail and justification.

## Prerequisites and setup requirements

You must have access to Security Copilot and Defender XDR or Sentinel Log Analytics or Sentinel Data lake to use the Agent.

### Access and setup requirements

Review the following access and setup requirements before configuring the agent.

- **Access Requirements**

You must have read access to either Microsoft Defender XDR, Microsoft Sentinel Log Analytics Workspace, or Microsoft Sentinel Data Lake, depending on the data source you chose.

- **RBAC and User-specific Setup**

When you configure the agent, it is tied to your identity and applies only to your user instance.

- **Multi-user support**

Other users in the same tenant can also configure the agent using their own identity, provided they have the required access to the selected data sources.

## Data sources used by the Security Analyst Agent

The agent currently supports three data sources:

| Data source | Description |
| --- | --- |
| **Defender XDR** (default) | Microsoft Defender XDR telemetry |
| **Sentinel Log Analytics** | Microsoft Sentinel Log Analytics Workspace |
| **Sentinel Data Lake** (mandatory step for Sentinel Data Lake only) | Microsoft Sentinel Data Lake |

There are two methods for specifying the data source:

**Natural language prompts**: Add the data source to your instruction. Use the following sample prompt to ask the agent to investigate whether privilege escalation or role elevation events are followed by sensitive data access using Sentinel Log Analytics data:

```text
Analyze if there are privilege escalation or role elevation activities that are followed by sensitive data access in my enterprise. Please use Sentinel Log Analytics for this.
```

When you specify a data source in your instruction, the agent retrieves and analyzes security logs from that source. If there are multiple workspaces, the agent asks you to specify which one to use.

Once configured in a prompt, the data source setting persists for the entire session until changed. We recommend limiting data source changes in a given session to three for better performance.

**Agent Settings**: You can also specify the data source by editing the Agent Settings.

Important

The agent always honors your instructions. If there is a conflict between the Agent Settings and a prompt instruction, the prompt instruction takes precedence.

If no data source is specified using either method, the agent first tries to retrieve data from Defender XDR. If the Defender XDR retrieval attempt fails due to data unavailability or a permission issue, the agent retries from Sentinel Log Analytics.

## Configure the Security Analyst Agent (optional)

You can run the Security Analyst agent directly in Defender without completing setup. Agent setup is provided to support optional configuration scenarios, such as defining an agent identity or preconfiguring data sources. It does not affect your ability to run the agent in Defender.

Important

Configuring the data source is optional. You can specify the data source directly in your prompt, and the agent prioritizes these prompt-based instructions when performing the analysis. If no data source is specified in the prompt, the agent uses the data source configured in the agent settings.

1. Sign in to Security Copilot (https://securitycopilot.microsoft.com).
2. Select the home menu icon.
3. Navigate to **Agents**.
4. In the **Ready for setup** section, select **Security Analyst Agent**.
5. For first-time setup, locate the agent in the **Ready for setup** section, and select **Set up**. If the agent is already configured for at least one user, search for "Security Analyst Agent" under "Agents in Use" section and click "Go to agent".

    ![Image of Security Analyst Agent - Go to agent](media/security-analyst-agent/security-analysis-agent-go-to-agent.png)
6. Provide your preferred data sources details to configure the agent:

    - **Defender XDR**: Leave all fields blank and specify `Use Defender XDR` at the end of your instruction.
    - **Sentinel Data Lake** (mandatory):

        1. Enter `SentinelDataLake` in the **DataSource** field.
        2. Enter your workspace name in the **Sentinel Data Lake Workspace Name** field.
        3. Leave the remaining fields empty.
    - **Sentinel Log Analytics Workspace**:

        1. Enter `SentinelLogAnalyticsWorkspace` in the **DataSource** field.
        2. Fill in the following field: **Log Analytics Workspace Name**.
        3. Leave the **Sentinel Data Lake Workspace Name** field blank and save your settings.

        ![Image of Security Analyst Agent - Set up agent chat](media/security-analyst-agent/security-analysis-agent-chat-setup-agent.png)
7. Select **Chat with agent** at the top to interact with the agent.

    ![Image of Security Analyst Agent - chat with agent button](media/security-analyst-agent/security-analysis-agent-chat-with-agent.png)

    You can to start a new chat for a new analysis, view and access historical chats, and view agent setting details from any agent session.

    ![Image of Security Analyst Agent - new chat session](media/security-analyst-agent/security-analysis-agent-chat-new.png)

## Use the Security Analyst Agent

Perform the following steps to use the Security Analyst Agent in Microsoft Defender.

1. Go to the [Microsoft Defender portal](https://defender.microsoft.com), and then select **Advanced hunting** under **Investigation and response**.
2. Open Copilot, select the three-dot menu (**More actions**) in the side pane, and then select **Switch to Security Analyst Agent**.

    ![Screenshot of the More actions menu in the Security Copilot side pane, showing the Switch to Security Analyst Agent option.](media/security-analyst-agent/security-analyst-agent-select.png)
3. Enter your security analysis prompt in natural language, or select one of the suggested prompts.
4. If the task is broad, respond to the agent's clarifying questions so the agent can narrow the scope of analysis.
5. Optionally specify the data source in your prompt. If no data source is provided, the agent first tries Defender XDR and then Sentinel Log Analytics to identify and retrieve the needed data for analysis.
6. Review the response, including prioritized findings, supporting evidence, and recommendations.

    In the following example, the agent summarizes its findings along with evidence and also provides contextual recommendations on next steps, either deeper investigation or containment. The response also contains a list of suggested next prompts that the user may ask to continue to interaction.

    ![Screenshot of sample response from the Security Analyst agent.](media/security-analyst-agent/security-analyst-agent-sample-response.png)
7. Continue with follow-up prompts in the same session, or start a new session for a separate investigation.

    Note

    The agent can take a few minutes to complete complex analyses.
8. If you ran a KQL query and are looking to analyze the results to understand security risks, select the **Analyze with copilot** below the results tab of the query. The agent reasons on the generated results and presents a summary of prioritized insights needing urgent attention.

    ![Screenshot showing the Analyze with Copilot action in Advanced hunting query results.](media/security-analyst-agent/security-analyst-agent-sample-analyze.png)
9. Use the feedback buttons on the response to share whether the output was helpful.

## Switch back to the Threat Hunting Assistant

To return to the Threat Hunting Assistant, select the three-dot menu (**More actions**) in the Security Copilot side pane, and then select **Switch to Threat Hunting Assistant**.

![Screenshot of the More actions menu in the Security Analyst Agent side pane, showing the Switch to Threat Hunting Assistant option.](media/security-analyst-agent/security-analyst-agent-switch-back.png)

Note

Switching between the Security Analyst Agent and the Threat Hunting Assistant resets your conversation with Security Copilot.

## Interpret the Security Analyst Agent report

The report is organized into the following sections to help you review the analysis and supporting evidence.

### Review the executive summary

In the report, the Executive summary section provides a clear narrative of how the analysis was performed, outlining the steps taken and the data considered. It explains the filtering criteria, time ranges, and any ranking applied, all in straightforward language so readers can easily follow the process.

### Review key insights

Here you’ll find the most significant findings from the analysis, presented in a concise and meaningful way. Each insight includes a brief explanation of why it matters and, where relevant, references to supporting evidence.

### Interpret report visualizations

The Visualizations section contains charts or graphs that add depth and clarity to the report, helping readers quickly interpret patterns or relationships in the data. Visuals are included only when they provide unique value to the analysis.

### Review report artifacts

Artifacts are the supporting files that accompany the Security Analyst Agent report, such as a comprehensive CSV of all analyzed entities and, when applicable, detailed evidence files. These resources allow readers to explore the full dataset behind the findings. Artifacts include the KQL query that was used by the agent to retrieve the data (please note the agent only uses KQL for data retrieval, analysis is done in python), comprehensive plan that was formulated for performing the task.