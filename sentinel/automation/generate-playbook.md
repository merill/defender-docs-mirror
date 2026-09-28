---
layout: Conceptual
title: Generate playbooks using AI in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/generate-playbook
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
description: Generate playbooks through natural language conversations directly in the Defender portal.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-08-07T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 7b896006-a147-7dbc-15c2-844725f66732
document_version_independent_id: ead8b77c-15ba-b9e0-eb21-10931079ad57
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/generate-playbook.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/generate-playbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/generate-playbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: beeeadde-c92c-6687-354f-56ab1a804554
---

# Generate playbooks using AI in Microsoft Sentinel | Microsoft Learn

The SOAR playbook generator creates python based automation workflows coauthored through a conversational experience with Cline, an AI coding agent. You describe automation logic in natural language, and the system generates validated, code-based playbooks with complete documentation and visual flow diagrams. The playbook generation experience is powered by an embedded VS Code environment within the Defender portal, so you can author and refine playbooks without leaving the portal. Generated playbooks use alert data as input and dynamically generate the required API calls, as long as you configure the integration for the target provider.

This article describes how to generate playbooks by using AI, configure required integrations, and deploy your automation workflows.

The AI-powered playbook generator is available to Microsoft Sentinel customers in the Microsoft Defender portal. It doesn't require a separate Microsoft Security Copilot license or Security Compute Units.

Playbook generation provides the following capabilities:

- **Co-author with AI**: Build playbooks through natural language conversations with Cline, an AI coding agent hosted in a VS Code environment embedded in the Defender portal.
- **Testing**: Once the playbook is generated, you can test it by providing a real alert as input.
- **Automatic documentation**: Generate comprehensive playbook documentation and visual flow diagrams automatically
- **Third-party integrations**: Connect external tools and APIs seamlessly through integration profiles
- **Broad alert coverage**: Apply automation to alerts from Microsoft Sentinel, Microsoft Defender, and XDR platforms

An embedded VS Code environment within the Microsoft Defender portal powers the experience. You can author and refine playbooks without leaving the portal.

## Prerequisites

You don't need prior coding experience to generate a playbook, but it helps to be familiar with tools like VS Code and Entra ID app registration.

You also must meet the following requirements:

### Environment requirements

- **Microsoft Sentinel workspace**: You must have a Microsoft Sentinel workspace onboarded to the Microsoft Defender portal.

### Required roles and permissions

You need the following permissions in [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/custom-permissions-details):

- **To generate and deploy playbooks**:

    - Automation: **Automation Playbooks (Read and Write)**
- **To author automation rules**:

    - **Microsoft Sentinel Contributor** role on the relevant Workspaces or Resource Groups containing them in Defender.

Note

Permissions might take up to two hours to take effect after assignment.

## Key concepts

Before you generate a playbook, understand the following concepts that the playbook generator relies on.

### Integration profiles

Integration profiles are secure configurations that allow generated playbooks to interact with external APIs. Each integration includes:

- Base URL
- Authentication method
- Required credentials

The playbook generator uses each configured integration profile to execute API calls for its corresponding service. If the integration is missing, it prompts you to create one before proceeding with playbook generation. Manage integration profiles centrally in the Defender portal under the **Automation** tab. Before creating a playbook, ensure you configure all required integrations.

To add integration, select **Integration** from the Automation tab, or use the **Add integration** link on top of the VS Code page. You can't edit the URL of existing integration links. Create a new integration link if needed, and delete the old one.

### Enhanced alert trigger

The Enhanced Alert Trigger extends automation capabilities beyond the standard alert trigger by providing:

- **Broader coverage**: Target alerts across Microsoft Sentinel, Microsoft Defender, and XDR platforms
- **Tenant-level application**: Ensure consistency across multiple workspaces
- **Advanced conditions**: Define granular criteria for triggering automation

The Enhanced Alert Trigger enables automatic execution of generated playbooks across your security ecosystem.

## Generate a new playbook

To generate a new playbook, configure the required integration profiles and then create the playbook in the embedded VS Code environment.

### Step 1. Create a Graph API integration profile and add any other required integrations you want to utilize

Register a Microsoft Entra ID application and create a Graph API integration profile by completing the following steps:

