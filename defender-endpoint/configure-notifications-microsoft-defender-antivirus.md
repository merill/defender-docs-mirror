---
layout: Conceptual
title: Configure Microsoft Defender Antivirus notifications - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-notifications-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure and customize both standard and other Microsoft Defender Antivirus notifications on endpoints.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: chrisda
ms.topic: how-to
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-08-12T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 479abc12-6b20-a687-1123-71c0d7e6e8e8
document_version_independent_id: 479abc12-6b20-a687-1123-71c0d7e6e8e8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-notifications-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-notifications-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-notifications-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ca952074-f605-c1b7-3976-609740f207b0
---

# Configure Microsoft Defender Antivirus notifications - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to configure Microsoft Defender Antivirus notifications on Windows endpoints, including threat-detection, scan-completion, and reboot-required notifications.

In Windows 10 and Windows 11, application notifications about malware detection and remediation are more robust, consistent, and concise. Microsoft Defender Antivirus notifications appear on endpoints when scans are completed and threats are detected. Notifications follow both scheduled and manually triggered scans. Notifications for completed scans and detected threats also appear in the **Notification Center**, and a summary of scans and threat detections appear at regular time intervals.

If you're part of your organization's security team, you can configure how notifications appear on endpoints, such as notifications that prompt for a system reboot or that indicate a threat was detected and remediated.

## Prerequisites

### Supported operating systems

The following operating systems are supported:

- Windows 10
- Windows 11

## Configure antivirus notifications using Group Policy or the Windows Security app

You can configure the display of enhanced notifications (additional notification summaries such as recent threat detections) in the [Windows Security app](microsoft-defender-security-center-antivirus) and with Group Policy.

| Setting | Description |
| --- | --- |
| Configure time interval for service health reports | This policy setting configures the time interval (in minutes) for the service health reports to be sent from endpoints. If you disable or don't configure this setting, the default value is applied. The default value is set at 60 minutes (1 hour). If you configure this setting to 0, no service health reports are sent. The maximum value allowed to be set is 14400 minutes (10 days). |
| Configure time out for detections in critically failed state | This policy setting configures the time in minutes before a detection in the "critically failed" state to moves to either the "additional action" state or the "cleared" state. |
| Configure time out for detections in noncritical failed state | This policy setting configures the time in minutes before a detection in the "non-critically failed" state moves to the "cleared" state. |
| Configure time out for detections in recently remediated state | This policy setting configures the time in minutes before a detection in the "completed" state moves to the "cleared" state. |
| Configure time out for detections in requiring additional action | This policy setting configures the time in minutes before a detection in the "additional action" state moves to the "cleared" state. |
| Configure Watson events | This policy setting allows you to configure whether or not Watson events are sent. If you enable or don't configure this setting, Watson events are sent. If you disable this setting, Watson events aren't sent. |
| Configure whether to report Dynamic Signature dropped events | This policy setting configures whether to report Dynamic Signature dropped events. If you don't configure this setting, the default value is applied. The default value is set to disabled (such events aren't reported). If you configure this setting to be enabled, Dynamic Signature dropped events are reported. If you configure this setting to disabled, Dynamic Signature dropped events aren't reported. |
| Configure Windows software trace preprocessor components | This policy configures Windows software trace preprocessor (WPP Software Tracing) components. |
| Configure WPP tracing level | This policy allows you to configure tracing levels for Windows software trace preprocessor (WPP Software Tracing). Tracing levels are defined as: 1 - Error 2 - Warning 3 - Info 4 - Debug |
| Turn off enhanced notifications | Use this policy setting to specify if you want Microsoft Defender Antivirus enhanced notifications to display on clients. If you disable or do not configure this setting, Microsoft Defender Antivirus enhanced notifications will display on clients. If you enable this setting, Microsoft Defender Antivirus enhanced notifications will not display on clients. |

Note

In Windows 10, version 1607 the feature was called **Enhanced notifications** and was configured under **Windows Settings** &gt; **Update & security** &gt; **Windows Defender**. In Group Policy settings for all versions of Windows 10 and Windows 11, the notification feature is called **Enhanced notifications**.

### Use Group Policy to disable other notifications

Important

Disabling other notifications doesn't disable critical notifications, such as threat detection and remediation alerts.

To disable additional notifications by using Group Policy, perform the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Reporting**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Reporting**, open the **Turn off enhanced notifications** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, select **Enabled**, and then select **OK**.

    Enabling **Turn off enhanced notifications** prevents more notifications from appearing.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Reporting**.

### Use the Windows Security app to disable additional notifications

Important

Disabling other notifications doesn't disable critical notifications, such as threat detection and remediation alerts.

Use the following steps to disable additional notifications in the Windows Security app:

1. Open the Windows Security app by clicking the shield icon in the task bar or searching the start menu for **Security**.
2. Select **Virus & threat protection** tile (or the shield icon on the left menu bar) and, then select **Virus & threat protection settings**
3. Scroll to the **Notifications** section and select **Change notification settings**.
4. Slide the switch to **Off** or **On** to disable or enable other notifications.

## Configure standard notifications on endpoints using Group Policy

### Hide notifications with Group Policy

You can use Group Policy to configure Microsoft Defender Antivirus notifications in the following ways:

- Display more, customized text on endpoints when the user needs to perform an action
- Hide all notifications on endpoints
- Hide reboot notifications on endpoints

Hiding notifications can be useful in situations where you can't hide the entire Microsoft Defender Antivirus interface. See [Prevent users from seeing or interacting with the Microsoft Defender Antivirus user interface](prevent-end-user-interaction-microsoft-defender-antivirus) for more information. Hiding notifications will only occur on endpoints to which the policy is deployed. Notifications related to actions that must be taken (such as a reboot) will still appear on the [Microsoft Configuration Manager Endpoint Protection monitoring dashboard and reports](/en-us/intune/configmgr/protect/deploy-use/monitor-endpoint-protection).

To add custom contact information to endpoint notifications, see [Customize the Windows Security app for your organization](/en-us/windows/security/operating-system-security/system-security/windows-defender-security-center/windows-defender-security-center).

### Use Group Policy to hide notifications

To hide all notifications by using Group Policy, perform the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Client interface**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Client interface**, open the **Suppress all notifications** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Client interface**.

1. In the setting window that opens, select **Enabled**, and then select **OK**.

    Enabling **Suppress all notifications** prevents more notifications from appearing.

### Use Group Policy to hide reboot notifications

To hide reboot notifications by using Group Policy, perform the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Client interface**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Client interface**, open the **Suppresses reboot notifications** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Client interface**.

1. In the setting window that opens, select **Enabled**, and then select **OK**.

    Enabling **Suppresses reboot notifications** prevents reboot notifications from appearing.

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)