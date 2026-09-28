---
layout: Conceptual
title: Privacy for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-privacy
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Privacy controls, how to configure policy settings that impact privacy and information about the diagnostic data that is collected in Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: article
ms.subservice: linux
ms.date: 2024-10-11T00:00:00.0000000Z
locale: en-us
document_id: e70c32ab-e477-9b32-7146-af9694191beb
document_version_independent_id: e70c32ab-e477-9b32-7146-af9694191beb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-privacy.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-privacy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6379321a-ea85-e4bd-ea39-615cbfb64455
---

# Privacy for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft is committed to provide you with the information and controls you need to make choices about how your data is collected and used when you're using Defender for Endpoint on Linux.

This article describes the privacy controls available within the product, how to manage these controls with policy settings, and more details on the data events that are collected.

## Overview of privacy controls in Microsoft Defender for Endpoint on Linux

This section describes the privacy controls for the different types of data that is collected by Defender for Endpoint on Linux.

### Diagnostic data

Diagnostic data is used to keep Defender for Endpoint secure and up to date, detect, diagnose and fix problems, and also make product improvements.

Some diagnostic data is required, while some diagnostic data is optional. We give you the ability to choose whether to send us required or optional diagnostic data by using privacy controls, such as policy settings for organizations.

There are two levels of diagnostic data for Defender for Endpoint client software that you can choose from:

- **Required**: The minimum data necessary to help keep Defender for Endpoint secure, up to date, and performing as expected on the device it's installed on.
- **Optional**: Other data that helps Microsoft make product improvements and provides enhanced information to help detect, diagnose, and remediate issues.

By default, only required diagnostic data is sent to Microsoft.

### Cloud delivered protection data

Cloud delivered protection is used to provide increased and faster protection with access to the latest protection data in the cloud.

Enabling the cloud-delivered protection service is optional, however it's highly recommended because it provides important protection against malware on your endpoints and across your network.

### Sample data

Sample data is used to improve the protection capabilities of the product, by sending Microsoft suspicious samples so they can be analyzed. Enabling automatic sample submission is optional.

There are three levels for controlling sample submission:

- **None**: no suspicious samples are submitted to Microsoft.
- **Safe**: only suspicious samples that don't contain personally identifiable information (PII) are submitted automatically. This is the default value.
- **All**: all suspicious samples are submitted to Microsoft.

## Manage privacy controls with policy settings

If you're an IT administrator, you might want to configure these controls at the enterprise level.

The privacy controls for the various types of data that is described in the preceding section are described in detail in [Set preferences for Defender for Endpoint on Linux](linux-preferences).

As with any new policy settings, you should carefully test them out in a limited, controlled environment to ensure the settings that you configure have the desired effect before you implement the policy settings more widely in your organization.

## Diagnostic data events

This section describes what is considered required diagnostic data and what is considered optional diagnostic data, along with a description of the events and fields that are collected.

### Data fields that are common for all events

There's some information about events that is common to all events, regardless of category or data subtype.

The following fields are considered common for all events:

| Field | Description |
| --- | --- |
| platform | The broad classification of the platform on which the app is running. Allows Microsoft to identify on which platforms an issue may be occurring so that it can correctly be prioritized. |
| machine\_guid | Unique identifier associated with the device. Allows Microsoft to identify whether issues are impacting a select set of installs and how many users are impacted. |
| sense\_guid | Unique identifier associated with the device. Allows Microsoft to identify whether issues are impacting a select set of installs and how many users are impacted. |
| org\_id | Unique identifier associated with the enterprise that the device belongs to. Allows Microsoft to identify whether issues are impacting a select set of enterprises and how many enterprises are impacted. |
| hostname | Local device name (without DNS suffix). Allows Microsoft to identify whether issues are impacting a select set of installs and how many users are impacted. |
| product\_guid | Unique identifier of the product. Allows Microsoft to differentiate issues impacting different flavors of the product. |
| app\_version | Version of the Defender for Endpoint on Linux application. Allows Microsoft to identify which versions of the product are showing an issue so that it can correctly be prioritized. |
| sig\_version | Version of security intelligence database. Allows Microsoft to identify which versions of the security intelligence are showing an issue so that it can correctly be prioritized. |
| supported\_compressions | List of compression algorithms supported by the application, for example `['gzip']`. Allows Microsoft to understand what types of compressions can be used when it communicates with the application. |
| release\_ring | Ring that the device is associated with (for example Insider Fast, Insider Slow, Production). Allows Microsoft to identify on which release ring an issue may be occurring so that it can correctly be prioritized. |

