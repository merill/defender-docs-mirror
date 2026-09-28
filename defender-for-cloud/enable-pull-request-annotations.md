---
layout: Conceptual
title: Enable pull request annotations in GitHub or in Azure DevOps - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-pull-request-annotations
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Add pull request annotations in GitHub or in Azure DevOps. By adding pull request annotations, your SecOps, and developer teams so that they can be on the same page when it comes to mitigating issues.
ms.topic: overview
ms.date: 2025-07-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0fbb66d3-12d2-987a-4cb0-cee923aa4e5e
document_version_independent_id: 7afc6e6e-97d6-b203-1897-66be62146760
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-pull-request-annotations.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-pull-request-annotations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-pull-request-annotations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: c6cd1bbd-7377-b9b9-a118-8e6b31ea2353
---

# Enable pull request annotations in GitHub or in Azure DevOps - Microsoft Defender for Cloud | Microsoft Learn

DevOps security exposes security findings as annotations in Pull Requests (PR). Security operators can enable PR annotations in Microsoft Defender for Cloud. Any exposed issues can be remedied by developers. This process can prevent and fix potential security vulnerabilities and misconfigurations before they enter the production stage. DevOps security annotates vulnerabilities within the differences introduced during the pull request rather than all the vulnerabilities detected across the entire file. Developers are able to see annotations in their source code management systems and Security operators can see any unresolved findings in Microsoft Defender for Cloud.

With Microsoft Defender for Cloud, you can configure PR annotations in Azure DevOps. You can get PR annotations in GitHub if you're a GitHub Advanced Security customer.

Note

Pull request annotations, also known as merge request annotations (GitLab), aren't supported in GitLab projects that are connected to Defender for Cloud DevOps.

Defender for Cloud will present security findings for any connected GitLab repositories. However, GitLab merge requests don't show these findings as inline annotations.

GitHub supports pull request annotations when you enable GitHub Advanced Security.

## What are pull request annotations

Pull request annotations are comments that are added to a pull request in GitHub or Azure DevOps. These annotations provide feedback on the code changes made and identified security issues in the pull request and help reviewers understand the changes that are made.

Users with access to the repository can add annotations, to suggest changes, ask questions, or provide feedback on the code. Annotations can also be used to track issues and bugs that need to be fixed before the code is merged into the main branch. DevOps security in Defender for Cloud uses annotations to surface security findings.

## Prerequisites

**For GitHub**:

- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Be a [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security) customer.
- [Connect your GitHub repositories to Microsoft Defender for Cloud](quickstart-onboard-github).
- [Configure the Microsoft Security DevOps GitHub action](github-action).

**For Azure DevOps**:

- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Have write access (owner/contributor) to the Azure subscription](/en-us/azure/active-directory/privileged-identity-management/pim-how-to-activate-role).
- [Connect your Azure DevOps repositories to Microsoft Defender for Cloud](quickstart-onboard-devops).
- [Configure the Microsoft Security DevOps Azure DevOps extension](configure-azure-devops-extension).

## Enable pull request annotations in GitHub

By enabling pull request annotations in GitHub, your developers gain the ability to see their security issues when they create a PR directly to the main branch.

**To enable pull request annotations in GitHub**:

