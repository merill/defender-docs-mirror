---
layout: Conceptual
title: Configure the Microsoft Security DevOps GitHub Action - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/github-action
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
description: Configure the Microsoft Security DevOps GitHub action to run static analysis and security tools in your GitHub workflow.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 64852c0f-326f-70b3-26cf-58c898742d0c
document_version_independent_id: 0cd3375e-d594-7109-0c9c-4e848eed1605
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/github-action.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/github-action
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/github-action.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 12b09b48-360d-27a6-e65d-beb21fa31bd7
---

# Configure the Microsoft Security DevOps GitHub Action - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Security DevOps is a command-line application that integrates static analysis tools into the development lifecycle. Security DevOps installs, configures, and runs the latest versions of static analysis tools such as SDL, security, and compliance tools. Security DevOps is data-driven with portable configurations that enable deterministic execution across multiple environments.

Microsoft Security DevOps uses the following open-source tools:

| Name | Language | License |
| --- | --- | --- |
| [AntiMalware](https://www.microsoft.com/windows/comprehensive-security) | Anti-malware protection in Windows from Microsoft Defender for Endpoint that scans for malware and breaks the build if malware is found. This tool scans by default on windows-latest agent. | Not Open Source |
| [Bandit](https://github.com/PyCQA/bandit) | Python | [Apache License 2.0](https://github.com/PyCQA/bandit/blob/master/LICENSE) |
| [BinSkim](https://github.com/Microsoft/binskim) | Binary--Windows, ELF | [MIT License](https://github.com/microsoft/binskim/blob/main/LICENSE) |
| [Checkov](https://github.com/bridgecrewio/checkov) | Terraform, Terraform plan, CloudFormation, Amazon Web Services (AWS) SAM, Kubernetes, Helm charts, Kustomize, Dockerfile, Serverless, Bicep, OpenAPI, ARM | [Apache License 2.0](https://github.com/bridgecrewio/checkov/blob/main/LICENSE) |
| [ESlint](https://github.com/eslint/eslint) | JavaScript | [MIT License](https://github.com/eslint/eslint/blob/main/LICENSE) |
| [Template Analyzer](https://github.com/Azure/template-analyzer) | ARM Template, Bicep | [MIT License](https://github.com/Azure/template-analyzer/blob/main/LICENSE.txt) |
| [Terrascan](https://github.com/accurics/terrascan) | Terraform (HCL2), Kubernetes (JSON/YAML), Helm v3, Kustomize, Dockerfiles, CloudFormation | [Apache License 2.0](https://github.com/accurics/terrascan/blob/master/LICENSE) |
| [Trivy](https://github.com/aquasecurity/trivy) | container images, Infrastructure as Code (IaC) | [Apache License 2.0](https://github.com/aquasecurity/trivy/blob/main/LICENSE) |

## Prerequisites

Before you configure the Microsoft Security DevOps GitHub action, make sure you have the following prerequisites:

- An Azure subscription. If you don't have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- [Connect your GitHub repositories](quickstart-onboard-github).
- Open the [Microsoft Security DevOps GitHub action](https://github.com/marketplace/actions/security-devops-action) in a new window.
- Ensure that [Workflow permissions are set to Read and Write](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#setting-the-permissions-of-the-github_token-for-your-repository) on the GitHub repository. This step includes setting the `ID-token: write` permission in the GitHub workflow for federation with Microsoft Defender for Cloud.

## Set up the GitHub action workflow

To set up the GitHub action:

1. Sign in to [GitHub](https://www.github.com).
2. Select a repository you want to configure the GitHub action to.
3. Select **Actions**.

    ![Screenshot that shows you where the Actions button is located.](media/msdo-github-action/actions.png)
4. Select **New workflow**.
5. On **Get started with GitHub Actions**, select **set up a workflow yourself**.

    ![Screenshot showing where to select the new workflow button.](media/msdo-github-action/new-workflow.png)
6. Enter a name for your workflow file. For example, *msdevopssec.yml*.

    ![Screenshot that shows you where to enter a name for your new workflow.](media/msdo-github-action/devops.png)
7. Copy and paste the following [sample action workflow](https://github.com/microsoft/security-devops-action/blob/main/.github/workflows/sample-workflow.yml) into the **Edit new file** tab.

    ```yml
    name: MSDO
    on:
      push:
        branches:
          - main
    
    jobs:
      sample:
        name: Microsoft Security DevOps
    
        # Windows and Linux agents are supported
        runs-on: windows-latest
    
        permissions:
          contents: read
          id-token: write
          actions: read
          # Write access for security-events is only required for customers looking for MSDO results to appear in the codeQL security alerts tab on GitHub (Requires GHAS)
          security-events: write
    
        steps:
    
          # Checkout your code repository to scan
        - uses: actions/checkout@v3
    
          # Run analyzers
        - name: Run Microsoft Security DevOps
          uses: microsoft/security-devops-action@latest
          id: msdo
        # with:
          # config: string. Optional. A file path to an MSDO configuration file ('*.gdnconfig').
          # policy: 'GitHub' | 'microsoft' | 'none'. Optional. The name of a well-known Microsoft policy. If no configuration file or list of tools is provided, the policy may instruct MSDO which tools to run. Default: GitHub.
          # categories: string. Optional. A comma-separated list of analyzer categories to run. Values: 'code', 'artifacts', 'IaC', 'containers'. Example: 'IaC, containers'. Defaults to all.
          # languages: string. Optional. A comma-separated list of languages to analyze. Example: 'javascript,typescript'. Defaults to all.
          # tools: string. Optional. A comma-separated list of analyzer tools to run. Values: 'bandit', 'binskim', 'checkov', 'eslint', 'templateanalyzer', 'terrascan', 'trivy'.
    
          # Upload alerts to the Security tab - required for MSDO results to appear in the codeQL security alerts tab on GitHub (Requires GHAS)
        # - name: Upload alerts to Security tab
        #  uses: github/codeql-action/upload-sarif@v3
        #  with:
        #    sarif_file: ${{ steps.msdo.outputs.sarifFile }}
    
          # Upload alerts file as a workflow artifact - required for MSDO results to appear in the codeQL security alerts tab on GitHub (Requires GHAS)
        # - name: Upload alerts file as a workflow artifact
        #  uses: actions/upload-artifact@v3
        #  with:  
        #    name: alerts
        #    path: ${{ steps.msdo.outputs.sarifFile }}
    ```

    Note

    For more tool configuration options and instructions, see [the Microsoft Security DevOps wiki](https://github.com/microsoft/security-devops-action/wiki).
8. Select **Start commit**.

    [![Screenshot showing you where to select start commit.](media/msdo-github-action/start-commit.png)](media/msdo-github-action/start-commit.png#lightbox)
9. Select **Commit new file**. The process can take up to one minute to complete.

    ![Screenshot showing you how to commit a new file.](media/msdo-github-action/commit-new.png)
10. Select **Actions** and verify the new action is running.

    [![Screenshot showing you where to navigate to, to see that your new action is running.](media/msdo-github-action/verify-actions.png)](media/msdo-github-action/verify-actions.png#lightbox)

## View scan results

**To view your scan results**:

1. Sign in to Azure.
2. Go to **Defender for Cloud** &gt; **DevOps Security**.
3. From the DevOps security pane, you can see the same Microsoft Security DevOps (MSDO) security results. Developers see these results in their CI logs for the associated repository in minutes. Customers with GitHub Advanced Security also see the findings ingested from these tools.