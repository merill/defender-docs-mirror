---
layout: Conceptual
title: Build an agent in Azure AI Foundry | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/build-agent-azure-ai-foundry
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how to build and test a security investigation agent in Azure AI Foundry using Microsoft Sentinel data lake telemetry.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: 
ms.date: 2026-06-10T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: 226acc30-9a78-fd17-d90b-4b45ca6fd733
document_version_independent_id: 1aeac80a-79f9-e22b-4d6d-d38d2219013f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/build-agent-azure-ai-foundry.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/build-agent-azure-ai-foundry
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/build-agent-azure-ai-foundry.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 7218e238-03e9-ea72-657d-f9da4bbc9184
---

# Build an agent in Azure AI Foundry | Microsoft Learn

Build a security investigation agent that reasons over identity risk, authentication signals, access telemetry, and endpoint activity using telemetry streamed into the Microsoft Sentinel data lake.

This article is part of a series that walks you through [ingesting test data to the data lake](ingest-sample-data), [developing an agent](build-agent-security-copilot), and [publishing](publish-agent-to-security-store) the example *IdentityDrift* platform solution. The solution includes a Security Copilot agent that correlates identity, endpoint, and cloud security signals to automate threat investigations.

In this how-to guide, you:

- Author agent instructions that follow grounding rules
- Create and test an agent using Azure AI Foundry

Note

This how-to article uses Azure AI Foundry as a developer playground to build, test, and refine agent instructions. You can experiment with agent instructions, validate that the agent performs analysis correctly, and iterate on the instructions based on test outcomes.

Once you're satisfied with the agent's behavior and investigation outcomes, use these validated instructions to [build the agent in Security Copilot](build-agent-security-copilot), test it in that environment, and then [publish to the Security Store](publish-agent-to-security-store). Use Azure AI Foundry as a sandbox for rapid prototyping and instruction refinement before building and publishing in Microsoft Copilot for Security.

## Agent scenario

The agent correlates the following inputs to identify potential security threats:

- Risky sign-in events
- User identity and role context
- Access to vulnerable or high-value workloads

**Example**:

A user signs in from a previously unseen geography, triggering a medium-risk identity alert. On its own, the alert is inconclusive. When correlated with IdentityDrift access telemetry, the user is found to have administrative access to a Kubernetes cluster running an unpatched ingress controller. Additional correlation shows recent privilege escalation activity within the cluster.

**Outcome**:

The sign-in is treated as an initial access event rather than a benign anomaly, prompting immediate containment of the identity and isolation of the affected workload.

## Prerequisites

Before you start, complete the previous steps in the series:

- [Sentinel data lake Onboarding](sentinel-data-lake-onboarding)
- [Ingest Data to Sentinel data lake](ingest-sample-data)

### Verify sample data is ingested into Sentinel data lake

All KQL jobs created in [Ingest Data to Sentinel data Lake](ingest-sample-data) must be running and populating the following tables:

