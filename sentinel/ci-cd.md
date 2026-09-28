---
layout: Conceptual
title: Deploy Custom Content from your Repository - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/ci-cd
breadcrumb_path: breadcrumb/toc.json
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
description: This article describes how to create connections with a GitHub or Azure DevOps repository where you can manage your custom content and deploy it to Microsoft Sentinel.
author: mberdugo
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: monaberdugo
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016 - build-2025
locale: en-us
document_id: 4875d9a7-d76f-51ed-f6ba-c5a77ed1849a
document_version_independent_id: 1e183a2e-5b81-39d8-434b-125c40801980
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/ci-cd.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/ci-cd
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/ci-cd.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: bc2f5e38-be09-bb35-e964-e5c223954345
---

# Deploy Custom Content from your Repository - Microsoft Sentinel | Microsoft Learn

When creating custom content, you can manage it from your own Microsoft Sentinel workspaces or an external source control repository. This article describes how to create and manage connections between Microsoft Sentinel and GitHub or Azure DevOps repositories. Managing your content in an external repository allows you to make updates to that content outside of Microsoft Sentinel and have the updated content automatically deployed to your workspaces. For more information, see [Update custom content with repository connections](ci-cd-custom-content).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Prerequisites

Microsoft Sentinel currently supports connections to GitHub and Azure DevOps repositories. Before connecting your Microsoft Sentinel workspace to your source control repository, make sure that:

