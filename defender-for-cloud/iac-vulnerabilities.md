---
layout: Conceptual
title: Scan for misconfigurations in Infrastructure as Code - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/iac-vulnerabilities
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
description: Learn how to use Microsoft Security DevOps scanning with Microsoft Defender for Cloud to find misconfigurations in Infrastructure as Code (IaC).
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: f291b123-3c85-7148-97f2-db36236b52e6
document_version_independent_id: ef2a4412-b831-a78c-89bc-d0ecba602a2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/iac-vulnerabilities.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/iac-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/iac-vulnerabilities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 90de07de-9651-be39-207b-a1895aae2c22
---

# Scan for misconfigurations in Infrastructure as Code - Microsoft Defender for Cloud | Microsoft Learn

You can set up Microsoft Security DevOps to scan your connected GitHub repository or Azure DevOps project. Use a GitHub action or an Azure DevOps extension to run Microsoft Security DevOps only on your Infrastructure as Code (IaC) source code, and help reduce your pipeline runtime.

This article shows you how to apply a template YAML configuration file to scan your connected repository or project specifically for IaC security issues by using Microsoft Security DevOps rules. Before you begin, make sure you have a connected GitHub repository or Azure DevOps project and review the prerequisites.

## Prerequisites

- For Microsoft Security DevOps, set up the GitHub action or the Azure DevOps extension based on your source code management system:
    - If your repository is in GitHub, set up the [Microsoft Security DevOps GitHub action](github-action).
    - If you manage your source code in Azure DevOps, set up the [Microsoft Security DevOps Azure DevOps extension](configure-azure-devops-extension).
- Ensure that you have an IaC template in your repository.

## Set up and run a GitHub action to scan your connected IaC source code

To set up an action and view scan results in GitHub:

