---
layout: Conceptual
title: Getting Started with Codename MDASH - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/ai-code-security-onboarding
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Onboard agentic code security in the Microsoft Defender portal by accepting terms, connecting your Microsoft Foundry resource, and completing agentic code scanning setup.
ms.topic: how-to
ms.date: 2026-08-31T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1026
ai-usage: ai-assisted
locale: en-us
document_id: a2de5317-7813-ae17-4889-9e9500a6f20f
document_version_independent_id: a2de5317-7813-ae17-4889-9e9500a6f20f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/ai-code-security-onboarding.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ai-code-security-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/ai-code-security-onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/de19c5b8-e208-412e-9238-db3f631dea5b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ea7bf5d6-7154-4ba9-8ebc-59117ccacd49
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: 0a7a754f-2d1a-2e18-f9d1-43bfd0069a17
---

# Getting Started with Codename MDASH - Microsoft Security Exposure Management | Microsoft Learn

Confirm you have everything in place before you begin, then follow the steps to connect your organization to agentic code security, codename MDASH, and start running scans on your code.

## Prerequisites checklist

To complete this setup, you need:

- **Global Administrator** or **Security Administrator** role in Microsoft Entra ID to complete the agentic code security onboarding process in the Microsoft Defender portal.
- Authority to accept the codename MDASH terms and conditions on behalf of your organization during onboarding.
- An Azure subscription and resource group in which to create a dedicated Microsoft Foundry resource used exclusively for codename MDASH. For full details, see [Connect Microsoft Foundry](mdash-foundry-integration).
- Permission to deploy the models required. For list of models, see [Deploy the required models](mdash-foundry-integration#deploy-the-required-models).
- If the Foundry resource's networking is set to **Selected networks and private endpoints**, action is required to allow codename MDASH access. For more information, see [Allow Codename MDASH to access your Microsoft Foundry resource](mdash-foundry-integration#allow-codename-mdash-to-access-your-microsoft-foundry-resource).
- At least one of the following AI scanning paths:

    - **Option 1 — Remote scan (recommended).** For full details, see either [Create a GitHub connector](create-github-connector) or [Create Azure DevOps connector](create-azure-devops-connector).
    - **Option 2 — Defender CLI.** For full details, see [Defender CLI setup](defender-cli-authentication).
- If outbound traffic is restricted, allow the required domains. For more information, see [Allow list](ai-code-security-overview#allow-list).
- Access to the [Microsoft Defender portal](https://security.microsoft.com) with permission to open **Exposure Management** and **Initiatives**.
- The Foundry project endpoint. MDASH supports two authentication methods for the Foundry connection. For details about the available authentication methods, see [Authentication methods](mdash-foundry-integration#authentication-methods).
- Defender unified RBAC permissions assigned. For the required permissions and how to assign them, see Assign permissions to users using Defender RBAC.

## Assign permissions to users using Defender RBAC

Use Microsoft Defender unified role-based access control (RBAC) to grant users and groups the agentic code security permissions required to run scans, upload results, and review or manage findings. In this step, you create a custom, feature-scoped role in Microsoft Defender for these specific capabilities, and then assign the role to the users who need access.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. In the navigation pane, select **System** &gt; **Permissions**.
3. Under **Microsoft Defender XDR**, select **Roles** &gt; **Create custom role**.
4. On the **Basics** tab, enter a role name and description.
5. If users need to open the Exposure Management experience in the Defender portal:

    1. On **Choose permissions**, expand **Security posture**, and then select **Select custom permissions**.
    2. Under **Posture management**, select **Exposure Management (Read)**. This permission can provide access to Exposure Management insights beyond codename MDASH. For more information, see [Security posture – Posture management](/en-us/defender-xdr/custom-permissions-details#security-posture--posture-management).
    3. Select **Apply**.
6. On **Choose permissions**, expand **Agentic code security**.
7. Under **AI Scan Security**, set the permission levels you need (for more information, see [Security posture – AI code scan](/en-us/defender-xdr/custom-permissions-details#security-posture--ai-code-scan):

    - **Run scan (Manage)** — required to trigger on-demand or CLI scans.
    - **Upload results (Manage)** — required to upload CLI scan results to Defender.
    - **Scan results (Manage)** — required to triage, dismiss, or otherwise manage findings.
    - **Scan results (Read)** — required to view findings in the Defender portal and the initiative. This permission alone does not grant access to the Exposure Management experience.
8. Review the permissions, and select **Apply**.
9. Select **Next** to go to **Assign users and data sources**. Assign the users who should receive this role.
10. Select **Add assignment**, and configure users, groups, and data sources.
11. Under **Data sources**, keep both **Microsoft Defender for Cloud** and **Microsoft Security Exposure Management** selected.
12. Select **Add**, review the assignments, and select **Next**.
13. Review the role details and select **Submit**.

For more information, see [Create custom roles with Microsoft Defender unified RBAC](/en-us/defender-xdr/create-custom-rbac-roles).

## Entry points

Start the onboarding flow from either of these locations in the [Microsoft Defender portal](https://security.microsoft.com):

- **Exposure Management** &gt; **Overview**: Select **Agentic code security**.
- **Exposure Management** &gt; **Initiatives**: Select the **Codename MDASH - Agentic code scanner** initiative.

## Step 1: Accept terms and conditions

Review and accept the terms and conditions before you proceed.

1. Review the terms and conditions in the onboarding flow.
2. Select the checkbox to confirm acceptance.
3. You must accept the terms and conditions before you can select **Save**.

## Step 2: Connect a Microsoft Foundry resource

For step-by-step instructions on creating an Microsoft Foundry resource and deploying the required models, see [Connect Microsoft Foundry](mdash-foundry-integration).

## Step 3: Defender portal onboarding

Provide the required details to connect your Microsoft Foundry resource and validate the connection.

1. Enter the **Project endpoint** (for example: `https://your-foundry.azure.com`) and **API key**.
2. Choose an authentication method: **Keyless** (recommended) or API key. For details, see [Authentication methods](mdash-foundry-integration#authentication-methods).
3. Select Validate to verify the connection.
4. Select **Save** to finish onboarding. You must successfully validate the resource before you can select Save.

***Note:** MDASH uses the **Standard** scan configuration by default. You can update the default configuration during onboarding or change it later*

## Step 4: Set up AI scanning

### Remote scan (recommended)

Note

You can create the GitHub or Azure DevOps connector either before or after codename MDASH onboarding.

Create a GitHub or Azure DevOps connector to connect your SCM organization and trigger on-demand scans through the Defender portal without installing anything locally.

To create an SCM connector, you need access to the Microsoft Defender portal with permission to manage connectors, and you must have either the **Global Administrator** or **Security Administrator** role in Microsoft Entra ID. You must also have the **Organization Owner** role in the GitHub organization or **Project Collection Administrator** role in the Azure DevOps organization that you want to connect.

1. [Create a GitHub connector](create-github-connector) to connect your GitHub organization or [Create an Azure DevOps connector](create-azure-devops-connector) to connect your Azure DevOps organization.
2. [Trigger an on-demand agentic scan](trigger-on-demand-scan) for any onboarded repository.

### Defender CLI

To onboard agentic code security with Defender CLI, you need the **Global Administrator** or **Security Administrator** role in Microsoft Entra ID.

1. [Defender CLI setup](defender-cli-authentication)
2. [Install and run Defender CLI](defender-cli).

## Step 5: Review security findings

After scans run, view security findings in the [Microsoft Defender portal](https://security.microsoft.com).

For details, see [Codename MDASH - Agentic code scanner initiative](mdash-initiative).