### Required diagnostic data

**Required diagnostic data** is the minimum data necessary to help keep Defender for Endpoint secure, up to date, and perform as expected on the device it's installed on.

Required diagnostic data helps to identify problems with Microsoft Defender for Endpoint that may be related to a device or software configuration. For example, it can help determine if a Defender for Endpoint feature crashes more frequently on a particular operating system version, with newly introduced features, or when certain Defender for Endpoint features are disabled. Required diagnostic data helps Microsoft detect, diagnose, and fix these problems more quickly so the impact to users or organizations is reduced.

#### Software setup and inventory data events

**Microsoft Defender for Endpoint installation / uninstallation**:

The following fields are collected:

| Field | Description |
| --- | --- |
| correlation\_id | Unique identifier associated with the installation. |
| version | Version of the package. |
| severity | Severity of the message (for example Informational). |
| code | Code that describes the operation. |
| text | Additional information associated with the product installation. |

**Microsoft Defender for Endpoint configuration**:

The following fields are collected:

| Field | Description |
| --- | --- |
| antivirus\_engine.enable\_real\_time\_protection | Whether real-time protection is enabled on the device or not. |
| antivirus\_engine.passive\_mode | Whether passive mode is enabled on the device or not. |
| cloud\_service.enabled | Whether cloud delivered protection is enabled on the device or not. |
| cloud\_service.timeout | Time out when the application communicates with the Defender for Endpoint cloud. |
| cloud\_service.heartbeat\_interval | Interval between consecutive heartbeats sent by the product to the cloud. |
| cloud\_service.service\_uri | URI used to communicate with the cloud. |
| cloud\_service.diagnostic\_level | Diagnostic level of the device (required, optional). |
| cloud\_service.automatic\_sample\_submission | Automatic sample submission level of the device (none, safe, all). |
| cloud\_service.automatic\_definition\_update\_enabled | Whether automatic definition update is turned on or not. |
| edr.early\_preview | Whether the device should run EDR early preview features. |
| edr.group\_id | Group identifier used by the detection and response component. |
| edr.tags | User-defined tags. |
| features.[optional feature name] | List of preview features, along with whether they're enabled or not. |

#### Product and service usage data events

**Security intelligence update report**:

The following fields are collected:

| Field | Description |
| --- | --- |
| from\_version | Original security intelligence version. |
| to\_version | New security intelligence version. |
| status | Status of the update indicating success or failure. |
| using\_proxy | Whether the update was done over a proxy. |
| error | Error code if the update failed. |
| reason | Error message if the update failed. |

#### Product and service performance data events for required diagnostic data

**Kernel extension statistics**:

The following fields are collected:

| Field | Description |
| --- | --- |
| version | Version of Defender for Endpoint on Linux. |
| instance\_id | Unique identifier generated on kernel extension startup. |
| trace\_level | Trace level of the kernel extension. |
| subsystem | The underlying subsystem used for real-time protection. |
| ipc.connects | Number of connection requests received by the kernel extension. |
| ipc.rejects | Number of connection requests rejected by the kernel extension. |
| ipc.connected | Whether there's any active connection to the kernel extension. |

#### Support data

**Diagnostic logs**:

Diagnostic logs are collected only with the consent of the user as part of the feedback submission feature. The following files are collected as part of the support logs:

- All files under */var/log/microsoft/mdatp*
- Subset of files under */etc/opt/microsoft/mdatp* that are created and used by Defender for Endpoint on Linux
- Product installation and uninstallation logs under /var/log/microsoft/mdatp/\*.log

### Optional diagnostic data

**Optional diagnostic data** is additional data that helps Microsoft make product improvements and provides enhanced information to help detect, diagnose, and fix issues.

If you choose to send us optional diagnostic data, required diagnostic data is also included.

Examples of optional diagnostic data include data Microsoft collects about product configuration (for example number of exclusions set on the device) and product performance (aggregate measures about the performance of components of the product).

#### Software setup and inventory data events for optional diagnostic data

**Microsoft Defender for Endpoint configuration**:

The following fields are collected:

