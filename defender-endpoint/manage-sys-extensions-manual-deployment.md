---
layout: Conceptual
title: Manage system extensions using the manual methods of deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-sys-extensions-manual-deployment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Manually approve system extensions, grant Accessibility and Full Disk Access permissions, and enable notifications for Microsoft Defender for Endpoint on macOS.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 759a8517-ff2a-ea36-b416-30f3ee7c071f
document_version_independent_id: 759a8517-ff2a-ea36-b416-30f3ee7c071f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-sys-extensions-manual-deployment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-sys-extensions-manual-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-sys-extensions-manual-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: db334099-f21c-1813-15c7-7612bac7337c
---

# Manage system extensions using the manual methods of deployment - Microsoft Defender for Endpoint | Microsoft Learn

When you deploy Microsoft Defender for Endpoint on macOS without a mobile device management (MDM) solution, you must manually approve system extensions and grant the required permissions. This article walks macOS administrators through approving system extensions, granting Accessibility and Full Disk Access permissions, enabling notifications, and verifying a healthy deployment state.

## Configure system extensions and permissions using manual deployment

### Approve system extensions manually

You might see the prompt that's shown in the following screenshot:

[![The system extensions blocked prompt screen.](media/system-extension-blocked-prompt.png)](media/system-extension-blocked-prompt.png#lightbox)

1. Select **OK**. You might get a second prompt as shown in the following screenshot:

    [![The second prompt regarding system extensions being blocked.](media/system-extension-blocked-second-prompt.png)](media/system-extension-blocked-second-prompt.png#lightbox)
2. From this second-prompt screen, select **OK**. You receive a notification message that reads **Installation succeeded**, as shown in the following screenshot:

    [![The screen displaying the installation succeeded notification message.](media/installation-succeeded-notification-message.png)](media/installation-succeeded-notification-message.png#lightbox)
3. On the screen displaying the **Installation succeeded** notification message, select **OK**. You return to the following screen:

    [![The Microsoft Defender for Endpoint menu containing the x symbol.](media/mde-menu.png)](media/mde-menu.png#lightbox)
4. From the menu bar, select the **x** symbol on the shield. You get the options shown in the following screenshot:

    [![The screen on clicking the x symbol in the shield.](media/options-on-clicking-x-symbol.png)](media/options-on-clicking-x-symbol.png#lightbox)
5. Select **Action needed**. The following screen appears:

    [![The Virus &amp; threat protection screen containing the Fix button.](media/virus-and-threat-protection-screen.png)](media/virus-and-threat-protection-screen.png#lightbox)
6. Select **Fix** in the upper-right corner of the **Virus & threat protection** screen. You get a prompt, as shown in the following screenshot:

    [![The prompt dialog box on the Virus &amp; threat protection screen.](media/prompt-on-virus-and-threat-protection-screen.png)](media/prompt-on-virus-and-threat-protection-screen.png#lightbox)
7. Enter your password and select **OK**.
8. Select [![The System Preferences icon.](media/system-preferences-icon.png)](media/system-preferences-icon.png#lightbox)

    The **System Preferences** screen appears.

    [![The System Preferences screen.](media/system-preferences-screen.png)](media/system-preferences-screen.png#lightbox)
9. Select **Security & Privacy**. The **Security & Privacy** screen appears.

    [![The Security &amp; Privacy screen.](media/security-and-privacy-screen.png)](media/security-and-privacy-screen.png#lightbox)
10. Select **Click the lock to make changes**. You get a prompt as shown in the following screenshot:

    [![The prompt on the Security &amp; Privacy screen.](media/prompt-on-security-and-privacy-screen.png)](media/prompt-on-security-and-privacy-screen.png#lightbox)
11. Enter your password and click **Unlock**. The following screen appears:

    [![The screen that is displayed on clicking Unlock.](media/screen-on-clicking-unlock.png)](media/screen-on-clicking-unlock.png#lightbox)
12. Select **Details**, next to **Some software system requires your attention before it can be used**.

    [![The screen that is displayed on clicking Details.](media/screen-on-clicking-details.png)](media/screen-on-clicking-details.png#lightbox)
13. Check both the **Microsoft Defender** checkboxes, and select **OK**. You get two pop-up screens, as shown in the following screenshot:

    [![The popup that appears on checking both the checkboxes.](media/popup-after-checking-both-md-checkboxes.png)](media/popup-after-checking-both-md-checkboxes.png#lightbox)
14. On the **"Microsoft Defender" Would like to Filter Network Content** pop-up screen, select **Allow**.
15. On the **Microsoft Defender wants to make changes** pop-up screen, enter your password and select **OK**.

If you run `systemextensionsctl list`, you see output similar to the following screenshot showing the registered system extensions:

[![The resultant screen of running the systemextensionsdcl list.](media/result-of-running-systemextenstionsctl-list.png)](media/result-of-running-systemextenstionsctl-list.png#lightbox)

### Grant Accessibility permissions manually

Perform the following steps to grant Accessibility access to Microsoft Defender:

1. On the **Security & Privacy** screen, select the **Privacy** tab.

    [![The Privacy tab.](media/privacy-tab.png)](media/privacy-tab.png#lightbox)
2. Select **Accessibility** from the left navigation pane, and select **+**.

    [![The Accessibility menu item and the Plus icon.](media/accessibility-and-plus-icon.png)](media/accessibility-and-plus-icon.png#lightbox)
3. In the file selection dialog, select **Applications** from the **Favorites** pane in the left-side of the screen; select **Microsoft Defender**; and then select **Open** at the bottom-right of the screen.

    [![The process of selecting Applications and Microsoft Defender.](media/applications-md-options.png)](media/applications-md-options.png#lightbox)
4. In the **Accessibility** list, check the **Microsoft Defender** checkbox.

    [![Checking the Microsoft Defender checkbox.](media/checking-md-checkbox.png)](media/checking-md-checkbox.png#lightbox)

### Grant Full Disk Access manually

Perform the following steps to grant Full Disk Access to Microsoft Defender:

1. On the **Security & Privacy** screen, select the **Privacy** tab.
2. Select **Full Disk Access** from the left navigation pane, and then select the **Lock** icon.

    [![The Full Disk Access option in the menu and the Lock icon.](media/full-disk-access-and-lock-icon.png)](media/full-disk-access-and-lock-icon.png#lightbox)
3. Confirm that the Microsoft Defender extension has full disk access; if not, check the **Microsoft Defender** checkbox.

    [![Checking the MD checkbox.](media/check-md-checkbox.png)](media/check-md-checkbox.png#lightbox)

### Enable notifications manually

Use the following steps to enable notifications for Microsoft Defender:

1. From the **System Preferences** home screen, select **Notifications**.

    [![The Notifications option in the System Preferences screen.](media/notifications-option.png)](media/notifications-option.png#lightbox)

    The **Notifications** screen appears.
2. Select **Microsoft Defender** from the left navigation pane.
3. Enable the **Allow Notifications** option and select **Alerts**. No further changes are required; leave all other notification settings at their defaults.

    [![Selecting Microsoft Defender option from the Notifications screen.](media/notifications-md.png)](media/notifications-md.png#lightbox)

### Verify a healthy system state

#### Review mdatp health output

After completing the manual deployment steps, run `mdatp health` in Terminal to confirm that Microsoft Defender for Endpoint is running correctly. The following screenshot shows an example of healthy output. In a healthy system, real-time protection is enabled, definitions are up to date, and the system extensions are active.

[![The mdatp health output screen.](media/mdatp-health-output.png)](media/mdatp-health-output.png#lightbox)

#### Check the system extensions

In terminal, run the following command to check the system extensions:

`systemextensionsctl list`

The following screenshot shows the expected output of `systemextensionsctl list` on a healthy system:

[![The command to check the system extensions.](media/command-to-check-system-extensions.png)](media/command-to-check-system-extensions.png#lightbox)