---
layout: Conceptual
title: Validate Your Microsoft Defender for APIs Alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-apis-validation
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
description: Walk through triggering a test alert in Defender for APIs to validate detection capabilities by simulating suspicious user-agent activity.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: references_regions, sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 63991398-06de-92f2-2e4c-56bc5e93f6fa
document_version_independent_id: 43a1db78-03c1-e2e1-c160-289ba87b0c59
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-apis-validation.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-apis-validation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-apis-validation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bf4dbf7f-261c-4ae9-9fee-5989668a780a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1c4b5d48-3f26-4bd8-9592-816d9c1a3420
platformId: 1b8dfc85-ee62-5ddd-dc24-f029e52ec720
---

# Validate Your Microsoft Defender for APIs Alerts - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for APIs provides protection, detection, and response coverage for APIs published in Azure API Management. It spots anomalies at runtime by using machine learning and rule-based methods. A key feature is the detection of OWASP API Top 10 vulnerabilities.

In this article, learn how to trigger a test alert for one of your API endpoints. The alert covers detection of a suspicious user agent.

## Prerequisites

Before you begin, ensure that you have the following prerequisites:

- Create a service instance by following [Create a new Azure API Management service instance in the Azure portal](/en-us/azure/api-management/get-started-create-service-instance).
- Check the [support and prerequisites for Defender for APIs deployment](defender-for-apis-prepare).
- Import and publish your API by using [Import and publish your first API](/en-us/azure/api-management/import-and-publish).
- Deploy the feature by using [Onboard Defender for APIs](defender-for-apis-deploy).

## Simulate an alert

Check that Defender for APIs is working as expected. Send a request to your endpoint with a suspicious user agent to simulate an alert.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **API Management services**.

    [![Screenshot that shows where on the Azure portal to search for and select API Management service.](media/defender-for-apis-validation/api-management.png)](media/defender-for-apis-validation/api-management.png#lightbox)
3. Select the relevant API.
4. Select **APIs**.

    [![Screenshot that shows where to select APIs from the menu.](media/defender-for-apis-validation/apis-section.png)](media/defender-for-apis-validation/apis-section.png#lightbox)
5. Select an API endpoint.

    ![Screenshot that shows where to select an API endpoint.](media/defender-for-apis-validation/api-endpoint.png)
6. Select **Test** &gt; **Get Retrieve resource (cashed)**.
7. In the **Headers** section, select **User-Agent** in the name dropdown menu.

    [![Screenshot of the Headers section of the APIs showing how to select the User-Agent option under the name dropdown menu.](media/defender-for-apis-validation/user-agent.png)](media/defender-for-apis-validation/user-agent.png#lightbox)
8. In the value field, enter *javascript:*.
9. Select **Send**.

    A 200 OK appears, letting you know that it succeeded.

    [![Screenshot that shows the result 200 OK.](media/defender-for-apis-validation/200-ok.png)](media/defender-for-apis-validation/200-ok.png#lightbox)

## Expected results

After some time, Defender for APIs triggers an alert with detailed information about the simulated suspicious user-agent activity.