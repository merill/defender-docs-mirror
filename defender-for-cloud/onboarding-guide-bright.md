---
layout: Conceptual
title: Technical Onboarding Guide for Bright Security (preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/onboarding-guide-bright
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
description: Learn how to use Bright Security with Microsoft Defender for Cloud to enhance your application security testing.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 21d20a1e-0cc7-c840-38b3-e82f4897e977
document_version_independent_id: abfd415d-a3c5-9357-8e4a-c75533724752
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/onboarding-guide-bright.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/onboarding-guide-bright
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/onboarding-guide-bright.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 8e72fc4a-7aff-364c-8561-c3a3cd49039c
---

# Technical Onboarding Guide for Bright Security (preview) - Microsoft Defender for Cloud | Microsoft Learn

Bright provides a developer-centric enterprise Dynamic Application Security Testing (DAST) solution. It scans applications and APIs from the outside-in, mimicking how a hacker would approach the application, and tests for vulnerabilities that bad actors could use to exploit.

Unlike legacy DAST tools designed for expert security users after the application is already in production, Bright's tool is built to be *developer-first*. It is designed to empower developers to create more secure applications and APIs starting in early development phases and for all stages leading up to and including production so that vulnerabilities are caught and remediated as early as possible.

Scans can start as early as the Unit Testing phase in the software development lifecycle and progress from there to find as many vulnerabilities as possible early in the development lifecycle. Remediating vulnerabilities early saves significant developer time and reduces risk.

The solution is both developer and AppSec friendly. The solution has unique capabilities, including quick setup, minimal false positives, developer focused remediation suggestions, the ability to run the solution from a UI, or CLI, and seamless integration with the developer toolchain.

## Security testing approach

Bright API security validation is based on three main phases:

- Map the API attack surface.

    Bright can parse and learn the exact valid structure of REST and GraphQL APIs, from an OAS file (swagger) or an Introspection (GraphQL schema description). In addition, Bright can learn API content from HAR files. These methods provide a comprehensive way to visualize the attack surface.
- Conduct an attack simulation on the discovered APIs.

    After the baseline of the API behavior is known, Bright manipulates the requests (payloads, endpoint parameters, and so on) and automatically analyzes the response, verifying the correct response code and the content of the response payload to ensure no vulnerability exists. The attack simulations include OWASP API top 10, NIST, business logic tests, and more.
- Bright provides a clear indication of any found vulnerability.

    Indications include screenshots to ease the triage, investigation of the issue and suggestions on how to remediate that vulnerability.

## Purchase Bright Security from Azure Marketplace

You can purchase Bright Security solutions through Azure Marketplace. For more information, see the [Bright Security DAST listing on Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/brightsec.bright-dast?tab=Overview).

## Connect your DevOps environments to Microsoft Defender for Cloud

To use the Bright Security integration, connect your DevOps environment to Defender for Cloud. Follow the onboarding guide for your environment to connect your DevOps organization before you configure the Bright Security scan:

- [Onboard your GitHub organizations](quickstart-onboard-github)
- [Onboard your Azure DevOps organizations](quickstart-onboard-devops)

## Configure Bright Security API security testing scan

### Configure Bright Security scans for GitHub environments

Note

For more information on how to configure Bright Security for GitHub Actions along with links to sample GitHub Action workflows, see [GitHub Actions](https://docs.brightsec.com/docs/github-actions).

This workflow assumes you have GitHub Code Scanning enabled. If enabled, ensure the **upload-to-code-scanning** option is set to **true**. If you don't have GitHub Code Scanning enabled, set **upload-to-code-scanning** to **false** and use the steps in Enable Defender for Cloud integration without GitHub Code Scanning.

Install the Bright Security plugin within your CI/CD pipeline by completing the following step:

1. Sign in to GitHub.
2. Select a repository you want to configure the GitHub action to.
3. Select **Actions**.
4. Select **New Workflow**.
5. Filter by searching for *NeuraLegion*.
6. Select **Configure** for the NeuraLegion workflow.
7. If the APIs to be tested are in an internal environment that requires authentication, create an authentication object following the instructions in [Creating authentication](https://docs.brightsec.com/docs/creating-authentication).
8. Define a discovery of the APIs to be tested following the instructions in [Discovery](https://docs.brightsec.com/docs/discovery).
9. Run the attack simulation by following the instructions in [Creating a modern scan](https://docs.brightsec.com/docs/creating-a-modern-scan).
10. Select **Commit changes**. You can either directly commit to the main branch or create a pull request. We recommend following GitHub best practices by creating a PR, because the default workflow launches when a PR is opened against the main branch.
11. Select **Actions** and verify the new action is running.
12. After the workflow completes, select **Security**, then select **Code scanning** to view the results.
13. Select a Code Scanning alert detected by Neuralegion. You can also filter by tool in the Code scanning tab. Filter on *Neuralegion*.

The Bright Security (NeuraLegion GitHub workflow) scan results should now appear in GitHub Code Scanning. Next, verify that the Bright Security GitHub scan results are available within Defender for Cloud. It might take up to 30 minutes for results to show in Defender for Cloud.

#### Enable Defender for Cloud integration without GitHub Code Scanning

If you don't have GitHub Code Scanning for your environment and want to integrate security scan results from Bright Security into Defender for Cloud, use the following GitHub workflow steps to send scan results directly to Defender for Cloud. After you add the Bright Security scan step (NeuraLegion workflow) to your GitHub workflow, add the following steps to send scan results directly to Defender for Cloud using the Microsoft Security DevOps GitHub Action.

```yml
      - name: Download SARIF file
        id: sarif
        env:
          api_token: ${{ secrets.BRIGHT_TOKEN }}
          scanId: ${{ steps.start.outputs.id }}
        run: |
          curl -X GET "https://app.brightsec.com/api/v1/scans/$scanId/reports/sarif" -H "Authorization: Api-Key $api_token" -o bright.sarif.gz
          gzip -d bright.sarif.gz
      - name: Upload SARIF file
        uses: actions/upload-artifact@v4
        with: 
          name: BrightSecurity_Report_${{ github.run_id }}
          path: bright.sarif
      - name: Upload results to MSDO
        uses: microsoft/security-devops-action@v1
        id: msdo
        with:
          existingFilename: bright.sarif
```

Next, add the required permission to the workflow by setting **id-token** to `write`. For more information, see [OpenID Connect](https://docs.github.com/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect).

After you run the workflow, it might take up to 30 minutes for the results to show in Defender for Cloud.

#### Navigate to Defender for Cloud

To verify that Bright Security scan findings appear in Defender for Cloud, perform the following steps:

1. Select **Recommendations**.
2. Filter by searching for **API security testing**.
3. Select the recommendation **GitHub repositories should have API security testing findings resolved**.

[![Screenshot of GitHub repositories should have API security testing findings resolved recommendation.](media/onboarding-guide-stackhawk/github-recommendations-result.png)](media/onboarding-guide-stackhawk/github-recommendations-result.png#lightbox)

### Configure Bright Security scans for Azure DevOps environments

Note

For more information about configuring Bright Security for Azure DevOps, along with links to sample Azure DevOps Workflows, see [Azure Pipelines](https://docs.brightsec.com/docs/azure-pipelines).

1. Install the [NexPloit DevOps Integration](https://marketplace.visualstudio.com/items?itemName=Neuralegion.nexploit) on your Azure DevOps organization.
2. Create a new pipeline in your Azure DevOps project. For a tutorial, see [Create your first pipeline](/en-us/azure/devops/pipelines/create-first-pipeline).
3. Edit the created pipeline. Follow the steps in [Azure DevOps Integration](https://docs.brightsec.com/docs/azure-devops-integration).
4. Run the pipeline.
5. To verify the results are published correctly in Azure DevOps, check that *NeuraLegion\_ScanReport.SARIF* is uploaded to the build artifacts under the *CodeAnalysisLogs* folder.

    [![Screenshot of NeuraLegion_ScanReport.SARIF uploaded to Build Artifacts.](media/onboarding-guide-bright/artifacts-uploaded.png)](media/onboarding-guide-bright/artifacts-uploaded.png#lightbox)

You completed the onboarding process. Next, verify the results show in Defender for Cloud.

**Navigate to Defender for Cloud**:

1. Select **Recommendations**.
2. Filter by searching for **API security testing**.
3. Select the recommendation **Azure DevOps repositories should have API security testing findings resolved**.

[![Screenshot of Azure DevOps repositories should have API security testing findings resolved recommendation.](media/onboarding-guide-42crunch/azure-devops-recommendation.png)](media/onboarding-guide-42crunch/azure-devops-recommendation.png#lightbox)