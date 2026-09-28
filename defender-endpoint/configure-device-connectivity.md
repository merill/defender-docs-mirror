---
layout: Conceptual
title: Onboard devices using streamlined connectivity for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-device-connectivity
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure streamlined connectivity and onboard devices to Microsoft Defender for Endpoint by using consolidated domains or static IP ranges.
author: paulinbar
ms.author: painbar
ms.date: 2026-09-21T00:00:00.0000000Z
ms.topic: how-to
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.reviewer: pahuijbr
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 548311a0-c395-cb47-54db-365168968197
document_version_independent_id: 548311a0-c395-cb47-54db-365168968197
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-device-connectivity.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-device-connectivity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-device-connectivity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: c78fa359-7ad1-ae02-60de-6251cc3fbf17
---

# Onboard devices using streamlined connectivity for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

You can use streamlined device connectivity to onboard devices to Microsoft Defender for Endpoint through a consolidated domain or static IP ranges. Streamlined connectivity reduces the number of network destinations required for core Defender for Endpoint services. Devices might still require supporting endpoints for operating system services, updates, and deployment tools. Before you begin, verify the component and operating system requirements in Prerequisites.

This article describes the requirements and process for onboarding new devices. To update devices that are already onboarded, see [Migrate devices to streamlined connectivity](migrate-devices-streamlined).

## Understand the Defender for Endpoint-recognized simplified domain

Defender for Endpoint uses the following consolidated domains for streamlined connectivity:

- **Commercial environments**: `*.endpoint.security.microsoft.com`
- **US Government environments (Preview)**: `*.endpoint.security.microsoft.us`

The applicable domain consolidates connections to the following core Defender for Endpoint services:

- Cloud-delivered protection
- Malware sample submission storage
- Automated investigation and remediation sample storage
- Defender for Endpoint command and control
- Defender for Endpoint cyber and diagnostic data

For the complete network configuration process and current destination lists, see [Configure network connectivity to Microsoft Defender for Endpoint](configure-environment).

For network devices that don't support wildcard-based rules, you can instead configure dedicated Defender for Endpoint static IP ranges. For more information, see Configure connectivity using static IP ranges.

Note

- Streamlined connectivity **doesn't change Defender for Endpoint functionality or the user experience**. It changes only the URLs or IP addresses that devices use to connect to the service.
- There are no plans to deprecate the standard service URLs. Devices onboarded with standard connectivity continue to function. For future services, maintain access to `*.endpoint.security.microsoft.com` for commercial environments or `*.endpoint.security.microsoft.us` for US Government environments (Preview).
- Service connections use certificate pinning and TLS. Traffic inspection is not supported. Connections are device-initiated, not user-initiated. Enforcing proxy (user) authentication breaks connectivity.

## Prerequisites

Before you use streamlined connectivity, verify that devices meet the following component and operating system requirements.

### Minimum component versions

- Defender for Endpoint sensor (SENSE): `10.8040.*` (March 2022) or later. For the corresponding Windows updates, see the minimum update table in this section.
- Microsoft Defender Antivirus antimalware client: `4.18.2211.5` (November 2022) or later.
- Microsoft Defender Antivirus engine: `1.1.19900.2` (November 2022) or later.
- Microsoft Defender Antivirus security intelligence: `1.391.345.0` (June 2023) or later.
- Defender for Endpoint on macOS and Linux: `101.24022.*` (March 2024) or later.

### Supported operating systems

The following operating systems support streamlined connectivity:

- Windows 11.
- Windows 10, version 1809 (October 2018) or later.
- Windows 10, versions 1607 (August 2016) to 1803 (April 2018). These versions support the streamlined onboarding package but require the longer URL list in [Microsoft Defender for Endpoint streamlined connectivity URLs for commercial environments](streamlined-device-connectivity-urls-commercial).
- Windows Server 2019 (November 2018) and later.
- Windows Server 2016 and Windows Server 2012 R2 when fully updated and running the Defender for Endpoint modern unified solution, which is installed through a Windows Installer (`.msi`) package.
- [Supported macOS versions](microsoft-defender-endpoint-mac) running Defender for Endpoint version `101.24022.*` (March 2024) or later.
- [Supported Linux versions](microsoft-defender-endpoint-linux) running Defender for Endpoint version `101.24022.*` (March 2024) or later.
- Azure Stack HCI OS, version 23H2 (February 2024) or later.

