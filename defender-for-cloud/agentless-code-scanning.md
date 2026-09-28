---
layout: Conceptual
title: Configure agentless code scanning (Preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/agentless-code-scanning
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
description: Learn how to configure agentless code scanning in Microsoft Defender for Cloud to detect code and dependency risks across Azure DevOps and GitHub repositories.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: references_regions, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 5b5092fd-9669-d821-e8e3-79eed6c9b70e
document_version_independent_id: d2465852-1332-5f5e-9bcd-5528fbaa69ce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/agentless-code-scanning.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/agentless-code-scanning
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/agentless-code-scanning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 27cc4571-0395-617a-1859-3e5abed892bc
---

# Configure agentless code scanning (Preview) - Microsoft Defender for Cloud | Microsoft Learn

Agentless code scanning in Microsoft Defender for Cloud offers fast and scalable security coverage for all repositories in Azure DevOps and GitHub. It automatically scans code, open-source dependencies, and infrastructure-as-code (IaC) to identify vulnerabilities and misconfigurations. You don't need to change build or deployment pipelines. Agentless code scanning simplifies setup and maintenance with a single Azure DevOps or GitHub connector and provides broad coverage, continuous insights, and actionable security findings. It lets security and development teams focus on fixing risks without interrupting development workflows.

You can customize which scanners to run and define exactly which organizations, projects, or repositories to include or exclude from scanning.

## Prerequisites

Before you enable agentless code scanning, make sure you meet the following requirements:

- **Supported use cases**:

    - [Security recommendations to prioritize and fix code vulnerabilities](defender-for-devops-introduction#manage-your-devops-environments-in-defender-for-cloud)
    - [Security recommendations to prioritize and fix Infrastructure-as-Code (IaC) misconfigurations](iac-vulnerabilities)
    - Cloud Security Explorer queries to locate repositories, including dependencies resulting from a software bill of materials (SBOM).
- [Supported cloud availability](support-matrix-defender-for-cloud).
- **Supported regions**: Australia East, Canada Central, Central US, East Asia, East US, North Europe, Sweden Central, UK South, West Europe.
- **Supported environments**: Azure DevOps connector and GitHub connector.

**Roles and permissions**:

- To set up and configure the connector:

    - **Project Collection Admin**: Required in Azure DevOps to perform the initial setup.
    - **Subscription Contributor**: Needed on the Azure subscription to create and configure the connector.
- To view security results:

    - **Security Admin**: Can manage security settings, policies, and alerts but can't modify the connector.
    - **Security Reader**: Can view recommendations, alerts, and policies but can't make any changes.

## Key benefits

Agentless code scanning in Microsoft Defender for Cloud provides the following benefits:

- **Proactive risk management**: Identify risks early in the development process. Early risk identification enables secure coding practices and reduces vulnerabilities before they reach production.
- **Effortless onboarding**: Set up quickly with minimal configuration and without pipeline changes.
- **Enterprise-scale, centralized management**: Automatically scan code across multiple repositories using a single connector. Centralized management offers extensive coverage for large environments.
- **Rapid insights for quick remediation**: Receive actionable vulnerability insights right after onboarding, which allows quick fixes and reduces exposure time.
- **Developer-friendly and seamless**: Operate independently of continuous integration and continuous deployment (CI/CD) pipelines, without changes or direct developer involvement needed. Operating independently of CI/CD pipelines allows for continuous security monitoring without disrupting developer productivity or workflows.
- **Flexible coverage and control:** Choose which scanners run and what gets scanned. You can cover everything by default or customize settings to include or exclude specific organizations, projects, or repositories. These customization options allow you to match security coverage to your risk profile and operational needs, without extra complexity.
- **Software Bill of Materials (SBOM) creation**: Automatically generating an SBOM on every scan gives teams a precise, queryable inventory of dependencies and versions across their repositories, without additional workflow changes. This enables rapid impact analysis, faster response to newly disclosed vulnerabilities, and confident decision-making when assessing exposure to specific packages or versions.

## Risk detection capabilities

Agentless code scanning improves security by delivering targeted, actionable recommendations across application code, infrastructure-as-code (IaC) templates, and third-party dependencies. This is in addition to the cloud security posture management security recommendations provided through the connector. Key detection capabilities include:

- **Code vulnerabilities**: Find common coding errors, unsafe coding practices, and known vulnerabilities in multiple programming languages.
- **Infrastructure-as-Code misconfigurations**: Detect security misconfigurations in IaC templates that could lead to insecure deployments.
- **Dependency vulnerabilities**: Identify known vulnerabilities in open-source packages and OS packages discovered in repositories.
- **Software Bill of Materials (SBOM)**: Automatically generate a comprehensive, queryable inventory of dependencies and their versions for each repository.

Creating the connector enhances security by providing foundational cloud security posture management recommendations for repositories, pipelines, and service connections.

## Supported scanning tools

Agentless code scanning uses open-source tools to find vulnerabilities and misconfigurations in code and infrastructure-as-code (IaC) templates:

| **Tool** | **Supported IaC/Languages** | **License** |
| --- | --- | --- |
| **[Template Analyzer](https://github.com/Azure/template-analyzer)** | ARM IaC templates, Bicep IaC templates | [Template Analyzer MIT license](https://github.com/Azure/template-analyzer/blob/main/LICENSE.txt) |
| **[Checkov](https://github.com/bridgecrewio/checkov)** | Terraform IaC templates, Terraform plan files, AWS CloudFormation templates, Kubernetes manifest files, Helm chart files, Dockerfiles, Azure Resource Manager (ARM) IaC templates, Azure Bicep IaC templates, AWS SAM templates (Serverless Application Model), Kustomize files, Serverless framework templates, OpenAPI specification files | [Checkov Apache 2.0 license](https://github.com/bridgecrewio/checkov/blob/main/LICENSE) |
| **[Bandit](https://github.com/PyCQA/bandit)** | Python | [Bandit Apache 2.0 license](https://github.com/PyCQA/bandit/blob/master/LICENSE) |
| **[ESLint](https://github.com/eslint/eslint)** | JavaScript, TypeScript, JSX, TSX | [ESLint MIT license](https://github.com/eslint/eslint/blob/main/LICENSE) |
| **[Trivy](https://www.github.com/aquasecurity/trivy/)** | Dependency and OS package vulnerability scanning from repository manifests and lockfiles (filesystem mode) | [Trivy Apache 2.0 license](https://github.com/aquasecurity/trivy/blob/main/LICENSE) |
| **[Syft](https://github.com/anchore/syft/)** | Alpine (apk), Bitnami packages, C (conan), C++ (conan), Dart (pubs), Debian (dpkg), Dotnet (deps.json), Objective-C (cocoapods), Elixir (mix), Erlang (rebar3), Go (go.mod, Go binaries), GitHub (workflows, actions), Haskell (cabal, stack), Java (jar, ear, war, par, sar, nar, rar, native-image), JavaScript (npm, yarn), Jenkins Plugins (jpi, hpi), Linux kernel archives (vmlinuz), Linux kernel modules (ko), Nix (outputs in /nix/store), PHP (composer, PECL, Pear), Python (wheel, egg, poetry, requirements.txt, uv), Red Hat (rpm), Ruby (gem), Rust (cargo.lock, auditable binary), Swift (cocoapods, swift-package-manager), Wordpress plugins, Terraform providers (.terraform.lock.hcl) | [Syft Apache 2.0 license](https://github.com/anchore/syft/blob/main/LICENSE) |

The scanning tools listed in the preceding table support a wide range of languages and infrastructure-as-code (IaC) frameworks, ensuring thorough security analysis across your codebase.

### Supported systems and file types

#### Version control systems

Agentless code scanning supports the following version control systems:

- **Azure DevOps**: Full support for repositories connected via the Azure DevOps connector.
- **GitHub**: Full support for repositories connected via the GitHub connector.

#### Programming languages

Agentless code scanning supports the following programming languages and dependency ecosystems:

- **Static code analysis**: Python; JavaScript/TypeScript.
- **Dependency ecosystems (via Trivy)**: Node.js (npm, yarn), Python (pip, Pipenv, Poetry), Java (Maven, Gradle), .NET (NuGet), Go modules, Ruby (RubyGems), PHP (Composer), Rust (Cargo), and other supported languages and package ecosystems via manifests and lockfiles.

#### Infrastructure-as-Code (IaC) platforms and configurations

The following table lists the IaC platforms and file types supported by agentless code scanning:

| **IaC Platform** | **Supported file types** | **Notes** |
| --- | --- | --- |
| **Terraform** | `.tf`, `.tfvars` | Supports Terraform IaC templates in HCL2 language, including variable files in `.tfvars`. |
| **Terraform Plan** | JSON files | Includes JSON files representing planned configurations, used for analysis and scanning. |
| **AWS CloudFormation** | JSON, YAML files | Supports AWS CloudFormation templates for defining AWS resources. |
| **Kubernetes** | YAML, JSON files | Supports Kubernetes manifest files for defining configurations in clusters. |
| **Helm** | Helm chart directory structure, YAML files | Follows Helm's standard chart structure and supports Helm v3 chart files. |
| **Docker** | Files named Dockerfile | Supports Dockerfiles for container configurations. |
| **Azure ARM Templates** | JSON files | Supports Azure Resource Manager (ARM) IaC templates in JSON format. |
| **Azure Bicep** | `.bicep` files | Supports Bicep IaC templates, a domain-specific language (DSL) for ARM. |
| **AWS SAM** | YAML files | Supports AWS Serverless Application Model (SAM) templates for serverless resources. |
| **Kustomize** | YAML files | Supports configuration files for Kubernetes customization (Kustomize). |
| **Serverless Framework** | YAML files | Supports templates for the Serverless framework in defining serverless architectures. |
| **OpenAPI** | YAML, JSON files | Supports OpenAPI specification files for defining RESTful APIs. |

## Enable agentless code scanning on your Azure DevOps and GitHub organizations

You can connect both Azure DevOps and GitHub organizations to Defender for Cloud to enable agentless code scanning. To set up the connection, use one of these guides:

- [Connect your Azure DevOps organizations](quickstart-onboard-devops#connect-your-azure-devops-organization)
- [Connect your GitHub organizations](quickstart-onboard-github#connect-your-github-environment)

[![Diagram showing an animated walkthrough of the Defender for Cloud connector setup that enables agentless code scanning for Azure DevOps and GitHub.](media/agentless-code-scanning/agentless-code-scanning-setup.gif)](media/agentless-code-scanning/agentless-code-scanning-setup.gif#lightbox)

### Customize scanner coverage and scope

For both GitHub and Azure DevOps, you can control which scanners run and specify exactly which repositories are included or excluded from agentless scanning.

[![Screenshot of agentless code scanning settings that shows scanner toggles and custom scope options for organizations, projects, and repositories.](media/agentless-code-scanning/custom-settings-agentless-scanning.png)](media/agentless-code-scanning/custom-settings-agentless-scanning.png#lightbox)

- **Select scanners:** Turn each code and infrastructure-as-code (IaC) scanner on or off based on your needs.
- **Set scanning scope:** Decide if you want to scan all repositories by default, or define a custom scope to include or exclude specific organizations, projects, or repositories.

    - **Exclusion mode:** Scan everything except what you list.
    - **Inclusion mode:** Only scan what you list.
- **Custom scope options:**

    - For **GitHub**, set scope by owner or repository.
    - For **Azure DevOps**, set scope by organization, project, or repository.
- **Auto-discover new repositories:** Autodiscovery of new repositories is always limited to the organizations or projects included in the connector’s scope. It's enabled by default when using exclusion mode and no custom scope list is set. Newly created repositories are scanned automatically.

 Autodiscovery isn't available in inclusion mode, because only the listed repositories are scanned.

 These scope configuration options let you match scanning to your security needs, keep coverage up to date as your environment grows, and avoid unnecessary scans or gaps.

## How agentless code scanning works

Agentless code scanning works independently of CI/CD pipelines. It uses the Azure DevOps or GitHub connector to automatically scan code and infrastructure-as-code (IaC) configurations. You don't need to modify pipelines or add extensions. Using the connector without pipeline modifications enables broad and continuous security analysis across multiple repositories. Results are processed and shown directly in Microsoft Defender for Cloud.

[![Diagram showing the architecture of agentless code scanning.](media/agentless-code-scanning/agentless-code-scanning-architecture.png)](media/agentless-code-scanning/agentless-code-scanning-architecture.png#lightbox)

### Agentless code scanning process

Once you enable the agentless code scanning feature within a connector, the scanning process includes these steps:

1. **Repository discovery**: The system automatically identifies all repositories linked through the Azure DevOps and GitHub connector immediately after connector creation and then every 8 hours.
2. **Code retrieval**: It securely retrieves the latest code from the default (main) branch of each repository for analysis, initially after connector setup and then daily.
3. **Analysis**: The system uses built-in scanning tools that Microsoft Defender for Cloud manages and updates. These tools find vulnerabilities and misconfigurations in code and infrastructure-as-code (IaC) templates. The system also creates an SBOM to support package queries.
4. **Findings processing**: It processes scan findings through Defender for Cloud’s backend to create actionable security recommendations.
5. **Results delivery**: The system shows findings in Defender for Cloud as security recommendations. For details about DevOps security recommendations, see [DevOps security recommendations reference](recommendations-reference-devops).

### Scan frequency and duration

Agentless code scanning uses the following schedule:

- **Scan frequency**:

    - The security posture of repositories, pipelines, and service connections is assessed when you create the connector and then every eight hours.
    - The system scans code and infrastructure-as-code (IaC) templates for vulnerabilities after you create the connector and then daily.
- **Scan duration**: Scans typically finish within 15 to 60 minutes, depending on the size and complexity of the repository.

## View and manage scan results

After the scans finish, you can access security findings within Microsoft Defender for Cloud.

### View agentless code scanning findings

To access findings:

1. In Microsoft Defender for Cloud, go to the Security recommendations tab: [Open Security recommendations](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/5).
2. Review recommendations for both Azure DevOps and GitHub repositories, such as:

    - [Repositories should have code scanning findings resolved](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsWithRulesBlade/assessmentKey/99232bb2-9b21-4bbb-8e3c-763673b9923d/showSecurityCenterCommandBar%7E/false) - Indicates vulnerabilities found in code repositories. [![Screenshot of recommendation Azure DevOps repositories should have code scanning findings resolved.](media/agentless-code-scanning/code-scanning-findings.png)](media/agentless-code-scanning/code-scanning-findings.png#lightbox)
    - [Repositories should have infrastructure as code scanning findings resolved](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsWithRulesBlade/assessmentKey/6588c4d4-fbbb-4fb8-be45-7c2de7dc1b3b/showSecurityCenterCommandBar%7E/false) - Flags security misconfigurations in IaC templates.[![Screenshot of recommendation Azure DevOps repositories should have infrastructure as code scanning findings resolved.](media/agentless-code-scanning/infrastructure-as-code-scanning-findings.png)](media/agentless-code-scanning/infrastructure-as-code-scanning-findings.png#lightbox)
    - [Repositories should have dependency vulnerability scanning findings resolved](recommendations-reference-devops#azure-devops-repositories-should-have-dependency-vulnerability-scanning-findings-resolved) - Indicates vulnerable open-source packages detected in repositories.
3. For the full range of recommendations supported for both platforms, see [Azure DevOps and GitHub security recommendations](recommendations-reference-devops).

    Azure DevOps and GitHub security recommendations include items such as requiring multi-reviewer approvals, restricting secret access, and enforcing best practices for both Azure DevOps and GitHub environments.

    Select any recommendation to view details on affected files, severity, and remediation steps.

## Difference between agentless code scanning and in-pipeline scanning

### Agentless vs. in-pipeline scanning

Agentless code scanning and in-pipeline scanning with the Microsoft Security DevOps extension both provide security scanning in Azure DevOps and GitHub. They serve different needs and can complement each other. The following table summarizes the main differences so you can choose the option that best fits your environment.

| **Aspect** | **Agentless code scanning** | **In-pipeline scanning** |
| --- | --- | --- |
| **Use case fit** | Offers broad coverage with minimal disruption to developers | Provides detailed, pipeline-integrated scans with customizable controls |
| **Scan scope and coverage** | Focuses on Infrastructure-as-Code (IaC), code vulnerabilities, and open-source dependency vulnerabilities on a scheduled basis (daily) | Offers extensive coverage, including binaries and container images, triggered on each pipeline run |
| **Setup and configuration** | Requires no further setup after creating the connector | Requires manual installation and configuration in each CI/CD pipeline |
| **Pipeline integration** | Runs independently of CI/CD pipelines without modifying workflows | Integrates within the CI/CD pipeline, requiring configuration in each pipeline |
| **Scanner customization** | Allows you to select which scanners run | Allows customization with specific scanners, categories, languages, sensitivity levels, and non-Microsoft tools |
| **Results and feedback** | Provides access to findings within Defender for Cloud | Offers near real-time feedback within the CI/CD pipeline, with results also visible in Defender for Cloud |
| **Break and fail criteria** | Can't break builds | Can be configured to break builds based on the severity of security findings |

### Scalability and performance impact

Agentless code scanning avoids creating resources in the subscription and doesn't require scanning during the pipeline process. It uses the Azure DevOps and GitHub REST API to pull metadata and code. This means API calls count toward Azure DevOps and GitHub rate limits, but you don't incur direct data transfer costs. The service manages scans to ensure they stay within Azure DevOps and GitHub rate limits without interrupting the development environment. This method provides efficient, high-performance scanning across repositories without affecting DevOps workflows. For more information, see [Azure DevOps rate and usage limits](/en-us/azure/devops/integrate/concepts/rate-limits) and [Rate limits for the GitHub REST API](https://docs.github.com/rest/using-the-rest-api/rate-limits-for-the-rest-api).

## Data security, compliance, and access control for agentless code scanning

Microsoft Defender for Cloud's agentless code scanning service helps protect your code with data security and privacy controls:

- **Data encryption and access control**: The system encrypts all data in transit using industry-standard protocols. Only authorized Defender for Cloud services can access your code.
- **Data residency and retention**: Scans run in the same geo as your Azure DevOps and GitHub connectors (US or EU) to support data protection requirements. The system processes code during scanning and then securely deletes it. It doesn't keep long-term code storage.
- **Access to repositories**: The service generates a secure access token for Azure DevOps and GitHub to run scans. This token lets the service retrieve required metadata and code without creating resources in your subscription. Only Defender for Cloud components can use this access.
- **Compliance support**: The service aligns with regulatory and security standards for data handling and privacy to support secure, regional processing of customer code.

These measures ensure a secure, compliant, and efficient code scanning process, maintaining your data’s privacy and integrity.

## Limitations (public preview)

During the **public preview** phase, the following limitations apply:

- **No binary scanning**: Only code (SAST) and IaC scanning tools are executed.
- **Scan frequency**: Agentless code scanning scans repositories when you enable the feature and then once per day.
- **Repository size**: Agentless code scanning supports repositories under 1 GB.
- **Branch coverage**: Scans cover only the default branch (usually `main`).
- **Tool customization**: You can't customize scanning tools.

Syft (SBOM) currently has the following limitations:

- SBOMs can't be downloaded. You can query Syft results to find specific packages and the repositories that use them. For guidance, see [Query software bill of materials](/en-us/azure/defender-for-cloud/query-software-bill-of-materials).
- A repository needs a lock file. Otherwise, only direct dependencies are found.
- The SBOM size limitation is restricted to 1MB. If there are a lot of packages identified, our ingestion into the Cloud Map will fail.
- SBOM enablement isn't configurable or downloadable. An SBOM is generated on every agentless scan.
- Timeout is set to 15 minutes for the SBOM tool to run.
- Disabling agentless code scanning doesn't delete the SBOM recommendations.