---
layout: Conceptual
title: Support and prerequisites - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/devops-support
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
description: Understand support and prerequisites for DevOps security in Microsoft Defender for Cloud
ms.date: 2026-09-18T00:00:00.0000000Z
ms.topic: feature-availability
ms.custom: ignite-2023, references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 4d51b5a1-60e5-662d-acd1-0d81d9c44de8
document_version_independent_id: 8a319b95-d8fe-3ced-edca-c3275498669d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/devops-support.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/devops-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/devops-support.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 4e28ce08-65d3-a26e-b23a-41734a0519ef
---

# Support and prerequisites - Microsoft Defender for Cloud | Microsoft Learn

Use the following support information to plan DevOps security capabilities in Microsoft Defender for Cloud.

DevOps security provides visibility into your DevOps environments, helping security teams discover misconfigurations, exposed secrets, and code vulnerabilities in repositories and CI/CD pipelines in Azure DevOps, GitHub, and GitLab.

## Cloud and region support

DevOps security is available in the Azure commercial cloud, in these regions:

- Asia (East Asia)
- Australia (Australia East)
- Canada (Canada Central)
- Europe (West Europe, North Europe, Sweden Central)
- UK (UK South)
- US (East US, Central US)

## DevOps platform support

DevOps security currently supports the following DevOps platforms:

