---
layout: Conceptual
title: Review CI/CD Pipeline Results in Cloud Security Explorer - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-cli-reviewing-results
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
description: Learn how to use Cloud Security Explorer in Microsoft Defender for Cloud to review CI/CD pipeline results and map them to container images effectively.
ms.date: 2025-11-06T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: a8699191-7c80-a372-c7ea-b1961073c85f
document_version_independent_id: 6e8d3a3e-5be7-d08c-fdd0-f38c373c0ee7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-cli-reviewing-results.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-cli-reviewing-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-cli-reviewing-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 46ae146d-3a4d-4416-cfc9-7074d81ff89d
---

# Review CI/CD Pipeline Results in Cloud Security Explorer - Microsoft Defender for Cloud | Microsoft Learn

After your CI/CD pipeline completes a scan with Defender for Cloud CLI, you can review the results in Cloud Security Explorer. Cloud Security Explorer lets you query and visualize the relationship between your CI/CD pipelines and container images, helping you identify vulnerabilities and track security findings across your DevOps environment.

## Query pipeline results

1. After the pipeline runs successfully, go to Microsoft Defender for Cloud.
2. In the **Defender for Cloud** menu, select **Cloud Security Explorer**.
3. Select **Select resource types** dropdown, select **DevOps**, and then select **Done**.

    ![Screenshot of CI/CD pipeline in Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer.png)
4. Select the + icon to add new search criteria.

    ![Screenshot of new search in Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer-search.png)
5. Choose the **Select condition** dropdown. Then select **Data**, and then select **Pushes**.

    ![Screenshot of selecting condition Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer-push.png)
6. Choose the **Select resource types** dropdown. Then select **Containers**, then **Container Images**, and then select **Done**.

    ![Screenshot of selecting container images in Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer-containers.png)
7. Select the scope you selected during the creation of the integration in Environment settings.

    ![Screenshot of selecting scope in Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer-scope.png)
8. Select **Search**.

    ![Screenshot of CI/CD pipeline in Cloud Security Explorer.](media/cli-cicd/cloud-security-explorer.png)
9. See the results of pipeline to images mapping.

## Correlate with monitored containers

1. In Cloud Security Explorer, enter the following query: **CI/CD Pipeline** -&gt; **Pipeline** + **Container Images** -&gt; **Contained in** + **Container registries (group)**.
2. Review the resource names to see the container mapping.