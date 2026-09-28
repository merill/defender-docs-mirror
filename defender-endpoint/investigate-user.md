---
layout: Conceptual
title: Investigate a user account in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-user
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Investigate a user account in Microsoft Defender for Endpoint to assess possible credential compromise, review related activity, and pivot to associated investigation data.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.subservice: edr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ffe5e7c9-727a-c4f1-fe9b-30f010a4aee4
document_version_independent_id: ffe5e7c9-727a-c4f1-fe9b-30f010a4aee4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-user.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-user.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ffe3e133-1fb1-4786-26dd-65dd5ac5e2b5
---

# Investigate a user account in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

## Investigate user account entities

Identify user accounts with the most active alerts (displayed on dashboard as "Users at risk") and investigate cases of potential compromised credentials, or pivot on the associated user account when investigating an alert or device to identify possible lateral movement between devices with that user account.

You can find user account information in the following views:

- Dashboard
- Alert queue
- Device details page

In the Dashboard, Alert queue, and Device details page views, a clickable user account link takes you to the user account details page, where you can see more information about the account.

When you investigate a user account entity, you can see:

- User account details, Microsoft Defender for Identity alerts, and logged on devices, role, logon type, and other details
- Overview of the incidents and user's devices
- Alerts related to this user
- Observed in organization (devices logged on to)

[![The user account entity details page](media/atp-user-details-view.png)](media/atp-user-details-view.png#lightbox)

### Review user details

The **User details** pane on left provides information about the user, such as related open incidents, active alerts, Security Account Manager (SAM) name, security identifier (SID), Microsoft Defender for Identity alerts, number of devices the user is logged on to, when the user was first and last seen, role, and logon types. Depending on the integration features you've enabled, you can see other details. For example, if you enable the Skype for business integration, you're able to contact the user from the portal. The **Azure ATP alerts** section contains a link to the user's alerts page in Microsoft Defender for Identity, if you've enabled the Microsoft Defender for Identity feature and there are alerts related to the user. The user's alerts page in Microsoft Defender for Identity provides more information about the alerts.

Note

You'll need to enable the integration on both Microsoft Defender for Identity and Defender for Endpoint to use this feature. In Defender for Endpoint, you can enable this feature in advanced features. For more information on how to enable advanced features, see [Turn on advanced features](advanced-features).

On the user account details page, the Overview, Alerts, and Observed in organization tabs display various attributes for the selected user account.

Note

For Linux devices, information about logged in users isn't displayed.

Note

Microsoft Defender for Business doesn't include Microsoft Defender for Identity (MDI) by default. In SMB-based environments, Logon User data won't be available unless MDI sensors (installed on domain controllers to collect identity-related signals) are deployed. To ensure visibility into logon events, customers must deploy MDI sensors.

### Overview

The **Overview** tab shows the incident details and a list of the devices that the user has logged on to. You can expand each device entry to see details of the logon events for that device.

### Review alerts associated with the user account

The **Alerts** tab provides a list of alerts that are associated with the user account. This list is a filtered view of the [Alert queue](alerts-queue), and shows alerts where the user context is the selected user account, the date when the last activity was detected, a short description of the alert, the device associated with the alert, the alert's severity, the alert's status in the queue, and who is assigned the alert.

### User account activity observed in the organization

The **Observed in organization** tab allows you to specify a date range to see a list of devices where the selected user account was observed logged on to, the most frequent and least frequent logged on user account for each of these devices, and total observed users on each device.

Selecting an item on the Observed in organization table expands the item, revealing more details about the device. Directly selecting a device link within an item opens the device details page for that device.

## Search for specific user accounts

To find a specific user account in Microsoft Defender for Endpoint, follow these steps:

1. Select **User** from the **Search bar** drop-down menu.
2. Enter the user account in the **Search** field.
3. Click the search icon or press **Enter**.

A list of users matching the query text is displayed. You can see the user account's domain and name, when the user account was last seen, and the total number of devices it was observed logged on to in the last 30 days.

You can filter the results by the following time periods:

- 1 day
- 3 days
- 7 days
- 30 days
- 6 months