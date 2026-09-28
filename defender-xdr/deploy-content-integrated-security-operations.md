---
layout: Conceptual
title: Deploy content as code from your repository for an ISOC workspace - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/deploy-content-integrated-security-operations
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to connect an ISOC workspace to a GitHub or Azure DevOps repository to manage and deploy security content by using CI/CD.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.topic: how-to
ms.service: microsoft-sentinel
ms.date: 2026-09-14T00:00:00.0000000Z
ms.collection:
- m365-security
- tier1
- usx-security
- msftsolution-secops
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 96b39cb0-55c2-44c8-aeda-c7cc4072cdce
document_version_independent_id: 96b39cb0-55c2-44c8-aeda-c7cc4072cdce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/deploy-content-integrated-security-operations.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy-content-integrated-security-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/deploy-content-integrated-security-operations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 10132765-3845-3159-f177-45eabfa4d0cb
---

# Deploy content as code from your repository for an ISOC workspace - Microsoft Defender XDR | Microsoft Learn

Use repositories with Integrated Security Operations Center (ISOC) in Microsoft Defender to manage and deploy custom security content to your ISOC workspace by using CI/CD.

You can manage content from the Microsoft Defender portal or an external GitHub or Azure DevOps repository. Managing content in an external repository lets you update content outside of Microsoft Defender and automatically deploy those updates to your ISOC workspace.

The CI/CD experience and supported content types for an ISOC workspace are the same as the existing Microsoft Sentinel repository experience.

Note

This feature is in preview. Capabilities and availability might change during the preview period.

## Prerequisites

Before you begin, make sure the following requirements are met:

