---
layout: Conceptual
title: Create a Ticket in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/create-ticket-servicenow
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
description: Learn how to create a ticket in Defender for Cloud that connects and synchronizes with your ServiceNow account.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 899f9d82-43cb-d62c-6ab2-11b7a612b655
document_version_independent_id: 71b620a4-b52d-946b-7a16-b11c8c22654f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/create-ticket-servicenow.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/create-ticket-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/create-ticket-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f63d2baf-df0e-73d0-3cbe-403e08ce6d5e
---

# Create a Ticket in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

The integration between Defender for Cloud and ServiceNow's IT Service Management (ITSM) module allows Defender for Cloud customers to create tickets in Defender for Cloud that connect to a ServiceNow account. When a ticket is connected to a recommendation, the two platforms can facilitate efficient incident management and resolution.

## Prerequisites

Before you create tickets in ServiceNow, ensure you meet the following requirements:

- An [application registry in ServiceNow](https://www.opslogix.com/knowledgebase/servicenow/kb-create-a-servicenow-api-key-and-secret-for-the-scom-servicenow-incident-connector).
- [Defender Cloud Security Posture Management (CSPM)](tutorial-enable-cspm-plan) enabled on your Azure subscription.
- The following roles:

    - To create an assignment: Admin permissions to ServiceNow.

## Create a new ticket based on a recommendation to ServiceNow

Security administrators can create and assign tickets directly from the Defender for Cloud portal.

1. Sign in to [the Azure portal](https://aka.ms/integrations).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Select a recommendation you want to create a ServiceNow ticket for, and assign an owner to.
4. Select **View recommendation for all resources**.
5. Expand the **Affected resources** section.
6. In **Unhealthy resources**, select the relevant resource, and then select **Assign owner**.

    [![Screenshot of how to create an assignment.](media/create-ticket-servicenow/create-assignment.png)](media/create-ticket-servicenow/create-assignment.png#lightbox)
7. For **Type**, select **ServiceNow**.

    ![Screenshot that shows the create assignment window and the type field where you select ServiceNow.](media/create-ticket-servicenow/type-servicenow.png)
8. Select the integration instance.
9. Select the ticket type.

    ![Screenshot of how to complete the assignment type.](media/create-ticket-servicenow/assignment-type.png)

    Note

    In ServiceNow, there are several types of tickets that you can use to manage and track different types of incidents, requests, and tasks. Defender for Cloud and ServiceNow ITSM integration supports only incident, change request, and problem ticket types.
10. Expand the **Assignment details** section.
11. Complete the following fields:

    - **Assigned to**: Select an owner for the recommendation.
    - **Caller**: Specify the user defining the assignment.
    - **Description and Short Description**: Enter a description and short description.
    - **Set remediation timeframe**: Select the remediation timeframe.
    - **Apply grace period**: (Optional) Apply a grace period.
    - **Set email notifications**: (Optional) You can send a reminder to the owners or the owner's direct manager.

        ![Screenshot of how to complete the assignment details.](media/create-ticket-servicenow/assignment-details.png)
12. Select **Create**.

After you create the assignment, the Ticket ID assigned to this affected resource appears next to the resource in the recommendation. The Ticket ID represents the ticket created in the ServiceNow portal. You can select the Ticket ID to go to the newly created incident in the ServiceNow portal.

Note

When you delete the Defender for Cloud–ServiceNow integration instance, all associated assignments are deleted. Deletion can take up to 24 hours.