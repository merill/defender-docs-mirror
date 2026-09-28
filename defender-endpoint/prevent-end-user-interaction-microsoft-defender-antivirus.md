---
layout: Conceptual
title: Hide the Microsoft Defender Antivirus interface - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/prevent-end-user-interaction-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Group Policy to hide the Microsoft Defender Antivirus interface in the Windows Security app and prevent users from pausing scans.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: paulinbar
ms.author: painbar
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 6ec3405d-3b4f-428f-7fb1-fd3c950b817f
document_version_independent_id: 6ec3405d-3b4f-428f-7fb1-fd3c950b817f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/prevent-end-user-interaction-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prevent-end-user-interaction-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/prevent-end-user-interaction-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6c02f528-8985-a1be-60cb-0cf053a512e4
---

# Hide the Microsoft Defender Antivirus interface - Microsoft Defender for Endpoint | Microsoft Learn

You can use Group Policy to prevent users on endpoints from seeing the Microsoft Defender Antivirus interface. You can also prevent them from pausing scans.

## Prerequisites

### Supported operating systems

This feature is supported on the following operating systems:

- Windows

## Hide the Microsoft Defender Antivirus interface

In Windows 10, versions 1703, hiding the interface hides Microsoft Defender Antivirus notifications and prevent the Virus & threat protection tile from appearing in the Windows Security app.

With the setting set to **Enabled**:

[![The Windows Security without the shield icon and virus and threat protection sections](/en-us/defender/media/wdav-headless-mode-off-1703.png)](/en-us/defender/media/wdav-headless-mode-off-1703.png#lightbox)

With the setting set to **Disabled** or not configured:

[![The Windows Security with shield icon and threat protection sections](/en-us/defender/media/wdav-headless-mode-1703.png)](/en-us/defender/media/wdav-headless-mode-1703.png#lightbox)

Note

Hiding the interface will also prevent Microsoft Defender Antivirus notifications from appearing on the endpoint. Microsoft Defender for Endpoint notifications will still appear. You can also individually [configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus)

In earlier versions of Windows 10, the **Enable headless UI mode** setting hides the Windows Defender client interface. If the user attempts to open the Windows Defender client interface, they'll receive a warning that says, "Your system administrator has restricted access to this app."

[![The warning message when headless mode is enabled in Windows 10, versions earlier than 1703](/en-us/defender/media/wdav-headless-mode-1607.png)](/en-us/defender/media/wdav-headless-mode-1607.png#lightbox)

## Use Group Policy to hide the Microsoft Defender Antivirus interface from users

To hide the Microsoft Defender Antivirus interface by using Group Policy, perform the following steps:

1. On your Group Policy management machine, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and select **Edit**.
2. Using the **Group Policy Management Editor** go to **Computer configuration**.
3. Select **Administrative templates**.
4. Expand the tree to **Windows components &gt; Microsoft Defender Antivirus &gt; Client interface**.
5. Double-click the **Enable headless UI mode** setting and set the option to **Enabled**. Select **OK**.

See [Prevent users from locally modifying policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) for other Microsoft Defender Antivirus policy settings that prevent users from modifying protection on their PCs.

## Prevent users from pausing a scan

You can prevent users from pausing scans, which can be helpful to ensure scheduled or on-demand scans aren't interrupted by users.

Note

The **Allow users to pause scan** setting is not supported on Windows 10.

### Use Group Policy to prevent users from pausing a scan

To prevent users from pausing a scan by using Group Policy, perform the following steps:

1. On your Group Policy management machine, open the [Group Policy Management Console](/en-us/previous-versions/windows/desktop/gpmc/group-policy-management-console-portal), right-click the Group Policy Object you want to configure and select **Edit**.
2. Using the **Group Policy Management Editor** go to **Computer configuration**.
3. Select **Administrative templates**.
4. Expand the tree to **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Scan**.
5. Double-click the **Allow users to pause scan** setting and set the option to **Disabled**. Select **OK**.

## Use PowerShell to configure UI Lockdown mode

The `UILockdown` parameter indicates whether to disable UI Lockdown mode. If you specify a value of `$True`, Microsoft Defender Antivirus disables UI Lockdown mode. If you specify a value of `$False` or don't specify a value, UI Lockdown mode is enabled.

```powershell
PS C:\>Set-MpPreference -UILockdown $true
```