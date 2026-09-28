---
layout: Conceptual
title: Security Copilot Threat Intelligence Briefing Agent in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/threat-intel-briefing-agent-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn what the Security Copilot Threat Intelligence Briefing Agent does in Microsoft Defender, how to set it up, view briefings, and provide feedback.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- security-copilot
- msec-ai-copilot
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 29f66553-ac77-9640-cb5b-c18e6c365f1a
document_version_independent_id: 29f66553-ac77-9640-cb5b-c18e6c365f1a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/threat-intel-briefing-agent-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-intel-briefing-agent-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/threat-intel-briefing-agent-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: a7b086a1-3dee-da1c-fc36-a9068063bc56
---

# Security Copilot Threat Intelligence Briefing Agent in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Note

This article discusses the Threat Intelligence Briefing Agent embedded experience in Microsoft Defender portal. To learn more about the standalone experience in Security Copilot, read [Threat Intelligence Briefing Agent (standalone experience)](/en-us/copilot/security/threat-intel-briefing-agent).

Threat intelligence analysts face many challenges when they create useful, actionable briefings. Building a briefing requires collecting data from multiple threat feeds, tools, and portals. Analysts must then filter, correlate, and analyze this data to map risks to their organization. All of this work happens before they can even start writing the report. Because these steps can take hours or even days, threats often change before the briefing is ready, which can make the briefing outdated.

The Microsoft Security Copilot Threat Intelligence Briefing Agent in Microsoft Defender addresses these pain points. It generates threat intelligence briefings based on the latest threat actor activity and both internal and external vulnerability information in a matter of minutes. It can help security teams save time by creating a customized, relevant report that provides CISOs, security managers, and analysts with key situational awareness and a solid foundation for defense work.

The agent uses automation and generative AI along with broad threat intelligence data. As it builds the briefing, it picks each next step based on the result of the previous one. This lets it decide in real time which threats to include and rank. The agent then turns the collected threat intelligence and vulnerability findings into a clear report that different audiences can read and act on.

The Threat Intelligence Briefing Agent is best suited for customers who turn on Microsoft Defender for Endpoint and Microsoft Defender External Attack Surface, as the agent relies on signals and insights from these first-party integrations to deliver accurate and context-rich reports. Before you get started, review the prerequisites to ensure you have the required products, plugins, and permissions in place.

Watch this video to see the Threat Intelligence Briefing Agent in action, from setup to generating your first briefing.

## Where to find the Threat Intelligence Briefing Agent

You can find the Threat Intelligence Briefing Agent as a banner at the top of the [Threat analytics](threat-analytics) page in the Defender portal.