1. In the Azure portal, go to **Microsoft Entra ID** &gt; **Manage** &gt; **App registrations**.
2. Select **New registration**.

    [![Screenshot of the New registration page in Microsoft Entra ID.](media/generate-playbook/new-registration.png)](media/generate-playbook/new-registration.png#lightbox)
3. After the registration finishes, select the app registration and go to **Overview**.
4. Copy the **Application (client) ID** and **Directory (tenant) ID**. Save these values for later use.
5. Go to **Manage** &gt; **Certificates & secrets** &gt; **Client secrets**.
6. Select **New client secret**, provide a name and expiration date, and then select **Add**.

    [![Screenshot of the New client secret page in Microsoft Entra ID.](media/generate-playbook/client-secrets.png)](media/generate-playbook/client-secrets.png#lightbox)
7. Immediately copy the client secret **Value** and store it securely. You can't retrieve this value again.

#### Create the integration profile

After you register the app, create the integration profile in the Microsoft Defender portal:

1. In the Microsoft Defender portal, go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
2. Select the **Integration Profiles** tab.
3. Select **Create** and provide the following information:

    | Field | Value |
    | --- | --- |
    | **Integration name** | Any descriptive name, for example, "Graph Integration" |
    | **Description** | Short description, for example, "Integration with Microsoft Graph APIs" |
    | **Base API URL** | `https://graph.microsoft.com` |
    | **Authentication method** | **OAuth2** |
    | **Client ID** | Paste the Application (client) ID you copied earlier |
    | **Client secret** | Paste the client secret Value you copied earlier |
    | **Token endpoint** | `https://login.microsoftonline.com/{TENANT_ID}/oauth2/v2.0/token`(Replace {TENANT\_ID} with your Directory (tenant) ID) |
    | **Scopes** | `https://graph.microsoft.com/.default` |

    [![Screenshot of the Integration Profile creation page in Microsoft Sentinel.](media/generate-playbook/integration-profile.png)](media/generate-playbook/integration-profile.png#lightbox)
4. Verify under **Microsoft Graph / Application** that **SecurityAlert.Read.All** is listed and the Status is **Granted for &lt;tenant&gt;**.

[![Screenshot of API permissions in Microsoft Entra ID.](media/generate-playbook/api-permissions.png)](media/generate-playbook/api-permissions.png#lightbox)

### Create additional integration profiles

Configure integration profiles for any other third-party services your playbooks use. Each integration requires:

- A unique name and description
- The service's base API URL
- An authentication method (OAuth2 Client Credentials, API Key, AWS Auth, User and Password, Bearer/JWT, or Hawk)
- Appropriate credentials for the selected authentication method

Note

You can't change the API URL and authentication method after creation. You can only edit the integration name and description.

### Step 2. Create a generated playbook

Create the generated playbook in the Microsoft Defender portal by completing the following steps:

1. Select the **Playbooks** tab.
2. Select **Create** &gt; **Playbook Generator**.
3. Enter a name for your playbook and select **Continue**.

    An embedded Visual Studio Code environment opens with Cline.

    [![Screenshot of the embedded Visual Studio Code environment with the playbook generator.](media/generate-playbook/playbook-name.png)](media/generate-playbook/playbook-name.png#lightbox)

#### Work in Plan mode

When the editor opens, the playbook generator session starts in **Plan mode**. In this mode, you describe your automation requirements and the playbook generator generates a plan for review.

1. In the chat interface, describe your playbook requirements in detail. Be explicit about:

    - What data to process
    - What actions to perform
    - What conditions to evaluate
    - Expected outcomes

    **Example**: "Create a playbook that triggers on phishing alerts. Extract the sender email address. Check if the user exists in our directory, and if so, temporarily disable their account and notify the security team." For other example prompts, see Example use case.
2. If the playbook generator requests approval to fetch documentation URLs, approve the request. This approval allows the playbook generator to access relevant API documentation to generate accurate code.

    [![Screenshot of the approval request dialog in the embedded Visual Studio Code environment.](media/generate-playbook/approval-request.png)](media/generate-playbook/approval-request.png#lightbox)
3. The playbook generator analyzes your request and might:

    - Ask clarifying questions
    - Request API documentation if it can't be accessed via web search
    - Notify you of missing integration profiles
    - Generate a preliminary plan and flow diagram
4. If the playbook generator identifies missing integration profiles:

    1. Select **Save** and exit the VS Code environment.
    2. Create the missing integration profiles in the **Integration Profiles** tab.
    3. Return to edit the playbook to continue.

    [![Screenshot showing missing integration profiles in the embedded Visual Studio Code environment.](media/generate-playbook/add-integration.png)](media/generate-playbook/add-integration.png#lightbox)

#### Review and approve the plan

After the playbook generator produces a plan, review and approve it before proceeding to code generation:

1. Review the generated plan and flow diagram carefully.
2. If you need changes, describe the modifications in the chat. The playbook generator revises the plan accordingly.
3. When satisfied with the plan, follow instructions and switch to **Act mode**.

    [![Screenshot of the embedded Visual Studio Code environment in Act mode with the playbook generator.](media/generate-playbook/act-mode.png)](media/generate-playbook/act-mode.png#lightbox)

#### Generate the playbook in Act mode

1. After you switch the playbook generator session to Act mode, the playbook generator delivers:

    - The complete playbook code in Python
    - Code validation
    - Comprehensive documentation, including a visual flow diagram and description of the playbook in natural language
2. The playbook generator asks the user for an Alert ID to run a test of the playbook. Before it executes the test, the playbook generator outlines the changes that will be applied to the environment and requests the user’s approval to proceed.
3. The playbook generator might request approval for code generation. To enable automatic generation without approval prompts, select the **Edit** checkbox under **Auto-approve**.

    [![Screenshot of the Autoapprove checkbox in the embedded Visual Studio Code environment.](media/generate-playbook/auto-approve.png)](media/generate-playbook/auto-approve.png#lightbox)

    Tip

    When you select **Save** in the chat, the playbook generator saves the current step and confirms your approval. **It doesn't save the entire playbook**.

#### Validate and save your playbook

Important

Newly created playbooks are disabled by default. After you validate and save your playbook, you must enable it before it can run.

1. To ensure correctness, manually review the generated code and documentation.
2. To preview the documentation in Markdown format:

    - **Windows/Linux**: Press Ctrl + Shift + V
    - **macOS**: Press Cmd + Shift + V
3. Select **Save** at the bottom-left of the editor.

    The playbook is created in a disabled state.
4. Close the editor when finished.

    [![Screenshot of the preview of an alert notification created with the playbook generator.](media/generate-playbook/preview.png)](media/generate-playbook/preview.png#lightbox)

## Enable and deploy your playbook

After creation, your generated playbook requires activation and an alert trigger to begin automating responses.

### Enable the playbook

Generated playbooks are created in a disabled state. Enable the playbook by completing the following steps:

1. In the **Automation** page, select the **Active Playbooks** tab.
2. Locate your newly created playbook.
3. Switch the playbook status to **Activate**.

### Create an enhanced alert trigger

Create an enhanced alert trigger to automatically run the playbook when specific alert conditions are met:

1. Go to the **Automation Rules** tab.
2. Select **Create** to define a new rule with enhanced trigger.
3. Set up the trigger conditions:

    | Setting | Description |
    | --- | --- |
    | **Conditions** | Define criteria such as alert title, severity, provider, or other attributes |
    | **Workspaces** | Select one or more workspaces where this rule applies. Workspaces requiring additional permissions appear grayed out |
    | **Actions** | Select **Run Playbook** and choose your enabled playbook |
4. Select **Save**.

Your generated playbook now automatically runs when alerts that match your specified conditions are generated.

Tip

Enhanced Alert Triggers work at the tenant level. You can apply automation across multiple workspaces and alert sources for comprehensive coverage.

## Monitor playbook execution

To view execution details for your generated playbook:

1. Go to the incident page that contains the relevant alert.
2. Select the **Activities** tab.
3. Find the row labeled **run playbook** to view the execution status and details.

Note

You can view the automation rule run results in the **incidents activity** tab, but not in the Microsoft Sentinel Health Table.

## Example use case

The following are examples of prompts you can use to generate playbooks for common scenarios:

- Create a playbook that enriches alert URL entities with VirusTotal data and adds the results as a comment to the related incident.
- Create a playbook that blocks an AWS IAM user, assigns the alert to John, and adds a remediation comment when a high severity alert includes an IAM user entity.

## Limitations of AI-generated playbooks

Be aware of the following limitations when working with generated playbooks:

### Playbook limitations

Generated playbooks have the following limitations:

- **Language support**: Only Python is supported for playbook authoring
- **Input constraints**: Playbooks currently accept alerts as the sole input type
- **Concurrent editing**: A single user can edit only one playbook at a time. However, multiple users can edit different playbooks simultaneously
- **Library support**: External libraries aren't currently supported
- **Code validation**: No automatic code validation is provided. Users must manually verify correctness
- **Number of playbooks**: You can create up to 100 playbooks per tenant
- **Playbook size**: Each playbook can have up to 5,000 lines
- **Runtime**: Maximum runtime per playbook execution is 10 minutes
- **Integrations**: Maximum number of integrations per tenant is 500.
- **AI interactions**: Maximum of 8M tokens per day per tenant
- **Playbook nesting**: Playbook-to-playbook calls aren't supported. A playbook can't invoke another playbook.

### Integration profiles limitations

Integration profiles have the following limitations:

- **Integration limitations**: Microsoft Graph and Azure Resource Manager integrations aren't enabled by default and must be manually created
- **Authentication methods**: Available methods include OAuth2 Client Credentials, API Key, AWS Auth, User and Password, Bearer/JWT Authentication, and Hawk
- **Integration configuration**: The API URL and authentication method can't be changed after creation

### Automation rule alert trigger limitations

Enhanced alert trigger rules have the following limitations:

- **Trigger limitations**: Enhanced Alert Trigger rules don't support priority ordering or expiration dates
- **Available actions**: Currently, the only available actions are triggering generated Playbooks and updating action alerts
- **Workspace permissions** – You must explicitly specify the workspaces where you have permissions; the trigger doesn't apply to workspaces you can't access.
- **Separate rule tables** – Enhanced Alert Trigger rules live alongside Standard Alert Trigger rules in a separate Automation Rules table. Currently, there's no automatic migration of Standard Alert Trigger rules.
- **Run result visibility** – Automation rule run results are **not written to the Sentinel Health Table**. However, you can view the runs and their outcomes in the **Activity tab of the Incident** that contains the targeted alert.
- The maximum number of active automation rules you can create is 500 per tenant.
- You can execute one action per rule.