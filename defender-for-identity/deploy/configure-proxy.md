---
layout: Conceptual
title: Connect to the Defender for Identity service - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/configure-proxy
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
description: Learn how to set up your firewall or proxy to allow communication between the Microsoft Defender for Identity cloud service and Microsoft Defender for Identity sensors.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: sfi-ropc-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: cfde0370-bbe4-0923-33d8-40f4b22a7fd2
document_version_independent_id: cfde0370-bbe4-0923-33d8-40f4b22a7fd2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/configure-proxy.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/configure-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/configure-proxy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
platformId: 212e2b87-cf51-9144-7b2f-d1b7b1a81e5c
---

# Connect to the Defender for Identity service - Microsoft Defender for Identity | Microsoft Learn

Each Microsoft Defender for Identity sensor requires internet connectivity to the Defender for Identity cloud service to report sensor data and operate successfully.

In some organizations, the domain controllers aren't directly connected to the internet, but are connected through a web proxy connection, and SSL inspection and intercepting proxies are not supported for security reasons. In such cases, your proxy server must allow sensor traffic to pass directly from the Defender for Identity sensors to the required Defender for Identity service URLs without interception.

Important

Microsoft does not provide a proxy server. This article describes how to ensure that the required URLs are accessible via a proxy server that you configure.

## Enable access to Defender for Identity service URLs in the proxy server

To ensure maximal security and data privacy, Defender for Identity uses certificate-based, mutual authentication between each Defender for Identity sensor and the Defender for Identity cloud back-end. SSL inspection and interception are not supported, because these proxy behaviors interfere in the certificate-based mutual authentication process.

To enable access to Defender for Identity, make sure to allow traffic to the sensor URL, using the following syntax: `<your-workspace-name>sensorapi.atp.azure.com`. For example, `contoso-corpsensorapi.atp.azure.com`.

