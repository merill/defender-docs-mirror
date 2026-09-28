---
layout: Conceptual
title: Configure network connectivity to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-environment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure firewall and proxy access for Microsoft Defender for Endpoint service URLs, including streamlined and standard connectivity.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: pahuijbr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-09-21T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 440c7274-8fd3-0587-9b46-d2af3555fa50
document_version_independent_id: 440c7274-8fd3-0587-9b46-d2af3555fa50
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-environment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-environment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-environment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 3d712430-7f9c-8dc0-ecf1-fc2c516feb68
---

# Configure network connectivity to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Before you onboard devices to Microsoft Defender for Endpoint, configure firewall or proxy access to the required service URLs. Allow outbound connections, and bypass HTTPS inspection for streamlined connectivity. This article identifies the URL lists to use and includes proxy and firewall requirements for older Windows devices that use Microsoft Monitoring Agent (MMA).

For streamlined connectivity, exclude traffic to `*.endpoint.security.microsoft.com` from SSL/TLS inspection, HTTPS interception, and man-in-the-middle (MITM) proxying. If you enable SSL inspection, Defender for Endpoint sensors might fail to communicate with backend services, resulting in onboarding or connectivity failures.

Note

- Starting May 8, 2024, [streamlined connectivity](https://aka.ms/MDE-streamlined-urls) is the default onboarding method. On the **Optional features** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, use the **Default to streamlined connectivity when onboarding devices in Defender portal** setting to choose whether onboarding uses streamlined or standard connectivity. For onboarding through Microsoft Intune or Microsoft Defender for Cloud, set the **Apply streamlined connectivity settings to devices managed by Intune and Defender for Cloud** setting to ![](media/toggle-on.png)**On**. This setting applies to newly onboarded devices. Existing devices aren't reonboarded automatically. To migrate existing devices, see [Migrate devices to use the streamlined connectivity method](migrate-devices-streamlined).
- For current and future functionality, devices must be able to reach the consolidated domain for their cloud environment, even if they use standard connectivity:

    - `*.endpoint.security.microsoft.com` for commercial environments.
    - `*.endpoint.security.microsoft.us` for US Government environments (Preview).
- New regions default to streamlined connectivity and can't downgrade to standard connectivity. For more information, see [Onboarding devices using streamlined connectivity for Microsoft Defender for Endpoint](configure-device-connectivity).

## Enable access to Microsoft Defender for Endpoint service URLs in the proxy server

The following sections specify the services and associated URLs that devices in your network must be able to connect to. Make sure no firewall or network filtering rules deny access to these URLs. You might need to create an *allow* rule specifically for them.

Streamlined connectivity consolidates core Defender for Endpoint service traffic, but it doesn't replace supporting service dependencies. Review the common endpoints in the applicable streamlined URL list, including operating system, update, certificate validation, and scenario-specific endpoints. For example, the [Defender deployment tool for Linux](linux-install-with-defender-deployment-tool#prerequisites-and-system-requirements) requires a separate download endpoint.

### Streamlined connectivity URL lists

- **Streamlined connectivity for commercial customers**: Use the [streamlined connectivity URLs for commercial customers](streamlined-device-connectivity-urls-commercial).
- **Streamlined connectivity for US Government, GCC, and DoD customers (Preview)**: Use the [streamlined connectivity URLs for government customers](streamlined-device-connectivity-urls-gov).

For the complete list of operating system requirements for streamlined connectivity, see [Streamlined connectivity prerequisites](configure-device-connectivity#prerequisites). The following operating systems and versions are supported:

- Windows 11.
- Windows 10, version 1809 (October 2018) or later.
- Windows Server 2019 or later.
- Windows Server 2016 and Windows Server 2012 R2 running the [Defender for Endpoint modern unified solution](onboard-server), which requires installation through an MSI package.
- Supported macOS versions running Defender for Endpoint version `101.24022.*` (March 2024) or later.
- Supported Linux versions running Defender for Endpoint version `101.24022.*` (March 2024) or later.
- Azure Stack HCI OS, version 23H2 or later.

Streamlined connectivity requires the following minimum component versions:

- Antimalware client: `4.18.2211.5` (November 2022) or later.
- Engine: `1.1.19900.2` (November 2022) or later.
- Security intelligence: `1.391.345.0` (June 2023) or later.
- Cross-platform client: `101.24022.*` (March 2024) or later.
- Defender for Endpoint sensor (SENSE): `10.8040.*` (March 2022) or later.

If you're moving previously onboarded devices to streamlined connectivity, see [Migrate device connectivity](migrate-devices-streamlined).

Windows 10 versions 1607 (August 2016) to 1803 (April 2018) are supported through the streamlined onboarding package but require the longer URL list in the applicable article. These versions don't support reonboarding. You must fully offboard them first.

Devices running Windows 7, Windows 8.1, Windows Server 2008 R2 with Microsoft Monitoring Agent (MMA), or servers that haven't been upgraded to the unified solution must continue using the MMA onboarding method.

### Standard connectivity URL lists

- **Standard connectivity for commercial customers**: Use the [standard connectivity URLs for commercial customers](standard-device-connectivity-urls-commercial). Defender for Endpoint Plan 1 and Plan 2 use the same proxy service URLs. In your firewall, open all URLs where the geography column is `WW`. For other rows, open the URLs for your specific data location. To verify your data location, see [Verify data storage location and update data retention settings for Microsoft Defender for Endpoint](preferences-setup). Don't exclude `*.blob.core.windows.net` from network inspection. Exclude only the Defender for Endpoint blob URLs listed in the URL list.
- **Standard connectivity for US Government, GCC, and DoD customers**: Use the [standard connectivity URLs for government customers](standard-device-connectivity-urls-gov).

Important

- Connections originate from the operating system or Defender client services, so proxies shouldn't require authentication for these destinations. For streamlined connectivity, configure your proxy and network security policies to bypass inspection for `*.endpoint.security.microsoft.com` or `*.endpoint.security.microsoft.us` traffic. Don't scan, inspect, intercept, or use a man-in-the-middle (MITM) proxy for this traffic.
- Microsoft doesn't provide a proxy server. These URLs are accessible via the proxy server that you configure.
- Defender for Endpoint processes data according to the geographic location identified when your tenant is provisioned. Based on the client location, traffic might flow through any associated IP region, which corresponds to an Azure datacenter region. For more information, see [Data storage and privacy](data-storage-privacy).

## Configure proxy and firewall requirements for commercial MMA devices

In commercial environments, allow the following destinations so Defender for Endpoint can communicate through MMA on Windows 7 SP1, Windows 8.1, and Windows Server 2008 R2. For US Government environments, use the MMA destinations in [Microsoft Defender for Endpoint standard connectivity URLs for US Government](standard-device-connectivity-urls-gov).

| Agent destination | Port | Direction | Bypass HTTPS inspection |
| --- | --- | --- | --- |
| `*.ods.opinsights.azure.com` | 443 | Outbound | Yes |
| `*.oms.opinsights.azure.com` | 443 | Outbound | Yes |
| `*.blob.core.windows.net` | 443 | Outbound | Yes |
| `*.agentsvc.azure-automation.net` | 443 | Outbound | Yes |

To determine the exact destinations in use for your subscription within the Log Analytics agent domains in the preceding table, see [Microsoft Monitoring Agent (MMA) Service URL connections](verify-connectivity#microsoft-monitoring-agent-mma-service-url-connections).

Note

MMA-based solutions don't support streamlined connectivity through consolidated URLs or static IP addresses. For Windows Server 2016 and Windows Server 2012 R2, upgrade to the unified solution. To onboard these operating systems with the unified solution, see [Onboard Windows servers](onboard-server). To migrate devices already onboarded through MMA, see [Server migration scenarios in Microsoft Defender for Endpoint](server-migration).

## Connect devices without direct internet access

For devices without a direct internet connection, use a proxy. If your network allows only IP-based rules instead of domain-based rules, configure firewall or gateway devices to allow the required IP ranges. For more information, see [Streamlined device connectivity](configure-device-connectivity).

Important

- Microsoft Defender for Endpoint is a cloud security solution. Devices must connect directly or through a proxy or other network device to Defender cloud services, and Domain Name System (DNS) resolution is always required. A system-wide proxy configuration is recommended.
- Windows clients and Windows Server devices in disconnected environments must be able to update certificate trust lists (CTLs) offline through an internal file or web server.
- For instructions, see [Configure a file or web server to download the CTL files](/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265983%28v=ws.11%29#configure-a-file-or-web-server-to-download-the-ctl-files).