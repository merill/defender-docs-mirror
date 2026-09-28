---
layout: Conceptual
title: Authentication and password management API reference for OT monitoring sensors - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/api/sensor-auth-apis
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
description: Learn about the authentication and password management REST APIs supported for Microsoft Defender for IoT OT monitoring sensors.
ms.date: 2022-06-13T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 16adee47-4143-cffc-30c1-8e9dc258db05
document_version_independent_id: 01ecc9f5-f6f8-f7a9-4863-f3b8372442e0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/api/sensor-auth-apis.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/api/sensor-auth-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/api/sensor-auth-apis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c2cf1ff7-2464-0b7c-dec9-afb77de35f55
---

# Authentication and password management API reference for OT monitoring sensors - Microsoft Defender for IoT | Microsoft Learn

This article lists the authentication and password management APIs supported for Defender for IoT OT sensors.

## set\_password (Change your password)

Use this API to let users change their own passwords.

You don't need a Defender for IoT access token to use this API.

**URI**: `/external/authentication/set_password`

### POST

# [Request](#tab/set-password-request)
**Type**: JSON

**Example**:

```rest
request:

{
    "username": "test",
    "password": "Test12345\!",
    "new_password": "Test54321\!"
}
```

#### Request parameters

| **Name** | **Type** | **Required / Optional** |
| --- | --- | --- |
| **username** | String | Required |
| **password** | String | Required |
| **new\_password** | String | Required |

# [Response](#tab/set-password-response)
**Type**: JSON

Message string with the operation status details:

| Message | Description |
| --- | --- |
| **Success – msg** | Password has been replaced |
| **Failure – error** | User authentication failure |
| **Failure – error** | Password does not match security policy |

**Example**:

```rest
response:

{
    "error": {
        "userDisplayErrorMessage": "User authentication failure"
    }
}
```

# [cURL command](#tab/set-password-curl)
**Type**: POST

**API**:

```rest
curl -k -X POST -d '{"username": "<USER_NAME>","password": "<CURRENT_PASSWORD>","new_password": "<NEW_PASSWORD>"}' -H 'Content-Type: application/json'  https://<IP_ADDRESS>/api/external/authentication/set_password
```

**Example**:

```rest
curl -k -X POST -d '{"username": "myUser","password": "1234@abcd","new_password": "abcd@1234"}' -H 'Content-Type: application/json'  https://127.0.0.1/api/external/authentication/set_password
```

---

## set\_password\_by\_admin (Update a user password by admin)

Use this API to let system administrators change passwords for specified users. Defender for IoT administrator user roles can work with the API.

You don't need a Defender for IoT access token to use this API.

**URI**: `/external/authentication/set_password_by_admin`

### POST

# [Request](#tab/set-password-by-admin-request)
**Type**: JSON

#### Request example

```rest
request:

{
    "admin_username": "admin",
    "admin_password: "Test0987"
    "username": "test",
    "new_password": "Test54321\!"
}
```

#### Request parameters

| **Name** | **Type** | **Required / Optional** |
| --- | --- | --- |
| **admin\_username** | String | Required |
| **admin\_password** | String | Required |
| **username** | String | Required |
| **new\_password** | String | Required |

# [Response](#tab/set-password-by-admin-response)
**Type**: JSON

Message string with the operation status details:

| Message | Description |
| --- | --- |
| **Success – msg** | Password has been replaced |
| **Failure – error** | User authentication failure |
| **Failure – error** | User does not exist |
| **Failure – error** | Password doesn't match security policy |
| **Failure – error** | User does not have the permissions to change password |

#### Response example

```rest
response:

{
    "error": {
        "userDisplayErrorMessage": "The user 'test_user' doesn't exist",
        "internalSystemErrorMessage": "The user 'test_user' doesn't exist"
    }
}

```

# [cURL command](#tab/set-password-by-admin-curl)
**Type**: POST

**API**:

```rest
curl -k -X POST -d '{"admin_username":"<ADMIN_USERNAME>","admin_password":"<ADMIN_PASSWORD>","username": "<USER_NAME>","new_password": "<NEW_PASSWORD>"}' -H 'Content-Type: application/json'  https://<IP_ADDRESS>/api/external/authentication/set_password_by_admin
```

**Example**:

```rest
curl -k -X POST -d '{"admin_user":"adminUser","admin_password": "1234@abcd","username": "myUser","new_password": "abcd@1234"}' -H 'Content-Type: application/json'  https://127.0.0.1/api/external/authentication/set_password_by_admin
```

---

## validation (Validate user credentials)

Use this API to validate a Defender for IoT username and password.

You don't need a Defender for IoT access token to use this API.

**URI**: `/api/external/authentication/validation`

### POST

# [Request](#tab/validation-request)
**Request type**: JSON

#### Query parameters

| **Name** | **Type** | **Required/Optional** |
| --- | --- | --- |
| **username** | String | Required |
| **password** | String | Required |

#### Request example:

```rest
request:
{
    "username": "test",
    "password": "Test12345\!"
}
```

# [Response](#tab/validation-response)
**Type**: JSON

Message string with the operation status details:

| Message | Description |
| --- | --- |
| **Success - msg** | Authentication succeeded |
| **Failure - error** | Credentials validation failed |

#### Response example

```rest
response:
{
    "msg": "Authentication succeeded."
}
```

# [cURL command](#tab/validation-curl)
**Type**: POST

**API**:

```rest
curl -k -X POST -H "Authorization: <AUTH_TOKEN>" -H "Content-Type: application/json" -d '{"username": <USER NAME>, "password": <PASSWORD>}' https://<IP_ADDRESS>/api/external/authentication/validation
```

**Example**:

```rest
curl -k -X POST -H "Authorization: 1234b734a9244d54ab8d40aedddcabcd" -H "Content-Type: application/json" -d '{"username": "test", "password": "test"}' https://127.0.0.1/api/external/authentication/validation
```

---