- To get your workspace name, see the [Defender for Identity settings page](https://security.microsoft.com/settings/identities) in the Microsoft Defender portal.
- If your proxy or firewall uses explicit allowlists, we also recommend ensuring that the following URLs are allowed:

    - `crl.microsoft.com`
    - `ctldl.windowsupdate.com`
    - `www.microsoft.com/pkiops/*`
    - `www.microsoft.com/pki/*`
- Occasionally, the Defender for Identity service IP addresses may change. If you manually configure IP addresses, or if your proxy automatically resolves DNS names to their IP address and uses them, we recommend that you periodically check that the configured IP addresses are still up-to-date.
- If you've previously configured your proxy using legacy options, including WiniNet or a registry key update, you'll need to make any changes using the method you used originally. For more information, see Change proxy configuration using legacy methods.

### Enable access with a service tag

Instead of manually enabling access to specific endpoints, download the [Azure IP Ranges and Service Tags - Public Cloud](https://www.microsoft.com/download/details.aspx?id=56519), and use the IP address ranges in the **AzureAdvancedThreatProtection** Azure service tag to enable access to Defender for Identity.

For more information, see [Virtual network service tags](/en-us/azure/virtual-network/service-tags-overview). For US Government offerings, see [Get started with US Government offerings](../us-govt-gcc-high).

## Change proxy configuration using the CLI

You can use the CLI to set or clear the sensor's proxy configuration by running the deployment executable directly.

**Prerequisites**: Locate the `Microsoft.Tri.Sensor.Deployment.Deployer.exe` file. This file is located together with the sensor installation. By default, this location is `C:\Program Files\Azure Advanced Threat Protection Sensor\version number\`

Use the deployment executable to configure an authenticated proxy for the current Defender for Identity sensor. This approach is useful during installation or when PowerShell cmdlets aren't available.

**To change the current sensor's proxy configuration**:

```cmd
Microsoft.Tri.Sensor.Deployment.Deployer.exe ProxyUrl="http://myproxy.contoso.local" ProxyUserName="CONTOSO\myProxyUser" ProxyUserPassword="myPr0xyPa55w0rd"
```

The command uses the following parameters:

| Parameter | Description |
| --- | --- |
| `ProxyUrl` | The URL of the proxy server, including the protocol and port. For example, `http://myproxy.contoso.local`. |
| `ProxyUserName` | The user name for authenticating to the proxy server, in `DOMAIN\username` format. |
| `ProxyUserPassword` | The password for the proxy user account. |

**To remove the current sensor's proxy configuration entirely**:

To remove any proxy settings configured through the deployment tool and return the sensor to direct connectivity, run the following command:

```cmd
Microsoft.Tri.Sensor.Deployment.Deployer.exe ClearProxyConfiguration
```

## Change proxy configuration using PowerShell

**Prerequisites**: Before running Defender for Identity PowerShell commands, make sure that you've downloaded the [Defender for Identity PowerShell module](https://www.powershellgallery.com/packages/DefenderForIdentity/).

You can view and change the proxy configuration for your sensor using PowerShell. To do so, sign into your sensor server and run commands as shown in the following examples:

**To view the current sensor's proxy configuration**:

```powershell
Get-MDISensorProxyConfiguration
```

**To change the current sensor's proxy configuration**:

```powershell
Set-MDISensorProxyConfiguration -ProxyUrl 'http://proxy.contoso.com:8080'
```

The preceding command sets the proxy configuration for the Defender for Identity sensor to use the specified proxy server without any credentials.

**To remove the current sensor's proxy configuration entirely**:

```powershell
Clear-MDISensorProxyConfiguration
```

For more information, see the following [DefenderForIdentity PowerShell references](/en-us/powershell/defenderforidentity/overview-defenderforidentity):

- [Get-MDISensorProxyConfiguration](/en-us/powershell/module/defenderforidentity/get-mdisensorproxyconfiguration)
- [Set-MDISensorProxyConfiguration](/en-us/powershell/module/defenderforidentity/set-mdisensorproxyconfiguration)
- [Clear-MDISensorProxyConfiguration](/en-us/powershell/module/defenderforidentity/clear-mdisensorproxyconfiguration)

## Change proxy configuration using legacy methods

If you'd previously configured your proxy settings via either WinINet or a registry key and need to update them, you'll need to use the matching method: update WinINet settings through WinINet, or update registry-based settings through the registry.

While configuring your proxy from the command line during installation ensures that only the Defender for Identity sensor services communicate through the proxy, using WinINet or a registry allow other services running under the LocalSystem or LocalService accounts to also direct traffic through the proxy.

### Configure a proxy server using WinINet

When configuring the proxy using WinINet, keep in mind that the embedded Defender for Identity sensor service runs in system context using the **LocalService** account, and that the Defender for Identity Sensor updater service runs in the system context using **LocalSystem** account.

- If you use WinHTTP for proxy configuration, you still need to configure Windows Internet (WinINet) browser proxy settings for communication between the sensor and the Defender for Identity cloud service.
- If you're using Transparent proxy or WPAD in your network topology, you don't need to configure WinINet for your proxy.

### Configure a proxy server using the registry

The following procedure describes how to configure a static proxy server manually by using a registry-based static proxy.

Important

Configuring a proxy via the registry affects all applications that use WinINet with the **LocalService** and **LocalSystem** accounts, including Windows services.

Apply registry changes only to the **LocalService** and **LocalSystem** accounts.

To configure your proxy, copy your proxy configuration in user context to the **LocalSystem** and **LocalService** accounts as follows:

1. Back up your registry keys.
2. In the registry, search for the `DefaultConnectionSettings` value as `REG_BINARY`, under the `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key, and copy it.
3. If the `LocalSystem` doesn't have the correct proxy settings, copy the proxy setting from the `Current_User` to the `LocalSystem`, under the `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key.

    Make sure to paste the value from the `Current_User`'s `DefaultConnectionSettings` registry key as `REG_BINARY`.

    This may happen if your proxy settings aren't configured, or if they're different from the `Current_User`.
4. If the `LocalService` doesn't have the correct proxy settings, then copy the proxy setting from the `Current_User` to the `LocalService`, under the `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registry key.

    Make sure to paste the value from the `Current_User`'s `DefaultConnectionSettings` registry key as `REG_BINARY`.