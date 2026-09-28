---
layout: Conceptual
title: Build Cloud Security Explorer queries for software vulnerabilities in VMs and container images - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cloud-security-explorer-software-vulnerabilities
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
description: Learn how to build Cloud Security Explorer queries in Microsoft Defender for Cloud to identify software vulnerabilities in virtual machines and container images.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 5b5783d2-b578-f1a0-e0ff-1d7a2aeb6976
document_version_independent_id: e9751c5e-9d15-79bc-3636-bb7d30e00fe1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cloud-security-explorer-software-vulnerabilities.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cloud-security-explorer-software-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cloud-security-explorer-software-vulnerabilities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 56ee4874-7762-24f8-1358-e5d2a01eb207
---

# Build Cloud Security Explorer queries for software vulnerabilities in VMs and container images - Microsoft Defender for Cloud | Microsoft Learn

You can use Cloud Security Explorer to identify software vulnerabilities. The following examples show how to build queries for virtual machines (VMs) and container images.

For an introduction to Cloud Security Explorer queries, see [Build queries with Cloud Security Explorer](how-to-manage-cloud-security-explorer).

## Create a query to identify software vulnerabilities in VMs

To create a query that finds software vulnerabilities in VMs:

1. Sign in to the [Microsoft Defender for Cloud in the Azure portal](https://portal.azure.com).
2. Go to [Microsoft Defender for Cloud &gt; Cloud Security Explorer](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/SecurityGraph).

    [![Screenshot of main page of Cloud Security Explorer.](media/cloud-security-explorer-software-vulnerabilities/cloud-security-explorer-main-page.png)](media/concept-cloud-map/cloud-security-explorer-main-page.png#lightbox)
3. Filter for the software installed on VMs.

    [![Screenshot of Cloud Security Explorer query options to retrieve list of VMs with software installed.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query.png#lightbox)
4. Select **View details** for the VM you want to investigate.
5. In the **Result details** pane, go to **Insights** and select the software from the drop-down list for review.

    [![Screenshot shows results of Cloud Security Explorer query to retrieve VMs with software installed.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query-result-details.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query-result-details.png#lightbox)
6. View the details of the installed software in the Insights section.

    [![Screenshot shows Cloud Security Explorer query result details and insight results from the selected VM.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query-result-details-insights.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-vm-query-result-details-insights.png#lightbox)

## Create a query to identify software vulnerabilities in container images

To create a query that finds software vulnerabilities in container images:

1. Sign in to the [Microsoft Defender for Cloud in the Azure portal](https://portal.azure.com).
2. Go to [Microsoft Defender for Cloud &gt; Cloud Security Explorer](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/%7E/SecurityGraph).

    [![Screenshot of main page of Cloud Security Explorer.](media/cloud-security-explorer-software-vulnerabilities/cloud-security-explorer-main-page.png)](media/concept-cloud-map/cloud-security-explorer-main-page.png#lightbox)
3. Filter for the software installed in container images.

    [![Screenshot of Cloud Security Explorer query options to retrieve list of container images with software installed.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query.png#lightbox)
4. Select **View details** for the container image you want to investigate.
5. In the **Result details** pane, go to **Insights** and select the software from the drop-down list for review.

    [![Screenshot shows results of Cloud Security Explorer query to retrieve container images with software installed.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query-result-details.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query-result-details.png#lightbox)
6. View the details of the installed software in the Insights section.

    [![Screenshot shows Cloud Security Explorer query result details and insight results from the selected containers image.](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query-result-details-insights.png)](media/cloud-security-explorer-software-vulnerabilities/security-explorer-containers-query-result-details-insights.png#lightbox)