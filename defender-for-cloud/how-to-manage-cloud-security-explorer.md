---
layout: Conceptual
title: Build queries with cloud security explorer - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/how-to-manage-cloud-security-explorer
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
description: Learn how to build queries with cloud security explorer in Microsoft Defender for Cloud to proactively identify security risks in your cloud environment.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 16b243b7-820e-5c97-022f-0bf1ac2f02e1
document_version_independent_id: 6008bc5b-88ed-1a4c-727c-28704327ae8d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/how-to-manage-cloud-security-explorer.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/how-to-manage-cloud-security-explorer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/how-to-manage-cloud-security-explorer.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 45011ed2-94d4-db9f-1576-c8beb541971b
---

# Build queries with cloud security explorer - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud's contextual security capabilities help security teams reduce the risk of significant breaches. Defender for Cloud uses environmental context to assess security issues, identify the biggest risks, and distinguish them from less risky issues. The cloud security explorer uses snapshot publishing, a method of publishing data at regular intervals known as snapshots. Snapshots ensure that the workload configuration data is refreshed daily, keeping it fresh and accurate.

Use the cloud security explorer to identify security risks in your cloud environment. Run graph-based queries on the cloud security graph, Defender for Cloud's context engine. Prioritize your security team's concerns while considering your organization's specific context and conventions.

Use the cloud security explorer to query security issues and environment context, including asset inventory, internet exposure, permissions, and lateral movement between resources across Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP).

## Prerequisites

Before you use cloud security explorer, make sure the following requirements are met:

- You must [enable Defender Cloud Security Posture Management (CSPM)](connect-azure-subscription)

    - You must [enable agentless scanning](enable-agentless-scanning-vms).

    For agentless container posture, you must enable the following extensions:

    - [K8S API access](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan)
    - [Registry access](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan)

    Note

    With only [Defender for Servers P2](tutorial-enable-servers-plan) plan 2 enabled, you can query for keys and secrets. However, you need Defender CSPM to use the full explorer.
- Required roles and permissions: You need one of the following Azure roles to use cloud security explorer:

    - Security Reader
    - Security Admin
    - Reader
    - Contributor
    - Owner

Check the [cloud availability tables](supported-machines-endpoint-solutions-clouds-servers) to see which government and cloud environments are supported.

## Build a query

The cloud security explorer lets you build queries to proactively hunt for security risks in your environments with dynamic and efficient features such as:

- **Multi-cloud and multi-resource queries** - The entity selection control filters are grouped and combined into logical control categories to help you build queries across cloud environments and resources simultaneously.
- **Custom Search** - Use the dropdown menus to apply filters and build your query.
- **Query templates** - Use any of the available prebuilt query templates to build your query more efficiently.
- **Share query link** - Copy and share a link to your query with others.

**To build a query**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.

    [![Screenshot of the cloud security explorer page.](media/concept-cloud-map/cloud-security-explorer-main-page.png)](media/concept-cloud-map/cloud-security-explorer-main-page.png#lightbox)
3. Find and select a resource from the drop-down menu.

    [![Screenshot of the resource drop-down menu.](media/how-to-manage-cloud-security/cloud-security-explorer-select-resource.png)](media/how-to-manage-cloud-security/cloud-security-explorer-select-resource.png#lightbox)
4. Select **+** to add more filters to your query.

    [![Screenshot that shows a full query and where to select on the screen to perform the search.](media/how-to-manage-cloud-security/cloud-security-explorer-query-search.png)](media/how-to-manage-cloud-security/cloud-security-explorer-query-search.png#lightbox)
5. Add subfilters if necessary.
6. After building your query, select **Search** to run it.

    [![Screenshot that shows where to select search to run the query and results populated.](media/how-to-manage-cloud-security/cloud-security-explorer-query-search-populated.png)](media/how-to-manage-cloud-security/cloud-security-explorer-query-search-populated.png#lightbox)
7. To save a copy of your results locally, select the **Download CSV report** button to save your search results as a CSV file.

    ![Screenshot that shows where the download CSV report button is located on the screen.](media/how-to-manage-cloud-security/download-csv-report.png)

## Use query templates

Query templates are ready-made searches that use common filters. To use a template, scroll to the bottom of the page and select **Open query**.

[![Screenshot that shows you the location of the query templates.](media/how-to-manage-cloud-security/cloud-security-explorer-query-templates.png)](media/how-to-manage-cloud-security/cloud-security-explorer-query-templates.png#lightbox)

You can change any template to fit your needs. Update the query, then select **Search** to see your results.

## Share a query

You can share any query with others. After you create a query, select **Share query link** to copy it to your clipboard.

[![Screenshot showing the Share Query Link icon.](media/how-to-manage-cloud-security/cloud-security-explorer-share-query.png)](media/how-to-manage-cloud-security/cloud-security-explorer-share-query.png#lightbox)