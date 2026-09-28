---
layout: Conceptual
title: Microsoft Defender for Cloud DevOps Security Benefits - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-devops-introduction
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
description: Learn about the benefits and features of Microsoft Defender for Cloud DevOps security, including visibility, posture management, and threat protection.
ms.date: 2025-03-12T00:00:00.0000000Z
ms.topic: overview
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 8a4b7fff-4ffa-ccba-4f02-93b4289206b0
document_version_independent_id: e32c93cd-deca-ea88-acd6-7ab513e8075e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-devops-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-devops-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-devops-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c77a3041-2c25-8f16-8d08-7724de2cb061
---

# Microsoft Defender for Cloud DevOps Security Benefits - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud enables comprehensive visibility, posture management, and threat protection across multicloud environments, including Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and on-premises resources.

DevOps security in Defender for Cloud uses a central console to help security teams protect applications and resources from code to cloud across multi-pipeline environments, including Azure DevOps, GitHub, and GitLab. DevOps security recommendations can be correlated with other contextual cloud security insights to prioritize remediation in code. Key DevOps security capabilities include:

- **Unified visibility into DevOps security posture**: Security administrators have full visibility into DevOps inventory and the security posture of preproduction application code across multi-pipeline and multicloud environments. They can see findings from code, secrets, and open-source dependency vulnerability scans. They can also [assess the security configurations of their DevOps environment](concept-devops-posture-management-overview).
- **Strengthen cloud resource configurations throughout the development lifecycle**: You can secure Infrastructure as Code (IaC) templates and container images to minimize cloud misconfigurations reaching production environments, allowing security administrators to focus on critical evolving threats.
- **Prioritize remediation of critical issues in code**: Apply comprehensive code-to-cloud contextual insights within Defender for Cloud. Security admins help developers prioritize critical code fixes with pull request annotations and assign developer ownership by triggering custom workflows that feed directly into the tools developers use.

These features help unify, strengthen, and manage multi-pipeline DevOps resources.

## Manage your DevOps environments in Defender for Cloud

DevOps security in Defender for Cloud lets you manage your connected environments. It provides your security teams with a high-level overview of issues discovered in those environments through the [DevOps security console](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/DevOpsSecurity).

[![Screenshot of the top of the DevOps security page that shows all of your onboarded environments and their metrics.](media/defender-for-devops-introduction/devops-security-overview-2.png)](media/defender-for-devops-introduction/devops-metrics.png#lightbox)

Here, you can add [Azure DevOps](quickstart-onboard-devops), [GitHub](quickstart-onboard-github), and [GitLab](quickstart-onboard-gitlab) environments, customize the [DevOps workbook](custom-dashboards-azure-workbooks#use-the-devops-security-workbook) to show your desired metrics, [configure pull request annotations](enable-pull-request-annotations), view our guides, and give feedback.

### Understand your DevOps security

| Page section | Description |
| --- | --- |
| ![Screenshot of the scan finding metrics sections of the page.](media/defender-for-devops-introduction/security-overview.png) | Total number of DevOps security scan findings (code, secrets, dependency, infrastructure-as-code) grouped by severity level and by finding type. |
| ![Screenshot of the DevOps environment posture management recommendation card.](media/defender-for-devops-introduction/posture-management.png) | Provides visibility into the number of DevOps environment posture management recommendations highlighting high severity findings and number of affected resources. |
| ![Screenshot of DevOps advanced security coverage per source code management system onboarded.](media/defender-for-devops-introduction/advanced-security.png) | Provides visibility into the number of DevOps resources with advanced security capabilities out of the total number of resources onboarded by environment. |

### Review your findings

The DevOps inventory table lets you review onboarded DevOps resources and their related security information.

[![Screenshot that shows the DevOps inventory table on the DevOps security overview page.](media/defender-for-devops-introduction/inventory-grid.png)](media/defender-for-devops-introduction/bottom-of-page.png#lightbox)

In this section, you see:

- **Name** - Lists onboarded DevOps resources from Azure DevOps, GitHub, and GitLab. Select a resource to view its health page.
- **DevOps environment** - Describes the DevOps environment for the resource (Azure DevOps, GitHub, GitLab). Use this column to sort by environment if multiple environments are onboarded.
- **Advanced security status** - Indicates whether advanced security features are enabled for the DevOps resource.

    - `On` - Advanced security is enabled.
    - `Off` - Advanced security isn't enabled.
    - `Partially enabled` - Certain advanced security features aren't enabled (for example, code scanning is off)
    - `N/A` - Defender for Cloud doesn't have information about enablement.

        Note

        This information is currently available only for Azure DevOps and GitHub repositories.
- **Pull request annotation status** - Indicates whether PR annotations are enabled for the repository.

    - `On` - PR annotations are enabled.
    - `Off` - PR annotations aren't enabled.
    - `N/A` - Defender for Cloud doesn't have information about enablement.

        Note

        This information is currently available only for Azure DevOps repositories.
- **Findings** - Indicates the total number of codes, secrets, dependency, and infrastructure-as-code findings identified in the DevOps resource.

You can view this table as a flat view at the DevOps resource level (repositories for Azure DevOps and GitHub, projects for GitLab) or in a grouping view showing organizations, projects, and groups hierarchy. You can also filter the table by subscription, resource type, finding type, or severity.