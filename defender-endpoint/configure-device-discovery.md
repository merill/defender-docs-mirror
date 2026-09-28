---
layout: Conceptual
title: Configure device discovery in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-device-discovery
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender for Endpoint device discovery modes, scanner devices, exclusions, monitored networks, and advanced hunting queries.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-09-21T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 64c2c539-1a99-1de5-99a1-a09fb4cb78eb
document_version_independent_id: 64c2c539-1a99-1de5-99a1-a09fb4cb78eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-device-discovery.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-device-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-device-discovery.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 40fda8ee-456e-4727-0d9e-b2998749c5b5
---

# Configure device discovery in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

You can configure [device discovery](device-discovery) to identify unmanaged devices on your organization's networks, assess their security posture, and determine which devices need protection. Choose basic or standard discovery, select the onboarded devices that perform active scans, exclude sensitive targets, and manage monitored networks.

Before you begin, review the supported operating systems and required permissions in Prerequisites.

## Prerequisites

Make sure your environment meets the following requirements:

- A Microsoft Defender for Endpoint Plan 2 subscription.
- Onboarded scanning devices that run a [supported operating system](device-discovery#supported-operating-systems).
- An account with permission to manage Defender for Endpoint security settings. For more information, see [Permission options](user-roles#permission-options).
- Device tags assigned to the scanner devices if you plan to limit standard discovery to tagged devices.

## Set up device discovery

On the **Device discovery** page in the Microsoft Defender portal at https://security.microsoft.com/settings/device-discovery, configure the discovery mode:

1. Under **Discovery mode**, select one of the following options:

    - **Standard discovery (recommended)**: Uses passive observation, common discovery protocols, multicast queries, and active scanning to provide a more complete device inventory.
    - **Basic**: Passively observes network traffic without actively probing devices. Use this mode for sensitive or legacy networks where active scanning isn't appropriate.
2. If you select standard discovery, choose which onboarded devices perform active scans:

    - **All devices (recommended)**: Use all onboarded devices that support device discovery.
    - **Select tags**: Use only devices with the selected device tags. This option is useful when you want scanner devices in specific network segments.
3. Select **Save**.

Tip

Standard discovery is the default and recommended mode because it provides richer device details. You can switch to basic discovery when active probing isn't appropriate. For more information, see [Discovery modes and scans](device-discovery#discovery-modes-and-scans).

## Control which devices perform standard discovery

The devices selected in [Set up device discovery](configure-device-discovery#set-up-device-discovery) act as scanners for standard discovery:

- Select **All devices (recommended)** to use every onboarded device that supports device discovery.
- Select **Select tags** to use only onboarded devices with the specified tags. Onboarded devices outside the selected tags continue to perform basic discovery.

## Exclude devices from standard discovery

Exclude IP addresses or subnets when active scanning could interfere with sensitive devices, network lures, or other security tools. Exclusions stop active scans but don't prevent passive or multicast discovery.

To exclude a device:

1. On the **Device discovery** page in the Microsoft Defender portal at https://security.microsoft.com/settings/device-discovery, select **Exclusions**.
2. Select **Add exclusion**.
3. On the **Add exclusion** page, enter the IP address or subnet to exclude from standard scans.
4. Enter a description for the exclusion.
5. Select **Save**.

The exclusion appears in the **Exclusions** list. Select an exclusion to view, edit, or delete it.

Note

- Excluded devices might still reply to multicast discovery attempts in the network. These devices are discovered but aren't actively scanned.
- Passive discovery can identify any device that communicates with an onboarded device on a monitored network. Exclusions apply only to active standard-discovery scans.

## View and manage monitored networks

The **Monitored networks** tab lists networks detected by onboarded devices and shows whether device discovery monitors or ignores each network.

By default, Defender for Endpoint automatically monitors networks identified as corporate and ignores noncorporate networks. The page displays up to 50 networks, sorted by the number of devices seen on each network during the previous seven days.

For information about how Defender for Endpoint identifies corporate networks, see [Monitored networks](device-discovery#monitored-networks).

### Manage monitored networks

You can override the automatically assigned monitoring state for a network. Before monitoring a network identified as noncorporate, confirm that your organization has permission to discover devices on that network.

On the **Device discovery** page in the Microsoft Defender portal at https://security.microsoft.com/settings/device-discovery, select **Monitored networks**, select the three-dot menu next to the network, and select one of the following options:

| Option | Description | Result |
| --- | --- | --- |
| **Monitor this network** | Monitors a network that Defender for Endpoint doesn't monitor automatically. | Device discovery can identify devices outside your corporate network, including home or other noncorporate devices. |
| **Ignore this network from monitoring** | Stops monitoring and discovering devices on the network. | Previously discovered devices remain in inventory but aren't updated. Their details remain until the Defender for Endpoint data-retention period expires. |
| **Automatically monitor** | Uses the Defender for Endpoint corporate-network classification to determine whether to monitor the network. | Networks identified as corporate are monitored automatically. |

Important

Monitoring a network that Defender for Endpoint identifies as noncorporate can discover home or other noncorporate devices. Confirm that you have permission to discover devices on the network before you monitor it.

### Filter network list

On the **Monitored networks** tab, select **Filter**, select **Network monitor state**, choose one of the following states, and then select **Apply**:

- **Monitored**: Networks where device discovery is active.
- **Ignored**: Networks where device discovery isn't active.
- **All**: Monitored and ignored networks.

## Review and assess devices

To review and assess non-onboarded devices, and to find other device details, see [Review and assess devices](assess-devices).

## Disable device discovery

On the **Other options** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, set **Device discovery** to **Off**, and then select **Save preferences**. For more information about the setting, see [Advanced features](advanced-features).

Disabling device discovery stops Defender for Endpoint from discovering devices on your networks. The network detection and response sensor process, `SenseNDR.exe`, continues to run on onboarded devices.

## Troubleshoot device discovery

If you encounter issues with device discovery or authenticated network scans, see [Troubleshoot device discovery and authenticated network scans](troubleshoot-device-discovery-network-scans).

## Explore devices in the network

Use the `DeviceNetworkInfo` table to identify onboarded devices that connected to a network shown in the Monitored networks list during the previous seven days. For table and column details, see the [DeviceNetworkInfo table reference](/en-us/defender-xdr/advanced-hunting-devicenetworkinfo-table).

```kusto
DeviceNetworkInfo
| where Timestamp > ago(7d)
| where ConnectedNetworks  != ""
| extend ConnectedNetworksExp = parse_json(ConnectedNetworks)
| mv-expand bagexpansion = array ConnectedNetworks=ConnectedNetworksExp
| extend NetworkName = tostring(ConnectedNetworks ["Name"]), Description = tostring(ConnectedNetworks ["Description"]), NetworkCategory = tostring(ConnectedNetworks ["Category"])
| where NetworkName == "<your network name here>"
| summarize arg_max(Timestamp, *) by DeviceId
```

### Get information about a device

Use the `DeviceInfo` table to return the latest available record for each device ID associated with a specified device name. You can use the returned device IDs and platform details in subsequent hunting queries. For table and column details, see the [DeviceInfo table reference](/en-us/defender-xdr/advanced-hunting-deviceinfo-table).

```kusto
DeviceInfo
| where DeviceName == "<device name here>" and isnotempty(OSPlatform)
| summarize arg_max(Timestamp, *) by DeviceId
```