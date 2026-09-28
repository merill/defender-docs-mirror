---
layout: Conceptual
title: Transition from a Legacy On-premises Management Console to the Cloud - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/transition-on-premises-management-console-to-cloud
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
description: Migrate from the legacy on-premises management console to the cloud-based Defender for IoT architecture. Learn the updated architecture approach, key retirement considerations, and planning guidance for the transition.
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: a548326a-1b96-2e27-3a1f-15138d6303b1
document_version_independent_id: 43245214-0c92-94c3-43fc-11939e03e970
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/transition-on-premises-management-console-to-cloud.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/transition-on-premises-management-console-to-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/transition-on-premises-management-console-to-cloud.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 3998f7d8-dbe2-028b-5c36-48c4423ba364
---

# Transition from a Legacy On-premises Management Console to the Cloud - Microsoft Defender for IoT | Microsoft Learn

This article describes how to transition from the on-premises management console to the cloud.

Important

The on-premises management console won't be supported or available for download after January 1st, 2025. For more information, see [on-premises management console retirement](on-premises-management-console-retirement).

Our current architecture guidance is designed to be more efficient, secure, and reliable than using the legacy on-premises management console. The updated guidance has fewer components, which makes it easier to maintain and troubleshoot. The smart sensor technology used in the new architecture allows for on-premises processing, reducing the need for cloud resources and improving performance. The updated guidance keeps your data within your own network, providing better security than cloud computing.

## Architecture guidance

If you're an existing customer using an on-premises management console to manage your OT sensors, we recommend transitioning to the updated architecture guidance. The following image shows a graphical representation of the transition steps to the new recommendations:

![Diagram of the transition from a legacy on-premises management console to the newer recommendations.](../media/on-premises-architecture/transition-new.png)

## How to manage the transition period

The following stages describe how sensor connectivity changes during the transition period:

- **In your legacy configuration**, all sensors are connected to the on-premises management console.
- **During the transition period**, your sensors remain connected to the on-premises management console while you connect any sensors possible to the cloud.
- **After fully transitioning**, you'll remove the connection to the on-premises management console, keeping cloud connections where possible. Any sensors that must remain air-gapped are accessible directly from the sensor UI.

## Transition your architecture

Use the following steps to transition from the legacy on-premises management console architecture to the updated deployment model:

1. For each of your OT sensors, identify the legacy integrations in use and the permissions currently configured for on-premises security teams. For example, what backup systems are in place? Which user groups access the sensor data?
2. Connect your sensors to on-premises, Azure, and other cloud resources, as needed for each site. For example, connect to an on-premises SIEM, proxy servers, backup storage, and other partner systems. You may have multiple sites and adopt a hybrid approach, where only specific sites are kept completely air-gapped or isolated using data-diodes.

    For more information, see the information linked in the [air-gapped deployment procedure](air-gapped-deploy#deployment-steps), as well as the following cloud resources:

    - [Provision sensors for cloud management](provision-cloud-management)
    - [OT threat monitoring in enterprise SOCs](../concept-sentinel-integration)
    - [Securing IoT devices in the enterprise](../concept-enterprise)
3. Set up permissions and update procedures for accessing your sensors to match the new deployment architecture.
4. Review and validate that all security use cases and procedures have transitioned to the new architecture.
5. After your transition is complete, decommission the on-premises management console.