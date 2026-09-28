---
layout: Conceptual
title: Configure proxy connectivity for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-proxy-internet
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure proxy connectivity for Microsoft Defender for Endpoint sensors and Microsoft Defender Antivirus on Windows devices.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-09-22T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 8d5f6697-ce0d-25b6-7ca5-57c2931711a0
document_version_independent_id: 8d5f6697-ce0d-25b6-7ca5-57c2931711a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-proxy-internet.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-proxy-internet
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-proxy-internet.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 341b787d-f299-8172-4038-22181cc74376
---

# Configure proxy connectivity for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on Windows uses separate proxy settings for the endpoint detection and response (EDR) sensor and Microsoft Defender Antivirus. When devices must use a proxy to reach their respective cloud services, use this guidance to configure automatic discovery, component-specific static proxy settings, or a system-wide WinHTTP proxy. The guidance also covers proxy configuration for devices that use the Microsoft Monitoring Agent (MMA).

Important

Defender for Endpoint requires IPv4 connectivity. For an IPv6-only network, use a transition mechanism such as DNS64/NAT64 to provide end-to-end IPv4 connectivity. For more information, see [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements#ip-stack).

Configure separate proxy settings for the following components:

- [Endpoint detection and response (EDR) sensor](configure-proxy-internet#configure-the-proxy-server-manually-using-a-registry-based-static-proxy-setting).
- [Microsoft Defender Antivirus](configure-proxy-internet#configure-a-static-proxy-for-microsoft-defender-antivirus).

Use the proxy guidance for the operating system that you manage:

- For Windows devices, use [Configure device proxy and internet connectivity settings](configure-proxy-internet), beginning with Choose a Windows proxy configuration method.
- For Linux devices, see [Configure Microsoft Defender for Endpoint on Linux for static proxy discovery](linux-static-proxy-configuration).
- For macOS devices, see [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac-prerequisites#network-connectivity).

## Choose a Windows proxy configuration method

The Defender for Endpoint sensor runs in the `LocalSystem` context and uses Windows HTTP Services (WinHTTP) to report sensor data and communicate with Defender for Endpoint. The WinHTTP configuration is independent of Windows Internet (WinINet) proxy settings. For more information, see [WinINet versus WinHTTP](/en-us/windows/win32/wininet/wininet-vs-winhttp).

Tip

If you use forward proxies as a gateway to the internet, you can use network protection to [investigate connection events that occur behind forward proxies](investigate-behind-proxy).

Use one of the following proxy configuration methods:

- **Automatic discovery**:

    - Transparent proxy.
    - Web Proxy Auto-Discovery Protocol (WPAD).

    If your network uses a transparent proxy or WPAD, the sensor doesn't require a component-specific static proxy setting.
- **EDR sensor static proxy**: Configure `TelemetryProxyServer` through Group Policy when the sensor can't use automatic discovery or the system-wide WinHTTP proxy.
- **System-wide WinHTTP proxy**: Configure a static proxy by using `netsh winhttp`. This setting affects all applications and services that use the default WinHTTP proxy configuration. A system-wide static proxy is best suited to devices in a stable network topology.

Microsoft Defender Antivirus uses separate proxy policies for cloud-delivered protection. Configure those policies in Configure a static proxy for Microsoft Defender Antivirus.

## Configure an EDR sensor static proxy by using Group Policy

Configure a registry-based static proxy when the EDR sensor can't connect directly or use proxy discovery. Enter only the proxy host and port in `TelemetryProxyServer`. Don't include spaces.

Note

Install the latest Defender for Endpoint updates before you configure the static proxy.

Configure both settings in the Group Policy object (GPO) that applies to the target devices.

1. On your Group Policy management computer, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console).
2. In the GPMC console tree, expand **Group Policy Objects** in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Data Collection and Preview Builds**.
5. Open **Configure Authenticated Proxy usage for the Connected User Experience and Telemetry Service**, select **Enabled**, and then select **Disable Authenticated Proxy usage**.

    [![Screenshot of the Group Policy setting that disables authenticated proxy usage for telemetry.](media/atp-gpo-proxy1.png)](media/atp-gpo-proxy1.png#lightbox)
6. Open **Configure connected user experiences and telemetry**, enter the proxy as `<server-name-or-ip>:<port>`, and then select **OK**.

    [![Screenshot of the Group Policy setting for the telemetry proxy server address and port.](media/atp-gpo-proxy2.png)](media/atp-gpo-proxy2.png#lightbox)

The policies configure the following registry values:

| Group Policy | Registry path | Registry value | Value data |
| --- | --- | --- | --- |
| Configure authenticated proxy usage for the Connected User Experience and Telemetry service | `HKLM\Software\Policies\Microsoft\Windows\DataCollection` | `DisableEnterpriseAuthProxy` | `1` (`REG_DWORD`) |
| Configure connected user experiences and telemetry | `HKLM\Software\Policies\Microsoft\Windows\DataCollection` | `TelemetryProxyServer` | `<server-name-or-ip>:<port>` (`REG_SZ`), for example, `10.0.0.6:8080` |

Note

Don't deploy `TelemetryProxyServer` through mobile device management (MDM). The EDR sensor reads `TelemetryProxyServer` from the Group Policy registry location.

On devices that can't use the default WinHTTP proxy for certificate revocation lists or Windows Update, set `PreferStaticProxyForHttpRequest` to `1` to make a compatible EDR sensor prefer `TelemetryProxyServer`. Create the value under `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`.

The following command creates the registry value:

```dos
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection" /v PreferStaticProxyForHttpRequest /t REG_DWORD /d 1 /f
```

`PreferStaticProxyForHttpRequest` applies to supported sensor branches beginning with MsSense.exe version `10.8210.*` or `10.8049.*`. It doesn't apply to the previous MMA-based solution.

## Configure Microsoft Defender Antivirus proxy settings

Microsoft Defender Antivirus [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus) provides near-instant, automated protection against new and emerging threats. Cloud connectivity is required for [custom indicators](indicators-overview) when Microsoft Defender Antivirus is your active anti-malware solution. It's also required for [endpoint detection and response (EDR) in block mode](edr-in-block-mode), which provides a fallback when a non-Microsoft solution doesn't block a threat.

Note

Prefer a system-wide WinHTTP proxy that allows Windows to retrieve certificate revocation lists. If that configuration isn't possible, setting `SSLOptions` to `2` under `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\Spynet` disables certificate revocation checks for Microsoft Defender Antivirus cloud protection. Disabling revocation checks reduces certificate-validation protection and isn't a best practice. For the available values and risks, see [Configure and validate Microsoft Defender Antivirus network connections](configure-network-connections-microsoft-defender-antivirus).

Microsoft Defender Antivirus caches the last known working proxy. Don't use TLS inspection for Defender cloud connections because inspection breaks the secure connection.

Microsoft Defender Antivirus doesn't use the static proxy to connect to Windows Update or Microsoft Update for downloading updates. Instead, it uses a system-wide proxy when configured to use Windows Update, or it uses the configured internal update source according to the [Microsoft Defender Antivirus protection update fallback order](manage-protection-updates-microsoft-defender-antivirus).

### Configure proxy settings by using Group Policy

Use the procedure in [Configure Microsoft Defender Antivirus using Group Policy](use-group-policy-microsoft-defender-antivirus#configure-microsoft-defender-antivirus-using-group-policy) to open and edit a GPO that applies to the target devices. Then, configure the proxy-specific policy:

1. In the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus**.
2. Open **Define proxy server for connecting to the network**, select **Enabled**, and define the proxy server. Include `http://` or `https://`. Keep the Defender Antivirus platform current as described in [Manage Microsoft Defender Antivirus updates](microsoft-defender-antivirus-updates).

    [![Screenshot of the Microsoft Defender Antivirus policy for defining a proxy server.](media/proxy-server-mdav.png)](media/proxy-server-mdav.png#lightbox)

The policy creates the `ProxyServer` string value under `HKLM\Software\Policies\Microsoft\Windows Defender`. Use the following format:

`<protocol>://<server-name-or-ip>:<port>`

For example, `http://10.0.0.6:8080`.

To use a proxy auto-configuration (PAC) file, configure **Define proxy auto-config (.pac) for connecting to the network**. To bypass the proxy for specific destinations, configure **Define addresses to bypass proxy server**.

### Configure proxy settings by using PowerShell

Use Microsoft Defender Antivirus cmdlets in an elevated PowerShell session on the local device (a PowerShell window you opened by selecting **Run as administrator**).

- **Configure a static proxy server or a PAC file**:

    - **Configure a static proxy server**: Use the following syntax:

        ```powershell
        Set-MpPreference -ProxyServer "<protocol>://<server-name-or-ip>:<port>"
        ```

        For example:

        ```powershell
        Set-MpPreference -ProxyServer "http://10.0.0.6:8080"
        ```
    - **Configure a PAC file**: Use the following syntax\*\*:

        ```powershell
        Set-MpPreference -ProxyPacUrl "<pac-file-url>"
        ```

        For example:

        ```powershell
        Set-MpPreference -ProxyPacUrl "https://proxy.contoso.com/proxy.pac"
        ```
- **Bypass the proxy for specific destinations**: Use the following syntax:

    ```powershell
    Set-MpPreference -ProxyBypass "<address-1>","<address-2>"
    ```

    For example:

    ```powershell
    Set-MpPreference -ProxyBypass "intranet.contoso.com","updates.fabrikam.com"
    ```
- **Verify the configuration**:

    ```powershell
    Get-MpPreference | Select-Object ProxyServer, ProxyPacUrl, ProxyBypass
    ```

For more information, see [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](microsoft-defender-antivirus-using-powershell) and [**Set-MpPreference**](/en-us/powershell/module/defender/set-mppreference).

## Configure a system-wide static proxy by using `netsh`

On devices in a stable network topology, open Command Prompt by selecting **Run as administrator**, and use `netsh winhttp` to configure a system-wide static proxy.

Note

The configuration affects all applications and Windows services that use the default WinHTTP proxy configuration.

Use the following syntax:

```dos
netsh winhttp set proxy <proxy>:<port>
```

The following example configures the proxy server at `10.0.0.6` to use port `8080`:

```dos
netsh winhttp set proxy 10.0.0.6:8080
```

To remove the current WinHTTP proxy configuration and return to direct connectivity, run the following command:

```cmd
netsh winhttp reset proxy
```

To display the current configuration, configure bypass addresses, or use advanced WinHTTP proxy settings, see [netsh winhttp](/en-us/windows-server/administration/windows-commands/netsh-winhttp). For general `netsh` conventions, see [Netsh command syntax, contexts, and formatting](/en-us/windows-server/networking/technologies/netsh/netsh-contexts).

## Configure proxy settings for devices that use MMA

Windows 8.1 devices remain dependent on MMA for Defender for Endpoint. Windows 7 SP1, Windows Server 2008 R2 SP1, Windows Server 2012 R2, and Windows Server 2016 devices should use the newer Defender for Endpoint agent. For migration guidance, see [Update MMA on Windows devices](update-agent-mma-windows).

For Windows 8.1 and any other devices that temporarily continue to use MMA, configure a system-wide proxy, or configure MMA to connect through a proxy or Log Analytics gateway:

- **Proxy**: [Configure the Log Analytics agent to use a proxy](/en-us/azure/azure-monitor/agents/log-analytics-agent#proxy-configuration).
- **Gateway**: [Download the Log Analytics gateway](/en-us/azure/azure-monitor/platform/gateway#download-the-log-analytics-gateway).

For onboarding guidance, see [Onboard previous versions of Windows](onboard-downlevel).