1. Sign in to [GitHub](https://www.github.com).
2. Go to the main page of your repository.
3. In the file directory, select **.github** &gt; **workflows** &gt; **msdevopssec.yml**.

    For more information about working with an action in GitHub, see [Prerequisites](github-action#configure-the-microsoft-security-devops-github-action).
4. Select the **Edit this file** (pencil) icon.

    [![Screenshot that highlights the Edit this file icon for the msdevopssec.yml file.](media/tutorial-iac-vulnerabilities/workflow-yaml.png)](media/tutorial-iac-vulnerabilities/workflow-yaml.png#lightbox)
5. In the **Run analyzers** section of the YAML file, add the following code to enable Infrastructure as Code scanning:

    ```yaml
    with:
        categories: 'IaC'
    ```

    Note

    Values are case sensitive.

    The following screenshot shows an example of the updated YAML configuration:

    ![Screenshot that shows the information to add to the YAML file.](media/tutorial-iac-vulnerabilities/add-to-yaml.png)
6. Select **Commit changes . . .** .
7. Select **Commit changes**.

    ![Screenshot that shows where to select Commit changes on the GitHub page.](media/tutorial-iac-vulnerabilities/commit-change.png)
8. (Optional) Add an IaC template to your repository. If you already have an IaC template in your repository, skip this step.

    For example, commit an IaC template that you can use to [deploy a basic Linux web application](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/webapp-basic-linux).

    1. Select the **azuredeploy.json** file.

        ![Screenshot that shows where the azuredeploy.json file is located.](media/tutorial-iac-vulnerabilities/deploy-json.png)
    2. Select **Raw**.
    3. Copy all the information in the file, like in the following example:

        ```json
        {
          "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "webAppName": {
              "type": "string",
              "defaultValue": "AzureLinuxApp",
              "metadata": {
                "description": "The base name of the resource, such as the web app name or the App Service plan."
              },
              "minLength": 2
            },
            "sku": {
              "type": "string",
              "defaultValue": "S1",
              "metadata": {
                "description": "The SKU of the App Service plan."
              }
            },
            "linuxFxVersion": {
              "type": "string",
              "defaultValue": "php|7.4",
              "metadata": {
                "description": "The runtime stack of the current web app."
              }
            },
            "location": {
              "type": "string",
              "defaultValue": "[resourceGroup().location]",
              "metadata": {
                "description": "The location for all resources."
              }
            }
          },
          "variables": {
            "webAppPortalName": "[concat(parameters('webAppName'), '-webapp')]",
            "appServicePlanName": "[concat('AppServicePlan-', parameters('webAppName'))]"
          },
          "resources": [
            {
              "type": "Microsoft.Web/serverfarms",
              "apiVersion": "2020-06-01",
              "name": "[variables('appServicePlanName')]",
              "location": "[parameters('location')]",
              "sku": {
                "name": "[parameters('sku')]"
              },
              "kind": "linux",
              "properties": {
                "reserved": true
              }
            },
            {
              "type": "Microsoft.Web/sites",
              "apiVersion": "2020-06-01",
              "name": "[variables('webAppPortalName')]",
              "location": "[parameters('location')]",
              "kind": "app",
              "dependsOn": [
                "[resourceId('Microsoft.Web/serverfarms', variables('appServicePlanName'))]"
              ],
              "properties": {
                "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('appServicePlanName'))]",
                "siteConfig": {
                  "linuxFxVersion": "[parameters('linuxFxVersion')]"
                }
              }
            }
          ]
        }
        ```
    4. In your GitHub repository, go to the **.github/workflows** folder.
    5. Select **Add file** &gt; **Create new file**.

        [![Screenshot that shows you how to create a new file.](media/tutorial-iac-vulnerabilities/create-file.png)](media/tutorial-iac-vulnerabilities/create-file.png#lightbox)
    6. Enter a name for the file.
    7. Paste the copied information in the file.
    8. Select **Commit new file**.

    The template file is added to your repository.

    ![Screenshot that shows that the new file you created is added to your repository.](media/tutorial-iac-vulnerabilities/file-added.png)
9. Verify that the Microsoft Security DevOps scan is finished:

    1. For the repository, select **Actions**.
    2. Select the workflow to see the action status.
10. To view the results of the scan, use one of the following options:

    - Go to **Defender for Cloud** &gt; **DevOps security**. This option doesn't require a GitHub Advanced Security (GHAS) license.
    - If you have a GitHub Advanced Security (GHAS) license, go to **Security** &gt; **Code scanning alerts** natively in GitHub.

## Set up and run an Azure DevOps extension to scan your connected IaC source code

To set up an extension and view scan results in Azure DevOps:

1. Sign in to [Azure DevOps](https://dev.azure.com/).
2. Select your project.
3. Select **Pipelines**.
4. Select the pipeline where your Azure DevOps extension for Microsoft Security DevOps is configured.
5. Select **Edit pipeline**.
6. In the pipeline YAML configuration file, below the `displayName` line for the **MicrosoftSecurityDevOps@1** task, add the following code to enable Infrastructure as Code scanning:

    ```yaml
    inputs:
        categories: 'IaC'
    ```

    The following screenshot shows an example of the pipeline YAML configuration with the IaC category added:

    ![Screenshot that shows where to add the IaC categories line in the pipeline configuration YAML file.](media/tutorial-iac-vulnerabilities/addition-to-yaml.png)
7. Select **Save**.
8. (Optional) Add an IaC template to your Azure DevOps project. If you already have an IaC template in your project, skip this step.
9. Choose whether to commit directly to the main branch or to create a new branch for the commit, and then select **Save**.
10. To view the results of the IaC scan, select **Pipelines**, and then select the pipeline you modified.
11. To see more details, select a specific pipeline run.

## View details and remediation information for applied IaC rules

The IaC scanning tools that are included with Microsoft Security DevOps are [Template Analyzer](https://github.com/Azure/template-analyzer) ([PSRule](https://aka.ms/ps-rule-azure) is included in Template Analyzer), [Checkov](https://www.checkov.io/) and [Terrascan](https://github.com/tenable/terrascan).

Template Analyzer runs rules on Azure Resource Manager templates (ARM templates) and Bicep templates. See the [Template Analyzer rules and remediation details](https://github.com/Azure/template-analyzer/blob/main/docs/built-in-rules.md#built-in-rules).

Terrascan runs rules on ARM templates and templates for CloudFormation, Docker, Helm, Kubernetes, Kustomize, and Terraform. See the [Terrascan rules](https://runterrascan.io/docs/policies/).

Chekov runs rules on ARM templates and templates for CloudFormation, Docker, Helm, Kubernetes, Kustomize, and Terraform. See the [Checkov rules](https://www.checkov.io/5.Policy%20Index/all.html).

To learn more about the IaC scanning tools that are included with Microsoft Security DevOps, see:

- [Template Analyzer](https://github.com/Azure/template-analyzer)
- [Checkov](https://www.checkov.io/)
- [Terrascan](https://runterrascan.io/)