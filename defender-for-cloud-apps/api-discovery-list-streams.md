---
layout: Conceptual
title: List continuous reports - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-list-streams
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
description: This article describes the list continuous reports request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: d4e0042e-2f08-5d0d-6363-d53f526be5ec
document_version_independent_id: d4e0042e-2f08-5d0d-6363-d53f526be5ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-list-streams.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-list-streams
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-list-streams.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2aab8c8e-d113-ab61-a023-5941f7a1b5f6
---

# List continuous reports - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the GET request to fetch a list of continuous reports.

## HTTP request

```rest
GET api/discovery/streams/
```

## Example

### Request

Here is an example of the request.

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/discovery/streams/"
```

### Response

Returns a list of continuous reports in JSON format.

```json
{
  "anonymizeUsers": false,
  "displayName": "dependency_udp",
  "logType": 223,
  "receiverType": "syslog",
  "protocol": "udp",
  "streamType": 1,
  "isManual": false,
  "created": "2020-12-16T17:23:40.687Z",
  "lastModified": "2021-01-05T13:41:36.104Z",
  "logFilesHistoryCount": 2,
  "supportedEntityTypes": [],
  "supportedTrafficTypes": [1],
  "lastAlertProcessingTime": 1609853011480,
  "lastDataReceived": "2020-12-18T06:33:32.908Z",
  "logFilesFailsCount": 2,
  "currentServicesCollectionName": "discovery_services",
  "globalAggregated": true,
  "readTimeFramesFromSecond": true,
  "timeFrames2": {},
  "validTimeFrames2": [],
  "timeFrames": {},
  "validTimeFrames": [],
  "timeWithoutLogs": 0,
  "sourceStreams": []
}
```

The response object defines the following properties. Properties marked as *optional* may not appear for some continuous reports.

| Field name | Field type | Field description |
| --- | --- | --- |
| anonymizeMachines (*optional*) | boolean | **true** if machine information is anonymized |
| anonymizeUsers (*optional*) | boolean | **true** if user information is anonymized |
| builtInStreamType (*optional*) | int | The built-in type of the continuous report. Possible values are:**0**: PROXY**1**: WINDOWS\_DEFENDER |
| comment (*optional*) | string | The comment/description of the continuous report |
| created | date | The creation date of the continuous report |
| displayName | string | The display name of the continuous report |
| isManual (*optional*) | boolean | **true** if the continuous report is manual configured |
| globalAggregated | boolean | **true** if the continuous report data is aggregated into the global report |
| lastDataReceived | date | The date that data was last received |
| lastModified | date | The date the continuous report was last modified |
| logFilesHistoryCount (*optional*) | int | Count of log files history |
| logType | int | The log type of the continuous report. For possible values, see Supported log types |
| protocol (*optional*) | string | The protocol (TCP, UDP) used by the continuous report |
| receiverType | string | The receiver type of the continuous report. Possible values include: syslog and ftp |
| snapshotData (*optional*) | boolean | **true** if the data is from snapshot report |
| streamType | int | The type of the continuous report. Possible values are:**1**: INPUT (continuous report automatically created by log collector or data source)**3**: VIEW (continuous report manually created in the portal)**5**: PREVIEW (one-time continuous report created by snapshot report) |
| supportedEntityTypes | list | An array of discovery entity types. Possible values are:**0**: INVALID**1**: USER\_NAME**2**: IP\_ADDRESS**3**: MACHINE\_NAME**4**: RESOURCE |
| supportedTrafficTypes | list | An array of traffic types. Possible values are:**0**: INVALID**1**: TOTAL\_BYTES**2**: DOWNLOADED\_BYTES**3**: UPLOADED\_BYTES |
| timeFrames/timeframes2 | list | An array of time frame objects for the last 7, 30, or 60 days with totals such as: Machine names count or IP addresses count |
| userTags | list | An array of user tags |

## Supported log types

The following log types are currently supported:

| ID | Log type |
| --- | --- |
| 0 | INVALID |
| 1 | OTHER |
| 100 | LOG\_3COM |
| 101 | BARRACUDA |
| 102 | BLUECOAT |
| 103 | CHECKPOINT |
| 104 | CISCO\_ASA |
| 105 | CISCO\_SSL\_WEBVPN\_OR\_SVC\_VPN |
| 106 | CISCO\_IRONPORT\_PROXY |
| 107 | CISCO\_NETFLOW |
| 108 | FORTIGATE |
| 109 | JUNIPER\_NETWORKS |
| 110 | GREENPLUM |
| 111 | MICROSFOT\_ISA |
| 112 | PALO\_ALTO |
| 113 | SONICWALL |
| 114 | SQUID |
| 115 | SUN\_MICROSYSTEMS\_SUNSCREEN\_FIREWALL |
| 116 | SURICATA |
| 117 | SYMANTEC\_WEB\_SECURITY\_CLOUD |
| 118 | WEBSENSE |
| 119 | WATCH\_GUARD |
| 120 | ZSCALER |
| 121 | MCAFEE\_SWG |
| 122 | HP\_TIPPING\_POINT |
| 123 | HP\_NETWORKING |
| 124 | CISCO\_SCAN\_SAFE |
| 125 | CHECKPOINT\_OPSEC\_LEA |
| 126 | PALO\_ALTO\_SYSLOG |
| 127 | METADATA\_ACTIVE\_DIRECTORY\_LOGIN |
| 128 | COX\_SYSLOG |
| 129 | JUNIPER\_SRX |
| 130 | SOPHOS\_SG |
| 131 | METADATA\_HPE\_LOGIN |
| 132 | METADATA\_CISCO\_ISE |
| 133 | CISCO\_IRONPORT\_PROXY\_SYSLOG |
| 134 | ZSCALER\_NESTLE |
| 135 | WEBSENSE\_V7\_5 |
| 136 | FORTIGATE\_SYSLOG |
| 137 | PAN\_DELOITTE |
| 138 | WEBSENSE\_SIEM\_CEF |
| 139 | BLUECOAT\_SYSLOG |
| 140 | CHECKPOINT\_SYSLOG |
| 141 | CISCO\_ASA\_SYSLOG |
| 142 | CISCO\_SCAN\_SAFE\_SYSLOG |
| 143 | ZSCALER\_SYSLOG |
| 144 | MCAFEE\_SWG\_SYSLOG |
| 145 | CHECKPOINT\_OPSEC\_LEA\_SYSLOG |
| 146 | SQUID\_SYSLOG |
| 147 | JUNIPER\_SRX\_SYSLOG |
| 148 | SOPHOS\_SG\_SYSLOG |
| 149 | MICROSFOT\_ISA\_SYSLOG |
| 150 | WEBSENSE\_SYSLOG |
| 151 | WEBSENSE\_V7\_5\_SYSLOG |
| 152 | WEBSENSE\_SIEM\_CEF\_SYSLOG |
| 153 | MACHINE\_ZONE\_MERAKI |
| 154 | MACHINE\_ZONE\_MERAKI\_SYSLOG |
| 155 | SQUID\_NATIVE |
| 156 | SQUID\_NATIVE\_SYSLOG |
| 157 | CISCO\_FWSM |
| 158 | CISCO\_FWSM\_SYSLOG |
| 159 | MICROSOFT\_ISA\_W3C |
| 160 | SONICWALL\_SYSLOG |
| 161 | MICROSOFT\_ISA\_W3C\_SYSLOG |
| 162 | SOPHOS\_CYBEROAM |
| 163 | SOPHOS\_CYBEROAM\_SYSLOG |
| 164 | CLAVISTER |
| 165 | CLAVISTER\_SYSLOG |
| 166 | BARRACUDA\_SYSLOG |
| 167 | CUSTOM\_PARSER |
| 168 | JUNIPER\_SSG |
| 169 | JUNIPER\_SSG\_SYSLOG |
| 170 | ZSCALER\_QRADAR |
| 171 | ZSCALER\_QRADAR\_SYSLOG |
| 172 | JUNIPER\_SRX\_SD |
| 173 | JUNIPER\_SRX\_SD\_SYSLOG |
| 174 | JUNIPER\_SRX\_WELF |
| 175 | JUNIPER\_SRX\_WELF\_SYSLOG |
| 176 | ADALLOM\_PROXY\_RAW\_TRAFFIC |
| 177 | CISCO\_ASA\_FIREPOWER |
| 178 | CISCO\_ASA\_FIREPOWER\_SYSLOG |
| 179 | GENERIC\_CEF |
| 180 | GENERIC\_CEF\_SYSLOG |
| 181 | GENERIC\_LEEF |
| 182 | GENERIC\_LEEF\_SYSLOG |
| 183 | GENERIC\_W3C |
| 184 | GENERIC\_W3C\_SYSLOG |
| 185 | I\_FILTER |
| 186 | I\_FILTER\_SYSLOG |
| 187 | CHECKPOINT\_XML |
| 188 | CHECKPOINT\_XML\_SYSLOG |
| 189 | CHECKPOINT\_SMART\_VIEW\_TRACKER |
| 190 | CHECKPOINT\_SMART\_VIEW\_TRACKER\_SYSLOG |
| 191 | BARRACUDA\_NEXT\_GEN\_FW |
| 192 | BARRACUDA\_NEXT\_GEN\_FW\_SYSLOG |
| 193 | BARRACUDA\_NEXT\_GEN\_FW\_WEBLOG |
| 194 | BARRACUDA\_NEXT\_GEN\_FW\_WEBLOG\_SYSLOG |
| 195 | WDATP |
| 196 | ZSCALER\_CEF |
| 197 | ZSCALER\_CEF\_SYSLOG |
| 198 | SOPHOS\_XG |
| 199 | SOPHOS\_XG\_SYSLOG |
| 200 | IBOSS |
| 201 | IBOSS\_SYSLOG |
| 202 | FORCEPOINT |
| 203 | FORCEPOINT\_SYSLOG |
| 204 | FORTIOS |
| 205 | FORTIOS\_SYSLOG |
| 206 | CISCO\_IRONPORT\_WSA\_II |
| 207 | CISCO\_IRONPORT\_WSA\_II\_SYSLOG |
| 208 | PALO\_ALTO\_LEEF |
| 209 | PALO\_ALTO\_LEEF\_SYSLOG |
| 210 | FORCEPOINT\_LEEF |
| 211 | FORCEPOINT\_LEEF\_SYSLOG |
| 212 | STORMSHIELD |
| 213 | STORMSHIELD\_SYSLOG |
| 214 | CONTENTKEEPER |
| 215 | CONTENTKEEPER\_SYSLOG |
| 216 | CISCO\_IRONPORT\_WSA\_III |
| 217 | CISCO\_IRONPORT\_WSA\_III\_SYSLOG |
| 218 | CHECKPOINT\_CEF |
| 219 | CHECKPOINT\_CEF\_SYSLOG |
| 220 | CORRATA |
| 221 | CORRATA\_SYSLOG |
| 222 | CISCO\_FIREPOWER\_V6 |
| 223 | CISCO\_FIREPOWER\_V6\_SYSLOG |
| 224 | MENLO\_SECURITY\_CEF |
| 225 | WATCHGUARD\_XTM |
| 226 | WATCHGUARD\_XTM\_SYSLOG |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).