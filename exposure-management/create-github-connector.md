---
layout: Conceptual
title: Create a GitHub connector for agentic code security - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/create-github-connector
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Connect your GitHub organization to Microsoft Defender to enable remote on-demand agentic code scans across your repositories.
ms.topic: how-to
ms.date: 2026-07-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 29e258da-389d-87fb-81f3-b52057417c54
document_version_independent_id: 29e258da-389d-87fb-81f3-b52057417c54
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/create-github-connector.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-github-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/create-github-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: e84cf0e4-0258-6982-02a9-4432e573c44f
---

# Create a GitHub connector for agentic code security - Microsoft Security Exposure Management | Microsoft Learn

The GitHub connector is the recommended onboarding path for agentic code security. It lets you connect your GitHub organization and onboard its repositories through a simple flow. After onboarding your repositories, you can trigger a remote on-demand agentic scan for any onboarded repository.

## Prerequisites

- Access to the Microsoft Defender portal with at least the **Security Administrator** role in Microsoft Entra ID to create and manage connectors.
- The **Organization Owner** role in the GitHub organization that you want to connect.

Note

If the same GitHub organization is already connected through the Azure portal's GitHub connector and you want to connect it through the Defender portal, disconnect the Azure portal connector first.

> 
> After the Azure portal's GitHub connector is disconnected, the Microsoft Defender for DevOps Security capabilities associated with that connector are no longer available.

For information about Defender for DevOps Security support and prerequisites, see [Support and prerequisites](/en-us/azure/defender-for-cloud/devops-support).

## Step 1: Prepare your tenant

Cloud Security must be prepared in the tenant before you can access the GitHub connector creation flow.

If Cloud Security has already been activated in your Defender tenant, no action is required. The **Prepare my tenant** option won't be displayed, and you can proceed directly to creating the GitHub connector.

If the tenant hasn't used Cloud Security in the Defender portal:

1. Go to **Cloud security** &gt; **Overview**.
2. Select **Prepare my tenant**.
3. Confirm tenant preparation.

## Step 2: Open the connector wizard

1. In the Defender portal, go to MDASH Initiative &gt; **Settings**. For information about accessing the MDASH Initiative, see [Entry points](/en-us/security-exposure-management/ai-code-security-onboarding).

- In **Agentic code scanning management**, next to **Source code environment**, select **Add another**, and then select **GitHub.***You'll be redirected to the***GitHub*****connector flow.***
- Optionally, enter a connector name. If you leave it blank, a default name is assigned automatically.
- Select **Next**.

## Step 3: Configure access and permissions

The connector exposes two permission tiers:

- **Read** — Selected by default and can't be removed. Allows Defender for DevOps to scan your repositories and identify security issues without making any changes.
- **Write** — Selected by default and optional. Enables GitHub issue creation and pull request creation.

### Read access

Read access includes:

- Source code and repository metadata
- Actions, environments, and deployments
- Commit statuses and merge queues
- Packages, Pages, and repository projects
- Security-related data, including advisories and secrets

### Write access (optional)

Write access enables Defender for DevOps to take actions in your repositories and integrate findings into developer workflows. This access includes the ability to:

- Create and update issues and pull requests
- Post checks and security findings
- Manage Dependabot and secret scanning alerts
- Update repository metadata and properties
- Write security events and artifacts

Note

Write access is optional and is only required for scenarios where Defender needs to create, update, or post information back to GitHub repositories. Read access is sufficient for security scanning and discovery scenarios.

Review the permission selection and select **Next**.

## Step 4: Authorize and install the GitHub App

1. Select **Install**. The GitHub OAuth dialog opens.
2. Sign in to GitHub and select the organization to onboard.
3. On the GitHub App install screen, confirm the installation. The dialog closes.
4. When you see the success confirmation, select **Next**.

Note

The GitHub App can't be installed on a GitHub organization that's already connected via the Azure portal's GitHub connector. Selecting such an organization results in an error. To connect the same GitHub organization in the Defender portal, you must first delete the existing connector in the Azure portal.

## Step 5: Review and activate

The **Review and finish** page shows a summary of your flow:

- Name of the connector
- Permission scope
- Name of the GitHub organization being onboarded
- Number of repositories that will be onboarded

Select **Activate** to activate the connector.

After activating the GitHub connector, the ability to trigger an on-demand agentic scan for onboarded repositories becomes available within up to one hour.