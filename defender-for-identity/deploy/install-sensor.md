---
layout: Conceptual
title: Install the sensor v2.x - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/install-sensor
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
description: Learn how to download and install the Microsoft Defender for Identity sensor v2.x on domain controllers, AD FS servers, AD CS servers, or Microsoft Entra Connect servers.
ms.date: 2026-09-09T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: sfi-ropc-nochange, msecd-doc-authoring-1015
locale: en-us
document_id: fcfcd8d9-ae32-1fd0-9086-83772b334f00
document_version_independent_id: fcfcd8d9-ae32-1fd0-9086-83772b334f00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/install-sensor.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/install-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/install-sensor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: e266c008-0685-4766-32e5-6accdc1786ae
---

# Install the sensor v2.x - Microsoft Defender for Identity | Microsoft Learn

Download and install the Defender for Identity sensor v2.x on domain controllers, or on AD FS, AD CS, and Microsoft Entra Connect servers that aren't domain controllers. Standalone sensor installation is also covered in Install the v2.x sensor in the Defender portal. Before you begin, review the sensor installation prerequisites, including .NET Framework, server specifications, and certificate requirements.

Tip

For domain controllers running Windows Server 2019 or later, deploy the [Defender for Identity sensor v3.x](deploy-sensor-v3) instead. The v3.x sensor is activated from the Defender portal and doesn't require a downloaded installation package.

We recommend alternate installation methods for these use cases:

- When you're installing the sensor on Windows Server Core, or to deploy the sensor via a software deployment system, follow the steps to perform a Defender for Identity silent installation instead.
- If you're using a proxy, we recommend that you install the sensor and configure your proxy together by running a silent installation with proxy configuration. If you need to update your proxy settings later on, use PowerShell or the Azure CLI. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy).

## Prerequisites

Before you start, make sure that you have:

- Microsoft .NET Framework 4.7 or later installed on the machine. If Microsoft .NET Framework 4.7 or later isn't installed, the Defender for Identity sensor setup package installs it. Installation from the setup package might require a restart of the server.
- Relevant server specifications and network requirements. For more information, see:

    - [Microsoft Defender for Identity prerequisites](prerequisites-sensor-version-2)
    - [Configure sensors for AD FS, AD CS, and Microsoft Entra Connect](active-directory-federation-services)
    - [Microsoft Defender for Identity standalone sensor prerequisites](prerequisites-standalone)
