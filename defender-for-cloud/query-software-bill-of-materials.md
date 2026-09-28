---
layout: Conceptual
title: Query Software Bill of Materials (SBOM) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/query-software-bill-of-materials
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
description: Learn how to query Software Bill of Materials (SBOM) results in Microsoft Defender for Cloud's Cloud Security Explorer.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 2ba30756-c103-8ca6-be69-94a9e025a1e2
document_version_independent_id: 70c9bedf-87d4-a1a1-a3fe-dd08ab41b0eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/query-software-bill-of-materials.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/query-software-bill-of-materials
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/query-software-bill-of-materials.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 235cff14-1c16-407b-ca09-ab96d23fb53c
---

# Query Software Bill of Materials (SBOM) - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's DevOps Security agentless scanning capabilities automatically generate a Software Bill of Materials (SBOM) for connected code repositories. When a scan finishes, the process publishes the repository and identified packages to the [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph).

You can use Defender for Cloud's [cloud security explorer](concept-attack-path#what-is-cloud-security-explorer) to query the repository and package data in the cloud security graph. By using the cloud security explorer, you can locate specific packages (dependencies) and identify exactly which repositories use them. Use the query results to identify the impact radius of a vulnerable package version across your organization.

## Prerequisites

Before you build a package query, make sure the following prerequisites are met:

- [Enable agentless scanning](agentless-code-scanning#enable-agentless-code-scanning-on-your-azure-devops-and-github-organizations) in your DevOps connector.
- Wait for the initial scan to complete so the Software Bill of Materials (SBOM) data is populated in the Cloud Map.

## Build a package query

By using Cloud Security Explorer in Microsoft Defender for Cloud, you can build a query to find repositories that include specific packages (dependencies) and versions.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. Select **Resource Type** &gt; **DevOps**.

    [![Screenshot that shows the cloud security explorer and where to select code repositories.](media/query-software-bill-of-materials/code-repository.png)](media/query-software-bill-of-materials/code-repository.png#lightbox)
4. Select the specific code repository type you want to filter for. For example, GitHub repositories.
5. Select **Done**.
6. Select **Search**.

The query returns all code repositories. Select a repository from the results to view more details about the installed software and its security posture.

### Add a dependency filter

To add a filter that searches for repositories containing specific packages (dependencies), continue building the query as follows.

1. Select **(+)**.
2. Select **Application** &gt; **Has installed software**.

    [![Screenshot that shows how to apply the dependency, has installed software.](media/query-software-bill-of-materials/has-installed-software.png)](media/query-software-bill-of-materials/has-installed-software.png#lightbox)
3. Select **(+)** next to `Has installed software`.
4. Select **Name** &gt; **Equals**.
5. Enter the package name. For example, `log4j`, `express`, or `newtonsoft.json`.
6. Select **Search**.

The query returns all repositories that contain the specified package. Select a repository from the results to view more details about the installed software and its security posture.

### Specify a version

To add a filter that searches for a specific package version, continue building the query as follows.

1. Select **(+)** next to `Has installed software`.
2. Select **Version**.

    [![A screenshot that shows where to navigate to, to select version.](media/query-software-bill-of-materials/version.png)](media/query-software-bill-of-materials/version.png#lightbox)
3. Enter a version number. For example, `2.14.1`.
4. Select **Search** to run the query.

The query returns all repositories that contain the specified package and version. Select a repository from the results to view more details about the installed software and its security posture.