---
layout: Conceptual
title: Manage and update Microsoft Defender for Identity sensors - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/sensor-settings
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
description: Learn how to view, manage, and update Microsoft Defender for Identity sensors in the Microsoft Defender portal, including sensor health, migration state, and delayed updates.
ms.date: 2026-09-09T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: a6713598-ccde-e05f-749d-cd5afd2c3b65
document_version_independent_id: a6713598-ccde-e05f-749d-cd5afd2c3b65
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/sensor-settings.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: sensor-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/sensor-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 96575b4f-b073-d9e8-0134-38e9fcf5b59d
---

# Manage and update Microsoft Defender for Identity sensors - Microsoft Defender for Identity | Microsoft Learn

View, manage, and update Defender for Identity sensors in the Microsoft Defender portal. Use this guidance to monitor sensor status and health, review sensor properties, manage updates, and configure proxy settings.

## View sensor settings and status

On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, review sensor settings and status.

The **Sensor management** tab shows Defender for Identity sensors deployed in your environment and servers discovered in Device Inventory. From this tab you can:

- **Filter** sensors by type, domain, delayed update, service status, sensor status, migration state, or health status.
- **Export** the sensor list to a CSV file.
- **Onboard a sensor** using the **+ Add sensor** option.
- **Customize columns** to show or hide specific fields.
- **Search** for a specific sensor by name.

Select a sensor row to open a details pane with information about the sensor and its health status. From the details pane, you can select **Manage sensor** to update sensor configuration, or select a health issue to see more details and reopen closed issues.

## Sensor status and property details

The **Sensor management** tab shows the following columns. For columns with multiple possible values, see the tables below.

- **Sensor**: The sensor's NetBIOS computer name.
- **Type**: The sensor type. For possible values, see Sensor type.
- **Domain**: The fully qualified domain name of the Active Directory domain where the sensor is installed.
- **Migration state**: Indicates if sensors are eligible for [migration from v2.x to v3.x](deploy/migrate-to-sensor-v3). For possible values, see Sensor migration state.
- **Service status**: The current state of the sensor service on the server. For possible values, see Sensor service status.
- **Sensor status**: The current update and configuration state of the sensor software. For possible values, see Sensor status values.
- **Version**: The sensor version installed.
- **Delayed update**: Whether delayed updates are enabled or disabled. Delayed updates are supported by version 2 of the sensor. For more information, see Delayed update for sensor v2.x.
- **Health issues**: The count of open health issues on the sensor.
- **Health status**: The overall health of the sensor based on the highest severity open health issue. For possible values, see Sensor health status.
- **Created**: The date the sensor was installed.

### Sensor type

The **Type** column indicates the sensor type based on the server role where the sensor is installed. If a sensor is installed on a domain controller that also runs Microsoft Entra Connect or AD CS, the type is **Domain controller sensor**.

| Type | Description |
| --- | --- |
| **Domain controller sensor** | Installed on an Active Directory domain controller. |
| **AD FS sensor** | Installed on an Active Directory Federation Services (AD FS) server. |
| **Standalone sensor** | Installed on a dedicated server that monitors domain controller traffic via port mirroring. |
| **Entra Connect sensor** | Installed on a Microsoft Entra Connect server. |
| **ADCS sensor** | Installed on an Active Directory Certificate Services (AD CS) server. |

### Sensor migration state

The migration state column indicates whether a Defender for Identity sensor running v2.x can be upgraded in place to v3.x. Possible values include **Ready for migration**, **Not ready for migration**, **Migrating**, **Up to date**, and **Migration failed**, as described in the table later in this section. For more information about the migration process, see [migration from v2.x to v3.x](deploy/migrate-to-sensor-v3).

For a server to be eligible for migration, it must:

- Be a domain controller, including a domain controller that also runs AD FS, AD CS, or Microsoft Entra Connect.
- Run Defender for Identity sensor v2.x.
- Run Windows Server 2019 or later.
- Have the July 2026 or later cumulative update installed.
- Have Microsoft Defender for Endpoint deployed.