- [Azure DevOps Services](https://azure.microsoft.com/products/devops/)
- [GitHub Enterprise Cloud](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-enterprise-cloud)
- [GitLab SaaS](https://docs.gitlab.com/ee/subscriptions/gitlab_com/)

Note

Defender for DevOps currently doesn't support GitHub Enterprise Cloud instances configured with data residency.

## Required permissions

DevOps security requires the following permissions:

| Feature | Permissions |
| --- | --- |
| Connect DevOps environments to Defender for Cloud | - Azure: Subscription Contributor or Security Admin<br>- Azure DevOps: Project Collection Administrator on target Organization<br>- GitHub: Organization Owner<br>- GitLab: Group Owner on target Group |
| Review security insights and findings | Security Reader |
| Configure pull request annotations | Subscription Contributor or Owner |
| Install the Microsoft Security DevOps extension in Azure DevOps | Azure DevOps Project Collection Administrator |
| Install the Microsoft Security DevOps action in GitHub | GitHub Write |

Note

To avoid setting highly privileged permissions on a subscription for read access to DevOps security insights and findings, apply the **Security Reader** role on the resource group or connector scope.

## Feature availability

DevOps security capabilities, such as code-to-cloud contextualization, security explorer, attack path analysis, and pull request annotations for Infrastructure-as-Code security findings, are available when you enable the paid Defender Cloud Security Posture Management (Defender CSPM) plan. For a detailed breakdown of posture management capabilities in cloud and DevOps platforms, see [DevOps Cloud Security Posture Management](concept-cloud-security-posture-management#devops-cloud-security-posture-management).

The following sections summarize the availability and prerequisites for each feature within the supported DevOps platforms.

## Agentless code scanning (Preview)

[Agentless code scanning (Preview)](agentless-code-scanning) provides security coverage for repositories connected through Azure DevOps and GitHub. It scans the default branch without requiring changes to CI/CD pipelines or developer workflows. The service identifies code vulnerabilities, Infrastructure-as-Code (IaC) misconfigurations, and open-source dependency vulnerabilities, and generates a queryable software bill of materials (SBOM).

Agentless code scanning supports these capabilities:

- **Code vulnerability scanning** for Python, JavaScript, TypeScript, JSX, and TSX.
- **Dependency vulnerability scanning** for package ecosystems such as npm, Yarn, pip, Pipenv, Poetry, Maven, Gradle, NuGet, Go modules, RubyGems, Composer, Cargo, and other ecosystems supported through repository manifests and lockfiles.
- **IaC misconfiguration scanning** for Terraform, Terraform plan files, AWS CloudFormation, Kubernetes manifests, Helm charts, Dockerfiles, Azure Resource Manager (ARM) templates, Bicep, AWS Serverless Application Model (SAM), Kustomize, Serverless Framework, and OpenAPI specifications.
- **SBOM generation** to identify dependencies and versions used by repositories.

Agentless code scanning uses the following managed open-source tools:

| Tool | Primary coverage |
| --- | --- |
| [Template Analyzer](https://github.com/Azure/template-analyzer) | ARM and Bicep templates |
| [Checkov](https://github.com/bridgecrewio/checkov) | Terraform, CloudFormation, Kubernetes, Helm, Dockerfiles, ARM, Bicep, SAM, Kustomize, Serverless Framework, and OpenAPI |
| [Bandit](https://github.com/PyCQA/bandit) | Python code |
| [ESLint](https://github.com/eslint/eslint) | JavaScript, TypeScript, JSX, and TSX |
| [Trivy](https://github.com/aquasecurity/trivy/) | Dependencies and operating system packages in repository manifests and lockfiles |
| [Syft](https://github.com/anchore/syft/) | SBOM generation for supported package ecosystems and binaries |

Agentless code scanning runs through Azure DevOps and GitHub connectors. Repository discovery occurs every eight hours, and code and IaC scans run daily. You can select the scanners to run and include or exclude organizations, projects, or repositories. Repositories must be smaller than 1 GB. For setup instructions, supported file types, findings, and limitations, see [Configure agentless code scanning](agentless-code-scanning).

## Azure DevOps

Connect Azure DevOps to Microsoft Defender for Cloud to gain posture management, code scanning, and risk analysis for Azure DevOps organizations and repositories. Learn how to [onboard Azure DevOps](quickstart-onboard-devops) and review [Azure DevOps prerequisites](quickstart-onboard-devops#prerequisites).

| Feature | Foundational CSPM | Defender CSPM | Prerequisites |
| --- | --- | --- | --- |
| [Inventory of Azure DevOps resources](quickstart-onboard-devops) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | - |
| [Security recommendations to fix DevOps environment misconfigurations](concept-devops-environment-posture-management-overview) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | - |
| [Security recommendations to fix code vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | One of: [Agentless code scanning (Preview)](agentless-code-scanning), [Microsoft Security DevOps extension](configure-azure-devops-extension), or [GHAS code scanning](/en-us/azure/devops/repos/security/github-advanced-security-code-scanning?view=azure-devops&amp;tabs=yaml&amp;preserve-view=true). |
| [Security recommendations to fix Infrastructure as Code (IaC) misconfigurations](iac-vulnerabilities) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | One of: [Agentless code scanning (Preview)](agentless-code-scanning) or [Microsoft Security DevOps extension](configure-azure-devops-extension). |
| [Security recommendations to discover exposed secrets](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitHub Advanced Security for Azure DevOps](/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&amp;tabs=yaml&amp;preserve-view=true). |
| [Security recommendations to fix open source vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitHub Advanced Security for Azure DevOps](/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&amp;tabs=yaml&amp;preserve-view=true). |
| [Query software bill of materials (SBOM)](query-software-bill-of-materials) | - | ![](media/icons/yes-icon.png) | Enable [agentless code scanning (Preview)](agentless-code-scanning) and wait for initial scan completion. |
| [Pull request annotations](review-pull-request-annotations) | - | ![](media/icons/yes-icon.png) | See [pull request annotations prerequisites](enable-pull-request-annotations). |
| [Code to cloud mapping for Containers](container-image-mapping) | - | ![](media/icons/yes-icon.png) | [Microsoft Security DevOps extension](configure-azure-devops-extension#configure-the-microsoft-security-devops-azure-devops-extension). |
| [Code to cloud mapping for Infrastructure as Code (IaC) templates](iac-template-mapping) | - | ![](media/icons/yes-icon.png) | [Microsoft Security DevOps extension](configure-azure-devops-extension). |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |
| [Cloud security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |

## GitHub

Connect GitHub to Microsoft Defender for Cloud for inventory discovery, code and IaC vulnerability scanning, and code-to-cloud mapping. Learn how to [onboard GitHub](quickstart-onboard-github) and review [GitHub prerequisites](quickstart-onboard-github#prerequisites).

| Feature | Foundational CSPM | Defender CSPM | Prerequisites |
| --- | --- | --- | --- |
| [Inventory of GitHub DevOps resources](quickstart-onboard-github) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | - |
| [Security recommendations to fix DevOps environment misconfigurations](concept-devops-environment-posture-management-overview) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | - |
| [Security recommendations to fix code vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | One of: [Agentless code scanning (Preview)](agentless-code-scanning), [Microsoft Security DevOps action](github-action), or [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security). |
| [Security recommendations to fix Infrastructure as Code (IaC) misconfigurations](iac-vulnerabilities) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | One of: [Agentless code scanning (Preview)](agentless-code-scanning) or [Microsoft Security DevOps action](github-action). |
| [Security recommendations to discover exposed secrets](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security). |
| [Security recommendations to fix open source vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security). |
| [Query software bill of materials (SBOM)](query-software-bill-of-materials) | - | ![](media/icons/yes-icon.png) | Enable [agentless code scanning (Preview)](agentless-code-scanning) and wait for initial scan completion. |
| [Code to cloud mapping for Containers](container-image-mapping) | - | ![](media/icons/yes-icon.png) | [Microsoft Security DevOps action](github-action). |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |
| [Cloud security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |

## GitLab

Connect GitLab to Microsoft Defender for Cloud for security recommendations and security explorer risk hunting in your GitLab projects. Learn how to [onboard GitLab](quickstart-onboard-gitlab) and review [GitLab prerequisites](quickstart-onboard-gitlab#prerequisites).

| Feature | Foundational CSPM | Defender CSPM | Prerequisites |
| --- | --- | --- | --- |
| [Security recommendations to fix code vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitLab Ultimate](https://about.gitlab.com/pricing/ultimate/). |
| [Security recommendations to fix infrastructure as code (IaC) misconfigurations](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitLab Ultimate](https://about.gitlab.com/pricing/ultimate/). |
| [Security recommendations to discover exposed secrets](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitLab Ultimate](https://about.gitlab.com/pricing/ultimate/). |
| [Security recommendations to fix open source vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | [GitLab Ultimate](https://about.gitlab.com/pricing/ultimate/). |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |
| [Cloud security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) | Enable Defender CSPM on an Azure subscription, AWS connector, or GCP connector in the same tenant as the DevOps connector. |

## External registries

External registry connectors extend Defender for Cloud to container images outside your Azure, AWS, and GCP subscriptions. Foundational CSPM provides inventory. Defender CSPM provides vulnerability assessment and contextual risk signals. For Defender for Containers coverage, see [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).

## Docker Hub

Connect Docker Hub to Microsoft Defender for Cloud to enable asset inventory and agentless vulnerability assessment for container images in your Docker Hub organization. Learn how to [configure vulnerability assessment for Docker Hub](agentless-vulnerability-assessment-docker-hub) and review [Docker Hub prerequisites](agentless-vulnerability-assessment-docker-hub#prerequisites).

| Capability | Foundational CSPM | Defender CSPM | Prerequisites |
| --- | --- | --- | --- |
| [Inventory discovery of container images in the registry](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | A Docker Hub organization with admin permissions and a read-only access token. Create one connector for each Docker Hub organization. |
| [Agentless vulnerability assessment for container images](agentless-vulnerability-assessment-docker-hub) | - | ![](media/icons/yes-icon.png) | - |
| [Code-to-cloud mapping for containers](container-image-mapping) | - | ![](media/icons/yes-icon.png) | Configure supported code-to-cloud mapping. |
| [Code-to-cloud mapping for Infrastructure as Code (IaC)](iac-template-mapping) | - | ![](media/icons/yes-icon.png) | Configure supported code-to-cloud mapping. |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) | - |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) | - |
| [Risk prioritization](risk-prioritization) | - | ![](media/icons/yes-icon.png) | - |

## JFrog Artifactory

Connect JFrog Artifactory to Microsoft Defender for Cloud to enable asset inventory and agentless vulnerability assessment for container images in your JFrog Artifactory Cloud tenant. Learn how to [configure vulnerability assessment for JFrog Artifactory](agentless-vulnerability-assessment-jfrog-artifactory) and review [JFrog Artifactory prerequisites](agentless-vulnerability-assessment-jfrog-artifactory#prerequisites). Defender CSPM adds contextual risk signals to the JFrog Artifactory registry capabilities in this table. The Defender CSPM plan details list broader CSPM capabilities, but only capabilities that support the JFrog connector apply to its registry images.

| Capability | Foundational CSPM | Defender CSPM | Prerequisites |
| --- | --- | --- | --- |
| [Inventory discovery of container images in the registry](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | A JFrog Artifactory Cloud tenant with administrative access. Create one connector for each tenant. |
| [Agentless vulnerability assessment for container images](agentless-vulnerability-assessment-jfrog-artifactory) | - | ![](media/icons/yes-icon.png) | Also requires [JFrog CLI](https://jfrog.com/help/r/jfrog-applications-and-cli-documentation/download-and-install-the-jfrog-cli) and `jq` JSON parser. |
| [Code-to-cloud mapping for containers](container-image-mapping) | - | ![](media/icons/yes-icon.png) | Configure supported code-to-cloud mapping. |
| [Code-to-cloud mapping for Infrastructure as Code (IaC)](iac-template-mapping) | - | ![](media/icons/yes-icon.png) | Configure supported code-to-cloud mapping. |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) | - |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) | - |
| [Risk prioritization](risk-prioritization) | - | ![](media/icons/yes-icon.png) | - |

For container registry vulnerability assessment and runtime assessment requirements, see [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).