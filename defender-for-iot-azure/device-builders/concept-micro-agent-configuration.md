---
layout: Conceptual
title: Micro agent configurations - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-micro-agent-configuration
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: The collector sends all current data immediately after any configuration change is made. The configuration changes are then applied.
ms.date: 2022-05-03T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 19dc6bf0-e069-16fd-a6a7-e50e5fbef35e
document_version_independent_id: ce028cf9-d16d-a66f-0e51-0f18c6776e02
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-micro-agent-configuration.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-micro-agent-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-micro-agent-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 33d9e551-ce3f-ab58-4878-7b44860fabd6
---

# Micro agent configurations - Microsoft Defender for IoT | Microsoft Learn

This article describes the different types of configurations that the micro agent supports. Customers can configure the micro agent to fit the needs of their devices, and network environments.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

The micro agent's behavior is configured by a set of module twin properties. You can configure the micro agent to best suit your needs. For example, you can turn off certain events to minimize power consumption, and reduce other resource usage.

After any change in configuration, the collector will immediately send all unsent event data. After the data is sent, the changes will be applied, and collectors will be restarted as needed.

## General configuration

Define the frequency in which messages are sent for each priority level. All values are required.

Default values are as follows:

| Frequency | Time period (in minutes) |
| --- | --- |
| **Low** | 1440 (24 hours) |
| **Medium** | 120 (2 hours) |
| **High** | 30 (.5 hours) |

To reduce resource consumption on the device, each priority should be set as a multiple of the one below it. For example, High: 60 minutes, Medium: 120 minutes, Low: 480 minutes.

The syntax for configuring the frequencies is as follows:

`"CollectorsCore_PriorityIntervals"` : `"<High>,<Medium>,<Low>"`

For example:

`"CollectorsCore_PriorityIntervals"` : `"30,120,1440"`

## Collector types and properties

Configure the micro agent using the following collector-specific properties and settings:

### Baseline collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Baseline\_Disabled** | `True`/`False` | Disables the Baseline collector. | `False` |
| **Baseline\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Baseline events. | `Low` |
| **Baseline\_GroupsDisabled** | A list of Baseline group names, separated by a comma. For example: `Time Synchronization, Network Parameters Host` | Defines the full list of Baseline group names that should be disabled. | `Null` |
| **Baseline\_ChecksDisabled** | A list of Baseline check IDs, separated by a comma. For example: `3.3.5,2.2.1.1` | Defines the full list of Baseline check IDs that should be disabled. | `Null` |

### System Information collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **SystemInformation\_Disabled** | `True`/`False` | Disables the System Information collector. | `False` |
| **SystemInformation\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send System Information events. | `Low` |
| **SystemInformation\_HardwareVendor** | string | Set hardware vendor information. | `None` |
| **SystemInformation\_HardwareModel** | string | Set hardware model information. | `None` |
| **SystemInformation\_HardwareSerialNumber** | string | Set hardware serial number information. | `None` |
| **SystemInformation\_FirmwareVendor** | string | Set firmware vendor information. | `None` |
| **SystemInformation\_FirmwareVersion** | string | Set firmware version information. | `None` |

### SBoM collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **SBoM\_Disabled** | `True`/`False` | Disables the SBoM collector. | `False` |
| **SBoM\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send SBoM events. | `Low` |

### Heartbeat collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Heartbeat\_Disabled** | `True`/`False` | Disables sending the Heartbeat event. | `False` |
| **Heartbeat\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Heartbeat events. | `Low` |

### Login collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Login\_Disabled** | `True`/`False` | Disables the Login collector. | `False` |
| **Login\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Login events. | `Medium` |
| **Login\_UsePAM** | `True`/`False` | Use a PAM module to gather login events. Without PAM, the agent uses a combination of reading UTMP and Syslog to gather login events. If the system doesn't have UTMP or Syslog enabled, using PAM is an option, but will require additional configuration to work properly. For more information, see [Configure Pluggable Authentication Modules (PAM) to audit sign-in events](configure-pam-to-audit-sign-in-events) | `False` |

### IoT Hub module-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **IothubModule\_MessageTimeout** | Positive integer, including limits | Defines the number of minutes to retain messages in the outbound queue to the IoT Hub, after which point the messages are dropped. | `2880` (=2 days) |

### Network Activity collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **NetworkActivity\_Disabled** | `True`/`False` | Disables the Network Activity collector. | `False` |
| **NetworkActivity\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Network Activity events. | `Medium` |
| **NetworkActivity\_Devices** | A list of the network devices separated by a comma. For example `eth0,eth1` | Defines the list of network devices (interfaces) that the agent will use to monitor the traffic. If a network device isn't listed, the network raw events won't be recorded for the missing device. | `eth0` |
| **NetworkActivity\_CacheSize** | Positive integer | The number of Network Activity events (after aggregation) to keep in the cache between send intervals. Beyond that number, older events will be dropped (lost). | `256` |
| **NetworkActivity\_PacketBufferSize** | Positive integer | Configure the buffer size (in bytes) that will be used to capture packets for a single device per direction (incoming or outcoming traffic). | `2097152 (=2MB)` |

### Process collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Process\_Disabled** | `True`/`False` | Disables the Process collector. | `False` |
| **Process\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Process events. | `Medium` |
| **Process\_PollingInterval** | Positive Integer | Defines the polling interval in microseconds. This value is used when the **Process\_Mode** is in `Polling` mode. | `100000` (=0.1 second) |
| **Process\_Mode** | `1` = Auto `2` = Netlink `3`= Polling | Determines the Process collector mode. In `Auto` mode, the agent first tries to enable the Netlink mode. If that fails, it will automatically fall back / switch to the Polling mode. | `1` |
| **Process\_CacheSize** | Positive integer | The number of Process events (after aggregation) to keep in the cache between send intervals. Beyond that number, older events will be dropped (lost). | `256` |

### Log collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **LogCollector\_Disabled** | `True`/`False` | Disables the Logs collector. | `False` |
| **LogCollector\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send Log events. | `Low` |

### File system collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **FileSystem\_Disabled** | `True`/`False` | Disables the file system collector. | `False` |
| **FileSystem\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send file system events. | `Low` |
| **FileSystem\_Recursive** | `True`/`False` | If set to true, monitors all directories under the given path. | `True` |
| **FileSystem\_Paths** | Paths to monitor.  For example: `/path/to/monitor`, `/another/path/to/monitor` | Defines which paths to monitor, more than one path can be monitored. | `Null` |
| **FileSystem\_CacheSize** | Positive integer | The number of File system events (after aggregation) to keep in the cache between send intervals. Beyond that number, older events will be dropped (lost). | `256` |

### Peripheral collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Peripheral\_Disabled** | `True`/`False` | Disables the peripheral collector. | `False` |
| **Peripheral\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send peripheral events. | `Low` |
| **Peripheral\_CacheSize** | Positive integer | The number of peripheral events (after aggregation) to keep in the cache between send intervals. Beyond that number, older events will be dropped (lost). | `256` |

### Statistics collector-specific settings

| Setting Name | Setting options | Description | Default |
| --- | --- | --- | --- |
| **Statistics\_Disabled** | `True`/`False` | Disables the statistics collector. | `False` |
| **Statistics\_MessageFrequency** | `Low`/`Medium`/`High` | Defines the frequency in which to send statistics events. | `Low` |
| **Statistics\_CacheSize** | Positive integer | The number of statistics events (after aggregation) to keep in the cache between send intervals. Beyond that number, older events will be dropped (lost). | `256` |