For the full list of v3.x requirements, see [Defender for Identity sensor v3.x prerequisites](deploy/deploy-sensor-v3).

| State | Description |
| --- | --- |
| **Ready for migration** | The server meets all prerequisites and can be migrated. |
| **Not ready for migration** | The server doesn't meet one or more prerequisites. |
| **Migrating** | The migration is in progress. |
| **Up to date** | The migration completed successfully. The server is running sensor v3.x. |
| **Migration failed** | The migration encountered an error. You can retry the migration. |

### Sensor service status

The service status column indicates the current operational state of the sensor service on the server.

| Status | Description |
| --- | --- |
| **Running** | The sensor service is running. |
| **Starting** | The sensor service is starting. |
| **Disabled** | The sensor service is disabled. |
| **Stopped** | The sensor service is stopped. |
| **Unknown** | The sensor is disconnected or unreachable. |

### Sensor status values

The sensor status column indicates the current update and configuration state of the sensor software.

| Status | Description |
| --- | --- |
| **Up to date** | The sensor is running the current version. |
| **Outdated** | The sensor is running a version that is at least three versions behind the current version. |
| **Updating** | The sensor software is being updated. |
| **Update failed** | The sensor failed to update to a new version. |
| **Not Configured** | The sensor requires more configuration before it's fully operational. This applies to sensors on AD FS, AD CS, or standalone servers. |
| **Start failed** | The sensor didn't pull configuration for more than 30 minutes. |
| **Syncing** | The sensor has configuration updates pending but didn't yet pull the new configuration. |
| **Disconnected** | No communication from this sensor in 10 minutes. |
| **Unreachable** | The domain controller was deleted from Active Directory, but the sensor wasn't uninstalled before decommissioning. You can safely delete this entry. |

### Sensor health status

The health status column indicates the overall health of the sensor based on the severity of any open health issues.

| Status | Description |
| --- | --- |
| **Healthy** (green icon) | No open health issues. |
| **Not healthy** (yellow icon) | The highest severity open health issue is low. |
| **Not healthy** (orange icon) | The highest severity open health issue is medium. |
| **Not healthy** (red icon) | The highest severity open health issue is high. |

## Update sensors

Defender for Identity sensor v3.x is delivered as a component of Microsoft Defender for Endpoint and is updated automatically through Windows Updates. No manual sensor update process is required for v3.x sensors.

Important

The v3.x sensor updates through Windows Update as part of the server's operating system update process. The per-sensor **Delayed update** option available for v2.x sensors doesn't apply to v3.x.

The following sensor update information applies only to Defender for Identity sensor v2.x.

### Defender for Identity sensor v2.x update types

The Defender for Identity service is typically updated a few times a month with new detections, features, and performance improvements. These updates usually include a corresponding minor update to the sensors.

Defender for Identity sensors v2.x support two kinds of updates:

- Minor version updates:

    - Frequent
    - Requires no MSI install, and no registry changes
    - Restarted: Defender for Identity sensor services
- Major version updates:

    - Rare
    - Contains significant changes
    - Restarted: Defender for Identity sensor services

Note

Defender for Identity sensors v2.x always reserve at least 15% of the available memory and CPU on the domain controller where the sensor is installed. If the service consumes too much memory, it's automatically stopped and restarted by the sensor updater service.

### Delayed update for sensor v2.x

You can define a subset of your sensors as a delayed update ring. Sensors not in the delayed ring are updated automatically each time the service is updated. Sensors set to **Delayed update** are updated 72 hours later, giving you time to confirm that the automatically updated sensors are working correctly.

Note

If an error occurs and a sensor does not update, open a support ticket. To further harden your proxy to only communicate with your workspace, see [Proxy configuration](configure-proxy).

