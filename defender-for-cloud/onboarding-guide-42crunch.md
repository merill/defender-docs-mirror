---
layout: Conceptual
title: Technical Onboarding Guide for 42Crunch (preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/onboarding-guide-42crunch
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
description: Onboard 42Crunch to Microsoft Defender for Cloud to integrate API security audit and scan findings into a centralized DevSecOps workflow (preview).
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: f730b207-a0d4-7717-268d-7cbea0af8f4f
document_version_independent_id: fd80c48d-ff12-f1e5-b50c-7204179c3b98
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/onboarding-guide-42crunch.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/onboarding-guide-42crunch
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/onboarding-guide-42crunch.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 5337edf2-3e8c-e9fd-c295-c5f81c4571eb
---

# Technical Onboarding Guide for 42Crunch (preview) - Microsoft Defender for Cloud | Microsoft Learn

42Crunch enables a standardized approach to securing APIs that automates the enforcement of API security compliance for distributed development and security teams. The 42Crunch API security platform empowers developers to build security from the integrated development environment (IDE) into the CI/CD pipeline. This seamless DevSecOps approach to API security reduces governance costs and accelerates the delivery of secure APIs.

## Security testing approach

Unlike traditional DAST tools that are used to scan web and mobile applications, 42Crunch runs a set of tests that are precisely crafted and targeted against each API based on their specific design. By using the OpenAPI definition (formerly known as Swagger) file as the primary source, the 42Crunch Scan engine runs a battery of tests that validate how closely the API conforms to the intended design. This *Conformance Scan* identifies various security issues including OWASP top 10 vulnerabilities, improper response codes, and schema violations. The scan reports these issues with rich context including possible exploit scenarios and remediation guidance.

Scans can run automatically as part of a CI/CD pipeline or manually through an IDE or the 42Crunch cloud platform.

Because the quality of the API specification largely determines the scan coverage and effectiveness, it's important to ensure that your OpenAPI specification is well-defined. 42Crunch Audit performs a static analysis of the OpenAPI specification file aimed at helping the developer to improve the security and quality of the specification. The Audit determines a composite security score from 0-100 for each specification file. As developers remediate security and semantic issues identified by the Audit, the score improves. 42Crunch recommends an [Audit score of at least 70 before running a Conformance scan](https://docs.42crunch.com/latest/content/concepts/data_dictionaries.htm).

## Enable 42Crunch in Microsoft Defender for Cloud

Note

The following steps walk through the process of setting up the free version of 42Crunch. See the FAQ section to learn about the differences between the free and paid versions of 42Crunch and how to purchase 42Crunch on Azure Marketplace.

By relying on the 42Crunch [Audit](https://42crunch.com/api-security-audit) and [Scan](https://42crunch.com/api-conformance-scan/) services, developers can proactively test and harden APIs within their CI/CD pipelines through static and dynamic testing of APIs against the top OWASP API risks and OpenAPI specification best practices.

The security scan results from 42Crunch are now available within Defender for Cloud, ensuring central security teams have visibility into the health of APIs within the Defender for Cloud recommendation experience, and can take governance steps natively available through Defender for Cloud recommendations.

## Connect your DevOps environments to Microsoft Defender for Cloud

Viewing 42Crunch scan results in Defender for Cloud requires connecting your DevOps environment to Defender for Cloud.

- See [how to onboard your GitHub organizations](quickstart-onboard-github).
- See [how to onboard your Azure DevOps organizations](quickstart-onboard-devops).

## Configure 42Crunch Audit service

The REST API Static Security Testing action locates REST API contracts that follow the OpenAPI Specification (OAS, formerly known as Swagger) and runs thorough security checks on them. The action supports both OAS v2 and v3, in both JSON and YAML formats.

The action uses [42Crunch API Security Audit](https://docs.42crunch.com/latest/content/concepts/api_contract_security_audit.htm). Security Audit performs a static analysis of the API definition that includes more than 300 checks on best practices and potential vulnerabilities. It checks how the API defines authentication, authorization, transport, and request/response schemas.

### Configure 42Crunch Audit for GitHub environments

Install the 42Crunch API Security Audit plugin within your CI/CD pipeline by completing the following steps:

1. Sign in to GitHub.
2. Select a repository you want to configure the GitHub action to.
3. Select **Actions**.
4. Select **New Workflow**.

    [![Screenshot showing new workflow selection.](media/onboarding-guide-42crunch/new-workflow.png)](media/onboarding-guide-42crunch/new-workflow.png#lightbox)

To create a new default workflow:

1. Choose **Setup a workflow yourself**.
2. Rename the workflow from `main.yaml` to `42crunch-audit.yml`.
3. Go to the [42Crunch REST API Static Security Testing full workflow example](https://github.com/marketplace/actions/42crunch-rest-api-static-security-testing-freemium#full-workflow-example).
4. Copy the full sample workflow and paste it in the workflow editor.

    Note

    This workflow assumes you have GitHub Code Scanning enabled. If enabled, ensure the **upload-to-code-scanning** option is set to **true**. If you don't have GitHub Code Scanning enabled, set **upload-to-code-scanning** to **false** and use the steps in Enable Defender for Cloud integration without GitHub Code Scanning.

    [![Screenshot showing GitHub workflow editor.](media/onboarding-guide-42crunch/workflow-editor.png)](media/onboarding-guide-42crunch/workflow-editor.png#lightbox)
5. Select **Commit changes**.

    You can either directly commit to the main branch or create a pull request. We recommend following GitHub best practices by creating a PR, because the default workflow launches when a PR is opened against the main branch.
6. Select **Actions** and verify the new action is running.

    [![Screenshot showing new action running.](media/onboarding-guide-42crunch/new-action.png)](media/onboarding-guide-42crunch/new-action.png#lightbox)
7. After the workflow completes, select **Security**, then select **Code scanning** to view the results.
8. Select a Code Scanning alert detected by 42Crunch REST API Static Security Testing. You can also filter by tool in the **Code scanning** tab. Filter on **42Crunch REST API Static Security Testing**.

    [![Screenshot showing code scanning alert.](media/onboarding-guide-42crunch/code-scanning-alert.png)](media/onboarding-guide-42crunch/code-scanning-alert.png#lightbox)

You verified that the Audit results are showing in GitHub Code Scanning. Next, verify that these Audit results are available within Defender for Cloud. It might take up to 30 minutes for results to show in Defender for Cloud.

#### Enable Defender for Cloud integration without GitHub Code Scanning

If you don't have GitHub Code Scanning for your environment and want to integrate security scan results from 42Crunch into Defender for Cloud, you can follow these steps. After adding the 42Crunch workflow step, add the following steps to your GitHub workflow to send scan results directly to Defender for Cloud using the Microsoft Security DevOps GitHub Action.

```yml
- name: save-sarif-report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: 42Crunch_AuditReport_${{ github.run_id }}
          path: 42Crunch_AuditReport_${{ github.run_id }}.SARIF
          if-no-files-found: error
- name: Upload results to MSDO
        uses: microsoft/security-devops-action@v1
        id: msdo
        with:
          existingFilename: 42Crunch_AuditReport_${{ github.run_id }}.SARIF
```

Next, add the required permission to the workflow by setting **id-token** to `write`. For more information, see [OpenID Connect](https://docs.github.com/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect).

After running the workflow, it might take up to 30 minutes for the results to show in Defender for Cloud.

#### Navigate to Defender for Cloud

To view the 42Crunch Audit findings in Defender for Cloud, complete the following steps:

1. Select **Recommendations**.
2. Select **All recommendations**.
3. Filter by searching for **API security testing**.
4. Select the recommendation **GitHub repositories should have API security testing findings resolved**.

The selected recommendation shows all 42Crunch Audit findings. You completed the onboarding for the 42Crunch Audit step.

[![Screenshot showing API summary.](media/onboarding-guide-42crunch/api-recommendations.png)](media/onboarding-guide-42crunch/api-recommendations.png#lightbox)

### Configure 42Crunch Audit for Azure DevOps environments

To configure 42Crunch Audit in Azure DevOps, complete the following steps:

1. Install the [42Crunch Azure DevOps extension](https://marketplace.visualstudio.com/items?itemName=42Crunch.42c-cicd-audit-freemium) on your organization.
2. Create a new pipeline in your Azure DevOps project. For a tutorial, see [Create your first pipeline](/en-us/azure/devops/pipelines/create-first-pipeline).
3. Edit the created pipeline, by copying in the following workflow:

    ```yml
    trigger:
    branches:
       include:
          - main
    
    jobs:
    - job: run_42crunch_audit
       displayName: 'Run Audit'
       pool:
          vmImage: 'ubuntu-latest'
       steps:
          - task: UsePythonVersion@0
          inputs:
             versionSpec: '3.11'
             addToPath: true
             architecture:  x64
          - task: APISecurityAuditFreemium@1
          inputs:
             enforceSQG: false
             sarifReport: '$(Build.Repository.LocalPath)/42Crunch_AuditReport.sarif'
             exportAsPDF: '$(Build.Repository.LocalPath)/42Crunch_AuditReport.pdf'
          - task: PublishBuildArtifacts@1
          displayName: publishAuditSarif
          inputs:
             PathtoPublish: '$(Build.Repository.LocalPath)/42Crunch_AuditReport.sarif '
             ArtifactName: 'CodeAnalysisLogs'
             publishLocation: 'Container'
    ```
4. Run the pipeline.
5. To verify that the results are published correctly in Azure DevOps, check that *42Crunch-AuditReport.sarif* is uploaded to the Build Artifacts under the *CodeAnalysisLogs* folder.

You completed the onboarding process. Next, verify that the results appear in Defender for Cloud.

1. Go to Defender for Cloud.
2. Select **Recommendations**.
3. Select **All recommendations**.
4. Filter by searching for **API security testing**.
5. Select the recommendation **AzureDevOps repositories should have API security testing findings resolved**.

The selected recommendation shows all 42Crunch Audit findings. You completed the onboarding for the 42Crunch Audit step.

[![Screenshot showing Azure DevOps recommendation.](media/onboarding-guide-42crunch/azure-devops-recommendation.png)](media/onboarding-guide-42crunch/azure-devops-recommendation.png#lightbox)

## Configure 42Crunch Scan service

API Scan continually scans the API to ensure conformance to the OpenAPI contract and detects vulnerabilities at testing time. It detects OWASP API Security Top 10 issues early in the API lifecycle and validates that your APIs can handle unexpected requests.

The scan requires a nonproduction live API endpoint, and the required credentials (API key/access token). To configure the 42Crunch Scan, see the [42Crunch API security tutorial](https://github.com/42Crunch/apisecurity-tutorial).

For the Azure DevOps-specific tasks, see the **azure-pipelines-scan.yaml** file in the [42Crunch API Security tutorial](https://github.com/42Crunch/apisecurity-tutorial).

## FAQ

### How does 42Crunch help developers identify and remediate API security issues?

The 42Crunch security Audit and Conformance scan identify potential vulnerabilities that exist in APIs early on in the development lifecycle. Scan results include rich context including a description of the vulnerability and associated exploit, and detailed remediation guidance. Scans can run automatically in the CI/CD platform or incrementally by the developer within their IDE through one of the [42Crunch IDE extensions](https://marketplace.visualstudio.com/items?itemName=42Crunch.vscode-openapi).

### Can 42Crunch be used to enforce compliance with minimum quality and security standards for developers?

Yes. 42Crunch includes the ability to enforce compliance using [Security Quality Gates (SQG)](https://docs.42crunch.com/latest/content/concepts/security_quality_gates.htm). SQGs are composed of certain criteria that must be met to successfully pass an Audit or Scan. For example, an SQG can ensure that an Audit or Scan with one or more critical severity issues doesn't pass. In CI/CD, the 42Crunch Audit or Scan can be configured to fail a build if it fails to pass an SQG, requiring a developer to resolve the underlying issue before pushing their code.

The free version of 42Crunch uses default SQGs for both Audit and Scan whereas the paid enterprise version allows for customization of SQGs and tags, which allow SQGs to be applied selectively to groupings of APIs.

### What data is stored within 42Crunch's SaaS service?

A limited free trial version of the 42Crunch security Audit and Conformance scan can be deployed in CI/CD, which generates reports locally without the need for a 42Crunch SaaS connection. In this version, there's no data shared with the 42Crunch platform.

For the full enterprise version of the 42Crunch platform, the following data is stored in the SaaS platform:

- First name, last name, and email addresses of users of the 42Crunch platform.
- OpenAPI/Swagger files (descriptions of customer APIs).
- Reports that are generated during the security Audit and Conformance scan tasks performed by 42Crunch.

### How is 42Crunch licensed?

42Crunch licensing is based on a combination of the number of APIs and the number of developers you provision on the platform. For example pricing bundles, see the [42Crunch Developer-First API Security Platform marketplace listing](https://azuremarketplace.microsoft.com/marketplace/apps/42crunch1580391915541.42crunch_developer_first_api_security_platform?tab=overview).

Custom pricing is available through private offers on the Azure Commercial marketplace. For a custom quote, contact [Sales](mailto:sales@42crunch.com).

### What's the difference between the free and paid version of 42Crunch?

42Crunch offers both a free limited version and a paid enterprise version of the security Audit and Conformance scan.

For the free version of 42Crunch, the 42Crunch CI/CD plugins work as a standalone, with no requirement to sign in to the 42Crunch platform. Audit and scanning results are then available in Defender for Cloud, and in the CI/CD platform. Audits and scans are limited to up to 25 executions per month each, per repo, with a maximum of three repositories.

For the paid enterprise version of 42Crunch, Audits and scans still run locally in CI/CD but can sync with the 42Crunch platform service, where you can use several advanced features including customizable security quality gates, data dictionaries, and tagging. While the enterprise version is licensed for a certain number of APIs, there are no limits to the number of Audits and scans that you can run on a monthly basis.

### Is 42Crunch available on the Azure commercial marketplace?

Yes, you can purchase 42Crunch on the [42Crunch Developer-First API Security Platform offer on Microsoft commercial marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/42crunch1580391915541.42crunch_developer_first_api_security_platform).

Purchases of 42Crunch through the Azure Commercial marketplace count toward your Minimum Azure Consumption Commitments (MACC).