- Your tenant is [eligible for ISOC](isoc-overview).
- You have an [ISOC workspace](onboard-isoc-workspace) in a resource group where you have the **Owner** role.
- You have the **Global Administrator** role in Microsoft Entra ID for the initial CI/CD setup.
- Custom content files that you want to deploy to your workspace are in a supported format. For supported formats, see [Plan your repository content](/en-us/azure/sentinel/ci-cd-custom-content#plan-your-repository-content).
- The account you use to create the connection is in your home tenant. External identities such as B2B guest accounts and delegated access aren't supported.
- **(Custom detection rules only)** You have a Microsoft 365 E5 license or an equivalent license that includes Microsoft Defender XDR. For more information, see [Deploy custom detection rules as code](/en-us/azure/sentinel/ci-cd-custom-content#deploy-custom-detection-rules-as-code-preview).

### GitHub prerequisites

Before connecting to GitHub, make sure that:

- You have **Collaborator** access to your GitHub repository.
- GitHub Actions is enabled.

### Azure DevOps prerequisites

Before connecting to Azure DevOps, make sure that:

- You have **Project Administrator** access to your Azure DevOps repository.
- Third-party application access through OAuth is enabled for Azure DevOps [application connection policies](/en-us/azure/devops/organizations/accounts/change-application-access-policies#manage-a-policy).
- Your Azure DevOps connection is in the same tenant as your ISOC workspace.

For more information about deployable content types, see [Plan your repository content](/en-us/azure/sentinel/ci-cd-custom-content#plan-your-repository-content).

## Connect a repository

Use this procedure to connect a GitHub or Azure DevOps repository to your ISOC workspace.

Each connection can support multiple types of custom content, including analytics rules, automation rules, custom detection rules, hunting queries, parsers, playbooks, and workbooks. For more information, see [About Microsoft Sentinel content and solutions](/en-us/azure/sentinel/sentinel-solutions).

You can't create duplicate connections with the same repository and branch in a single ISOC workspace.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Make sure that you're signed in to your source control application with the credentials you want to use for the connection.
3. In the Defender portal, select **Microsoft Sentinel** &gt; **Content management** &gt; **Repositories**.
4. Select **Add new**.
5. On the **Create new deployment connection** page, enter a name for the connection.
6. Enter a description for the connection.
7. From **Source Control**, select the repository type that you want to connect.
8. Select **Authorize**.
9. Complete the steps for your source control provider:

# [GitHub](#tab/github)
1. Enter your GitHub credentials when prompted.

        The first time you add a connection, you're prompted to authorize the connection to Microsoft Sentinel. If you're already signed in to your GitHub account in the same browser, your GitHub credentials are populated automatically.
    2. In **Repository**, select the repository that you want to connect.
    3. Select **Add repository**.

        The first time you connect to a repository, a new browser window or tab opens and prompts you to install the **Azure-Sentinel** app.
    4. In GitHub, select the repository where you want to install the **Azure-Sentinel** app.
    5. Install the **Azure-Sentinel** app.
    6. Return to the **Create new deployment connection** page.
    7. From **Branch**, select the branch that you want to connect to your ISOC workspace.
    8. From **Content Types**, select the content that you want to deploy.

        Both parsers and hunting queries use the **Saved Searches** API to deploy content. If you select one of these content types and your branch contains the other type, both content types are deployed.

        For other content types, only the content types that you select are deployed.
    9. Select **Create**.

        For example:

        ![Screenshot of a new GitHub repository connection.](media/ci-cd/create-new-connection-github.png)

# [Azure DevOps](#tab/azure-devops)
Azure DevOps automatically authorizes you by using your current Azure credentials.

    1. Make sure that you're authorized to the same Azure DevOps tenant that you're connecting to from Microsoft Defender.
    2. From **Organization**, select your Azure DevOps organization.
    3. From **Project**, select your project.
    4. From **Repository**, select your repository.
    5. From **Branch**, select the branch that you want to connect to your ISOC workspace.
    6. From **Content Types**, select the content that you want to deploy.

        Both parsers and hunting queries use the **Saved Searches** API to deploy content. If you select one of these content types and your branch contains the other type, both content types are deployed.

        For other content types, only the content types that you select are deployed.
    7. Select **Create**.

        For example:

        ![Screenshot of a new Azure DevOps repository connection.](media/ci-cd/create-new-connection-devops.png)

---

After you create the connection, a new workflow or pipeline is generated in your repository. The content stored in your repository is deployed to your ISOC workspace.

Deployment time might vary depending on the amount of content that you're deploying.

## View the deployment status

To view the deployment status in GitHub:

1. Open your repository in GitHub.
2. Select the **Actions** tab.
3. Select the workflow `.yaml` file to view deployment logs and error messages.

To view the deployment status in Azure DevOps:

1. Open your repository in Azure DevOps.
2. Select the **Pipelines** tab.

After deployment is complete:

- The content stored in your repository appears on the corresponding Microsoft Sentinel pages in the Defender portal.
- The connection details on the **Repositories** page show the deployment status, time of the last deployment, and a link to the deployment logs.

For example:

![Screenshot of a repository connection showing deployment logs and status.](media/ci-cd/deployment-logs-status.png)

By default, the workflow deploys only content modified since the previous deployment. You can customize this behavior by changing deployment triggers, turning off smart deployments, or limiting deployments to a specific root folder.

For more information, see [Customize repository deployments](/en-us/azure/sentinel/ci-cd-custom-deploy).

## Edit content

After you create a repository connection, edit connected content in the repository instead of editing it directly in Microsoft Defender.

If you edit deployed content in Microsoft Defender, export the updated content back to your source control repository. Otherwise, your changes might be overwritten the next time content is deployed from the repository.

## Delete content

Deleting content from your repository doesn't delete it from your ISOC workspace.

To remove content that was deployed through a repository:

1. Delete the content from your repository.
2. Delete the corresponding content from Microsoft Sentinel in the Defender portal.

You can filter content by its source name to help identify content deployed from repositories.

[![Screenshot of analytics rules filtered by the source name of a repository.](media/ci-cd/delete-repo-content.png)](media/ci-cd/delete-repo-content.png#lightbox)

## Remove a repository connection

Removing a repository connection stops future content deployments. Content that was previously deployed remains in your ISOC workspace.

To use Bicep files, your repository connection must be newer than November 1, 2024. Remove and recreate an older connection to update it.

To remove a repository connection:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Microsoft Sentinel** &gt; **Content management** &gt; **Repositories**.
3. Select the connection that you want to remove.
4. Select **Delete**.
5. Select **Yes** to confirm the deletion.

After you remove the connection, content previously deployed through the connection remains in your ISOC workspace. Content added to the repository after you remove the connection isn't deployed.

If you encounter an error when removing a connection, check your source control repository and confirm that the associated GitHub workflow or Azure DevOps pipeline is deleted.

### Remove the Microsoft Sentinel app from your GitHub repository

Before you remove the Microsoft Sentinel app from a GitHub repository, remove all associated connections from the **Repositories** page in Microsoft Defender.

Each Microsoft Sentinel app installation has a unique ID that's used when adding and removing the connection. If the ID is missing or changed, remove the connection from the **Repositories** page and manually remove the workflow from your GitHub repository to prevent future content deployments.