| Field | Description |
| --- | --- |
| connection\_retry\_timeout | Connection retry time-out when communication with the cloud. |
| file\_hash\_cache\_maximum | Size of the product cache. |
| crash\_upload\_daily\_limit | Limit of crash logs uploaded daily. |
| antivirus\_engine.exclusions[].is\_directory | Whether the exclusion from scanning is a directory or not. |
| antivirus\_engine.exclusions[].path | Path that was excluded from scanning. |
| antivirus\_engine.exclusions[].extension | Extension excluded from scanning. |
| antivirus\_engine.exclusions[].name | Name of the file excluded from scanning. |
| antivirus\_engine.scan\_cache\_maximum | Size of the product cache. |
| antivirus\_engine.maximum\_scan\_threads | Maximum number of threads used for scanning. |
| antivirus\_engine.threat\_restoration\_exclusion\_time | Time out before a file restored from the quarantine can be detected again. |
| antivirus\_engine.threat\_type\_settings | Configuration for how different threat types are handled by the product. |
| filesystem\_scanner.full\_scan\_directory | Full scan directory. |
| filesystem\_scanner.quick\_scan\_directories | List of directories used in quick scan. |
| edr.latency\_mode | Latency mode used by the detection and response component. |
| edr.proxy\_address | Proxy address used by the detection and response component. |

**Microsoft Auto-Update configuration**:

The following fields are collected:

| Field | Description |
| --- | --- |
| how\_to\_check | Determines how product updates are checked (for example automatic or manual). |
| channel\_name | Update channel associated with the device. |
| manifest\_server | Server used for downloading updates. |
| update\_cache | Location of the cache used to store updates. |

### Product and service usage

#### Diagnostic log upload started report

The following fields are collected:

| Field | Description |
| --- | --- |
| sha256 | SHA256 identifier of the support log. |
| size | Size of the support log. |
| original\_path | Path to the support log (always under */var/opt/microsoft/mdatp/wdavdiag/*). |
| format | Format of the support log. |

#### Diagnostic log upload completed report

The following fields are collected:

| Field | Description |
| --- | --- |
| request\_id | Correlation ID for the support log upload request. |
| sha256 | SHA256 identifier of the support log. |
| blob\_sas\_uri | URI used by the application to upload the support log. |

#### Product and service performance data events for product service and usage

**Unexpected application exit (crash)**:

Unexpected application exits and the state of the application when that happens.

**Kernel extension statistics**:

The following fields are collected:

| Field | Description |
| --- | --- |
| pkt\_ack\_timeout | The following properties are aggregated numerical values, representing count of events that happened since kernel extension startup. |
| pkt\_ack\_conn\_timeout |  |
| ipc.ack\_pkts |  |
| ipc.nack\_pkts |  |
| ipc.send.ack\_no\_conn |  |
| ipc.send.nack\_no\_conn |  |
| ipc.send.ack\_no\_qsq |  |
| ipc.send.nack\_no\_qsq |  |
| ipc.ack.no\_space |  |
| ipc.ack.timeout |  |
| ipc.ack.ackd\_fast |  |
| ipc.ack.ackd |  |
| ipc.recv.bad\_pkt\_len |  |
| ipc.recv.bad\_reply\_len |  |
| ipc.recv.no\_waiter |  |
| ipc.recv.copy\_failed |  |
| ipc.kauth.vnode.mask |  |
| ipc.kauth.vnode.read |  |
| ipc.kauth.vnode.write |  |
| ipc.kauth.vnode.exec |  |
| ipc.kauth.vnode.del |  |
| ipc.kauth.vnode.read\_attr |  |
| ipc.kauth.vnode.write\_attr |  |
| ipc.kauth.vnode.read\_ex\_attr |  |
| ipc.kauth.vnode.write\_ex\_attr |  |
| ipc.kauth.vnode.read\_sec |  |
| ipc.kauth.vnode.write\_sec |  |
| ipc.kauth.vnode.take\_own |  |
| ipc.kauth.vnode.link |  |
| ipc.kauth.vnode.create |  |
| ipc.kauth.vnode.move |  |
| ipc.kauth.vnode.mount |  |
| ipc.kauth.vnode.denied |  |
| ipc.kauth.vnode.ackd\_before\_deadline |  |
| ipc.kauth.vnode.missed\_deadline |  |
| ipc.kauth.file\_op.mask |  |
| ipc.kauth\_file\_op.open |  |
| ipc.kauth.file\_op.close |  |
| ipc.kauth.file\_op.close\_modified |  |
| ipc.kauth.file\_op.move |  |
| ipc.kauth.file\_op.link |  |
| ipc.kauth.file\_op.exec |  |
| ipc.kauth.file\_op.remove |  |
| ipc.kauth.file\_op.unmount |  |
| ipc.kauth.file\_op.fork |  |
| ipc.kauth.file\_op.create |  |

## Resources

- [Privacy at Microsoft](https://privacy.microsoft.com/)