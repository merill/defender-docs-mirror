---
layout: Conceptual
title: Audit Microsoft Defender for IoT user activity - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/track-user-activity
breadcrumb_path: ../breadcrumb/toc.json
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
description: Learn how to track and audit user activity across Microsoft Defender for IoT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: cfc65843-e537-a8de-3806-8193733c3ce4
document_version_independent_id: 17cdf570-823c-c368-d5b0-bc9749e77264
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/track-user-activity.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/track-user-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/track-user-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5ceec7a9-878d-a64e-21c8-e123a83e8e9d
---

# Audit Microsoft Defender for IoT user activity - Microsoft Defender for IoT | Microsoft Learn

After you've set up user access in the [Azure portal](manage-users-portal) and on your [OT network sensors](manage-users-sensor), you can track and audit user activity across Microsoft Defender for IoT.

## Audit Azure user activity

Use Microsoft Entra user auditing resources to audit Azure user activity across Defender for IoT. For more information, see:

- [Audit logs in Microsoft Entra ID](/en-us/azure/active-directory/reports-monitoring/concept-audit-logs)
- [Microsoft Entra audit activity reference](/en-us/azure/active-directory/reports-monitoring/reference-audit-activities)

## Audit user activity on an OT network sensor

Audit and track user activity on a sensor's **Event timeline**. The **Event timeline** displays events that occurred on the sensor, affected devices for each event, and the time and date that the event occurred.

### Prerequisites

You must be a default, privileged *admin* user or have an **Admin** role on the sensor.

**To use the sensor's Event Timeline**:

1. Sign into the sensor console as the default, privileged *admin* users or any user with an **Admin** role.
2. On the sensor, select **Event Timeline** from the left-hand menu. Make sure that the filter is set to show **User Operations**.

    For example:

    ![Screenshot of the Event Timeline on the sensor showing user activity.](media/manage-users-sensor/track-user-activity.png)
3. Use additional filters or search using **CTRL+F** to find the information of interest to you.

    For more information on the event timeline, see [Track network and sensor activity with the event timeline](how-to-track-sensor-activity)