- Trusted root certificates on your machine. If your trusted root CA-signed certificates are missing, you might receive a connection error. For more information, see [Troubleshoot proxy authentication connection errors](../troubleshooting-known-issues#proxy-authentication-problem-presents-as-a-connection-error).

## Download the sensor package

Use **Download onboarding package** to choose the package that matches your deployment:

- **Windows Server 2019 or later**: Sensor v3.x onboarding without Defender for Endpoint deployment for supported domain controllers.
- **Windows Server 2016 or earlier**: Sensor v2.x deployment for supported servers.

To download the sensor installation package:

1. On the **Sensor management** tab of the **On-premises** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/identities, select **Download onboarding package**.
2. In the **Download onboarding package** pane, expand **Windows Server 2016 or earlier**, and save the sensor v2.x installation package locally. The downloaded ZIP file includes the following files:

    - The Defender for Identity sensor installer
    - The configuration setting file with the required information to connect to the Defender for Identity cloud service
    - [Npcap OEM version 1.0](https://npcap.com/), automatically installed during the sensor installation

    [![Screenshot of the Download onboarding package pane with Windows Server 2019 or later and Windows Server 2016 or earlier options.](media/activate-sensor/sensor-deployment-package-options.png)](media/activate-sensor/sensor-deployment-package-options.png#lightbox)
3. Copy the **Access key** value, and save it in a secure location. The access key is a one-time password used to deploy the sensor. After deployment, the sensor uses certificates for authentication and TLS encryption.

    Tip

    We recommend regenerating the access key using the **Regenerate key** button regularly. It won't affect any previously deployed sensors, because it's only used for initial registration of the sensor.
4. Copy the downloaded installation package to the dedicated server or domain controller where you're installing the Defender for Identity sensor.

    Note

    To download the installation package behind a firewall or proxy server, make sure you allow network traffic to the following FQDNs through TCP/443.

    - sensorpackage-prd.mdi.securitycenter.microsoft.com
    - sensorpackage-fm.mdi.securitycenter.microsoft.us
    - sensorpackage-ff.mdi.securitycenter.microsoft.us

## Install the v2.x sensor in the Defender portal

Perform the following steps on the domain controller, Active Directory Federation Services (AD FS) server, Active Directory Certificate Services (AD CS) server, or Microsoft Entra Connect server.

1. Verify that the machine has connectivity to the relevant [Defender for Identity cloud service endpoints](configure-proxy#enable-access-to-defender-for-identity-service-urls-in-the-proxy-server).
2. Extract the installation files from the .zip file. Installing directly from the .zip file fails.
3. Run **Azure ATP sensor setup.exe** with elevated privileges (**Run as administrator**) and follow the setup wizard.
4. On the **Welcome** page, select your language and then select **Next**.

    ![Screenshot of the Welcome page showing language selection for the Defender for Identity sensor installation wizard.](../media/sensor-install-language.png)

    The installation wizard automatically checks if the server is a domain controller, an AD FS server, an AD CS server, or a dedicated server. The server type determines the sensor type:

    - If the server is a domain controller, AD FS server, or AD CS server, the Defender for Identity sensor is installed.
    - If the server is dedicated, the Defender for Identity standalone sensor is installed.

    For example, the wizard displays the following page to indicate that a Defender for Identity sensor is installed on domain controllers.

    ![Screenshot of the deployment type page showing that the Defender for Identity sensor is selected for installation on a domain controller.](../media/sensor-install-deployment-type.png)
5. Select **Next**.

    The wizard issues a warning if the domain controller, AD FS server, AD CS server, or dedicated server doesn't meet the minimum hardware requirements for the installation.

    The warning doesn't prevent you from selecting **Next** and proceeding with the installation, which might still be the right option. For example, you need less room for data storage when you're installing a small lab test environment.

    For production environments, we highly recommend working with the [Defender for Identity sizing tool](capacity-planning) to make sure your domain controllers or dedicated servers meet the capacity requirements.
6. On the **Configure the sensor** page, enter the following information for the setup package:

    - **Installation path**: The location where the Defender for Identity sensor is installed. By default, the path is `%programfiles%\Azure Advanced Threat Protection sensor`. Leave the default value.
    - **Access key**: The one-time key copied from the **Download onboarding package** pane when you downloaded the sensor package. For details, see Download the sensor package.

    ![Screenshot of the Configure the sensor page showing the Installation path and Access key fields for the Defender for Identity sensor setup package.](../media/sensor-install-config.png)
7. Select **Install**. The following components are installed and configured during the installation of the Defender for Identity sensor:

    - **Defender for Identity sensor service** and **Defender for Identity sensor updater service**
    - **Npcap OEM version 1.0**

        Important

        Npcap OEM version 1.0 is automatically installed if no other version of Npcap is present. If you already have Npcap installed due to other software requirements or for any other reason, ensure that it's version 1.0 or later and that it has the [required settings for Defender for Identity](../technical-faq#how-do-i-download-and-install-or-upgrade-the-npcap-driver).

### Viewing sensor versions

Beginning with sensor version 2.176, when you're installing the sensor from a new package, the version under **Add/Remove Programs** appears with the full number, such as **2.176.x.y**. Previously, the version appeared as the static **2.0.0.0**.

The version shown under **Add/Remove Programs** continues to appear even after the Defender for Identity cloud services run automatic updates.

View the sensor's real version on the Microsoft Defender XDR [sensor settings page](https://security.microsoft.com/settings/identities?tabid=sensor), in the executable path or in the file version.

## Perform a Defender for Identity silent installation

The Defender for Identity silent installation for sensors is configured to automatically restart the server at the end of the installation, if necessary.

Schedule a silent installation only during a maintenance window. Because of a Windows Installer bug, you can't reliably use the `norestart` flag to make sure the server doesn't restart.

To track your deployment progress, monitor the Defender for Identity installer logs in `%localappdata%\Temp`.

### Silent installation via a deployment system

When you're silently deploying a Defender for Identity sensor via System Center Configuration Manager or another software deployment system, we recommend that you create two deployment packages:

- .NET Framework 4.7 or later, which might include restarting the domain controller
- The Defender for Identity sensor

Make the Defender for Identity sensor package dependent on the deployment of the .NET Framework package deployment. If necessary, get the [.NET Framework 4.7 offline deployment package](https://support.microsoft.com/topic/the-net-framework-4-7-offline-installer-for-windows-f32bcb33-5f94-57ce-6120-62c9526a91f2).

### Commands for running a silent installation

Use the following commands to perform a fully silent installation of the Defender for Identity sensor, by using the access key that you copied when you downloaded the sensor package.

#### cmd.exe syntax

Use the following cmd.exe syntax for a silent installation:

```cmd
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

#### PowerShell syntax

If you're launching the installer from PowerShell, use the following syntax for the same silent installation command:

```powershell
.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

Note

When you're using the PowerShell syntax, omitting the `.\` preface results in an error that prevents silent installation.

#### Installation options

The following table lists the available installation options for a silent installation.

| Name | Syntax | Mandatory for silent installation? | Description |
| --- | --- | --- | --- |
| `Quiet` | `/quiet` | Yes | Runs the installer without displaying UI or prompts. |
| `Help` | `/help` | No | Provides help and quick reference. Displays the correct use of the setup command, including a list of all options and behaviors. |
| `NetFrameworkCommandLineArguments="/q"` | `NetFrameworkCommandLineArguments="/q"` | Yes | Specifies the parameters for the .NET Framework installation. Must be set to enforce the silent installation of .NET Framework. |

#### Installation parameters

The following table describes the available installation parameters for a silent installation.

| Name | Syntax | Mandatory for silent installation? | Description |
| --- | --- | --- | --- |
| `InstallationPath` | `InstallationPath=""` | No | Sets the path for the installation of Defender for Identity sensor binaries. Default path: `%programfiles%\Azure Advanced Threat Protection Sensor`. |
| `AccessKey` | `AccessKey="\*\*"` | Yes | Sets the access key that's used to register the Defender for Identity sensor with the Defender for Identity workspace. |
| `AccessKeyFile` | `AccessKeyFile=""` | No | Sets the workspace access key from the provided text file path. |
| `DelayedUpdate` | `DelayedUpdate=true` | No | Sets the sensor's update mechanism to delay the update for 72 hours from the official release of each service update. For more information, see [Delayed sensor update](../sensor-settings#delayed-update-for-sensor-v2x). |
| `LogsPath` | `LogsPath=""` | No | Sets the path for the Defender for Identity sensor logs. Default path: `%programfiles%\Azure Advanced Threat Protection Sensor`. |

#### Examples

The following examples show common silent installation commands.

Use the following command to silently install the Defender for Identity sensor with the access key passed directly on the command line:

```cmd
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<access key value>"
```

Alternatively, use the following command to read the access key from a text file, which avoids exposing the key in process history:

```cmd
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKeyFile="C:\Path\myAccessKeyFile.txt"
```

### Command for running a silent installation with a proxy configuration

The following syntax shows the optional proxy parameters you can include when running a silent installation. Values in brackets are optional:

```cmd
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]`
```

Note

If you previously configured your proxy by using legacy options, including WinINet or a registry key update, you need to make any changes with the same method that you used originally. For more information, see [Change proxy configuration using legacy methods](configure-proxy#change-proxy-configuration-using-legacy-methods).

#### Proxy installation parameters

The following table lists the proxy-related installation parameters.

| Name | Syntax | Mandatory for silent installation? | Description |
| --- | --- | --- | --- |
| `ProxyUrl` | `ProxyUrl="http://proxy.contoso.com:8080"` | No | Specifies the proxy URL and port number for the Defender for Identity sensor. |
| `ProxyUserName` | `ProxyUserName="Contoso\ProxyUser"` | No | If your proxy service requires authentication, define a username in the `DOMAIN\user` format. |
| `ProxyUserPassword` | `ProxyUserPassword="P@ssw0rd"` | No | Specifies the password for your proxy username. The Defender for Identity sensor encrypts credentials and stores them locally. |

Tip

If you need to update your proxy settings later on, use PowerShell or the Azure CLI. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy). We recommend that you create and use a custom DNS A record for the proxy server. You can then use that record to change the proxy server's address when necessary and use the *hosts* file for testing.