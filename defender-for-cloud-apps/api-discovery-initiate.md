---
layout: Conceptual
title: Initiate file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-initiate
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes the upload_url request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 95c2cf3c-3d42-64dd-44df-28cf4ba9b79e
document_version_independent_id: 95c2cf3c-3d42-64dd-44df-28cf4ba9b79e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-initiate.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-initiate
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-initiate.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: f1450460-6e6c-bceb-cf74-1c8f90660946
---

# Initiate file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the GET request to initiate the upload process. This call, the first of the three, returns a URL that will later be used to perform the upload (PUT) request.

## HTTP request

```rest
GET /api/v1/discovery/upload_url/
```

## Request URL parameters

| Parameter | Description |
| --- | --- |
| filename | Name of the file you want to upload to cloud discovery processing |
| source | The type of cloud discovery log file being uploaded |

The following source types are currently supported:

- BLUECOAT
- BARRACUDA
- BARRACUDA\_NEXT\_GEN\_FW
- BARRACUDA\_NEXT\_GEN\_FW\_WEBLOG
- BARRACUDA\_SYSLOG
- BLUECOAT\_SYSLOG
- CHECKPOINT
- CHECKPOINT\_CEF\_SYSLOG
- CHECKPOINT\_SMART\_VIEW\_TRACKER
- CHECKPOINT\_XML
- CISCO\_ASA
- CISCO\_ASA\_FIREPOWER\_SYSLOG
- CISCO\_ASA\_SYSLOG
- CISCO\_FIREPOWER\_V6\_SYSLOG
- CISCO\_FWSM
- CISCO\_FWSM\_SYSLOG
- CISCO\_IRONPORT\_PROXY
- CISCO\_IRONPORT\_PROXY\_SYSLOG
- CISCO\_IRONPORT\_WSA\_II
- CISCO\_IRONPORT\_WSA\_III
- CISCO\_SCAN\_SAFE
- CLAVISTER\_SYSLOG
- CONTENTKEEPER\_SYSLOG
- CORRATA
- FORCEPOINT
- FORCEPOINT\_LEEF\_SYSLOG
- FORTIGATE
- FORTIGATE\_SYSLOG
- FORTIOS\_SYSLOG
- GENERIC\_CEF
- GENERIC\_CEF\_SYSLOG
- GENERIC\_LEEF
- GENERIC\_LEEF\_SYSLOG
- GENERIC\_W3C
- GENERIC\_W3C\_SYSLOG
- I\_FILTER
- I\_FILTER\_SYSLOG
- IBOSS
- JUNIPER\_SRX\_SD\_SYSLOG
- JUNIPER\_SRX\_SYSLOG
- JUNIPER\_SRX\_WELF\_SYSLOG
- JUNIPER\_SSG\_SYSLOG
- MACHINE\_ZONE\_MERAKI
- MACHINE\_ZONE\_MERAKI\_SYSLOG
- MCAFEE\_SWG
- MCAFEE\_SWG\_SYSLOG
- MENLO\_SECURITY\_CEF
- MICROSOFT\_ISA\_W3C
- OPEN\_SYSTEMS\_SECURE\_WEB\_GATEWAY
- PALO\_ALTO
- PALO\_ALTO\_LEEF
- PALO\_ALTO\_LEEF\_SYSLOG
- PALO\_ALTO\_SYSLOG
- SONICWALL\_SYSLOG
- SOPHOS\_CYBEROAM\_SYSLOG
- SOPHOS\_SG
- SOPHOS\_SG\_SYSLOG
- SOPHOS\_XG
- SOPHOS\_XG\_SYSLOG
- SQUID
- SQUID\_NATIVE
- SQUID\_NATIVE\_SYSLOG
- STORMSHIELD\_SYSLOG
- WANDERA\_SYSLOG
- WATCHGUARD\_XTM\_SYSLOG
- WEBSENSE\_SIEM\_CEF\_SYSLOG
- WEBSENSE\_V7\_5
- ZSCALER
- ZSCALER\_CEF\_SYSLOG
- ZSCALER\_QRADAR\_SYSLOG
- ZSCALER\_SYSLOG

Note

- When using a custom parser, Defender for Cloud Apps will use the custom parser attached to the selected data source.
- If you can't find your file format, perform a manual upload using the portal.

## Response parameters

| Parameter | Description |
| --- | --- |
| url | The target URL that will perform your cloud discovery upload. |
| provider | Either "azure" or "aws", an indication whether the upload is target to Windows Azure Storage and AWS S3 storage. |

## Example

### Request

Here is an example of the request.

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/discovery/upload_url/?filename=my_discovery_file.txt&source=GENERIC_CEF"
```

### Response

Here is an example of the JSON response.

```json
{
  "url": "https://<initiate_file_upload_response_url>",
  "provider": "azure"
}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).