1. Navigate to [GitHub](https://github.com/) and sign in.
2. Select a repository that you've onboarded to Defender for Cloud.
3. Navigate to **`Your repository's home page`** &gt; **.github/workflows**.

    [![Screenshot that shows where to navigate to, to select the GitHub workflow folder.](media/tutorial-enable-pr-annotations/workflow-folder.png)](media/tutorial-enable-pr-annotations/workflow-folder.png#lightbox)
4. Select **msdevopssec.yml**, which was created in the prerequisites.

    [![Screenshot that shows you where on the screen to select the msdevopssec.yml file.](media/tutorial-enable-pr-annotations/devopssec.png)](media/tutorial-enable-pr-annotations/devopssec.png#lightbox)
5. Select **edit**.

    [![Screenshot that shows you what the edit button looks like.](media/tutorial-enable-pr-annotations/edit-button.png)](media/tutorial-enable-pr-annotations/edit-button.png#lightbox)
6. Locate and update the trigger section to include:

    ```yml
    # Triggers the workflow on push or pull request events but only for the main branch
    pull_request:
      branches: ["main"]
    ```

    You can also view a [sample repository](https://github.com/microsoft/security-devops-action/tree/main/samples).

    (Optional) You can select which branches you want to run it on by entering the branch(es) under the trigger section. If you want to include all branches remove the lines with the branch list.
7. Select **Start commit**.
8. Select **Commit changes**.

    Any issues that are discovered by the scanner will be viewable in the Files changed section of your pull request.

    - **Used in tests** - The alert isn't in the production code.

## Enable pull request annotations in Azure DevOps

By enabling pull request annotations in Azure DevOps, your developers gain the ability to see their security issues when they create PRs directly to the main branch.

### Enable Build Validation policy for the CI Build

Before you can enable pull request annotations, your main branch must have enabled Build Validation policy for the CI Build.

**To enable Build Validation policy for the CI Build**:

1. Sign in to your Azure DevOps project.
2. Navigate to **Project settings** &gt; **Repositories**.

    ![Screenshot that shows you where to navigate to, to select repositories.](media/tutorial-enable-pr-annotations/project-settings.png)
3. Select the repository to enable pull requests on.
4. Select **Policies**.
5. Navigate to **Branch Policies** &gt; **Main branch**.

    [![Screenshot that shows where to locate the branch policies.](media/tutorial-enable-pr-annotations/branch-policies.png)](media/tutorial-enable-pr-annotations/branch-policies.png#lightbox)
6. Locate the Build Validation section.
7. Ensure the build validation for your repository is toggled to **On**.

    [![Screenshot that shows where the CI Build toggle is located.](media/tutorial-enable-pr-annotations/build-validation.png)](media/tutorial-enable-pr-annotations/build-validation.png#lightbox)
8. Select **Save**.

    [![Screenshot that shows the build validation.](media/tutorial-enable-pr-annotations/validation-policy.png)](media/tutorial-enable-pr-annotations/validation-policy.png#lightbox)

Once you've completed these steps, you can select the build pipeline you created previously and customize its settings to suit your needs.

### Enable pull request annotations

**To enable pull request annotations in Azure DevOps**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Defender for Cloud** &gt; **DevOps security**.
3. Select all relevant repositories to enable the pull request annotations on.
4. Select **Manage resources**.

    [![Screenshot that shows you how to manage resources.](media/tutorial-enable-pr-annotations/manage-resources.png)](media/tutorial-enable-pr-annotations/manage-resources.png#lightbox)
5. Toggle pull request annotations to **On**.

    [![Screenshot that shows the toggle switched to on.](media/tutorial-enable-pr-annotations/annotation-on.png)](media/tutorial-enable-pr-annotations/annotation-on.png#lightbox)
6. (Optional) Select a category from the drop-down menu.

    Note

    Only Infrastructure-as-Code misconfigurations (ARM, Bicep, Terraform, CloudFormation, Dockerfiles, Helm Charts, and more) results are currently supported.
7. (Optional) Select a severity level from the drop-down menu.
8. Select **Save**.

All annotations on your pull requests will be displayed from now on based on your configurations.

**To enable pull request annotations for my Projects and Organizations in Azure DevOps**:

You can do this programmatically by calling the Update Azure DevOps Resource API exposed the Microsoft. Security Resource Provider.

API Info:

**Http Method**: PATCH **URLs**:

- Azure DevOps Project Update: `https://management.azure.com/subscriptions/<subId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Security/securityConnectors/<connectorName>/devops/default/azureDevOpsOrgs/<adoOrgName>/projects/<adoProjectName>?api-version=2023-09-01-preview`
- Azure DevOps Org Update]: `https://management.azure.com/subscriptions/<subId>/resourcegroups/<resourceGroupName>/providers/Microsoft.Security/securityConnectors/<connectorName>/devops/default/azureDevOpsOrgs/<adoOrgName>?api-version=2023-09-01-preview`

Request Body:

```json
{
   "properties": {
"actionableRemediation": {
              "state": <ActionableRemediationState>,
              "categoryConfigurations":[
                    {"category": <Category>,"minimumSeverityLevel": <Severity>}
               ]
           }
    }
}
```

Parameters / Options Available

**`<ActionableRemediationState>`** **Description**: State of the PR Annotation Configuration **Options**: Enabled | Disabled

**`<Category>`** **Description**: Category of Findings that are annotated on pull requests. **Options**: IaC | Code | Artifacts | Dependencies | Containers **Note**: Only IaC is supported currently

**`<Severity>`** **Description**: The minimum severity of a finding that is considered when creating PR annotations. **Options**: High | Medium | Low

Example of enabling an Azure DevOps Org's PR Annotations for the IaC category with a minimum severity of Medium using the az cli tool.

Update Org:

```azurecli
az --method patch --uri https://management.azure.com/subscriptions/4383331f-878a-426f-822d-530fb00e440e/resourcegroups/myrg/providers/Microsoft.Security/securityConnectors/myconnector/devops/default/azureDevOpsOrgs/testOrg?api-version=2023-09-01-preview --body "{'properties':{'actionableRemediation':{'state':'Enabled','categoryConfigurations':[{'category':'IaC','minimumSeverityLevel':'Medium'}]}}}
```

Example of enabling an Azure DevOps Project's PR Annotations for the IaC category with a minimum severity of High using the az cli tool.

Update Project:

```azurecli
az --method patch --uri https://management.azure.com/subscriptions/4383331f-878a-426f-822d-530fb00e440e/resourcegroups/myrg/providers/Microsoft.Security/securityConnectors/myconnector/devops/default/azureDevOpsOrgs/testOrg/projects/testProject?api-version=2023-09-01-preview --body "{'properties':{'actionableRemediation':{'state':'Enabled','categoryConfigurations':[{'category':'IaC','minimumSeverityLevel':'High'}]}}}"
```

## Learn more

- Learn more about [DevOps security](defender-for-devops-introduction).
- Learn more about [DevOps security in Infrastructure as Code](iac-vulnerabilities).