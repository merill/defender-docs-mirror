---
layout: Conceptual
title: Offboard Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-off-board-endpoints
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Describes how to offboard Linux servers from Microsoft Defender for Endpoint and optionally uninstall the agent.
ms.service: defender-endpoint
ms.subservice: linux
ms.topic: article
author: paulinbar
ms.author: painbar
ms.reviewer: gopkr, pahuijbr, megphapriya
audience: ITPro
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
search.appverid: met150
ms.date: 2026-08-11T00:00:00.0000000Z
locale: en-us
document_id: e2822fd1-f801-b9bd-7498-736dd2d9762f
document_version_independent_id: e2822fd1-f801-b9bd-7498-736dd2d9762f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-off-board-endpoints.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-off-board-endpoints
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-off-board-endpoints.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 13431c11-40c2-ba2d-2130-0e028bc17899
---

# Offboard Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

This article is intended for IT administrators and security professionals who need to offboard or uninstall Microsoft Defender for Endpoint from Linux servers. It explains the difference between offboarding and uninstalling, helps you decide which option is right for your scenario, and provides step-by-step instructions for each method. It also describes how offboarded and uninstalled devices appear in the Microsoft Defender portal.

## Overview

When you offboard a device from Defender for Endpoint or uninstall the Defender application, no new detections, vulnerability, or security data are sent to the Microsoft Defender portal. Seven days after offboarding a device, its sensor health state changes to [inactive](fix-unhealthy-sensors#inactive-devices). Past data, such as alerts, vulnerabilities, and the device timeline, for an offboarded or uninstalled device remains visible in the Microsoft Defender portal until the [configured retention period](data-storage-privacy#data-retention) expires. You also see the device profile (without data) in the device inventory for up to 180 days. Devices that weren't active within the past 30 days are not factored into your organization's [exposure score](/en-us/defender-vulnerability-management/tvm-exposure-score).

To view data for active devices only, you can use filters, such as [sensor health state](machines-view-overview#apply-filters), [device tags](machine-tags), or [device groups](machine-groups).

## What is the difference between offboarding and uninstalling?

There are important differences between offboarding and uninstalling:

- Offboarding disconnects a device from the Defender service so it stops sending security data while leaving the agent installed.
- Uninstalling removes the Defender for Endpoint software and services from the device entirely and stops sending security data.

## How to choose between offboarding and uninstalling

- **Offboard** when you want to temporarily stop Defender from communicating with the Defender service while keeping the Defender application installed on the Linux server. This option is recommended if you plan to reenable Defender later without reinstalling the agent. For example, you might want to offboard if you need to troubleshoot an issue with the Defender application, or if you want to temporarily stop Defender while performing maintenance on the server.
- **Uninstall** when you want to completely remove the Defender application from the Linux server, for example, when changing the installation ring (Prod/Insider Slow/Insider Fast), or when you no longer plan to use Microsoft Defender on the device.

## How do offboarded and uninstalled devices behave?

After a device has been successfully offboarded or uninstalled, the Defender application behaves as follows:

- It stops sending telemetry (such as alerts and vulnerabilities) to the Microsoft Defender portal.
- It becomes unlicensed and nonfunctional.
- Security policies applied through Microsoft Defender are removed.

## How do offboarded and uninstalled devices appear in the Defender portal?

- The sensor health state of the offboarded or uninstalled device changes to *Inactive* after seven days of no telemetry.
- Offboarded and uninstalled devices remain visible for up to 180 days. For more information about data retention, see [Microsoft Defender for Endpoint data storage and privacy](data-storage-privacy).
- Historical data (alerts, timeline, software inventory) remains accessible during the retention period.
- No explicit *Offboarded* or *Uninstalled* label is shown in the portal. To distinguish between offboarded or uninstalled devices and ones that are merely disconnected or inactive, we recommend adding a tag to the device before offboarding or uninstalling it. This makes it easier to identify and filter those devices later.

## Offboard a device

Three methods are available to offboard a Linux server from Microsoft Defender for Endpoint:

- Offboard using a script.
- Offboard using an offboarding JSON file.
- Offboard using the API.

All methods achieve the same result, so you can choose the one that best fits your scenario.

### Offboard using a script

1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, under **System**, choose **Settings** &gt; **Endpoints**, and then, under **Device management**, choose **Offboarding**.
3. Select **Linux Server** as the operating system, and then in the **Deployment method** section, choose **Local script**.
4. Select **Download package** and then select **Download**. The zipped folder that is downloaded is named *WindowsDefenderATPOffboardingPackage\_valid\_until\_YYYY-MM-DD.zip* (where YYYY-MM-DD is the expiry date of the package).
5. On your Linux server, extract the contents of the ZIP file to a local directory.
6. Open a terminal, and navigate to the directory where the *MicrosoftDefenderATPOffboardingLinuxServer\_valid\_until\_YYYY-MM-DD* file is located.
7. Type `sudo python3 MicrosoftDefenderATPOffboardingLinuxServer_valid_until_YYYY-MM-DD.py` in the terminal. This runs the offboarding script, which offboards the device from Microsoft Defender for Endpoint.

### Offboard using an offboarding JSON file

Note

This method can be performed either manually or automatically using your preferred Linux configuration management tool.

1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, under **System**, choose **Settings** &gt; **Endpoints**, and then, under **Device management**, choose **Offboarding**.
3. Select **Linux Server** as the operating system, and then in the **Deployment method** section, choose your preferred Linux configuration management tool.
4. Select **Download package** and then select **Download**. The zipped folder is named *WindowsDefenderATPOffboardingPackage\_valid\_until\_YYYY-MM-DD.zip* (where YYYY-MM-DD is the expiry date of the package).
5. Extract the contents of the ZIP file and locate the *mdatp\_offboard.json* file.
6. Copy *mdatp\_offboard.json* to the following location on the Linux server: `/etc/opt/microsoft/mdatp/mdatp_offboard.json`

### Offboard using the API

Use the [Offboard machine API](api/offboard-machine-api) to automate offboarding a Linux server from Defender for Endpoint.

## Uninstall the Defender application from a Linux server

Two methods are available to uninstall the Defender application from a Linux server: Uninstall using the Defender deployment tool (Recommended) or manual uninstallation. Both methods achieve the same result, so you can choose the one that best fits your scenario.

### Uninstall using Defender deployment tool (Recommended)

This is the recommended method, as it allows you to uninstall the Defender application in a single step.

1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, under **System**, choose **Settings** &gt; **Endpoints**, and then, under **Device management**, choose **Onboarding**.
3. Select **Linux Server** as the operating system.
4. Go to Defender deployment tool as the deployment method and select **Download package** (a ZIP file is downloaded).
5. Extract the package and run the following command. This removes the Defender application and cleans up the repository:

    ```bash
    ./defender_deployment_tool.sh --remove --clean 
    ```

### Manual uninstallation

To manually remove the Defender application and clean up the repository, run one of the following commands (whichever is appropriate, depending on your Linux distribution):

**Red Hat Enterprise Linux (RHEL) and variants (CentOS and Oracle Linux)**

```bash
sudo yum remove mdatp
```

or

```bash
sudo dnf remove mdatp
```

**SUSE Linux Enterprise Server (SLES) and variants**

```bash
sudo zypper remove mdatp
```

**Ubuntu and Debian**

```bash
sudo apt-get purge mdatp
```

**Mariner**

```bash
sudo dnf remove mdatp
```

## How to verify a device's offboarding state

To verify a device's offboarding state, run the following command:

```bash
mdatp health --field health_issues
```

Expected output

```console
ATTENTION: No license found. Contact your administrator for help. ["missing license"]
```

The Defender application remains installed on the device unless it's manually uninstalled.