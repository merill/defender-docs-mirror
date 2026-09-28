---
layout: Conceptual
title: Microsoft Defender for Endpoint on macOS prerequisites - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint-mac-prerequisites
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: joshbregman
description: Review the licensing, supported macOS versions, permissions, management, and network requirements for Microsoft Defender for Endpoint on macOS.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: article
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: b9062c36-f8cc-40f4-5cdb-28ccfe8988e6
document_version_independent_id: b9062c36-f8cc-40f4-5cdb-28ccfe8988e6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-endpoint-mac-prerequisites.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-endpoint-mac-prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-endpoint-mac-prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9fbf49cd-7e0b-b703-5e00-27ff07ae953d
---

# Microsoft Defender for Endpoint on macOS prerequisites - Microsoft Defender for Endpoint | Microsoft Learn

Review these requirements before you deploy [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac). Security and IT administrators can use this article to prepare supported macOS devices, required permissions, device management, licensing, and network connectivity.

> 
> Important
> 
> If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).
> 
> You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Product and administrator requirements

- A Defender for Endpoint subscription.
- Access to the Microsoft Defender portal at https://security.microsoft.com.
- A supported macOS device that meets the system requirements.
- Network connectivity to the Defender for Endpoint service.
- For a managed deployment, access to a mobile device management (MDM) solution and permission to deploy apps and device configuration profiles.
- For a manual deployment, local administrator privileges on the macOS device.

## System requirements

Defender for Endpoint supports the three most recent major macOS releases:

- 27 (Golden Gate).
- 26 (Tahoe).
- 15 (Sequoia).

Note

Beta versions of macOS aren't supported. New major macOS releases are supported from the first day that Apple makes the release generally available.

The macOS device must meet these hardware requirements:

- **Processor**: Intel 64-bit (x64) or Apple silicon (ARM64).
- **Disk space**: 1 GB.

Important

Keep [System Integrity Protection](https://support.apple.com/HT204899) (SIP) enabled. SIP is enabled by default and helps prevent low-level changes to macOS.

## System extensions and macOS permissions

Defender for Endpoint uses the following system extensions:

| Extension | Bundle identifier | Function |
| --- | --- | --- |
| Endpoint Security extension | `com.microsoft.wdav.epsext` | Monitors files, processes, and system events for real-time protection. |
| Network extension | `com.microsoft.wdav.netext` | Inspects network traffic for network protection, web content filtering, and custom indicators. |

On macOS 11 (Big Sur) and later, system extensions require approval before they can run. For managed deployments, use device-level MDM configuration profiles to preapprove the extensions and required permissions. For manual deployments, a local administrator approves the requests in macOS.

In addition to system extension approval, the Defender for Endpoint deployment includes profiles or local approval for:

- Network content filtering.
- Full Disk Access.
- Background services on applicable macOS versions.
- Notifications.

Microsoft Purview features can require more permissions, including:

- Accessibility.
- Bluetooth access when you use Bluetooth-based Device Control policies.

For troubleshooting, see [Troubleshoot system extension issues](mac-support-sys-ext).

## Deployment method requirements

Choose a method in [Deploy Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos). The exact requirements depend on whether you use MDM or install Defender for Endpoint manually.

### Managed deployment requirements

For a managed deployment, the MDM solution must support the following capabilities:

- Deploy the signed Defender for Endpoint `.pkg` installation package without repackaging it.
- Deploy device-level Apple configuration profiles to managed macOS devices.
- Deploy the onboarding profile that associates the device with your organization.
- Assign the app and profiles to the required device groups.

Support for running an administrator-configured script or command is recommended for collecting status and automating maintenance or removal tasks.

Use [Microsoft Intune](mac-install-with-intune), [Jamf Pro](mac-install-with-jamf), or [another MDM solution](mac-install-with-other-mdm) for a managed deployment. [Security settings management](/en-us/intune/intune-service/protect/mde-security-integration) can manage supported security settings on onboarded devices, but it doesn't install the Defender for Endpoint app or replace the initial onboarding process.

### Manual deployment requirements

A manual deployment requires local administrator privileges to install the app, install the onboarding configuration profile, and approve macOS system extensions and permissions. Use [manual deployment](mac-install-manually) for an individual evaluation or test device. Use MDM to apply and maintain settings on centrally managed production devices.

## Licensing requirements

The available features depend on your Defender for Endpoint subscription. This article applies to the subscriptions listed in the article metadata. For current product entitlements and device limits, see [Microsoft Defender licensing guidance](https://www.microsoft.com/licensing/guidance/microsoft-defender).

Note

A user subscription license lets your organization protect up to five client or mobile devices assigned to the licensed user. Server operating systems require server-based licensing.

For the announcement that introduced Defender for Endpoint Plan 1 availability with Microsoft 365 E3, see [Microsoft Defender for Endpoint Plan 1 availability](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/microsoft-defender-for-endpoint-plan-1-now-included-in-m365-e3/ba-p/3060639). Check current licensing guidance before making purchase or deployment decisions.

## Network connectivity

macOS devices must connect to Defender for Endpoint cloud services. Before onboarding, [configure your network environment for Defender for Endpoint connectivity](configure-environment). For Streamlined connectivity, allow `*.endpoint.security.microsoft.com`, the supporting service dependencies in the applicable URL list, and the required SSL/TLS inspection exclusions.

Streamlined connectivity on macOS requires Defender for Endpoint version `101.23102.*` (November 2023) or later.

Defender for Endpoint on macOS supports the following proxy configurations:

- Proxy Auto-Configuration (PAC).
- Web Proxy Autodiscovery Protocol (WPAD).
- Manual static proxy configuration.

Connections to Defender for Endpoint service URLs originate from the operating system or Defender services. Configure the proxy to allow these connections without authentication.

Warning

Authenticated proxies aren't supported. SSL/TLS inspection and intercepting proxies are also unsupported. Configure the proxy or network security product to pass Defender for Endpoint traffic directly to the required service URLs without inspection.

### Test network connectivity before deployment

Before onboarding, run the [Defender for Endpoint Client Analyzer](overview-client-analyzer) to assess device prerequisites and network connectivity. The analyzer can run on a supported macOS device before or after onboarding.

As a supplementary check, open `https://x.cp.wd.microsoft.com/api/report` and `https://cdn.x.cp.wd.microsoft.com/ping` in a browser. These endpoints don't represent the complete list required for Standard or Streamlined connectivity.

To test the same two endpoints from Terminal, run the following command:

```bash
curl -w ' %{url_effective}\n' 'https://x.cp.wd.microsoft.com/api/report' 'https://cdn.x.cp.wd.microsoft.com/ping'
```

The command should return the following results:

```console
OK https://x.cp.wd.microsoft.com/api/report
OK https://cdn.x.cp.wd.microsoft.com/ping
```

### Test connectivity after installation

After you install Defender for Endpoint, run the following command in Terminal to test all configured service connections:

```bash
mdatp connectivity test
```