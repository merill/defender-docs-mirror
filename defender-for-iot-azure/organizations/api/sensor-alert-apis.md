---
layout: Conceptual
title: Alert management API reference for OT monitoring sensors - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/api/sensor-alert-apis
breadcrumb_path: ../../breadcrumb/toc.json
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
description: Learn about the alert management REST APIs supported for Microsoft Defender for IoT OT monitoring sensors.
ms.date: 2022-05-25T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 46a2d2e2-4647-07c4-b8e5-1e0b653505fb
document_version_independent_id: 0128d518-423e-77ca-9882-9adb89f533f5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/api/sensor-alert-apis.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/api/sensor-alert-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/api/sensor-alert-apis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 1ba99b24-6d41-4f62-401d-dbb9075ec582
---

# Alert management API reference for OT monitoring sensors - Microsoft Defender for IoT | Microsoft Learn

This article lists the alert management REST APIs supported for Microsoft Defender for IoT OT monitoring sensors.

## alerts (Retrieve alert information)

Use this API to request a list of all the alerts that the Defender for IoT sensor has detected.

**URI**: `/api/v1/alerts`

### GET

# [Request](#tab/alerts-request)
#### Query parameters

| Name | Description | Example | Required / Optional |
| --- | --- | --- | --- |
| **state** | Get only handled or unhandled alerts. Supported values: - `handled`- `unhandled` | `/api/v1/alerts?state=handled` | Optional |
| **fromTime** | Get alerts created starting at a given time, in milliseconds from [Epoch time](../references-work-with-defender-for-iot-apis#epoch-time) and in UTC timezone. | `/api/v1/alerts?fromTime=<epoch>` | Optional |
| **toTime** | Get alerts created only before at a given time, in milliseconds from [Epoch time](../references-work-with-defender-for-iot-apis#epoch-time) and in UTC timezone. | `/api/v1/alerts?toTime=<epoch>` | Optional |
| **type** | Get alerts of a specific type only. Supported values: - `unexpected new devices`- `disconnections`All other values are ignored. | `/api/v1/alerts?type=disconnections` | Optional |

# [Response](#tab/alerts-response)
**Type**: JSON

A list of alerts with the following fields:

| Name | Type | Nullable / Not nullable | List of values |
| --- | --- | --- | --- |
| **ID** | Numeric | Not nullable | - |
| **time** | Numeric | Not nullable | Milliseconds from [Epoch time](../references-work-with-defender-for-iot-apis#epoch-time), in UTC timezone |
| **title** | String | Not nullable | - |
| **message** | String | Not nullable | - |
| **severity** | String | Not nullable | `Warning`, `Minor`, `Major`, or `Critical` |
| **engine** | String | Not nullable | `Protocol Violation`, `Policy Violation`, `Malware`, `Anomaly`, or `Operational` |
| **sourceDevice** | Numeric | Nullable | Device ID |
| **destinationDevice** | Numeric | Nullable | Device ID |
| **additionalInformation** | Additional information object | Nullable | - |

#### Additional information fields

| Name | Type | Nullable / Not nullable | List of values |
| --- | --- | --- | --- |
| **description** | String | Not nullable | - |
| **information** | JSON array | Not nullable | String |

**Added for V2**:

| Name | Type | Nullable / Not nullable | List of values |
| --- | --- | --- | --- |
| **sourceDeviceAddress** | String | Nullable | IP or MAC address |
| **destinationDeviceAddress** | String | Nullable | IP or MAC address |
| **remediationSteps** | JSON array | Not nullable | Strings, remediation steps described in alert |

For more information, see [Sensor API version reference](../references-work-with-defender-for-iot-apis#sensor-api-version-reference).

#### Response example

```rest
[
    {
        "engine": "Policy Violation",
        "severity": "Major",
        "title": "Internet Access Detected",
        "additionalinformation": {
            "information": [
                "170.60.50.201 over port BACnet (47808)"
            ],
            "description": "External Addresses"
        },
        "sourceDevice": null,
        "destinationDevice": null,
        "time": 1509881077000,
        "message": "Device 192.168.0.13 tried to access an external IP address which is an address in the Internet and is not allowed by policy. It is recommended to notify the security officer of the incident.",
        "id": 1
    },
    {
        "engine": "Protocol Violation",
        "severity": "Major",
        "title": "Illegal MODBUS Operation (Exception Raised by Master)",
        "sourceDevice": 3,
        "destinationDevice": 4,
        "time": 1505651605000,
        "message": "A MODBUS master 192.168.110.131 attempted to initiate an illegal operation.\nThe operation is considered to be illegal since it incorporated function code \#129 which should not be used by a master.\nIt is recommended to notify the security officer of the incident.",
        "id": 2,
        "additionalInformation": null,
    }
]
```

# [cURL command](#tab/alerts-curl)
**Type**: GET

**API**:

```rest
curl -k -H "Authorization: <AUTH_TOKEN>" 'https://<IP_ADDRESS>/api/v1/alerts?state=<STATE>&fromTime=<FROM_TIME>&toTime=<TO_TIME>&type=<TYPE>'
```

**Example**:

```rest
curl -k -H "Authorization: 1234b734a9244d54ab8d40aedddcabcd" 'https://127.0.0.1/api/v1/alerts?state=unhandled&fromTime=1594550986000&toTime=1594550986001&type=disconnections'
```

---

## events (Retrieve timeline events)

Use this API to request a list of events reported to the event timeline.

Note

Running the identical API within the same hour, with the exact same parameter values, returns a cached value. If you are running this API twice in an hour, we recommend that you modify the query parameters to get an updated response.

**URI**: `/api/v1/events`

### GET

# [Request](#tab/events-request)
#### Query parameters

| Name | Description | Example | Required / Optional |
| --- | --- | --- | --- |
| **minutesTimeFrame** | Filter results by a given time frame during which events were reported. Defined backwards from the current time. Maximum = `4320` (3 days). Any larger value is treated as 4320, with no error | `/api/v1/events?minutesTimeFrame=20` | Optional |
| **type** | Filter results for a specific type only. Any value other than supported types is ignored. For more information, see Event `type` and `title` reference. | `/api/v1/events?type=DEVICE_CONNECTION_CREATED``/api/v1/events?type=REMOTE_ACCESS&minutesTimeFrame` | Optional |

# [Response](#tab/events-response)
**Type**: JSON

Array of JSON objects that represent the latest 100 events, sorted by event timestamp, with the latest event first.

Event fields include:

| Name | Type | Nullable / Not nullable | List of values |
| --- | --- | --- | --- |
| **timestamp** | Numeric | Not nullable | Milliseconds from [Epoch time](../references-work-with-defender-for-iot-apis#epoch-time), in UTC timezone |
| **type** | String | Not nullable | One of the supported types |
| **title** | String | Not nullable | One of the supported titles |
| **severity** | String | Not nullable | `INFO`, `NOTICE`, or `ALERT` |
| **owner** | String | Nullable | String. If the event was created manually, this field will include the username that created the event. |
| **content** | String | Not nullable | String that describes the event. |

#### Response example

```rest
[
    {
        "severity": "INFO",
        "title": "Back to Normal",
        "timestamp": 1504097077000,
        "content": "Device 10.2.1.15 was found responsive, after being suspected as disconnected",
        "owner": null,
        "type": "BACK_TO_NORMAL"
    },
    {
        "severity": "ALERT",
        "title": "Alert Detected",
        "timestamp": 1504096909000,
        "content": "Device 10.2.1.15 is suspected to be disconnected (unresponsive).",
        "owner": null,
        "type": "ALERT_REPORTED"
    },
    {
        "severity": "ALERT",
        "title": "Alert Detected",
        "timestamp": 1504094446000,
        "content": "A DNP3 Master 10.2.1.14 attempted to initiate a request which is not allowed by policy.\nThe policy indicates the allowed function codes, address ranges, point indexes and time intervals.\nIt is recommended to notify the security officer of the incident.",
        "owner": null,
        "type": "ALERT_REPORTED"
    },
    {
        "severity": "NOTICE",
        "title": "PLC Program Update",
        "timestamp": 1504094344000,
        "content": "Program update detected, sent from 10.2.1.25 to 10.2.1.14",
        "owner": null,
        "type": "PROGRAM_DEVICE"
    }
]
```

# [cURL command](#tab/events-curl)
**Type**: GET

**API**:

```rest
curl -k -H "Authorization: <AUTH_TOKEN>" 'https://<IP_ADDRESS>/api/v1/events?minutesTimeFrame=<TIME_FRAEM>&type=<TYPE>'
```

**Example**:

```rest
curl -k -H "Authorization: 1234b734a9244d54ab8d40aedddcabcd" 'https://127.0.0.1/api/v1/events?minutesTimeFrame=20&type=DEVICE_CONNECTION_CREATED'`
```

---

## Event `type` and `title` reference

This section lists the values supported as event *type* and *title* values for the events API.

| Event type | Event title |
| --- | --- |
| DEVICE\_CREATE | Device Detected |
| DEVICE\_UPDATE | Device Updated |
| ALERT\_REPORTED | Alert Detected |
| ALERT\_UPDATED | Alert Updated |
| SCAN | Scan Device Detected |
| PROGRAM\_DEVICE | PLC Programming |
| MMS\_PROGRAM\_DEVICE | PLC Program Update |
| SCL\_UPLOADED | SCL Uploaded |
| EXCLUSION\_RULE\_CREATED | Exclusion Rule Created |
| EXCLUSION\_RULE\_REMOVED | Exclusion Rule Removed |
| EXCLUSION\_RULE\_UPDATED | Exclusion Rule Updated |
| DEVICE\_CONNECTION\_CREATED | Device Connection Detected |
| USER\_LOGIN | User Login Attempt |
| FILE\_TRANSFER | File Transfer Detected |
| CUSTOM\_EVENT | User Defined Event |
| REMOTE\_ACCESS | Remote Access Connection Established |
| BACK\_TO\_NORMAL | Back to Normal |
| MMS\_MEMORY\_BLOCK\_OPERATION | MMS Memory Block Operation |
| MMS\_PROGRAM\_OPERATION | MMS Program Operation |
| HTTP\_BASIC\_AUTHENTICATION | HTTP Basic Authentication |
| SIEMENS\_S\_7\_MEMORY\_BLOCK\_OPERATION | Siemens S7 Memory Block Operation |
| SIEMENS\_S\_7\_AUTHENTICATION | Siemens S7 Authentication |
| REPORT\_CREATED | Report Created |
| SNMP\_TRAP | SNMP Trap detected |
| DATABASE\_ACTION | Database Structure Manipulation |
| PLC\_MODULE\_CHANGE | PLC Module Change |
| FIRMWARE\_UPDATE | Firmware Update |
| PLC\_START | PLC Start |
| SRTP\_PLC\_RESET | PLC Reset |
| SRTP\_PLC\_COPY\_FIRMWARE | Firmware Update |
| SRTP\_LOGIN\_PROGRAMMING | PLC Programming Mode Set |
| SRTP\_PLC\_CHANGE\_PASSWORD | PLC Password Change |
| OPC\_DATA\_ACCESS\_GROUP\_MANAGEMENT\_OPERATION | OPC Data Access Group Management Operation |
| OPC\_DATA\_ACCESS\_ITEM\_MANAGEMENT\_OPERATION | OPC Data Access Item Management Operation |
| OPC\_DATA\_ACCESS\_IO\_SUBSCRIPTION\_MANAGEMENT\_OPERATION | OPC Data Access IO Subscription Management Operation |
| OPC\_AE\_EVENT\_SUBSCRIPTION | OPC AE Event Subscription |
| OPC\_AE\_EVENT\_CONDITION\_MANAGEMENT\_OPERATION | OPC AE Event Condition Management Operation |
| OPC\_AE\_EVENT | OPC AE Event |
| SRTP\_CHANGE\_PRIVILEGE | PLC Change access level |
| SRTP\_CHANGE\_LEVEL\_FAILED | PLC Change access level failed |
| SUITELINK\_INIT\_CONNECTION | Wonderware session initialized |
| USER\_OPERATION | User Operation |
| DIP\_UPLOADED | Data Intelligence Package Uploaded |
| FTP\_AUTHENTICATION\_FAILURE | FTP Authentication Failure |
| PROFINET\_DPC\_VALUE\_SET | Profinet SET operation |
| S7PLUS\_PLC\_MODE\_CHANGE | PLC Mode Change |
| S7\_PLC\_MODE\_CHANGE | PLC Mode Change |
| DELETE\_DEVICE | Device Deleted |
| S7PLUS\_PROGRAMMING | PLC Programming |
| FIRMWARE\_CHANGED | PLC Firmware Changed |
| DELTAV\_PROGRAMMING | DeltaV Install Script |
| USER\_DEFINED\_RULE\_CREATED | User Defined Rule Created |
| USER\_DEFINED\_RULE\_EDITED | User Defined Rule Edited |
| USER\_DEFINED\_RULE\_DELETED | User Defined Rule Deleted |
| USER\_DEFINED\_RULE\_OPERATION | User Defined Rule Operation |
| REMOTE\_PROCESS\_EXECUTION | Remote Process Execution |
| DEVICE\_UNIFICATION | Device Updated |
| NOTIFICATION | Notification was resolved manually |
| ENIP\_CONTROLLER\_PROGRAM\_DELETE | Controller Program Delete |
| ENIP\_CONTROLLER\_PROGRAM\_RESET | Controller Program Reset |
| ENIP\_CONTROLLER\_GENERIC\_RESET | Controller Reset |
| ENIP\_CONTROLLER\_GENERIC\_STOP | Controller Stop |
| ENIP\_CONTROLLER\_GENERIC\_START | Controller Start |
| TELNET\_AUTHENTICATION\_FAILURE | Telnet Authentication Failure |
| CONFIGURATION\_OF\_CLEARTEXT\_PASSWORD | Configuration Of Cleartext Password |
| CLEARTEXT\_AUTHENTICATION | Cleartext Authentication |
| PROGRAM\_UPLOAD\_DEVICE | PLC Program Upload |
| CONFIGURATION\_CHANGE | PLC Configuration Write |
| CONFIGURATION\_READ | PLC Configuration Read |
| SYSLOG\_MSG | Syslog Message |
| INTERNET\_ACCESS | Internet Access |
| CAMP\_MEMORY\_WRITE\_OPERATION | Common ASCII Message Protocol Memory Write Operation |
| MUTED\_ALERT | Event Detected and Muted |
| DHCP\_UPDATE | Address Update |
| DIP\_FAILURE | Data Intelligence Package Installation Failure |
| DELETE\_DEVICE\_SCHEDULE | Inactive Devices Scheduled for deletion |
| PLC\_OPERATING\_MODE\_CHANGED | PLC Operating Mode Change Detected |
| HARDWARE\_UPDATE\_BY\_IDENTIFIER | Address Update |