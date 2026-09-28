---
layout: Conceptual
title: Manage the Defender for APIs plan - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-apis-manage
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
description: Manage your Defender for APIs deployment in Microsoft Defender for Cloud
ms.topic: concept-article
ms.date: 2025-07-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a9564c16-2dfa-42b8-dfd1-65c0d9c079cf
document_version_independent_id: ab10ea5a-0a6b-b070-147b-7fb1a8ab8534
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-apis-manage.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-apis-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-apis-manage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 795285e9-d8f5-fe7d-e932-937c90b938bf
---

# Manage the Defender for APIs plan - Microsoft Defender for Cloud | Microsoft Learn

This article describes how to manage your [Microsoft Defender for APIs](defender-for-apis-introduction) plan deployment in Microsoft Defender for Cloud. Management tasks include offboarding APIs from Defender for APIs.

## Offboard an API

1. In the Defender for Cloud portal, select **Workload protections**.
2. Select **API security**.
3. Next to the API you want to offboard from Defender for APIs, select the ***ellipsis*** (...) &gt; **Remove**.

    [![Screenshot of the review API information in Cloud Security Explorer.](media/defender-for-apis-manage/api-remove.png)](media/defender-for-apis-manage/api-remove.png#lightbox)
4. **Optional**: You can also select multiple APIs to offboard by selecting the APIs in the checkbox and then selecting **Remove**:

    [![Screenshot showing selected APIs to remove.](media/defender-for-apis-manage/select-remove.png)](media/defender-for-apis-manage/select-remove.png#lightbox)

## Query your APIs with the cloud security explorer

You can use the cloud security explorer to run graph-based queries on the cloud security graph. By utilizing the cloud security explorer, you can proactively identify potential security risks to your APIs.

There are three types of APIs you can query:

- **API Collections**: API collections enable software applications to communicate and exchange data. They're an essential component of modern software applications and microservice architectures. API collections include one or more API endpoints that represent a specific resource or operation provided by an organization. API collections provide functionality for specific types of applications or services. API collections are typically managed and configured by API management/gateway services.
- **API Endpoints**: API endpoints represent a specific URL, function, or resource within an API collection. Each API endpoint provides a specific functionality that developers, applications, or other systems can access.
- **API Management services**: API management services are platforms that provide tools and infrastructure for managing APIs, typically through a web-based interface. They often include features such as: API gateway, API portal, API analytics, and API security.

**To query APIs in the cloud security graph**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. From the drop-down menu, select APIs:

    [![Screenshot of Defender for Cloud's cloud security explorer that shows how to select APIs.](media/defender-for-apis-manage/cloud-explorer-apis.png)](media/defender-for-apis-manage/cloud-explorer-apis.png#lightbox)
4. Select all relevant options.
5. Select **Done**.
6. Add any other conditions.
7. Select **Search**.

You can learn more about how to [build queries with cloud security explorer](how-to-manage-cloud-security-explorer).