Important

- Devices that use Microsoft Monitoring Agent (MMA) don't support streamlined connectivity and must continue to use standard connectivity. These devices include Windows 7, Windows 8.1, Windows Server 2008 R2 with MMA, and Windows Server 2012 R2 (October 2013) or Windows Server 2016 (October 2016) that haven't been upgraded to the modern unified solution.
- Upgrade Windows Server 2012 R2 and Windows Server 2016 to the modern unified solution before you use streamlined connectivity.

| Windows operating system | Minimum update or requirement |
| --- | --- |
| Windows 11 (October 2021) | KB5011493 (March 8, 2022) |
| Windows 10, version 1809 (October 2018); Windows Server 2019 (November 2018) | KB5011503 (March 8, 2022) |
| Windows 10, version 1909 (November 2019) | KB5011485 (March 8, 2022) |
| Windows 10, versions 20H2 (October 2020) and 21H2 (November 2021) | KB5011487 (March 8, 2022) |
| Windows 10, version 22H2 (October 2022) | KB5020953 (October 28, 2022) |
| Windows 10, version 1803 (April 2018) | End of service |
| Windows 10, version 1709 (October 2017) | End of service |
| Windows Server 2022 (August 2021) | KB5011497 (March 8, 2022) |
| Windows Server 2012 R2 (October 2013) and Windows Server 2016 (October 2016) | Modern unified solution |

## Streamlined connectivity process

The following illustration shows the stages for configuring and using streamlined connectivity:

![Diagram of the four-stage streamlined connectivity process, from network configuration through device onboarding.](media/streamlined-connectivity-process.png)

### Stage 1. Configure your network environment for cloud connectivity

After you confirm that devices meet the prerequisites, follow [Configure network connectivity to Microsoft Defender for Endpoint](configure-environment). Use the streamlined URL list for your cloud environment, and retain all supporting endpoints required for the operating system, update method, deployment method, and enabled features.

