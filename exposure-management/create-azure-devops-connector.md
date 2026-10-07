---
layout: Conceptual
title: Create an Azure DevOps connector for agentic code security - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/create-azure-devops-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Connect your Azure DevOps organization to Microsoft Defender to enable remote on-demand agentic code scans across your repositories.
ms.topic: how-to
ms.date: 2026-07-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 60d97014-71ca-4d93-e5a0-0cd210643fa4
document_version_independent_id: 60d97014-71ca-4d93-e5a0-0cd210643fa4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/create-azure-devops-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-azure-devops-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/create-azure-devops-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: db53f5b1-3e17-3ae5-f681-806e266a17d8
---

# Create an Azure DevOps connector for agentic code security - Microsoft Security Exposure Management | Microsoft Learn

The Azure DevOps (ADO) connector is the recommended onboarding path for agentic code security for organizations that use Azure DevOps as their source code management (SCM) platform. It lets you connect your Azure DevOps organization and onboard its repositories through a simple flow. After onboarding your repositories, you can trigger a remote on-demand agentic scan for any onboarded repository.

## Prerequisites

You must have all of the following permissions to successfully authorize or reauthorize the connector:

- Access to the Microsoft Defender portal with at least the **Security Administrator** role in Microsoft Entra ID.
- The **Project Collection Administrator** role on each Azure DevOps organization you want to connect (**Organization Settings** &gt; **Security** &gt; **Permissions**).
- The **Basic** or **Basic + Test Plans** access level in each Azure DevOps organization (**Organization Settings** &gt; **Users**). The **Stakeholder** access level isn't sufficient.

The Microsoft Defender Code app must also be provisioned in your tenant. You can skip the provisioning script only if both of the following conditions are met:

- Your organization has a Microsoft 365 E5 license. The app is provisioned automatically during MDASH onboarding.
- The Azure DevOps organization tenant is the same as the Defender tenant.

Otherwise, run the provisioning script before creating the Azure DevOps connector. For more information, see [Microsoft Defender Code script for Azure DevOps connector](microsoft-defender-code-script-azure-devops-connector).

Note

If the same Azure DevOps organization is already connected through the Azure portal's Azure DevOps connector and you want to connect it through the Defender portal, disconnect the Azure portal connector first.

After the Azure portal's Azure DevOps connector is disconnected, the Microsoft Defender for DevOps Security capabilities associated with that connector are no longer available. For information about the affected capabilities, see [Support and prerequisites](/en-us/azure/defender-for-cloud/devops-support).

## Step 1: Prepare your tenant

Cloud Security must be prepared in the tenant before you can access the Azure DevOps connector creation flow.

If Cloud Security has already been activated in your Defender tenant, no action is required. The **Prepare my tenant** option won't be displayed, and you can proceed directly to creating the connector.

If the tenant hasn't used Cloud Security in the Defender portal:

1. Go to **Cloud security** &gt; **Overview**.
2. Select **Prepare my tenant**.
3. Confirm tenant preparation.

## Step 2: Open the connector wizard

In the Defender portal, go to **MDASH Initiative** &gt; **Settings**. For information about accessing the MDASH Initiative, see [Entry points](/en-us/security-exposure-management/ai-code-security-onboarding).

- In **Agentic code scanning management**, next to **Source code environment**, select **Add another**, and then select **Azure DevOps.***You'll be redirected to the***Azure DevOps*****connector flow.***
- Optionally, enter a connector name. If you leave it blank, a default name is assigned automatically.
- Select **Next**.

## Step 3: Configure access and permissions

The connector exposes two permission tiers:

- **Read** — Selected by default and can't be removed. Allows Defender for DevOps to scan your Azure DevOps repositories and identify security issues without making any changes.
- **Write** — Selected by default and optional. Required only for a limited set of Azure DevOps operations that inherently need write access, such as creating pull requests.

### Read access

Read access includes:

- Source code and repository metadata
- Pipelines and service connections
- Security-related signals across the connected organizations and projects

### Write access (optional)

Write access enables Defender for DevOps to take actions in your repositories and integrate findings into developer workflows. This access includes the ability to:

- Create pull requests that carry AI-generated fixes
- Update repository content and metadata as part of remediation flows

Note

Write access is optional and is only required for scenarios where Defender needs to create, update, or post information back to Azure DevOps repositories. Read access is sufficient for security scanning and discovery scenarios.

Review the permission selection and select **Next**.

## Step 4: Authorize and configure

Grant the DevOps security app permission to access your Azure DevOps resources and select the organizations to onboard.

1. Select **Authorize Entra ID**.
2. In the sign-in dialog, select the account that has **Project Collection Administrator** on the target Azure DevOps organizations.
3. After authorization succeeds, the wizard lists all Azure DevOps organizations discovered for that account, with the number of projects in each.
4. Select the organizations you want to onboard, then select **Next**.

Note

You can select a subset of the discovered organizations. Unselected organizations are ignored and can be added later by editing the connector.

## Step 5: Review and activate

The **Review and finish** page shows a summary of your flow:

- Display name of the connector
- List of Azure DevOps organizations being onboarded, with project counts
- Access and permissions scope (**Read** and, if selected, **Write**)

Select **Activate** to activate the connector.

After activating the Azure DevOps connector, the ability to trigger an on-demand agentic scan for onboarded repositories becomes available within up to one hour.