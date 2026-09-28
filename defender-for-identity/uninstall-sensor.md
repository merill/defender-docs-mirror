---
layout: Conceptual
title: Remove the Microsoft Defender for Identity sensor - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/uninstall-sensor
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Remove the Microsoft Defender for Identity sensor from servers by deleting, uninstalling, or cleaning up orphaned and duplicate entries in the Microsoft Defender portal.
ms.date: 2026-09-09T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 5b1a0eb8-2989-dc6b-f007-928e5c96c046
document_version_independent_id: 5b1a0eb8-2989-dc6b-f007-928e5c96c046
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/uninstall-sensor.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: uninstall-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/uninstall-sensor.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 956293f4-c9be-c774-103b-3c49f82b9c9e
---

# Remove the Microsoft Defender for Identity sensor - Microsoft Defender for Identity | Microsoft Learn

Remove the Microsoft Defender for Identity sensor when you need to decommission a server, clean up orphaned or duplicate sensor entries, or stop Defender for Identity monitoring on a specific server. For sensors onboarded without Microsoft Defender for Endpoint deployment, follow the dedicated offboarding procedure before removing the sensor entry.

## Offboard a domain controller without Defender for Endpoint deployment (Preview)

For a domain controller onboarded without Defender for Endpoint deployment, run the offboarding package on the domain controller before removing the sensor from the portal. Removing the portal entry alone doesn't uninstall the sensor component. The sensor can continue sending data and reactivate.

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, select the v3.x sensor, and then select **Delete**.
2. In the removal dialog, select **Download offboarding package**.

    [![Screenshot of the Remove sensor dialog with the Download offboarding package option highlighted.](media/remove-sensor-without-defender-for-endpoint-deployment.png)](media/remove-sensor-without-defender-for-endpoint-deployment.png#lightbox)
3. Copy the downloaded offboarding package to the domain controller.
4. Open PowerShell as an administrator, and change to the folder that contains the offboarding package.
5. Run the deployment tool with the full path to the `.offboarding` file:

    ```powershell
    .\DefenderDeploymentTool_Offboard.exe -Offboard -File:"C:\Path\WindowsDefenderATP_valid_until_YYYY-MM-DD.offboarding"
    ```

    To run without confirmation prompts or dialogs, add the optional `-YES` and `-Quiet` parameters.
6. After offboarding finishes, return to the **Sensor management** tab and remove the sensor.

## Delete a sensor

### For sensor v3.x

Important

For a sensor onboarded without Defender for Endpoint deployment, complete Offboard a domain controller without Defender for Endpoint deployment before deleting the sensor entry.

To delete a v3.x sensor from the Microsoft Defender portal, follow these steps:

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, select the domain controller where you want to deactivate Defender for Identity capabilities.
2. Select **Delete**, and confirm your selection.

    [![Screenshot of the Sensor management tab with the Delete action for a selected sensor.](media/screenshot-that-shows-how-to-delete-a-sensor.png)](media/screenshot-that-shows-how-to-delete-a-sensor.png#lightbox)

## Delete and uninstall a sensor v2.x from a domain controller

Important

We recommend removing the sensor from the domain controller before demoting the domain controller.

To remove sensor v2.x from a domain controller and delete its portal entry, follow these steps:

1. Sign in to the domain controller with administrative privileges.
2. From the Windows **Start** menu, select **Settings** &gt; **Control Panel** &gt; **Add/ Remove Programs**.
3. Select the sensor installation, select **Uninstall**, and follow the instructions to remove the sensor.
4. After the uninstall finishes, open the [Microsoft Defender portal](https://security.microsoft.com).
5. On the **Sensor management** tab of the **On-premises** page at https://security.microsoft.com/securitysettings/identities, select the domain controller, and then select **Delete**.

## Remove an orphaned sensor

A sensor can be orphaned when a domain controller was deleted without first uninstalling the sensor, and the sensor still appears in the Microsoft Defender portal.

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, locate the orphaned sensor and select **Delete** (trash can icon).

    ![Screenshot of the Defender for Identity sensors page showing the delete option for an orphaned sensor.](media/delete-orphaned-sensor.png)

## Remove a duplicate sensor

A duplicate sensor entry can appear after an in-place sensor upgrade, where the sensor is listed twice in the Microsoft Defender portal.

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, locate the duplicate sensor. It is the entry with the **Unknown** status.
2. At the end of the row, select **Delete** (trash can icon).

## Uninstall the Defender for Identity sensor silently

Use the following command to perform a silent uninstall of the Defender for Identity sensor:

### Syntax

The following command shows the available options for removing the sensor from the command line, including optional silent and help switches.

```cmd
"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]
```

### Installation options

| Name | Syntax | Mandatory for silent uninstallation? | Description |
| --- | --- | --- | --- |
| Quiet | /quiet | Yes | Runs the uninstaller displaying no UI and no prompts. |
| Uninstall | /uninstall | Yes | Runs the silent uninstallation of the Defender for Identity sensor from the server. |
| Help | /help | No | Provides help and quick reference. Displays the correct use of the setup command including a list of all options and behaviors. |

### Examples

To silently uninstall the Defender for Identity sensor from the server:

```cmd
"Azure ATP sensor Setup.exe" /quiet /uninstall
```