The consolidated domain (`*.endpoint.security.microsoft.com` or `*.endpoint.security.microsoft.us`) replaces the standard URLs only for the core Defender for Endpoint services listed earlier. Review the [streamlined connectivity URL list](streamlined-device-connectivity-urls-commercial#common-endpoints) for update, certificate validation, operating system, and scenario-specific dependencies. For example, Linux devices that use the Defender deployment tool also require the [deployment tool download endpoint](linux-install-with-defender-deployment-tool#prerequisites-and-system-requirements).

Choose one of the following options to configure connections to core Defender for Endpoint services:

- Option 1: Use the simplified domain
- Option 2: Use static IP ranges

#### Option 1: Configure connectivity using the simplified domain

Configure your environment to allow connections to the consolidated Defender for Endpoint domain:

- For commercial devices: `*.endpoint.security.microsoft.com`
- For US government devices (Preview): `*.endpoint.security.microsoft.us`

For configuration instructions, see [Configure network connectivity to Microsoft Defender for Endpoint](configure-environment).

Maintain connectivity with the supporting services listed in the [Microsoft Defender for Endpoint streamlined connectivity URLs for commercial environments](streamlined-device-connectivity-urls-commercial#common-endpoints) or [Microsoft Defender for Endpoint streamlined connectivity URLs for government environments](streamlined-device-connectivity-urls-gov). Depending on the operating system, features, deployment method, and update method, these services can include certificate revocation lists, Windows Update, SmartScreen, Linux product repositories, and scenario-specific download endpoints.

#### Option 2: Configure connectivity using static IP ranges

If your network devices don't support wildcard-based rules, use the dedicated static IP ranges as an alternative to the consolidated domain. The `MicrosoftDefenderForEndpoint` service tag covers the following services:

- Microsoft Active Protection Service (MAPS)
- Malware Sample Submission Storage
- Automated investigation and remediation sample storage
- Defender for Endpoint command and control

Important

If you use static IP ranges, you must also allow the `OneDsCollector` service tag for Defender for Endpoint cyber and diagnostic data. The `MicrosoftDefenderForEndpoint` service tag doesn't include this traffic. Maintain access to all other required services, including SmartScreen, certificate revocation lists, Windows Update, and applicable supporting endpoints.

Use the following Azure service tags to keep the IP ranges current. For the latest ranges, see [Azure IP ranges](https://azureipranges.azurewebsites.net/).

| Service tag name | Defender for Endpoint services included |
| --- | --- |
| `MicrosoftDefenderForEndpoint` | Cloud-delivered protection, malware sample submission storage, automated investigation and remediation sample storage, and Defender for Endpoint command and control. |
| `OneDsCollector` | Defender for Endpoint cyber and diagnostic data. Traffic under this service tag isn't limited to Defender for Endpoint and can include diagnostic data for other Microsoft services. |

For the latest list of Azure service tags, including the Defender for Endpoint-related tags listed in the preceding table, refer to the [Azure service tags](/en-us/azure/virtual-network/service-tags-overview) documentation.

Important

Defender for Endpoint processes and stores data according to the geographic location identified when your organization is provisioned. Based on the device location, traffic might flow through any associated IP region, which corresponds to an Azure datacenter region. For more information, see [Data storage and privacy](data-storage-privacy).

### Stage 2. Configure your devices to connect to Defender for Endpoint service

Configure devices to use your proxy or other connectivity infrastructure. For operating system-specific proxy configuration methods, see [Configure device proxy and internet connection settings](configure-proxy-internet).

### Stage 3. Verify client connectivity pre-onboarding

Use the [Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer) to verify connectivity before onboarding. For the complete procedure, see [Verify client connectivity](verify-connectivity).

On Windows, run the analyzer from the `MDEClientAnalyzer` folder by using one of the following methods:

- Run `mdeclientanalyzer.cmd -o <path to onboarding cmd file>`. The analyzer reads the geographic parameters from the streamlined onboarding script and tests the applicable destinations.
- Run `mdeclientanalyzer.cmd -g US`, `mdeclientanalyzer.cmd -g EU`, or `mdeclientanalyzer.cmd -g UK` to test the specified region without an onboarding script.

As a supplementary check, you can use the [Microsoft Defender for Endpoint Client Analyzer preview](https://aka.ms/MDEClientAnalyzerPreview) to test whether a device meets the prerequisites.

Note

On devices that aren't onboarded, the Client Analyzer tests the standard URL set by default. To test streamlined connectivity, use the `-o` switch with the onboarding script or the `-g` switch with the `US`, `EU`, or `UK` region value.

### Stage 4. Apply the new onboarding package required for streamlined connectivity

After you configure and verify the required connections, download a streamlined onboarding package:

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, confirm that the devices meet the streamlined connectivity prerequisites.
2. For **Step 1: Select an operating system to start deployment**, select the operating-system version group for the devices. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
3. For **Connectivity type**, select **Streamlined**.
4. Select the deployment method, and download the onboarding package.
5. Follow the applicable onboarding article:

    - [Onboard to Microsoft Defender for Endpoint](onboarding)
    - [Onboard client devices running Windows or macOS](onboard-client)
    - [Onboard servers through Microsoft Defender for Endpoint's onboarding experience](onboard-server)
    - [Run a detection test on a device to verify it has been properly onboarded to Microsoft Defender for Endpoint](run-detection-test)
6. Exclude the devices from existing onboarding policies that use the standard onboarding package.

To update devices that are already onboarded, see [Migrate devices to streamlined connectivity](migrate-devices-streamlined). Follow the operating-system-specific restart guidance in that article after you apply the streamlined package.