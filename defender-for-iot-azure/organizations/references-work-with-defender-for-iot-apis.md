---
layout: Conceptual
title: Work with Defender for IoT APIs - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/references-work-with-defender-for-iot-apis
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
description: Use an external REST API to access the data discovered by sensors and perform actions with that data.
ms.date: 2022-06-13T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: bf83d9ad-e111-b8c7-dab3-53aa58ce8b54
document_version_independent_id: 2e777e39-cbcf-4367-6f03-e149c92abc21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/references-work-with-defender-for-iot-apis.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/references-work-with-defender-for-iot-apis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/references-work-with-defender-for-iot-apis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: a684c02c-54db-f43c-1870-793fd56bb77b
---

# Work with Defender for IoT APIs - Microsoft Defender for IoT | Microsoft Learn

This section describes the public APIs supported by Microsoft Defender for IoT. Defender for IoT APIs are governed by [Microsoft API License and Terms of use](/en-us/legal/microsoft-apis/terms-of-use).

Use Defender for IoT APIs to access data discovered by sensors and perform actions with that data.

API connections are secured over SSL.

## Generate an API access token

Many Defender for IoT APIs require an access token. Access tokens are *not* required for authentication APIs.

**To generate a token**:

1. In the **System Settings** window, select **Integrations** &gt; **Access Tokens**.
2. Select **Generate token**.
3. In **Description**, describe what the new token is for, and select **Generate**.
4. The access token appears. Copy it, because it won't be displayed again.
5. Select **Finish**.

    - The tokens that you create appear in the **Access Tokens** dialog box. The **Used** indicates the last time an external call with this token was received.
    - **N/A** in the **Used** field indicates that the connection between the sensor and the connected server isn't working.

After generating the token, add an HTTP header titled **Authorization** to your request, and set its value to the token that you generated.

## Sensor API version reference

| Version | Supported APIs |
| --- | --- |
| **No version** | **Authentication and password management**: - [set_password (Change your password)](api/sensor-auth-apis#set_password-change-your-password)- [set_password_by_admin (Update a user password by admin)](api/sensor-auth-apis#set_password_by_admin-update-a-user-password-by-admin) - [validation (Validate user credentials)](api/sensor-auth-apis#validation-validate-user-credentials) |
| **New in version 1** | **Inventory**:  - [connections (Retrieve device connection information)](api/sensor-inventory-apis#connections-retrieve-device-connection-information)- [cves (Retrieve information on CVEs)](api/sensor-inventory-apis#cves-retrieve-information-on-cves)- [devices (Retrieve device information)](api/sensor-inventory-apis#devices-retrieve-device-information)**Alerts**: - [alerts (Retrieve alert information)](api/sensor-alert-apis#alerts-retrieve-alert-information)- [events (Retrieve timeline events)](api/sensor-alert-apis#events-retrieve-timeline-events)**Vulnerabilities**: - [operational (Retrieve operational vulnerabilities)](api/sensor-vulnerability-apis#operational-retrieve-operational-vulnerabilities)- [devices (Retrieve device vulnerability information)](api/sensor-vulnerability-apis#devices-retrieve-device-vulnerability-information)- [mitigation (Retrieve mitigation steps)](api/sensor-vulnerability-apis#mitigation-retrieve-mitigation-steps)- [security (Retrieve security vulnerabilities)](api/sensor-vulnerability-apis#security-retrieve-security-vulnerabilities) |
| **New in version 2** | **Alerts**: - Updates to [alerts (Retrieve alert information)](api/sensor-alert-apis#alerts-retrieve-alert-information) |

Note

Integration APIs are meant to run continuously and create a constantly running data stream, such as to query for new data from the last five minutes. Integration APIs return data with a timestamp.

To simply query data, use the regular, non-integration APIs instead, for a specific sensor to query devices from that sensor only.

## Epoch time

In all Defender for IoT timestamp values, **Epoch time** is equal to **1/1/1970**.