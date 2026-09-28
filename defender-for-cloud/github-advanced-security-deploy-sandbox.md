---
layout: Conceptual
title: Deploy GitHub Advanced Security Integration with Microsoft Defender for Cloud (Sandbox project) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/github-advanced-security-deploy-sandbox
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
description: Set up and validate a sandbox environment to evaluate GitHub Advanced Security and Microsoft Defender for Cloud integration end to end.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 9fc93e4a-9901-df07-cf05-ed37e4511990
document_version_independent_id: c58a33bc-0d55-a3e7-e207-088c5f653f9b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/github-advanced-security-deploy-sandbox.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/github-advanced-security-deploy-sandbox
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/github-advanced-security-deploy-sandbox.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 508bede2-2857-4bc5-ca20-3f2bc393d3c1
---

# Deploy GitHub Advanced Security Integration with Microsoft Defender for Cloud (Sandbox project) - Microsoft Defender for Cloud | Microsoft Learn

This guide provides setup steps for a sandbox project that helps you evaluate GitHub Advanced Security (GHAS) and Microsoft Defender for Cloud integration end to end with a simple use case.

The GHAS and Defender for Cloud integration helps maximize Microsoft's cloud-native application security by correlating runtime risks and context with the originated code for faster AI-powered remediation.

By following this guide, you:

- Set up your GitHub repository for Defender for Cloud coverage.
- Create a runtime risk factor.
- Link code to runtime resources.
- Test real use cases in Defender for Cloud.

## Prerequisites

| **Aspect** | **Details** |
| --- | --- |
| Environmental requirements | - GitHub account with a connector created in Defender for Cloud- GHAS license- Defender Cloud Security Posture Management (DCSPM) enabled on the subscription- Microsoft Security Copilot (optional for automated remediation) |
| Roles and permissions | - Security Admin permissions- Security Admin on the Azure subscription (to view findings in Defender for Cloud)- GitHub organization owner |
| Cloud environments | Available in commercial clouds only (not in Azure Government, Azure operated by 21Vianet, or other sovereign clouds). |

## Prepare your environment

### Step 1: Set up the GitHub repository and run the workflow

To test the integration, use the Sandbox example GitHub repository that already has all the contents to build a vulnerable container image.

Before you set up a repository:

- Define a connector for the GitHub organization that you plan to use in the Defender for Cloud portal. Follow the steps in [Connect your GitHub environment to Microsoft Defender for Cloud](quickstart-onboard-github).
- Configure agentless code scanning for your GitHub connector. Follow the steps in [Configure agentless code scanning (preview)](agentless-code-scanning).
- Use a private repository for the integration.

1. Clone the following repository to your GitHub organization:

    - [mdc-customer-playbook](https://github.com/build25-woodgrove/mdc-customer-playbook)

    This repo has GHAS enabled and is onboarded to an Azure tenant that has Defender Cloud Security Posture Management enabled.
2. In the repository, follow these steps:

    1. Go to **Settings**.
    2. On the left pane, select **Secrets and variables** &gt; **Actions**. Then select **New repository secret**.
    3. Add the following secrets at the repository or organization level:

    | **Variable** | **Description** |
    | --- | --- |
    | ACR\_ENDPOINT | The authentication server of the container registry. |
    | ACR\_USERNAME | The username for the container registry. |
    | ACR\_PASSWORD | The password for the container registry. |

    Note

    You can choose any names for these variables. They don't need to follow a specific pattern.

You can find the container registry authentication server, username, and password in the Azure portal by following these steps:

1. Select the container registry that you want to deploy to.
2. Under **Settings**, select **Access keys**.
3. The **Access keys** pane shows the keys for the authentication server, username, and password.

In your repository, select **Actions**, select the **Build and Push to ACR** workflow, and then select **Run workflow**.

Check that the image was deployed to your container registry. For the example repository, the image should be in a registry called `mdc-mock-0001` with the tag `mdc-ghas-integration`.

Deploy the `mdc-mock-0001:mdc-ghas-integration` image as a running container on your cluster. One way to deploy the container image to your cluster is by connecting to the cluster and using the `kubectl run` command. Here's an example for Azure Kubernetes Service (AKS):

1. Set the cluster subscription:

    ```azurecli
    az account set --subscription $subscriptionID
    ```
2. Set the credentials for the cluster:

    ```azurecli
    az aks get-credentials --resource-group $resourceGroupName --name $kubernetesClusterName --overwrite-existing
    ```
3. Deploy the image:

    ```azurecli
    kubectl run $containerName --image=$registryName.azurecr.io/mdc-mock-0001:mdc-ghas-integration
    ```

### Step 2: Create the example risk factor (business-critical rule)

One of the risk factors that Defender for Cloud detects for this integration is business criticality. Organizations can create rules to label resources as business critical.

1. In the Defender for Cloud portal, go to **Environment settings** &gt; **Resource criticality**.
2. On the right pane, select the link to open Microsoft Defender.
3. Select **Create a new classification**.
4. Enter a name and description.
5. In the query builder, select **Cloud resource**. Write a query to set **Resource Name** equal to the name of the container that you deployed to your cluster for validation. Then select **Next**.
6. On the **Preview Assets** page, if Microsoft Defender already detected your resource, the name of the container appears with an asset type of **K8s-container** or **K8s-pod**. Even if the name isn't yet visible, continue with the next step.
7. Choose a criticality level, and then review and submit your classification rule.

Note

Defender applies the criticality label to the container after it detects the container. This process can take up to 24 hours.

### Step 3: Validate that your environment is ready

Validation confirms that your environment is correctly configured to surface code-to-runtime recommendations and generate actionable results.

During validation, Defender verifies full code-to-runtime visibility.

- Defender for Cloud continuously monitors source code repositories for security vulnerabilities.
- Build artifacts, such as container images, are scanned in container registries before deployment.
- Runtime workloads deployed to Kubernetes clusters are monitored for security risks.
- Defender for Cloud correlates and traces each artifact from code, through build and deployment, to runtime, and back.

Note

It can take up to 24 hours after the previous steps are applied to see the following results.

Test that GitHub agentless scanning picks up the repository.

Go to Cloud Security Explorer and run the validation queries described in the following list. These validation queries test whether Defender for Cloud can identify artifacts produced by your pipelines and workloads. If the queries return results, it indicates that scanning and correlation are working as expected.

Note

If no results are returned, it might indicate that artifacts aren't yet generated, scanning isn't configured, or permissions are missing.

- Validate that Defender for Cloud in Azure Container Registry scanned the container image and used it to create a container.
- In your query, add the conditions for your specific deployment.
- Validate that the container is running and that Defender for Cloud scanned the AKS cluster.
- Validate that the risk factors are configured correctly on the Defender for Cloud side. Search for your container name on the Defender for Cloud inventory page, and you should see it marked as critical.

Note

Validating the risk factor configuration is required only if risk factors aren't already configured in your environment.

Successful validation ensures that subsequent steps, such as recommendations, campaigns, and GitHub issue generation, produce meaningful results.