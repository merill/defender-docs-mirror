---
layout: Conceptual
title: Set up continuous export to an event hub behind a firewall - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/continuous-export-event-hub-firewall
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
description: Learn how to set up continuous export of Microsoft Defender for Cloud security alerts and recommendations to an event hub behind a firewall.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 9228b581-1cc7-1a3e-1fae-964848de78e1
document_version_independent_id: bb79ada1-04e1-6544-1dd7-1e92b27c2be9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/continuous-export-event-hub-firewall.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/continuous-export-event-hub-firewall
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/continuous-export-event-hub-firewall.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2ed2f492-d3db-acc7-dcf3-90fe3754c409
---

# Set up continuous export to an event hub behind a firewall - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud supports continuous export of alerts and recommendations to Azure Event Hubs. If your event hub is behind a firewall, you can allow Defender for Cloud as a trusted service so export can continue. This article explains how to configure that trusted-service access.

## Prerequisites

Before you enable trusted-service access, configure continuous export by using one of the following methods:

- [Set up continuous export in the Azure portal](continuous-export).
- [Set up continuous export with Azure Policy](continuous-export-azure-policy).
- [Set up continuous export with REST API](continuous-export-rest-api).

## Set up continuous export to the event hub

Enable continuous export as a trusted service to send data to an event hub protected by Azure Firewall.

**To grant access to continuous export as a trusted service**:

1. Sign in to [the Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant resource.
4. Select **Continuous export**.
5. Select **Export as a trusted service**.

    [![Screenshot that shows where the checkbox is located to select export as trusted service.](media/continuous-export-event-hub-firewall/export-as-trusted.png)](media/continuous-export-event-hub-firewall/export-as-trusted.png#lightbox)

## Add the relevant role assignment to the destination event hub

To add the relevant role assignment to the event hub configured as your continuous export destination:

1. Go to the event hub that you configured as the continuous export destination.
2. In the resource menu, select **Access control (IAM)** &gt; **Add role assignment**.

    [![Screenshot that shows the Add role assignment button.](media/continuous-export-event-hub-firewall/add-role-assignment.png)](media/continuous-export-event-hub-firewall/add-role-assignment.png#lightbox)
3. Select **Azure Event Hubs Data Sender**.
4. Select the **Members** tab.
5. Choose **+ Select members**.
6. Search for and then select **Windows Azure Security Resource Provider**.

    [![Screenshot that shows you where to enter and search for Microsoft Azure Security Resource Provider.](media/continuous-export-event-hub-firewall/windows-security-resource.png)](media/continuous-export-event-hub-firewall/windows-security-resource.png#lightbox)
7. Select **Review + assign**.