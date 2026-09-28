---
layout: Conceptual
title: Machine resource type - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/machine
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about the methods and properties of the Machine resource type in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: bae02ddc-31fb-910e-ca7d-3803461f0f3f
document_version_independent_id: bae02ddc-31fb-910e-ca7d-3803461f0f3f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/machine.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/machine
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/machine.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5f624e90-3a64-3d69-f342-1c85ae78f70d
---

# Machine resource type - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Properties

| Property | Type | Description |
| --- | --- | --- |
| id | String | [machine](machine) identity. |
| computerDnsName | String | [machine](machine) fully qualified name. |
| firstSeen | DateTimeOffset | First date and time where the [machine](machine) was observed by Microsoft Defender for Endpoint. |
| lastSeen | DateTimeOffset | Time and date of the last received full device report. A device typically sends a full report every 24 hours.  NOTE: This property doesn't correspond to the last seen value in the UI. It pertains to the last device update. |
| osPlatform | String | Operating system platform. |
| onboardingstatus | String | Status of machine onboarding. Possible values are: `onboarded`, `CanBeOnboarded`, `Unsupported`, and `InsufficientInfo`. |
| osProcessor | String | Operating system processor. Use osArchitecture property instead. |
| version | String | Operating system Version. |
| osBuild | Nullable long | Operating system build number. |
| lastIpAddress | String | Last IP on local NIC on the [machine](machine). |
| lastExternalIpAddress | String | Last IP through which the [machine](machine) accessed the internet. |
| healthStatus | Enum | [machine](machine) health status. Possible values are: `Active`, `Inactive`, `ImpairedCommunication`, `NoSensorData`, `NoSensorDataImpairedCommunication`, and `Unknown`. |
| rbacGroupName | String | Machine group Name. |
| rbacGroupId | String | Machine group ID. |
| riskScore | Nullable Enum | Risk score as evaluated by Microsoft Defender for Endpoint. Possible values are: `None`, `Informational`, `Low`, `Medium`, and `High`. |
| aadDeviceId | Nullable representation Guid | Microsoft Entra Device ID (when [machine](machine) is Microsoft Entra joined). |
| machineTags | String collection | Set of [machine](machine) tags. |
| exposureLevel | Nullable Enum | Exposure level as evaluated by Microsoft Defender for Endpoint. Possible values are: `None`, `Low`, `Medium`, and `High`. |
| deviceValue | Nullable Enum | The [value of the device](/en-us/defender-vulnerability-management/tvm-assign-device-value). Possible values are: `Normal`, `Low`, and `High`. |
| ipAddresses | IpAddress collection | Set of ***IpAddress*** objects. See [Get machines API](get-machines). |
| osArchitecture | String | Operating system architecture. Possible values are: `32-bit`, `64-bit`. Use this property instead of osProcessor. |