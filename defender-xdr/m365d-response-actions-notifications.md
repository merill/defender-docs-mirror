---
layout: Conceptual
title: Get email notifications for response actions - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-response-actions-notifications
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Set up email notifications to get notified of manual and automated response actions in Microsoft Defender XDR.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 6a7e8fd7-5050-f7b0-a224-1ee17e0cf724
document_version_independent_id: 6a7e8fd7-5050-f7b0-a224-1ee17e0cf724
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-response-actions-notifications.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-response-actions-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-response-actions-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 61b4510f-2f76-5ebe-9541-c76500134ace
---

# Get email notifications for response actions - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

You can set up email notifications in the Microsoft Defender portal to notify you about manual or automated response actions.

Manual response actions are actions that security teams can use to stop threats or aid in investigation of attacks. These actions vary depending on the Defender workload enabled in your environment.

Automated response actions are capabilities in Microsoft Defender that scale investigation and resolution to threats automatically. Automated remediation capabilities consist of [automatic attack disruption](automatic-attack-disruption) and [automated investigation and response](m365d-autoir).

Note

You need the **Manage security settings** permission to configure email notification settings. If you use basic permissions management, users with Security Administrator or higher roles can configure email notifications. Likewise, if your organization is using [role-based access control (RBAC)](manage-rbac), you can only create, edit, delete, and receive notifications based on device groups that you're allowed to manage.

## Create a rule for email notifications

Note

The response action email notification currently doesn't support custom detections containing response actions.

To create a rule for email notifications, perform the following steps:

1. In the navigation pane of the Microsoft Defender portal, select **Settings &gt; Microsoft Defender XDR**. Under **General**, select **Email notifications**. Go to the **Actions** tab.

    [![Actions tab in the Microsoft Defender XDR Settings page](media/m365d-response-actions-notifications/fig1-response-notifications.png)](media/m365d-response-actions-notifications/fig1-response-notifications.png#lightbox)
2. Select **Add notification rule**. Add a rule name and description under Basics. Both Name and Description fields accept letters, numbers, and spaces only.

    [![Basics section of the add notification rule](media/m365d-response-actions-notifications/fig2-response-notifications.png)](media/m365d-response-actions-notifications/fig2-response-notifications.png#lightbox)
3. Proceed to the **Notification settings** section by selecting **Next** at the bottom of the pane.
4. You can choose what type of action, what status, and where the action is sourced from in the **Notification settings** section.

    [![Notifications settings section of the add notification rule](media/m365d-response-actions-notifications/fig3-response-notifications.png)](media/m365d-response-actions-notifications/fig3-response-notifications.png#lightbox)
5. Under **Action source**, select if you want to be notified for manual or automated response actions. You can select both options.
6. Select the specific response actions in the checklist that appears under **Action**. You can choose multiple actions available in the checklist. Response actions vary depending on the Defender workload enabled in your environment. All actions selected appear in the Action field upon completion.

    [![Highlighting the Actions field in the Notification settings section of the add notification rule](media/m365d-response-actions-notifications/fig4-response-notifications.png)](media/m365d-response-actions-notifications/fig4-response-notifications.png#lightbox)
7. You can choose to be notified based on the device groups where the response actions are applied in the **Device groups scope**. To be notified of response actions taken in all current and future device groups, selecting **All device** groups. To be notified of response actions taken in devices that belong to your selected device group, choose **Selected device groups**.

    [![Highlighting the Device groups scope in the Notification settings section of the add notification rule](media/m365d-response-actions-notifications/fig5-response-notifications.png)](media/m365d-response-actions-notifications/fig5-response-notifications.png#lightbox)
8. Select if you want to be notified if an action is completed or failed in the **Action status** field. You can select all options available.
9. At the bottom of the pane, select **Next** to proceed to the **Recipients** section. Alternately, you can go back to the Basics section by selecting **Back**.
10. In the **Recipients** section, you can add one or more email addresses to receive notifications. Separate multiple addresses by adding a comma at the end of each address. Select **Add** to add the recipients. You can see the recipients at the bottom of the pane after successfully adding addresses.

    [![Adding multiple addresses in the Recipients section of the add notification rule](media/m365d-response-actions-notifications/fig6-response-notifications.png)](media/m365d-response-actions-notifications/fig6-response-notifications.png#lightbox)
11. Test the notification by selecting **Send test email**. Select **Next** at the bottom of the pane to proceed to the **Review rule** section.
12. Check the rule's details in the **Review rule** section. You can edit the details by selecting **Edit** under each section's details.

    [![Highlighting the Edit option while in the Review rule section](media/m365d-response-actions-notifications/fig7-response-notifications.png)](media/m365d-response-actions-notifications/fig7-response-notifications.png#lightbox)
13. Select **Submit** at the bottom of the pane to finish the rule creation. Recipients start receiving notifications through email based on the notification rule settings you configured. The new rule appears in the Notifications rule list under the Actions tab.
14. To edit or delete a notification rule, select the rule from the list. Select **Edit** to change the rule's details.

    Warning

    Deleting a notification rule is permanent and can't be undone.

    Select **Delete** to remove the rule.

    [![Highlighting the Edit and Delete options while in the rule list view](media/m365d-response-actions-notifications/fig8-response-notifications.png)](media/m365d-response-actions-notifications/fig8-response-notifications.png#lightbox)

Once you receive an email notification, you can go directly to the response action referenced in the notification to review or remediate it.