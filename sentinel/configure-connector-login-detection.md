---
layout: Conceptual
title: Configure the Security Events connector for anomalous RDP login detection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-connector-login-detection
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how to configure the Security Events or Windows Security Events connector for anomalous RDP login detection.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7e818d5e-51a6-ce3c-c599-c703e980d68b
document_version_independent_id: c2471f32-3b86-ef0d-bcb7-1fbc8db30d7b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-connector-login-detection.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-connector-login-detection
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-connector-login-detection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/691e3042-55ad-4ce1-b5e9-649b1cc47b5c
- https://authoring-docs-microsoft.poolparty.biz/devrel/d6f38669-3d05-40f2-afd8-e49f7dd20884
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b7d11190-096c-4ddb-87db-63764f603aac
- https://authoring-docs-microsoft.poolparty.biz/devrel/55265cca-de9b-48dc-a77a-9047cc39a575
platformId: f470b864-0a5d-eae2-1ffa-57907f3aa527
---

# Configure the Security Events connector for anomalous RDP login detection | Microsoft Learn

Microsoft Sentinel can apply machine learning (ML) to Security events data to identify anomalous Remote Desktop Protocol (RDP) login activity. This article explains how to configure the Security Events or Windows Security Events data connector to enable anomalous RDP login detection. Scenarios include:

- **Unusual IP** - the IP address has rarely or never been observed in the last 30 days
- **Unusual geo-location** - the IP address, city, country/region, and ASN have rarely or never been observed in the last 30 days
- **New user** - a new user logs in from an IP address and geo-location, both or either of which were not expected to be seen based on data from the 30 days prior.

Important

Anomalous RDP login detection is currently in public preview. This feature is provided without a service level agreement, and it's not recommended for production workloads. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Configure anomalous RDP login detection

To enable anomalous RDP login detection in Microsoft Sentinel, perform the following steps:

1. You must be collecting RDP login data (Event ID 4624) through the **Security events** or **Windows Security Events** data connectors. Make sure you have selected a [Windows security event set](windows-security-event-id-reference) besides "None", or created a data collection rule that includes this event ID, to stream into Microsoft Sentinel.

    Important

    The machine learning algorithm requires 30 days' worth of data to build a baseline profile of user behavior. Ensure that Windows Security events data has been collected for at least 30 days before you expect any incidents to be detected.
2. From the Microsoft Sentinel portal, select **Analytics**, and then select the **Rule templates** tab. Choose the **(Preview) Anomalous RDP Login Detection** rule, and move the **Status** slider to **Enabled**.