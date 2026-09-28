---
layout: Conceptual
title: Technical Onboarding Guide for StackHawk (preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/onboarding-guide-stackhawk
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
description: Learn how to use StackHawk with Microsoft Defender for Cloud to enhance your application security testing.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ff95268e-45a9-629d-3ef7-0b0c0da860c0
document_version_independent_id: 842fcb47-b242-33aa-a3c1-efa80548863a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/onboarding-guide-stackhawk.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/onboarding-guide-stackhawk
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/onboarding-guide-stackhawk.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: ddcd424c-7ef2-56aa-ad91-437b69aad2a1
---

# Technical Onboarding Guide for StackHawk (preview) - Microsoft Defender for Cloud | Microsoft Learn

StackHawk makes API and application security testing part of software delivery. The StackHawk platform offers engineering teams the ability to find and fix application bugs at any stage of software development and gives Security teams insight into the security posture of applications and APIs being developed.

## Security testing approach

StackHawk is a modern Dynamic Application Security Testing (DAST) and API security testing tool that runs in CI/CD. It enables developers to quickly find and fix security issues before they hit production.

StackHawk's modern DAST approach with an emphasis on shifting security left changes the way organizations develop and test applications today. An essential next step to helping security teams shift left is understanding what APIs they have, where they live, and who they belong to.

StackHawk incorporates generative AI technology into its tool for discovering security issues with code in GitHub repositories. It can identify hidden APIs within source code and describe associated problems via natural language responses.

## Enablement

Microsoft customers looking to prioritize application security now have a seamless path with StackHawk. The StackHawk platform is intricately woven into the Microsoft ecosystem, allowing developers to explore multiple paths tailored to their needs, whether orchestrating workflows through GitHub Actions or Azure DevOps. After Microsoft Defender for API is mapped to a GitHub or ADO repo, developers can turn on SARIF to take advantage of StackHawk's advanced security tooling.

Developers can [activate a free trial of StackHawk](https://auth.stackhawk.com/signup) and run a Hawkscan, and explore multiple paths tailored to their needs, whether orchestrating workflows through GitHub Actions or Azure DevOps.

## Connect your DevOps environments to Microsoft Defender for Cloud

StackHawk integration with Defender for Cloud requires connecting your DevOps environment to Defender for Cloud.

- See [Onboard GitHub organizations](quickstart-onboard-github).
- See [Onboard Azure DevOps organizations](quickstart-onboard-devops).

## Configure StackHawk API security testing scan

### Configure StackHawk scans for GitHub Actions CI/CD environments

Note

This workflow assumes you have GitHub Code Scanning enabled. If enabled, ensure the **upload-to-code-scanning** option is set to **true**. If you don't have GitHub Code Scanning enabled, set **upload-to-code-scanning** to **false** and use the steps in Enable Defender for Cloud integration without GitHub Code Scanning.

To use the [StackHawk HawkScan Action](https://github.com/marketplace/actions/stackhawk-hawkscan-action), sign in to [GitHub](https://github.com/login). You must have a [StackHawk account](http://auth.stackhawk.com/signup).

From GitHub, you can use a GitHub repository with a defined GitHub Actions workflow process already in place, or create a new workflow. The product scans this GitHub repository for API vulnerabilities as part of the GitHub Actions workflow.

Note

You should select to scan a GitHub repository that corresponds to a dynamic web API. This can be a REST, GraphQL, or gRPC API. HawkScan works better with a discoverable API specification file like an [OpenAPI specification](https://docs.stackhawk.com/hawkscan/configuration/openapi-configuration.html), and with [authenticated scanning](https://docs.stackhawk.com/hawkscan/authenticated-scanning/). StackHawk provides [JavaSpringVulny](https://github.com/kaakaww/javaspringvulny/) as an example vulnerable API you can fork and try, if you don't have your own vulnerable web API to scan.

1. From StackHawk, make sure you collected your API Key and have a StackHawk Application created, and the *stackhawk.yml* scan configuration checked into your GitHub repository.
2. Go to [StackHawk HawkScan Action](https://github.com/marketplace/actions/stackhawk-hawkscan-action) to view the details of the StackHawk HawkScan Action for GitHub Actions CI/CD. From your repository */settings/secrets/actions* page, assign your StackHawk API Key to `HAWK_API_KEY`. Then to add it to your GitHub actions workflow, add the following step to your build:

    ```yml
    # Make sure your app.host web application is started and accessible before you scan.
    #  - name: Start Web Application
    #     run: docker run --rm --detach --publish 8080:80 --name my_web_app nginx
       - name: API Scan with StackHawk
          uses: stackhawk/hawkscan-action@v2.1.3
          with:
          apiKey: ${{ secrets.HAWK_API_KEY }}
          env:
             SARIF_ARTIFACT: true
    ```

    The `stackhawk/hawkscan-action` step starts HawkScan on the runner pointed at the *app.host* defined in the *stackhawk.yml*. Be sure to include `with.env.SARIF_ARTIFACT: true` to get the SARIF output from the scan. The HawkScan action has documented configuration inputs, and the sample workflow at [sample HawkScan GitHub Actions workflow (hawkscan.yml)](https://github.com/kaakaww/javaspringvulny/blob/main/.github/workflows/hawkscan.yml#L21-L32) shows the HawkScan action in use.
3. You can also follow these steps to add *stackhawk/hawkscan-action* to a new workflow action:

    1. Sign in to GitHub.
    2. Select a GitHub repository you want to configure the GitHub action to.
    3. Select **Actions**.
    4. Select **New Workflow**.
    5. Filter by searching for *StackHawk HawkScan*.
    6. Select **Configure** for the *StackHawk* workflow.
    7. Modify the sample workflow in the editor. See [StackHawk GitHub Actions](https://docs.stackhawk.com/continuous-integration/github-actions/).
    8. Select **Commit changes**. You can either directly commit to the main branch or create a pull request. We recommend following GitHub best practices by creating a PR, because the default workflow launches when a PR is opened against the main branch.
    9. Select **Actions** and verify the new action is running.
    10. After the workflow is completed, select **Security**, then select **Code scanning** to view the results.
    11. Select a Code Scanning alert detected by StackHawk. You can also filter by tool in the Code scanning tab. Filter on **StackHawk**.

You now verified that the StackHawk security scan results are showing in GitHub Code Scanning. Next, verify that these scan results are available within Defender for Cloud. It might take up to 30 minutes for results to show in Defender for Cloud.

#### Enable Defender for Cloud integration without GitHub Code Scanning

If you don't have GitHub Code Scanning for your environment and want to integrate security scan results from StackHawk into Defender for Cloud, you can follow these steps. After adding in the StackHawk workflow step, add the following steps to your GitHub workflow to send scan results directly to Defender for Cloud using the Microsoft Security DevOps GitHub Action.

```yml
- name: Upload SARIF file
        uses: actions/upload-artifact@v4
        with:
          name: StackHawk_Report_${{ github.run_id }}
          path: stackhawk.sarif
          if-no-files-found: error
- name: Upload results to MSDO
        uses: microsoft/security-devops-action@v1
        id: msdo
        with:
          existingFilename: stackhawk.sarif
```

Next, add the required permission to the workflow by setting **id-token** to `write`. For more information, see [OpenID Connect](https://docs.github.com/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect).

After you run the workflow, it might take up to 30 minutes for the results to show in Defender for Cloud.

#### Navigate to Defender for Cloud

To view the imported StackHawk findings in Defender for Cloud, follow these steps:

1. Select **Recommendations**.
2. Filter by searching for **API security testing**.
3. Select the recommendation **GitHub repositories should have API security testing findings resolved**.

[![Screenshot of GitHub repositories should have API security testing findings resolved recommendation.](media/onboarding-guide-stackhawk/github-recommendations-result.png)](media/onboarding-guide-stackhawk/github-recommendations-result.png#lightbox)

### Configure StackHawk scans for Azure Pipelines environments

To use the [StackHawk HawkScan extension](https://marketplace.visualstudio.com/items?itemName=StackHawk.stackhawk-extensions), sign in to Azure Pipelines (`https://dev.azure.com/{yourorganization}`). You must have a [StackHawk account](http://auth.stackhawk.com/signup).

From Azure Pipelines, you can use a defined pipeline with a defined *azure-pipelines.yml* process already in place, or create a new workflow. The product scans this Azure DevOps repository for API vulnerabilities as part of the *azure-pipelines.yml* workflow.

[![Screenshot of tasks to install and run HawkScan.](media/onboarding-guide-stackhawk/hawkscan-tasks.png)](media/onboarding-guide-stackhawk/hawkscan-tasks.png#lightbox)

1. After you add the HawkScan extension to your Azure DevOps Organization, you can use the `HawkScanInstall` task and the `RunHawkScan` task to add HawkScan to your runner and start HawkScan as separate steps.

    ```yml
    - task: HawkScanInstall@1.2.8
       inputs:
       version: "3.7.0"
       installerType: "msi"
    
    # start your web application in the background
    # - script: |
    #    curl -Ls https://GitHub.com/kaakaww/javaspringvulny/releases/download/0.2.0/java-spring-vuly-0.2.0.jar -o ./java-spring-vuly-0.2.0.jar
    #    java -jar ./java-spring-vuly-0.2.0.jar &

    - task: RunHawkScan@1.2.8
       inputs:
       configFile: "stackhawk.yml"
       version: "3.7.0"
       env:
       HAWK_API_KEY: $(HAWK_API_KEY) # use variables in the azure devops ui to configure secrets and env vars
       APP_ENV: $(imageName)
       APP_ID: $(appId)
       SARIF_ARTIFACT: true
    ```

    These tasks install HawkScan on the runner and run it against the *app.host* defined in *stackhawk.yml*. Be sure to include `env.SARIF_ARTIFACT: true` on the task specification to get the SARIF output from the scan. The HawkScan action has documented configuration inputs, and the sample pipeline at [sample Azure Pipelines YAML file (azure-pipelines.yml)](https://github.com/kaakaww/javaspringvulny/blob/main/azure-pipelines.yml) shows the HawkScan tasks in use.
2. Install the [HawkScan Azure DevOps extension](https://marketplace.visualstudio.com/items?itemName=StackHawk.stackhawk-extensions) on your Azure DevOps organization.

    1. Visit the StackHawk website and [sign up for a free StackHawk trial](https://auth.stackhawk.com/signup).
    2. For Windows developers, reference this [sample app for building software on Windows](https://github.com/kaakaww/javaspringvulny/blob/main/azure-pipelines.yml).
    3. Review the [HawkScan and Azure Pipelines documentation](https://docs.stackhawk.com/continuous-integration/azure/azure-pipelines.html).
3. Create a new pipeline or clone [StackHawk's sample app](https://github.com/kaakaww/javaspringvulny/blob/main/ci-examples/azure-devops/azure-pipelines.yml) in your Azure DevOps project. For a tutorial, see [Create your first pipeline](/en-us/azure/devops/pipelines/create-first-pipeline).
4. Run the pipeline.
5. To verify that the results are published correctly in Azure DevOps, check that *stackhawk.sarif* is uploaded to the Build Artifacts under the *CodeAnalysisLogs* folder.

    [![Screenshot of stackhawk.sarif uploaded to Build Artifacts.](media/onboarding-guide-stackhawk/artifacts-upload.png)](media/onboarding-guide-stackhawk/artifacts-upload.png#lightbox)

You completed the onboarding process. Next, verify the results shown in Defender for Cloud.

**Navigate to Defender for Cloud**:

1. Select **Recommendations**.
2. Filter by searching for **API security testing**.
3. Select the recommendation **Azure DevOps repositories should have API security testing findings resolved**.

[![Screenshot of Azure DevOps repositories should have API security testing findings resolved recommendation.](media/onboarding-guide-42crunch/azure-devops-recommendation.png)](media/onboarding-guide-42crunch/azure-devops-recommendation.png#lightbox)

## FAQ

The following answers address common questions about StackHawk.

### How is StackHawk licensed?

StackHawk licenses the platform based on the number of code contributors you provision. For custom pricing, EULA, or a private contract, contact [Marketplace Orders](mailto:marketplace-orders@stackhawk.com).