[![Screenshot of the Threat Intelligence Briefing Agent banner on top of the Threat analytics page.](media/ti-briefing-agent/agent.png)](media/ti-briefing-agent/agent.png#lightbox)

To open Threat analytics, go to **Threat intelligence** &gt; **Threat analytics** in the navigation menu.

## Prerequisites

Before you set up the Threat Intelligence Briefing Agent, make sure you have the following products, plugins, and permissions in place.

### Required products

You need [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot) to run this agent.

### Security Copilot plugins

To run this agent, you need the following plugins:

- Microsoft Threat Intelligence
- Microsoft Threat Intelligence agents

The following plugin is optional but can add more context to the output:

- Microsoft Defender External Attack Surface Management

### User account permissions

Important

**Identity and permissions requirement:** This agent must connect to a user account or a new agent identity (service principal) (recommended). The agent can read data from Defender External Attack Surface Management and Defender Vulnerability Management. Set up the right permissions on the account or identity before you configure the agent.

The user account connected to the agent or the created agent identity must have these permissions:

**Required permissions:**

- **Microsoft Defender for Endpoint:** Access to Defender Vulnerability Management data
- **Security Reader:** Access to Threat Analytics and agent results
- **Security Admin:** Access to agent onboarding and configuration

**Optional permissions:**

- **Exposure Management (read):** Access to Microsoft Security Exposure Management insights, including External Attack Surface Management data

**Role-based access:**

- Owners and contributors can see the report generated by the Threat Intelligence Briefing Agent within the Microsoft Security Copilot agent library page

Important

After setting up permissions, activate the Microsoft Defender [unified role-based access control (RBAC)](manage-rbac) model for the role to take effect.

Tip

Consider using a dedicated service account for running agents to maintain separation of duties and enhance security monitoring.

### Agent trigger

This agent runs at the set time interval that you configured during setup, or manually when you want to run it.

## Set up an agent identity for the agent

A service principal is an application identity in Microsoft Entra ID that lets an app access resources on its own behalf. The Threat Intelligence Briefing Agent can run under a dedicated [agent identity](https://aka.ms/WhatAreAgentIdentities) (service principal) with only the minimal read permissions required in Microsoft Defender. This section describes how you can create or reuse a least-privileged role, register the agent's service principal, and assign the least-privileged role.

Before setting up an agent identity for the Threat Intelligence Briefing Agent, make sure that you have the agent in your environment. You must also have the following prerequisites:

- Tenant-level admin rights to register a service principal and assign roles.
- Azure CLI installed and authenticated (az login). For more information, see [Get started with Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).
- Access to Defender unified RBAC or equivalent permissions management.

To set up an agent identity:

1. **Create or reuse a least-privileged role**

    Create a role or reuse an existing role that includes the following minimum permissions:

    - Security operations &gt; Security data &gt; **Security data basics (read)**
    - Security posture &gt; Posture management &gt; **Vulnerability management (read)**

    You can reuse other roles that provide at least these levels of read access. Apply least privilege and scope assignments narrowly.
2. **Register the agent's service principal (agent identity)**

    First, get a Microsoft Graph access token. The following Azure CLI command retrieves a Microsoft Graph bearer token that you reuse in the subsequent curl requests to register the service principal. Run the following command as a tenant admin:

    ```azurecli
    TOKEN=$(az account get-access-token \
       --tenant <your tenant ID> \
       --resource-type ms-graph \
       --query accessToken -o tsv)
    ```

    Next, register the service principal for the agent identity in your tenant by sending a POST request to Microsoft Graph. This request creates the service principal object that the agent uses to authenticate:

    ```azurecli
    curl -X POST https://graph.microsoft.com/v1.0/servicePrincipals \
       -H "Authorization: Bearer $TOKEN" \
       -H "Content-Type: application/json" \
       -d '{
          "appId": "43d7b169-1d9e-4d32-8cd8-06c5974ed90c"
       }'
    ```

    **Optional:** To verify that the service principal was created successfully, run the following GET request. This request queries Microsoft Graph for the service principal by app ID and returns its details so you can validate the setup before proceeding:

    ```azurecli
    curl -X GET "https://graph.microsoft.com/v1.0/servicePrincipals?$filter=appId eq '43d7b169-1d9e-4d32-8cd8-06c5974ed90c'" \
      -H "Authorization: Bearer $TOKEN"
    ```
3. **Assign the least-privileged role to the service principal**

    1. In the Defender portal, go to **Settings** &gt; **Roles and permissions (Unified RBAC)** &gt; **Assignments** &gt; **Add assignment**
    2. Specify the following parameters:
        - **Principal:** Select the service principal created in step 2.
        - **Role:** Choose the custom role with the two read permissions mentioned in step 1.
        - **Scope:** Select the minimal scope required (specific assets or subscriptions).
    3. Save the assignment.
4. **Configure Defender for Endpoint role permissions**

    In addition to the Unified RBAC role assignment, the agent identity must have the required Defender for Endpoint permissions to access vulnerability and device data:

    1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
    2. Navigate to **Settings** &gt; **Endpoints** &gt; **Permissions** &gt; **Roles**.
    3. Locate the custom role assigned to the Threat Intelligence Briefing Agent (for example, "Threat Intelligence Briefing Agent").
    4. Edit the role and confirm that the following permissions are enabled:
        - **Advanced Hunting** – Read
        - **Vulnerability Management** – Read
        - **Machine Configuration** – Read
        - **Device Inventory** – Read
    5. Save any changes if updates are made.
5. **Grant Device Group access to the agent identity**

    The agent identity must also have access to the Device Groups that contain your endpoints. Without this access, the agent can't query device vulnerability data, and the Exposure Report section of the briefing may show as "not available" or return zero results.

    1. In the Microsoft Defender portal, go to **Settings** &gt; **Endpoints** &gt; **Device Groups**.
    2. For each Device Group that contains production endpoints:
        1. Open the Device Group.
        2. Select the **User Access** section.
        3. Add the Threat Intelligence Briefing Agent identity.
        4. Assign **Read** access.
    3. Save the changes.
6. **Wait for permissions to synchronize, then set up the agent**

    Important

    Allow time for permission updates to synchronize across Microsoft Defender services before running the agent.

    After permissions synchronize, set up the Threat Intelligence Briefing Agent and connect the created agent identity.

## Set up the agent

To run the Threat Intelligence Briefing Agent for the first time, follow these steps:

1. On the Threat Intelligence Briefing Agent banner at the top of the Threat analytics page, select **Set up agent**.

    [![Screenshot of the Threat Intelligence Briefing Agent banner on top of the Threat analytics page with the Setup agent button highlighted.](media/ti-briefing-agent/setup-agent.png)](media/ti-briefing-agent/setup-agent.png#lightbox)
2. On the pop-up window that appears, review the agent details, and then select **Next**.

    [![Screenshot of the Threat Intelligence Briefing Agent setup page showing the agent details.](media/ti-briefing-agent/review-details.png)](media/ti-briefing-agent/review-details.png#lightbox)
3. Connect a user account or agent identity, and then select **Continue**. A new window opens where you complete this step.

    [![Screenshots of the Threat Intelligence Briefing Agent setup page showing the steps to connect a user account.](media/ti-briefing-agent/connect-user.png)](media/ti-briefing-agent/connect-user.png#lightbox)
4. Wait for the agent to finish connecting to the identity or account, and then select **Continue**.

    [![Screenshot of the Threat Intelligence Briefing Agent setup page showing the user account details.](media/ti-briefing-agent/review-user.png)](media/ti-briefing-agent/review-user.png#lightbox)
5. Specify the following parameters to customize the agent output:

    - **Insights:** The number of vulnerabilities the agent researches for active threats.
    - **Look back days:** The number of days the agent goes back to research threats against your vulnerabilities.
    - **Region:** The geographical area that the agent checks for relevant threats.
    - **Industry:** The sector or industry vertical that the agent checks for relevant threats.
    - **Scheduled runs settings:** Choose whether to run the agent manually or send briefings at regular intervals. By default, the agent runs every seven days.
    - **Generated brief recipient:** The email address of the user or distribution group that the agent sends the briefing to.

    [![Screenshot of the Threat Intelligence Briefing Agent setup page showing the different parameters.](media/ti-briefing-agent/set-parameters.png)](media/ti-briefing-agent/set-parameters.png#lightbox)
6. Select **Deploy agent**. When the agent activates, you can go back to the Threat analytics page or select **Manage agent** to update your agent parameters.

    [![Screenshot of the Threat Intelligence Briefing Agent setup page showing successful agent deployment.](media/ti-briefing-agent/finish-setup.png)](media/ti-briefing-agent/finish-setup.png#lightbox)

## View briefing and manage the agent

Select **Run agent** to generate an ad-hoc or the most up-to-date briefing. Select **View full brief** to view the full report.

[![Screenshot of the Threat Intelligence Briefing Agent banner on top of the Threat analytics page with the View full brief and Run agent buttons highlighted.](media/ti-briefing-agent/run-agent.png)](media/ti-briefing-agent/run-agent.png#lightbox)

When you select **View full brief**, a side panel opens with a threat summary and detailed technical analysis. The panel covers actively exploited vulnerabilities and their possible impact on your organization. To download the report as a markdown file or copy its contents, select the matching icons at the top of the panel.

[![Screenshot of the Threat Intelligence Briefing Agent side panel in the Threat analytics page with the Download and Copy buttons highlighted.](media/ti-briefing-agent/full-brief.png)](media/ti-briefing-agent/full-brief.png#lightbox)

Select **Manage agent** to view and manage the agent's settings.

[![Screenshot of the Threat Intelligence Briefing Agent side panel in the Threat analytics page with the Manage agent button highlighted.](media/ti-briefing-agent/manage-agent.png)](media/ti-briefing-agent/manage-agent.png#lightbox)

You can also access the agent settings by:

- Select the three dots in the agent banner, then select **Manage agent**.
- Go to **Setup & configuration** &gt; **Settings** &gt; **Microsoft Defender XDR** &gt; **Threat Intelligence Briefing Agent** in the Defender portal.

    [![Screenshot of the Threat Intelligence Briefing Agent settings page in the Defender portal.](media/ti-briefing-agent/settings.png)](media/ti-briefing-agent/settings.png#lightbox)

## Assess and provide feedback on the agent’s output

The Threat Intelligence Briefing Agent saves the reports it generates in the Security Copilot standalone portal, under **Activity**. You can access this Activity page from the Defender portal by selecting **View agent activity** from the Threat Intelligence Briefing Agent settings page.

[![Screenshot of the Threat Intelligence Briefing Agent settings page in the Defender portal with View agent activity button highlighted.](media/ti-briefing-agent/view-agent-activity.png)](media/ti-briefing-agent/view-agent-activity.png#lightbox)

The Activity page displays the times the Threat Intelligence Briefing Agent ran to generate a report, the method of generation, and status. To assess the agent's output, select one of the reports.

[![Screenshot of the Threat Intelligence Briefing Agent activity page in the Security Copilot standalone portal.](media/ti-briefing-agent/agent-activity.png)](media/ti-briefing-agent/agent-activity.png#lightbox)

To view the agent’s progress toward producing a threat briefing, select **View activity**. This selection opens an activity map where you can see the details of the activity, providing you with transparency on the steps taken by the agent to produce the output. The Threat Intelligence Briefing Agent dynamically chooses the next step based on the outcome of the previous one as it builds the briefing.

[![Screenshot of a Threat Intelligence Briefing Agent report in the Security Copilot standalone portal with the View activity button highlighted.](media/ti-briefing-agent/view-activity.png)](media/ti-briefing-agent/view-activity.png#lightbox)

[![Screenshot of a Threat Intelligence Briefing Agent report activity map.](media/ti-briefing-agent/activity-map.png)](media/ti-briefing-agent/activity-map.png#lightbox)

To share feedback about the briefing, select the **thumbs up** or **thumbs down** icon. In the window that appears, type your feedback in the text box and select **Submit**. You can send feedback to the agent to help it learn what you prefer, or to Microsoft to help us improve the results.