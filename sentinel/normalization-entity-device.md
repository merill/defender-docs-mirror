---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Device Entity reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-entity-device
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: ofshezaf
description: This article displays the Microsoft Sentinel Device Entity schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2025-07-18T00:00:00.0000000Z
locale: en-us
document_id: 33326f62-c7ca-5f7c-31f7-63b6ae7debec
document_version_independent_id: 0c322b51-d09c-155f-2b37-883e4ca73d62
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-entity-device.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-entity-device
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-entity-device.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: b3a934dd-1a76-98ce-e5c8-c1bd8ff4bd6b
---

# The Advanced Security Information Model (ASIM) Device Entity reference | Microsoft Learn

Devices, or hosts, are the common terms used for the systems that take part in the event. The `Dvc` prefix is used to designate the primary device on which the event occurs. Some events, such as network sessions, have source and destination devices, designated by the prefix `Src` and `Dst`. In such a case, the `Dvc` prefix is used for the device reporting the event, which might be the source, destination, or a monitoring device.

## The device aliases

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Dvc**, **Src**, **Dst** | Mandatory | String | The `Dvc`, 'Src', or 'Dst' fields are used as a unique identifier of the device. It is set to the best available identified for the device. These fields can alias the FQDN, DvcId, Hostname, or IpAddr fields. For cloud sources, for which there is no apparent device, use the same value as the [Event Product](normalization-common-fields#eventproduct) field. |

## The device name

Reported device names may include a hostname only, or a fully qualified domain name (FQDN), which includes a hostname and a domain name. The FQDN might be expressed using several formats. The following fields enable supporting the different variants in which the device name might be provided.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Hostname** | Recommended | Hostname | The short hostname of the device. |
| **Domain** | Recommended | String | The domain of the device on which the event occurred, without the hostname. |
| **DomainType** | Recommended | Enumerated | The type of Domain. Supported values include `FQDN` and `Windows`. This field is required if the Domain field is used. |
| **FQDN** | Optional | String | The FQDN of the device including both Hostname and Domain . This field supports both traditional FQDN format and Windows domain\hostname format. The DomainType field reflects the format used. |

For example:

| Field | Value for input`appserver.contoso.com` | value for input`appserver` |
| --- | --- | --- |
| **Hostname** | `appserver` | `appserver` |
| **Domain** | `contoso.con` | &lt;empty&gt; |
| **DomainType** | `FQDN` | &lt;empty&gt; |
| **FQDN** | `appserver.contoso.com` | &lt;empty&gt; |

When the value provided by the source is an FQDN the parser should calculate the four values. This is true also when the value may be either and FQDN or a short hostname. Use the ASIM helper functions `_ASIM_ResolveFQDN`, `_ASIM_ResolveSrcFQDN`, `_ASIM_ResolveDstFQDN`, and `_ASIM_ResolveDvcFQDN` to easily set all four fields based on a single input value. For more information, see [ASIM helper functions](normalization-functions).

## The device ID and Scope

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DvcId** | Optional | String | The unique ID of the device. For example: `41502da5-21b7-48ec-81c9-baeea8d7d669` |
| **ScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **Scope** map to a subscription ID on Azure and to an account ID on AWS. |
| **Scope** | Optional | String | The cloud platform scope the device belongs to. **Scope** map to a subscription on Azure and to an account on AWS. |
| **DvcIdType** | Optional | Enumerated | The type of DvcId. Typically this field also identifies the type of Scope and ScopeId. This field is required if the DvcId field is used. |
| **DvcAzureResourceId**, **DvcMDEid**, **DvcMD4IoTid**, **DvcVMConnectionId**, **DvcVectraId**, **DvcAwsVpcId** | Optional | String | Fields used to store other device IDs, if the original event includes multiple device IDs. Select the device ID most associated with the event as the primary ID stored in DvcId. |

Fields names should prepend a role prefix such as `Src` or `Dst`, but should not prepend a second `Dvc` prefix if used in that role.

The allowed values for a device ID type are:

| Type | Description |
| --- | --- |
| **MDEid** | The system ID assigned by Microsoft Defender for Endpoint. |
| **AzureResourceId** | The Azure resource ID. |
| **MD4IoTid** | The Microsoft Defender for IoT resource ID. |
| **VMConnectionId** | The Azure Monitor VM Insights solution resource ID. |
| **AwsVpcId** | An AWS VPC ID. |
| **VectraId** | A Vectra AI assigned resource ID. |
| **Other** | An ID type not listed. |

For example, the Azure Monitor [VM Insights solution](/en-us/azure/azure-monitor/vm/vminsights-log-query) provides network sessions information in the `VMConnection`. The table provides an Azure Resource ID in the `_ResourceId` field and a VM insights specific device ID in the `Machine` field. Use the following mapping to represent those IDs:

| Field | Map to |
| --- | --- |
| **DvcId** | The `Machine` field in the `VMConnection` table. |
| **DvcIdType** | The value `VMConnectionId` |
| **DvcAzureResourceId** | The `_ResourceId` field in the `VMConnection` table. |

## Other device fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **IpAddr** | Recommended | IP address | The IP address of the device. Example: `45.21.42.12` |
| **DvcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **MacAddr** | Optional | MAC | The MAC address of the device on which the event occurred or which reported the event. Example: `00:1B:44:11:3A:B7` |
| **Zone** | Optional | String | The network on which the event occurred or which reported the event, depending on the schema. The reporting device defines the zone.Example: `Dmz` |
| **DvcOs** | Optional | String | The operating system running on the device on which the event occurred or which reported the event. Example: `Windows` |
| **DvcOsVersion** | Optional | String | The version of the operating system on the device on which the event occurred or which reported the event. Example: `10` |
| **DvcAction** | Optional | String | For reporting security systems, the action taken by the system, if applicable. Example: `Blocked` |
| **DvcOriginalAction** | Optional | String | The original DvcAction as provided by the reporting device. |
| **Interface** | Optional | String | The network interface on which data was captured. This field is typically relevant to network related activity captured by an intermediate or tap device. |

Fields named in the list with the Dvc prefix should prepend a role prefix such as `Src` or `Dst`, but should not prepend a second `Dvc` prefix if used in that role.