Authentication between your sensors and the Azure cloud service uses certificate-based mutual authentication. A self-signed client certificate is created during sensor installation and is valid for 2 years. The sensor updater service generates a new certificate before the existing one expires, using a 2-phase validation process to avoid authentication disruptions during the rollover.

To set a sensor to delayed update:

1. In the **Sensor management** tab, select the sensor you want to set for delayed updates.
2. Select the **Enabled delayed update** button.
3. In the confirmation window, select **Enable**.

To disable delayed updates, select the sensor and then select the **Disabled delayed update** button.

### Sensor v2.x update process

Every few minutes, v2.x sensors check whether a newer version is available. When the cloud service is updated, sensors start the update process:

1. The cloud service updates to the latest version.
2. The sensor updater service detects the new version.
3. Sensors that aren't set to **Delayed update** start the update process one at a time:

    1. The sensor updater service pulls the updated version from the cloud service (in *.cab* file format).
    2. The sensor updater validates the file signature.
    3. The sensor updater extracts the cab file to a new folder in the sensor's installation folder. By default it's extracted to *C:\Program Files\Azure Advanced Threat Protection Sensor&lt;version number&gt;*
    4. The sensor service points to the new files extracted from the cab file.
    5. The sensor updater restarts the sensor service. 
        Note

        Minor sensor updates install no MSI, change no registry values or any system files. A pending restart does not affect a sensor update.
    6. The sensor runs the newly updated version.
    7. The sensor receives clearance from the cloud service. You can verify sensor status on the **Sensor management** tab.
    8. The next sensor starts the update process.
4. Sensors selected for **Delayed update** start their update process 72 hours after the Defender for Identity cloud service is updated. These sensors will then use the same update process as automatically updated sensors.

    For any sensor that fails to complete the update process, a relevant [health alert](health-alerts) is triggered, and is sent as a notification.

### Silently update the Defender for Identity v2.x sensor

Use the following command to silently update the Defender for Identity v2.x sensor:

#### Syntax

The following command shows the basic syntax for running the sensor installer silently or interactively:

```cmd
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

#### Installation options

| Name | Syntax | Mandatory for silent installation? | Description |
| --- | --- | --- | --- |
| Quiet | /quiet | Yes | Runs the installer displaying no UI and no prompts. |
| Help | /help | No | Provides help and quick reference. Displays the correct use of the setup command including a list of all options and behaviors. |
| NetFrameworkCommandLineArguments="/q" | NetFrameworkCommandLineArguments="/q" | Yes | Specifies the parameters for the .Net Framework installation. Must be set to enforce the silent installation of .Net Framework. |

#### Examples

The following example runs the sensor installer silently from the command line without user interaction:

```cmd
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## Remove RPC auditing from a device

From sensor version 3.0.8, RPC auditing is enabled automatically when the sensor is upgraded and no longer requires a tag.

If you configured RPC auditing for an earlier v3.x sensor using the **Unified Sensor RPC Audit** tag, you can remove it by deleting the asset rule or modifying the rule conditions so the device no longer matches.

To manage asset rules, in the [Microsoft Defender portal](https://security.microsoft.com), go to **System &gt; Settings &gt; Microsoft Defender XDR &gt; Asset Rule Management**.

Note

It might take up to one hour for changes to be reflected in the portal.

Learn more about [asset management rules](/en-us/defender-xdr/configure-asset-rules).

## Configure proxy settings

We recommend that you configure initial proxy settings during silent installation [using command line switches](deploy/install-sensor#perform-a-defender-for-identity-silent-installation). If you need to update your proxy settings later on, use either the [CLI method](deploy/configure-proxy#change-proxy-configuration-using-the-cli) or [PowerShell method](deploy/configure-proxy#change-proxy-configuration-using-powershell).

If you'd previously configured your proxy settings via either WinINet or a registry key and need to update them, you'll need to [use the legacy proxy configuration method](deploy/configure-proxy#change-proxy-configuration-using-legacy-methods) you used originally.

For more information, see [Configure endpoint proxy and internet connectivity settings](deploy/configure-proxy).