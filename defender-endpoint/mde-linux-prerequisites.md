---
layout: Conceptual
title: Prerequisites for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-linux-prerequisites
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: gopkr, pahuijbr, megphapriya
description: Describes the requirements needed to install and use Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: article
ms.subservice: linux
ms.date: 2026-09-14T00:00:00.0000000Z
locale: en-us
document_id: d63eeebf-b524-81fe-8533-a5d259802002
document_version_independent_id: d63eeebf-b524-81fe-8533-a5d259802002
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-linux-prerequisites.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-linux-prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-linux-prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 423f6db8-50b0-80cc-c47a-b992f9c4b0a2
---

# Prerequisites for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

This article lists the prerequisites for deploying and onboarding Defender for Endpoint on Linux servers.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## License requirements

To onboard servers to Defender for Endpoint, server licenses are required. You can choose from the following options:

- Microsoft Defender for Servers Plan 1 or Plan 2
- Microsoft Defender for Endpoint for servers
- [Microsoft Defender for Business servers](/en-us/defender-business/get-defender-business?tabs=findpartner#how-to-get-microsoft-defender-for-business-servers) (for small and medium-sized businesses only)

To onboard desktops to Defender for Endpoint, choose the following option:

- Microsoft Defender for Endpoint P2 (Also available with Microsoft 365 E5 and Microsoft 365 E7)

For more detailed information about licensing requirements for Microsoft Defender for Endpoint, see [Microsoft Defender for Endpoint licensing information](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#microsoft-defender-for-endpoint).

For detailed licensing information, see [Product Terms: Microsoft Defender for Endpoint](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftDefenderforEndpoint/EAEAS) and work with your account team to learn more about the terms and conditions.

## System requirements

- **CPU**: One CPU core minimum. For high-performance workloads, more cores are recommended.
- **Disk Space**: 2 GB minimum. For high-performance workloads, more disk space might be needed.
- **Memory**: 1 GB of RAM minimum. For high-performance workloads, more memory might be needed.
- For installation at a custom path, refer to [Prerequisites and system requirements for custom location installation](linux-custom-location-installation#prerequisites-and-system-requirements).

Note

Performance tuning might be needed based on workloads. For more information, see [Performance tuning for Microsoft Defender for Endpoint on Linux](linux-support-perf)

## Software requirements

Linux server endpoints should have systemd (system manager) installed.

Note

Linux distributions using system manager support both SystemV and Upstart. The Microsoft Defender for Endpoint on Linux agent is independent from [Operation Management Suite (OMS) agent](/en-us/azure/azure-monitor/agents/azure-monitor-agent-overview#log-analytics-agent). Microsoft Defender for Endpoint relies on its own independent telemetry pipeline.

To use [device isolation functionality](respond-machine-alerts#isolate-devices-from-the-network), the following must be enabled:

- `iptables` and `ip6tables`, or `iptables-nft` and `ip6tables-nft`

## Network requirements

Linux server endpoints should be able to access the endpoints documented in:

- [Microsoft Defender for Endpoint streamlined connectivity URLs - commercial](streamlined-device-connectivity-urls-commercial) (commercial customers)
- [Microsoft Defender for Endpoint streamlined connectivity URLs - US government environments](streamlined-device-connectivity-urls-gov) (US Government customers).

If necessary, [configure static proxy discovery](linux-static-proxy-configuration).

Warning

PAC, WPAD, and authenticated proxies aren't supported. Use only static or transparent proxies. SSL inspection and intercepting proxies aren't supported for security reasons. Configure an exception for SSL inspection and your proxy server to allow direct data pass-through from Defender for Endpoint on Linux to the relevant URLs without interception. Adding your interception certificate to the global store doesn't enable interception.

### Verify if devices can connect to Defender for Endpoint cloud services

1. Prepare your environment, as described in Step 1 of the following article [Configure your network environment to ensure connectivity with Defender for Endpoint service](configure-environment).
2. Connect Defender for Endpoint on Linux through a proxy server by using the following discovery methods:

    - Transparent proxy
    - [Manual static proxy configuration](linux-static-proxy-configuration#installation-time-configuration)
3. Permit anonymous traffic in the previously listed URLs, if a proxy or firewall blocks traffic.

Note

Configuration for transparent proxies isn't needed for Defender for Endpoint. See [Manual Static Proxy Configuration.](linux-static-proxy-configuration)

For troubleshooting steps, see [Troubleshoot cloud connectivity issues for Microsoft Defender for Endpoint on Linux](linux-support-connectivity).

## Supported Linux distributions

Note

**Microsoft Defender for Endpoint now extends support to Linux desktops (Public Preview).** All Linux distributions currently supported on servers are also supported on Linux desktops. Defender support is based on the underlying distribution and kernel version, irrespective of the desktop environment running on top of the distribution. Deployment packages, methods and security capabilities remain the same across both Linux servers and desktops.

Microsoft Defender for Endpoint determines whether a Linux device should be classified as a Server or Workstation by evaluating multiple system and environment attributes in a predefined order. These signals include operating system metadata, distribution-specific product information, subscription and licensing details, system purpose declarations, cloud and vendor metadata, image SKUs, Ubuntu Pro contracts, VMware guest properties, virtual desktop indicators, installation records, and other distribution-specific attributes.

> 
> When the available signals do not conclusively identify a device as a Workstation, Microsoft Defender for Endpoint classifies the device as a Server by default. This behaviour is by design and ensures a deterministic classification when workstation-specific indicators are not present.

The following Linux server distributions are supported on servers and desktops:

| Distribution | x64 (AMD64/EM64T) | ARM64 |
| --- | --- | --- |
| Red Hat Enterprise Linux | 7.2+, 8.x, 9.x, 10.x | 8.x, 9.x, 10.x |
| CentOS | 7.2+, 8.x | - |
| CentOS Stream | 8.x, 9.x, 10.x | 8.x, 9.x, 10.x |
| Ubuntu LTS | 16.04, 18.04, 20.04, 22.04, 24.04, 26.04 | 20.04, 22.04, 24.04, 26.04 |
| Ubuntu Pro | 22.04, 24.04 | 22.04, 24.04 |
| Debian | 9–13 | 11, 12, 13 |
| SUSE Linux Enterprise Server | 12.x, 15.x, 16.x | 15 (SP5, SP6), 16.x |
| openSUSE Leap | 15.6, 16.x | 15.6, 16.x |
| Oracle Linux | 7.2+, 8.x, 9.x, 10.x | 8.x, 9.x, 10.x |
| Amazon Linux | 2, 2023 | 2 (Support retiring 31 October 2026. See notice below.)2023 |
| Fedora | 33–44 | 40–44 |
| Rocky Linux | 8.7+, 9.2+, 10.x | 8.7+, 9.2+, 10.x |
| Alma Linux | 8.4+, 9.2+, 10.x | 8.4+, 9.2+, 10.x |
| Mariner | 2 | 2 |

Important

**Support for Microsoft Defender for Endpoint on Amazon Linux 2 (AL2) running on ARM64 architecture will be deprecated on 31 October 2026**.

The last supported Defender version for AL2 (ARM64) is 101.25122.0004 (expiry 31 October 2026). **After that date, official support for AL2 (ARM64) will end**. Customers are advised to migrate to a supported Linux distribution before this date to ensure continued protection and support.

This change applies only to ARM64-based AL2 machines. **AMD64/x86\_64 architectures are not impacted**.

Note

Distributions and versions that aren't explicitly listed above are unsupported Microsoft Defender for Endpoint is kernel-version agnostic for all other supported distributions and versions. The minimal requirement for the kernel version is `3.10.0-327` or later.

Microsoft Defender for Endpoint on Linux **can be installed and may function** on customized operating systems that meet minimal kernel requirements and are derived from known, standard, vendor‑provided Linux distributions that Microsoft supports. Customers are free to onboard and run Defender for Endpoint on such environments; Microsoft doesn't block onboarding or execution. However, these customized environments aren't part of Microsoft's validated or maintained support baseline. As a result, they're treated as custom OS configurations from a support perspective. Customers are expected to validate Defender for Endpoint within these custom environments and, if needed, reproduce issues on a supported, standard (unmodified) Linux distribution. If an issue can't be reproduced on a supported standard base distribution, Microsoft might not be able to proceed with further investigation or remediation. For full support coverage and a predictable support experience, customers are recommended to run Defender for Endpoint on a supported, vendor-provided Linux distribution as outlined in the official prerequisites.

Warning

Running Defender for Endpoint on Linux alongside other Fanotify-based security solutions isn't supported and may lead to unpredictable behavior, including system hangs. If any applications use Fanotify in blocking mode, they'll appear in the conflicting\_applications field of the mdatp health command output. You can still safely take advantage of Defender for Endpoint on Linux by setting antivirus enforcement level to passive. See [Configure security settings in Microsoft Defender for Endpoint on Linux](linux-preferences). **EXCEPTION:** The Linux `FAPolicyD` feature, which also uses Fanotify in blocking mode, is supported with Defender for Endpoint in active mode on RHEL and Fedora platforms, provided that mdatp health reports a healthy status. This exception is based on validated compatibility specific to these distributions.

## Supported filesystems for real-time protection and quick, full, and custom scans

| Real-time protection and quick/full scans | Custom scans |
| --- | --- |
| `btrfs` | All filesystems that are supported for real-time protection and quick/full scans are also supported for custom scans. In addition, the filesystems listed below are also supported for custom scans. |
| `ecryptfs` | `Efs` |
| `ext2` | `S3fs` |
| `ext3` | `Blobfuse` |
| `ext4` | `Lustre` |
| `fuseblk` | `glusterfs` |
| `jfs` | `Afs` |
| `overlay` | `sshfs` |
| `ramfs` | `cifs` |
| `reiserfs` | `smb` |
| `tmpfs` | `gcsfuse` |
| `udf` | `sysfs` |
| `vfat` | `nfs` (v3) |
| `xfs` | `fuse` |
|  | `nfs4` |

Note

To scan NFS v3 mount points, make sure to set the `no_root_squash` export option. Without this option, scanning NFS v3 can potentially fail due to lack of permissions.

## Roles and permissions

- Administrative privileges on the Linux endpoint are required for installation.
- An appropriate role assigned in Defender for Endpoint. See [Role-based access control](prepare-deployment#role-based-access-control).

## Installation methods and tools

There are several methods and tools that you can use to deploy Microsoft Defender for Endpoint on supported Linux distributions.

It's recommended to use Deployment Tool based deployment, as it simplifies the onboarding process, reduces manual tasks, and supports a wide range of deployment scenarios, including custom installation paths, upgrades, and local repository. All deployment methods apply to servers as well as desktops. For more information, see

- [Deployment tool based deployment (Recommended)](linux-install-with-defender-deployment-tool)
- [Installer script based deployment](linux-installer-script)
- [Ansible based deployment](linux-install-with-ansible)
- [Chef based deployment](linux-deploy-defender-for-endpoint-with-chef)
- [Puppet based deployment](linux-install-with-puppet)
- [SaltStack based deployment](linux-install-with-saltack)
- [Golden Image based deployment](linux-deploy-defender-for-endpoint-using-golden-images)
- [Deployment to a custom location](linux-custom-location-installation)
- [Manual deployment](linux-install-manually)
- [Direct onboarding with Defender for Cloud](/en-us/azure/defender-for-cloud/onboard-machines-with-defender-for-endpoint)
- [Guidance for Defender for Endpoint on Linux endpoints with SAP](mde-linux-deployment-on-sap)

Important

On Linux, Microsoft Defender for Endpoint creates a mdatp user with random UID and GID values. If you want to control these values, create a mdatp user before installation using the `/usr/sbin/nologin` shell option. Here's an example: `mdatp:x:UID:GID::/home/mdatp:/usr/sbin/nologin`.

If you experience any installation issues, self-troubleshooting resources are available. See the links in the Related content section.