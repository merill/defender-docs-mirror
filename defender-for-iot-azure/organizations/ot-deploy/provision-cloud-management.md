---
layout: Conceptual
title: Provision OT Sensors for Cloud Management - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/provision-cloud-management
breadcrumb_path: ../../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn how to ensure that your OT sensor can connect to Azure by accessing a list of required endpoints to define in your firewalls rules.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 94ebf76d-dc89-123b-3182-aad9d1b225a4
document_version_independent_id: d12ceba4-fb9a-123d-845e-db4dbad4bd25
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/provision-cloud-management.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/provision-cloud-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/provision-cloud-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: e7822389-9d1d-1967-359e-97b682638a00
---

# Provision OT Sensors for Cloud Management - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to ensure that your firewall rules allow connectivity to Azure from your OT sensors.

[![Diagram of a progress bar with Site networking setup highlighted.](../media/deployment-paths/progress-network-level-deployment.png)](../media/deployment-paths/progress-network-level-deployment.png#lightbox)

If you're working with air-gapped environment and locally-managed sensors, you can skip downloading endpoint details and configuring firewall rules for Azure connectivity.

## Prerequisites

You need access to the Azure portal with one of these roles: [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader), [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).

Your connectivity teams download endpoint details and configure firewall rules.

## Allow connectivity to Azure

This section describes how to download a list of required endpoints to define in firewall rules, ensuring that your OT sensors can connect to Azure.

This endpoint-download procedure is also used to configure [direct connections](../architecture-connections#direct-connections) to Azure. If you're planning to use a proxy configuration instead, you'll [configure proxy settings](../connect-sensors) after installing and activating your sensor.

For more information, see [Methods for connecting sensors to Azure](../architecture-connections).

To download required endpoint details:

1. On the Azure portal, go to Defender for IoT &gt; **Sites and sensors**.
2. Select **More actions** &gt; **Download endpoint details**.

Configure your firewall rules so that your sensor can access the cloud on port 443, to each of the listed endpoints in the downloaded list.

Important

Azure public IP addresses are updated weekly. If you must define firewall rules based on IP addresses, make sure to download the new [Azure public IP ranges and service tags JSON file](https://www.microsoft.com/download/details.aspx?id=56519) each week and make the required changes on your site to correctly identify services running in Azure.