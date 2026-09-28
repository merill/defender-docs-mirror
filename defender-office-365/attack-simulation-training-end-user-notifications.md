---
layout: Conceptual
title: End-user notifications for Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/attack-simulation-training-end-user-notifications
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Admins can learn how to create end-user notification email messages for Attack simulation training in Microsoft Defender for Office 365 Plan 2.
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: eb5c4243-5da5-744e-fcea-a20bf70d0d11
document_version_independent_id: eb5c4243-5da5-744e-fcea-a20bf70d0d11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/attack-simulation-training-end-user-notifications.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-simulation-training-end-user-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/attack-simulation-training-end-user-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 0e5adb6d-53f4-77a7-16dd-d68a9f178c57
---

# End-user notifications for Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In Attack simulation training in Microsoft 365 E5 or Microsoft Defender for Office 365 Plan 2, end-user notifications are email messages that are sent to users as a result of [simulations](attack-simulation-training-simulations) or [simulation automations](attack-simulation-training-simulation-automations). The following types of end-user notifications are available:

- **Positive reinforcement notification**: Sent when users report a simulated phishing message.
- **Simulation notification**: Sent when users are included in a simulation or simulation automation, but no trainings are selected.
- **Training assignment notification**: Sent when users are assigned required trainings as a result of a simulation or simulation automations.
- **Training reminder notification**: Sent as reminders for required trainings.

To see the available end-user notifications, open the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; and then select **End user notifications**. To go directly to the **Content library** tab where you can select **End user notifications**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.

**End user notifications** in the **Content library** tab has two tabs:

- **Global notifications**: Contains the built-in, unmodifiable notifications.
- **Tenant notifications**: Contains the custom notifications that you created.

The following information is shown for each notification. You can sort the notifications by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Notifications**: The name of the notification.
- **⋮** (**Actions** control): Take action on the notification. The available actions depend on the **Status** value of the notification as described in Modify end-user notifications, Copy end-user notifications, and Remove end-user notifications.
- **Language**: If the notification contains multiple translations, the first two languages are shown directly. To see the remaining languages, hover over the numeric icon (for example, **+10**).
- **Type**: The value is **Positive reinforcement notification**, **Simulation notification**, **Training assignment notification**, or **Training reminder notification**.
- **Source**: For built-in notifications, the value is **Global**. For custom notifications, the value is **Tenant**.
- **Status**: The value is **Ready** or **Draft**. On the **Global notifications** tab, the value is always **Ready**.
- **Linked simulations**: The total number of [simulations](attack-simulation-training-simulations) or [simulation automations](attack-simulation-training-simulation-automations) that use the notification.
- **Created by**: For built-in notifications, the value is **Microsoft**. For custom notifications, the value is the user principal name (UPN) of the user who created the notification.
- **Created time**
- **Modified by**
- **Last modified time**

Tip

To see all columns, you likely need to do one or more of the following steps:

- Horizontally scroll in your web browser.
- Narrow the width of appropriate columns.
- Remove columns from the view.
- Zoom out in your web browser.

The **⋮** (**Actions** control) is associated with the **Notifications** column. If you remove that column from view, the **⋮** control goes away.

To find a notification in the list, type part of the notification name in the ![](media/defender-portal-icon-search.png)**Search** box and then press the ENTER key.

To group the notifications by type, select ![](media/defender-portal-icon-group.png)**Group** and then select **Notification type**. To ungroup the notifications, select **None**.

On the **Tenant notifications** tab only, select ![](media/defender-portal-icon-filter.png) to filter the notifications by one or more languages.

When you select a notification from the list, a details flyout appears with the following information:

- **Preview** tab: View the notification message as users see it. To view the message in different languages, use the **Select notification language** dropdown list.
- **Details**tab: View details about the notification:
    - **Notification description**
    - **Source**: For built-in notifications, the value is **Global**. For custom notifications, the value is **Tenant**.
    - **Notification type**
    - **Modified by**
    - **Last modified**
    - **Active training campaigns and phishing simulations**
        - **Name**
        - **Type**
        - **Status**
        - **End by**