- You have an **Owner** role in the resource group that contains your Microsoft Sentinel workspace.
- Custom content files you want to deploy to your workspaces are in a supported format. For supported formats, see [Plan your repository content](ci-cd-custom-content#plan-your-repository-content).
- The account you use to create the connection is in your home tenant. External identities such as B2B guest accounts and delegated access aren’t supported.
- **(Custom detection rules only)**: A Microsoft 365 E5 license (or equivalent license that includes Microsoft Defender XDR) and Microsoft Sentinel workspaces onboarded to the Microsoft Defender portal. For more information, see [Deploy custom detection rules as code](ci-cd-custom-content#deploy-custom-detection-rules-as-code-preview).

# [GitHub prerequisites](#tab/github)
Before connecting to GitHub, make sure you have the following prerequisites:

- Collaborator access to your GitHub repository
- Actions enabled for GitHub and Pipelines enabled for Azure DevOps

# [Azure DevOps prerequisites](#tab/azure-devops)
Before connecting to Azure DevOps, ensure that the following prerequisites are met:

- Project Administrator access to your Azure DevOps repository
- Third-party application access via OAuth enabled for Azure DevOps [application connection policies](/en-us/azure/devops/organizations/accounts/change-application-access-policies#manage-a-policy).
- An Azure DevOps connection in the same tenant as your Microsoft Sentinel workspace

---

For more information on deployable content types, see [Plan your repository content](ci-cd-custom-content#plan-your-repository-content).

## Connect a repository

This procedure describes how to connect a GitHub or Azure DevOps repository to your Microsoft Sentinel workspace.

Each connection can support multiple types of custom content, including analytics rules, automation rules, custom detection rules (Preview), hunting queries, parsers, playbooks, and workbooks. For more information, see [About Microsoft Sentinel content and solutions](sentinel-solutions).

You can't create duplicate connections, with the same repository and branch, in a single Microsoft Sentinel workspace.

**Create your connection**:

1. Make sure that you're signed into your source control app with the credentials you want to use for your connection. If you're currently signed in using different credentials, sign out first.
2. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Content management**, select **Repositories**.

    For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Repositories**.
3. Select **Add new**, and then, on the **Create new deployment connection** page, enter a meaningful name and description for your connection.
4. From the **Source Control** dropdown, select the type of repository you want to connect to, and then select **Authorize**.
5. Select one of the following tabs, depending on your connection type:

# [GitHub](#tab/github)
1. Enter your GitHub credentials when prompted.

        The first time you add a connection, you're prompted to authorize the connection to Microsoft Sentinel. If you're already logged into your GitHub account on the same browser, your GitHub credentials are autopopulated.
    2. A **Repository** area now shows on the **Create new deployment connection** page, where you can select an existing repository to connect to. Select your repository from the list, and then select **Add repository**.

        The first time you connect to a specific repository, you'll see a new browser window or tab, prompting you to install the **Azure-Sentinel** app on your repository. If you have multiple repositories, select the ones where you want to install the **Azure-Sentinel** app, and install it.

        You're directed to GitHub to continue the app installation.
    3. After the **Azure-Sentinel** app is installed in your repository, the **Branch** dropdown in the **Create new deployment connection** page is populated with your branches. Select the branch you want to connect to your Microsoft Sentinel workspace.
    4. From the **Content Types** dropdown, select the type of content you're deploying.

        - Both parsers and hunting queries use the **Saved Searches** API to deploy content to Microsoft Sentinel. If you select one of these content types, and also have content of the other type in your branch, both content types are deployed.
        - For all other content types, selecting a content type in the **Create new deployment connection** pane deploys only that content to Microsoft Sentinel. Content of other types isn't deployed.
    5. Select **Create** to create your connection. For example:

        ![Screenshot of a new GitHub repository connection.](media/ci-cd/create-new-connection-github.png)

# [Azure DevOps](#tab/azure-devops)
You're automatically authorized to Azure DevOps using your current Azure credentials. [Verify that you're authorized to the same Azure DevOps tenant](https://aex.dev.azure.com/) that you're connecting to from Microsoft Sentinel or use an InPrivate browser window to create your connection.

    1. In Microsoft Sentinel, from the dropdown lists that appear, select your **Organization**, **Project**, **Repository**, **Branch**, and **Content Types**.

        - Both parsers and hunting queries use the **Saved Searches** API to deploy content to Microsoft Sentinel. If you select one of these content types, and also have content of the other type in your branch, both content types are deployed.
        - For all other content types, selecting a content type in the **Create new deployment connection** pane deploys only that content to Microsoft Sentinel. Content of other types isn't deployed.
    2. Select **Create** to create your connection. For example:

        ![Screenshot of a new GitHub repository connection.](media/ci-cd/create-new-connection-devops.png)

---

After you create the connection, a new workflow or pipeline is generated in your repository. The content stored in your repository is deployed to your Microsoft Sentinel workspace.

The deployment time might vary depending on the volume of content that you're deploying.

## View the deployment status

**In GitHub**: On the repository's **Actions** tab, select the workflow **.yaml** file to access detailed deployment logs and any specific error messages.

**In Azure DevOps**: View the deployment status from the repository's **Pipelines** tab.

After the deployment is complete:

- The content stored in your repository is displayed in your Microsoft Sentinel workspace, in the relevant Microsoft Sentinel page.
- The connection details on the **Repositories** page are updated with the link to the connection's deployment logs and the status and time of the last deployment. For example:

    ![Screenshot of a GitHub repository connection's deployment logs.](media/ci-cd/deployment-logs-status.png)

The default workflow only deploys content modified since the last deployment based on commits to the repository, but you might want to turn off smart deployments or perform other customizations. For example, you can configure different deployment triggers, or deploy content exclusively from a specific root folder. To learn more, see [Customize repository deployments](ci-cd-custom-deploy).

## Edit content

When you successfully create a connection to your source control repository, your content is deployed to Sentinel. We recommend that you edit content stored in a connected repository *only* in the repository, and not in Microsoft Sentinel. For example, to make changes to your analytics rules, do so directly in GitHub or Azure DevOps.

If you edit the content in Microsoft Sentinel instead, make sure to export the edited content to your source control repository to prevent your changes from being overwritten the next time the repository content is deployed to your workspace.

## Delete content

Deleting content from your repository doesn't delete it from your Microsoft Sentinel workspace. If you want to remove content that was deployed through repositories, delete it from both your repository and Microsoft Sentinel. For example, set a filter for the content based on source name to make it easier to identify content from repositories.

![Screenshot of analytics rules filtered by source name of repositories.](media/ci-cd/delete-repo-content.png)

## Remove a repository connection

The following steps describe how to remove the connection to a source control repository from Microsoft Sentinel. In order to use Bicep files, your repository connection must be newer than November 1, 2024. Use this procedure to remove the connection and recreate it in order to update the connection.

To remove your connection:

1. In Microsoft Sentinel, under **Content management**, select **Repositories**.
2. In the grid, select the connection you want to remove, and then select **Delete**.
3. Select **Yes** to confirm the deletion.

After you remove your connection, content that was previously deployed via the connection remains in your Microsoft Sentinel workspace. Content added to the repository after removing the connection isn't deployed.

If you encounter issues or an error message when you delete your connection, we recommend that you check your source control. Confirm that the GitHub workflow or Azure DevOps pipeline associated with the connection is deleted.

### Remove the Microsoft Sentinel app from your GitHub repository

If you intend to delete the Microsoft Sentinel app from a GitHub repository, we recommend that you *first* remove all associated connections from the Microsoft Sentinel **Repositories** page.

Each Microsoft Sentinel App installation has a unique ID that's used when both adding and removing the connection. If the ID is missing or changed, remove the connection from the Microsoft Sentinel **Repositories** page and manually remove the workflow from your GitHub repository to prevent any future content deployments.