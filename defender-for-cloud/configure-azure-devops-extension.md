---
layout: Conceptual
title: Configure the Microsoft Security DevOps Azure DevOps extension - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/configure-azure-devops-extension
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
description: Install the Microsoft Security DevOps extension in Azure DevOps, configure YAML pipelines with static analysis tools, and upload SARIF findings to Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 8d82922c-b683-b33b-7780-3836504725be
document_version_independent_id: f89880c6-bb24-16e4-cf96-1d678e9f68f1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/configure-azure-devops-extension.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/configure-azure-devops-extension
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/configure-azure-devops-extension.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: bb9582e6-d1c3-fa34-363d-980fbc463e93
---

# Configure the Microsoft Security DevOps Azure DevOps extension - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Security DevOps is a command-line application that integrates static analysis into your development lifecycle. It installs, configures, and runs the latest SDL, security, and compliance analyzers using portable configurations to ensure consistent, deterministic execution across environments.

Microsoft Security DevOps uses the following open-source tools:

| Name | Language | License |
| --- | --- | --- |
| [AntiMalware](https://www.microsoft.com/windows/comprehensive-security) | Anti-malware protection in Windows from Microsoft Defender for Endpoint. Scans for malware and breaks the build if malicious content is detected. Runs by default on the Windows-latest agent. | Not open source |
| [Bandit](https://github.com/PyCQA/bandit) | Python | [Apache License 2.0](https://github.com/PyCQA/bandit/blob/master/LICENSE) |
| [BinSkim](https://github.com/Microsoft/binskim) | Binary targets: Windows, ELF | [MIT License](https://github.com/microsoft/binskim/blob/main/LICENSE) |
| [Checkov](https://github.com/bridgecrewio/checkov) | Terraform, Terraform plan, CloudFormation, AWS SAM, Kubernetes, Helm charts, Kustomize, Dockerfile, Serverless, Bicep, OpenAPI, ARM | [Apache License 2.0](https://github.com/bridgecrewio/checkov/blob/main/LICENSE) |
| [ESLint](https://github.com/eslint/eslint) | JavaScript | [MIT License](https://github.com/eslint/eslint/blob/main/LICENSE) |
| [IaCFileScanner](iac-template-mapping) | Template mapping tool for Terraform, CloudFormation, ARM templates, and Bicep | Not open source |
| [Template Analyzer](https://github.com/Azure/template-analyzer) | ARM templates, Bicep | [MIT License](https://github.com/Azure/template-analyzer/blob/main/LICENSE.txt) |
| [Terrascan](https://github.com/accurics/terrascan) | Terraform (HCL2), Kubernetes (JSON/YAML), Helm v3, Kustomize, Dockerfiles, CloudFormation | [Apache License 2.0](https://github.com/accurics/terrascan/blob/master/LICENSE) |
| [Trivy](https://github.com/aquasecurity/trivy) | Container images, infrastructure as code (IaC) | [Apache License 2.0](https://github.com/aquasecurity/trivy/blob/main/LICENSE) |

Note

As of September 20, 2023, the secrets scanning (CredScan) tool within the Microsoft Security DevOps (MSDO) Extension for Azure DevOps has been deprecated. MSDO secrets scanning is replaced with [GitHub Advanced Security for Azure DevOps](https://azure.microsoft.com/products/devops/github-advanced-security).

## Prerequisites

Before you install the extension, make sure you meet the following prerequisite:

- You need Project Collection Administrator privileges in your Azure DevOps organization to install the extension. If you don't have access, request these privileges from your Azure DevOps administrator.

## Install the extension

To install the Microsoft Security DevOps extension:

1. Sign in to [Azure DevOps](https://dev.azure.com/).
2. Go to **Shopping Bag** &gt; **Manage extensions**.

    ![Screenshot that shows how to navigate to the manage extensions screen.](media/msdo-azure-devops-extension/manage-extensions.png)
3. Select **Shared**.

    Note

    If you've already [installed the Microsoft Security DevOps extension](https://marketplace.visualstudio.com/items?itemName=ms-securitydevops.microsoft-security-devops-azdevops), it is listed in the Installed tab.
4. Select **Microsoft Security DevOps**.

    ![Screenshot that shows where to select Microsoft Security DevOps.](media/msdo-azure-devops-extension/marketplace-shared.png)
5. Select **Install**.
6. Select the appropriate organization from the dropdown menu.
7. Select **Install**.
8. Select **Proceed to organization**.

## Configure pipelines using YAML

Tip

Optional: Install the SARIF SAST Scans Tab extension if you want SARIF analysis results to appear automatically in the pipeline's **Scans** tab.

To configure a pipeline with YAML:

1. Sign into [Azure DevOps](https://dev.azure.com/).
2. Select your project.
3. Go to **Pipelines** &gt; **New pipeline**.

    [![Screenshot showing where to locate create pipeline in DevOps.](media/msdo-azure-devops-extension/create-pipeline.png)](media/msdo-azure-devops-extension/create-pipeline.png#lightbox)
4. Select **Azure Repos Git**.

    ![Screenshot that shows you where to navigate to, to select Azure repo git.](media/msdo-azure-devops-extension/repo-git.png)
5. Select the relevant repository.

    ![Screenshot showing where to select your repository.](media/msdo-azure-devops-extension/repository.png)
6. Select **Starter pipeline**.

    ![Screenshot showing where to select starter pipeline.](media/msdo-azure-devops-extension/starter-piepline.png)
7. Paste the following YAML into the pipeline:

    ```yml
    # Starter pipeline
    # Start with a minimal pipeline that you can customize to build and deploy your code.
    # Add steps that build, run tests, deploy, and more:
    # https://aka.ms/yaml
    trigger: none
    pool:
      # ubuntu-latest also supported.
      vmImage: 'windows-latest'
    steps:
    - task: MicrosoftSecurityDevOps@1
      displayName: 'Microsoft Security DevOps'
      # inputs:    
        # config: string. Optional. A file path to an MSDO configuration file ('*.gdnconfig'). Vist the MSDO GitHub wiki linked below for additional configuration instructions
        # policy: 'azuredevops' | 'microsoft' | 'none'. Optional. The name of a well-known Microsoft policy to determine the tools/checks to run. If no configuration file or list of tools is provided, the policy may instruct MSDO which tools to run. Default: azuredevops.
        # categories: string. Optional. A comma-separated list of analyzer categories to run. Values: 'code', 'artifacts', 'IaC', 'containers'. Example: 'IaC, containers'. Defaults to all.
        # languages: string. Optional. A comma-separated list of languages to analyze. Example: 'javascript,typescript'. Defaults to all.
        # tools: string. Optional. A comma-separated list of analyzer tools to run. Values: 'bandit', 'binskim', 'checkov', 'eslint', 'templateanalyzer', 'terrascan', 'trivy'. Example 'templateanalyzer, trivy'
        # break: boolean. Optional. If true, will fail this build step if any high severity level results are found. Default: false.
        # publish: boolean. Optional. If true, will publish the output SARIF results file to the chosen pipeline artifact. Default: true.
        # artifactName: string. Optional. The name of the pipeline artifact to publish the SARIF result file to. Default: CodeAnalysisLogs*.
    ```

    Note

    The artifactName 'CodeAnalysisLogs' is required for integration with Defender for Cloud. For additional tool configuration options and environment variables, see the [Microsoft Security DevOps wiki](https://github.com/microsoft/security-devops-action/wiki).
8. Select **Save and run** to commit and run the pipeline.

    Note

    Install the SARIF SAST Scans Tab extension to automatically display SARIF analysis results in the pipeline’s **Scans** tab.

## Uploading findings from third-party security tools into Defender for Cloud

Defender for Cloud can ingest SARIF results from other security tools for code-to-cloud visibility. To upload these results, ensure your Azure DevOps repositories are [onboarded to Defender for Cloud](quickstart-onboard-devops). After onboarding, Defender for Cloud continuously monitors the `CodeAnalysisLogs` artifact for SARIF output.

Use the `PublishBuildArtifacts@1` task to publish SARIF files to the `CodeAnalysisLogs` artifact. The following YAML step publishes the SARIF results file as a build artifact so that Defender for Cloud can ingest the findings:

```yml
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: 'results.sarif'
    ArtifactName: 'CodeAnalysisLogs'
```

Defender for Cloud displays these findings under the *Azure DevOps repositories should have code scanning findings resolved* assessment for the affected repository.