On the details flyout from the **Tenant notifications** tab only, select **Edit notification** to modify the notification.

Tip

To see details about other notifications without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

## Create end-user notifications

To create a custom end-user notification, use the following steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; **End user notifications** &gt; and then select the **Tenant notifications** tab. To go directly to the **Content library** tab where you can select **End user notifications**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.
2. On the **Tenant notifications** tab, select ![](media/defender-portal-icon-create.png)**Create new** to start the new end-user notification wizard.

    Note

    At any point after you name the notification during the new end-user notification wizard, you can select **Save and close** to save your progress and continue later. The incomplete notification has the **Status** value **Draft**. You can pick up where you left off by selecting the end-user notification from the list and then clicking the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.

    You can also create end-user notifications during the creation of simulations and simulation automations. For more information, see [Create a simulation: Select end user notifications](attack-simulation-training-simulations#select-end-user-notifications) and [Create a simulation automation: Select end user notifications](attack-simulation-training-simulation-automations#select-end-user-notifications).
3. On the **Define details** page\*\*, configure the following settings:

    - **Select notification type**: Select one of the following values:
        - **Positive reinforcement notification**
        - **Simulation notification**
        - **Training assignment notification**
        - **Training reminder notification**
    - **Name**: Enter a unique name.
    - **Description**: Enter an optional description.

    When you're finished n the **Define details** page, select **Next**.
4. On the **Define content** page, the only setting that's available is **Add content in business language**. When you select it, an **Add content in default language** flyout opens that contains the following settings:

    - **From display name**: Enter the display name of the sender.
    - **From email address**: Enter the email address of the sender.
    - **Select the language of the email**: Select one of the following languages: **Chinese (Simplified)**, **Chinese (Traditional, Taiwan)**, **English**, **French**, **German**, **Italian**, **Japanese**, **Korean**, **Portuguese**, **Russian**, **Spanish**, **Dutch**, **Polish**, **Arabic**, **Finnish**, **Greek**, **Hungarian**, **Indonesian**, **Norwegian Bokmål**, **Romanian**, **Slovak**, **Swedish**, **Thai**, **Turkish**, **Vietnamese**, **Catalan**, **Croatian**, or **Slovenian**.
    - **Mark this as the default language**: Because this language is the first and only language for the notification, this language value is selected as the default, and you can't change it.
    - **Subject**: The default that's used depends on the notification type that you selected in the previous step, but you can change it:

        - Positive reinforcement: **Thank you for reporting a phish!**
        - Simulation: **Thank you for participating in a phishing campaign!**
        - Training assignment: **Training assignment notification**
        - Training reminder: **Training reminder notification**
    - **Import email**: You can optionally select this button and then select **Choose file** to import an existing plain text message file.
    - Email content area: Two tabs are available:

        - **Text** tab: A rich text editor is available to create the notification. To see the typical font and formatting settings, toggle **Formatting controls** to ![](media/scc-toggle-on.png)**On**.

            The following controls are also available on the **Text** tab:

            - **Dynamic tag**: Select from the following tags based on the notification type:

                | Tag name | Tag value | Positivereinforcement | Simulation | Trainingassignment | Trainingreminder |
                | --- | --- | --- | --- | --- | --- |
                | **Insert User name** | `${userName}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert First name** | `${firstName}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Last name** | `${lastName}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert UPN** | `${upn}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Email** | `${emailAddress}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Department** | `${department}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Manager** | `${manager}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Mobile phone** | `${mobilePhone}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert City** | `${city}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert Date** | `${date|MM/dd/yyyy|offset}` | ✔ | ✔ | ✔ | ✔ |
                | **Insert training count** | `${trainingCount}` |  |  | ✔ | ✔ |
                | **Insert training due date** | `${trainingDueDate}` |  |  | ✔ | ✔ |
                | **Insert training duration** | `${trainingDuration}` |  |  | ✔ | ✔ |
                | **Insert training details** | `${trainingDetails}` |  |  | ✔ | ✔ |
                | **Insert payload** | `${payloadSnapshotEmailContent}` | ✔ | ✔ | ✔ |  |
            - **Use from default**: Select an available template to start with. You can modify the text and layout in the editing area. To reset the notification back to the default text and layout of the template, select **Reset to default**.

            Tip

            To add images, copy (CTRL+C) and paste (CTRL+V) the image into the editor on the **Text** tab. The editor automatically converts the image to Base64 as part of the HTML code.
        - **Code** tab: You can view and modify the HTML code directly.

    You can preview the results by selecting **Preview email** at the top of the page.

    When you're finished in new end-user notification wizard, select **Save**.

    Back on the **Define content** page, the notification is listed on the page. In the **Action** column, you can select ![](media/defender-portal-icon-edit.png)**Edit** or ![](media/defender-portal-icon-eye.png)**Preview** to edit or view the notification.

    Select ![](media/defender-portal-icon-create.png)**Add translation** to create up to 11 more translations of the notification in other languages (12 translations total).

    Other than the flyout title changing to **Add translation**, the same options are available as the **Add content in default language** flyout in the first notification you created. Now the **Mark this as default language** check box is available to select. Only one translation of the notification can be the default language.

    When two or more translations of the notification are listed on the **Define content** page, the ![](media/defender-portal-icon-delete.png)**Delete** icon is available in the **Actions** column to delete any notification translations that aren't designated as the default language.

    When you're finished on the **Define content** page, select **Next**.
5. On the **Review notification** page, you can review the details of your notification.

    You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review notification** page, select **Submit**.
6. On the **New training assignment notification created** page, you can use the links to create a new notification, launch a simulation, or view all notifications.

    When you're finished on the **New training assignment notification created** page, select **Done**.
7. Back on the **Tenant notifications** tab in **End user notifications**, the notification that you created is now listed.

## Modify end-user notifications

You can't modify built-in notifications on the **Global notifications** tab. You can only modify custom notifications on the **Tenant notifications** tab.

To modify an existing custom notification on the **Tenant notifications** tab, do one of the following steps:

- Select the notification from the list by selecting the check box next to the name. Select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
- Select **⋮** (**Actions**) next to the **Notifications** value, and then select ![](media/defender-portal-icon-edit.png)**Edit**.
- Select the notification from the list by clicking anywhere in the row other than the check box. In the details flyout that opens, select **Edit notification** at the bottom of the flyout.

The end-user notification wizard opens with the settings and values of the selected notification. The steps are the same as described in the Create end-user notifications section.

## Copy end-user notifications

To copy an existing notification on the **Tenant notifications** or **Global notifications** tabs, do one of the following steps:

- Select the notification from the list by clicking the check box, and then select the ![](media/defender-portal-icon-edit.png)**Create a copy** action that appears.
- Select **⋮** (**Actions**) next to the **Notifications** value, and then select ![](media/defender-portal-icon-edit.png)**Create a copy**.

When you copy a custom notification on the **Tenant notifications** tab, a copy of the notification named "&lt;OriginalName&gt; - Copy" is added to the list.

When you copy a built-in notification on the **Global notifications** tab, a **Create copy** dialog appears. The dialog confirms that a copy of the notification was created, and is available on the **Tenant notifications** tab. If you select **Go to Tenant notification** you're taken to the **Tenant notifications** tab, where the copied built-in notification is named "&lt;OriginalName&gt; - Copy" is available. If you select **Stay here** in the dialog, you return to the **Global notifications** tab.

After the copy is created, you can modify it by following the steps in Modify end-user notifications.

Tip

When you're creating or editing a notification, the **Use from default** control on the **Text** tab of the **Add content in default language** step in the end-user notification wizard also allows you to copy the contents of a built-in notification.

## Remove end-user notifications

You can't remove built-in notifications from the **Global notifications** tab. You can only remove custom notifications on the **Tenant notifications** tab. When you delete a notification, all translations of the notification are deleted.

To remove an existing custom notification from the **Tenant notifications** tab, do one of the following steps:

- Select the notification from the list by clicking the check box next to the name, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.
- Select **⋮** (**Actions**) next to the **Notifications** value, and then select ![](media/defender-portal-icon-delete.png)**Delete**.

In the confirmation dialog that opens, select **Delete**.