- [CommonSecurity_ID_KQL_CL](ingest-sample-data#data-ingest-kql)
- [SigninLogs_KQL_CL](ingest-sample-data#data-ingest-kql)
- [AADRiskyUsers_KQL_CL](ingest-sample-data#data-ingest-kql)
- [DeviceProcessEvents_KQL_CL](ingest-sample-data#data-ingest-kql)
- [SecurityAlerts_KQL_CL](ingest-sample-data#data-ingest-kql)

At this stage, the same user identity appears in all of the above tables, allowing your agent to correlate signals from identity, access, and endpoint data.

## Create the agent in Azure AI Foundry

Create an agent in Azure AI Foundry using the agent instructions provided below. The agent will use the Microsoft Sentinel Data Exploration tool to query the ingested data lake tables, reason over the correlated signals, and surface insights about risky sign-ins, identity risk posture, and suspicious access patterns.

1. Open a web browser and navigate to the [Azure AI Foundry](https://ai.azure.com/)
2. Sign in with credentials that have access to Azure AI Foundry
3. Select your existing Microsoft Foundry project or Create a project

### Create AI Agent

To create the IdentityDrift investigation agent, follow these steps:

1. Select **Start Building**, then select **Create Agent**

[![Screenshot of the Azure AI Foundry Start Building page with the Create Agent option highlighted.](media/build-agent-azure-ai-foundry/start-building-create-agent.png)](media/build-agent-azure-ai-foundry/start-building-create-agent.png#lightbox)

1. Name the agent *IdentityDrift-Investigation-Agent*
2. Select **Create**

[![Screenshot of the Create Agent dialog with the agent name field populated as IdentityDrift-Investigation-Agent.](media/build-agent-azure-ai-foundry/create-agent-name-dialog.png)](media/build-agent-azure-ai-foundry/create-agent-name-dialog.png#lightbox)

1. Add the following instructions in the **Instructions** field

    ```
    1. UserPrincipalName Input
    
    Ensure to use the UserPrincipalName input throughout the analysis.
    
    2. Global Query Rule (MANDATORY)
    
    Every query MUST filter to the last 24 hours:
    
    | where TimeGenerated > ago(24h)
    
    Never use 7 days, 30 days, or "all time." Always 24h. To avoid oversized responses, summarize and limit outputs (do not return raw     event dumps).
    
    3. Query Data Lake for CommonSecurity_ID_KQL_CL
    
    IMPORTANT:
    
    - Do NOT assume the existence of any specific columns such as Action, EventType, or Application
    - Use only columns that exist in the query result
    - Prefer the following safe fields when available:
      - TimeGenerated
      - SourceUserName
      - SourceIP
      - DestinationHostName
      - AdditionalExtensions
      - DeviceCustomString1
    
    Search commonsecurity_ID_KQL_CL table records for events that match the provided user input (use SourceUserName as the identifier).
    
    Sample KQL Query (replace {{UserPrincipalName}}):
    
    CommonSecurity_ID_KQL_CL
    | where TimeGenerated > ago(24h)
        and SourceUserName has '{{UserPrincipalName}}'
    | summarize
        TotalEvents=count(),
        MFA_Approved=countif(DeviceCustomString1 has "Approved"),
        PrivilegedActions=countif(DeviceCustomString1 has "Privilege"),
        SensitiveAccess=countif(DeviceCustomString1 has "Sensitive"),
        Activities=makeset(AdditionalExtensions),
        TargetResources=makeset(DestinationHostName),
        IPs=makeset(SourceIP)
        by SourceUserName
    
    4. Query Data Lake SigninLogs_KQL_CL Table
    
    - Same user input
    - Filter last 24 hours
    - Extract:
      - Sign-in success vs failure
      - IP diversity
      - Result descriptions
    
    5. Query Data Lake AADRiskyUsers_KQL_CL Table
    
    - Same user input
    - Filter last 24 hours
    - Extract:
      - RiskLevel
      - RiskState
      - RiskLastUpdatedDateTime
    
    6. Query Data Lake DeviceProcessEvents_KQL_CL Table
    
    - Same user input
    - Filter last 24 hours
    - Identify suspicious post-authentication activity
    
    Guidance:
    
    - Remove domain from UPN to derive AccountName
    - Look for LOLBins in FileName column 
      - powershell.exe
      - cmd.exe
      - kubectl.exe
      - az.exe
    
    7. Query Microsoft Defender for Cloud SecurityAlert Table
    
    Query SecurityAlert to identify confirmed runtime threats related to Kubernetes or cloud workloads that may correlate with identity activity.
    
    - Alerts generated by Microsoft Defender for Cloud Kubernetes‑related alert types such as:
      - K8S.NODE_MalwareBlocked
      - K8S.NODE_DriftBlocked
    
    Guidance:
    
    - Filter to last 24 hours
    - Do NOT expect user identity fields in SecurityAlert
    - Extract:
      - AlertType
      - AlertSeverity
      - CompromisedEntity (ClusterName)
      - Context from ExtendedProperties
    
    8. Correlation & Reasoning
    
    Use the Sentinel Data Exploration MCP tool to correlate activity between CommonSecurity_ID_KQL_CL , SigninLogs_KQL_CL, AADRiskyUsers_KQL_CL, DeviceProcessEvents_KQL_CL and SecurityAlert_KQL_CL
    
    Match overlapping:
    
    - User identifiers
    - IP addresses
    - Device names
    - Authentication privilege escalation
    - Suspicious endpoint execution post authentication compromise
    
    9. Surface Key Insights
    
    Identify:
    
    - Risky sign-ins followed by privileged access
    - Unexpected MFA approvals
    - Access to vulnerable or high-value workloads
    - Privilege escalation preceding endpoint activity and Kubernetes control‑plane actions
    - Suspicious endpoint or Kubernetes tooling execution
    - Defender for Cloud alerts occurring after identity or control‑plane activity
    
    10. Provide Summary Findings
    
    Summarize:
    
    - MFA outcomes
    - Sign-in success vs failure trends
    - Identity risk posture
    - Privileged access highlights
    - Endpoint execution signals
    - Defender for Cloud security alerts and their timing
    
    Highlight discrepancies or noteworthy observations across identity, access, and endpoint telemetry.
    
    ### Sample Automation Flow (Short Version)
    
    1. Query **CommonSecurity_ID_KQL_CL** for identity access context
    2. Query **SigninLogs_KQL_CL** and **AADRiskyUsers_KQL_CL** for authentication and risk posture
    3. Query **DeviceProcessEvents_KQL_CL** for endpoint behavior
    4. Query **SecurityAlert_KQL_CL** for Defender for Cloud runtime threats
    5. Correlate all signals using Sentinel MCP and surface actionable security insights   
    ```
2. Select **Add Tools** to select Sentinel Data Exploration MCP Server
3. Select **Browse all tools**.

[![Screenshot of the agent configuration page with the Browse all tools option highlighted.](media/build-agent-azure-ai-foundry/instructions-and-tools.png)](media/build-agent-azure-ai-foundry/instructions-and-tools.png#lightbox)

1. In the **Catalog** tab, search for *Sentinel* and select **Microsoft Sentinel Data Exploration**
2. Select **Create** to add the tool to your agent

[![Screenshot of the tool catalog with Sentinel entered in the search box and Microsoft Sentinel Data Exploration shown in the results.](media/build-agent-azure-ai-foundry/tool-catalog-sentinel-data-exploration.png)](media/build-agent-azure-ai-foundry/tool-catalog-sentinel-data-exploration.png#lightbox)

1. Provide a unique name for the tool.
2. Select **Connect** to connect it to Agent.

[![Screenshot of the tool configuration dialog showing the name field and the option to connect the tool to the agent.](media/build-agent-azure-ai-foundry/sentinel-tool-connect-to-agent.png)](media/build-agent-azure-ai-foundry/sentinel-tool-connect-to-agent.png#lightbox)

## Test the agent

To test the agent, run a sample query in the Azure AI Foundry playground:

Warning

Do we have to use u1291@contoso.onmicrosoft.com ? the".onmicrosoft: will not pass the filters as it is a real user. Can we use u1291@contoso.com ? Of course we'll have to update the sample data in the jobs to match.

1. Start testing the agent using a sample query: `do analysis on UPN: u1291@contoso.onmicrosoft.com`

[![Screenshot of the agent test panel with a sample UPN query entered in the chat input.](media/build-agent-azure-ai-foundry/agent-test-panel-upn-query.png)](media/build-agent-azure-ai-foundry/agent-test-panel-upn-query.png#lightbox)

1. The following screenshots show results from a sample agent run for `u1291@contoso.onmicrosoft.com`:

Warning

Is there something that we should highlight in these screenshots like we did in the Security Copilot article?

[![Screenshot of the agent analysis results showing identity access context and sign-in data.](media/build-agent-azure-ai-foundry/agent-results-identity-access.png)](media/build-agent-azure-ai-foundry/agent-results-identity-access.png#lightbox)

[![Screenshot of the agent analysis results showing identity risk posture and endpoint activity.](media/build-agent-azure-ai-foundry/agent-results-identity-risk-endpoint.png)](media/build-agent-azure-ai-foundry/agent-results-identity-risk-endpoint.png#lightbox)

[![Screenshot of the agent analysis results showing correlated security findings and insights.](media/build-agent-azure-ai-foundry/agent-results-correlated-findings.png)](media/build-agent-azure-ai-foundry/agent-results-correlated-findings.png#lightbox)

Your agent instructions are now been tested in Azure AI Foundry. The validated instructions are ready to use in Microsoft Copilot for Security.