---
layout: Conceptual
title: Create an onboarding or offboarding notification rule - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/onboarding-notification
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get a notification when a local onboarding or offboarding script is used.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0d686535-ae18-034e-9f55-d56ad75f5602
document_version_independent_id: 0d686535-ae18-034e-9f55-d56ad75f5602
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/onboarding-notification.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: onboarding-notification
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/onboarding-notification.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: cf623bd9-9ade-c958-c21f-5d1dcbb51d68
---

# Create an onboarding or offboarding notification rule - Microsoft Defender for Endpoint | Microsoft Learn

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

Create a notification rule so that when a local onboarding or offboarding script is used, you are notified.

## Before you begin

You need to have access to:

- Power Automate (Per-user plan at a minimum). For more information, see [Power Automate pricing page](https://make.powerautomate.com/pricing/).
- Azure Table or SharePoint List or Library / SQL DB.

## Create the notification flow

Perform the following steps to create the notification flow in Power Automate:

1. Go to the [Power Automate portal](https://make.powerautomate.com/) and sign in.
2. Navigate to **My flows &gt; New &gt; Scheduled - from blank**.

    [![The flow](media/new-flow.png)](media/new-flow.png#lightbox)
3. Build a scheduled flow.

    1. Enter a flow name.
    2. Specify the start and time.
    3. Specify the frequency. For example, every 5 minutes.

    [![The notification flow](media/build-flow.png)](media/build-flow.png#lightbox)
4. Select the + button to add a new action. This action adds an HTTP request to the Defender for Endpoint devices API. You can also replace it with the out-of-the-box **WDATP Connector** (action: **Machines - Get list of machines**).

    [![The recurrence and add action](media/recurrence-add.png)](media/recurrence-add.png#lightbox)
5. Enter the following HTTP fields:

    - Method: **GET** as a value to get the list of devices.
    - URI: Enter `https://api.securitycenter.microsoft.com/api/machines`.
    - Authentication: Select **Active Directory OAuth**.
    - Tenant: Sign-in to https://portal.azure.com and navigate to **Microsoft Entra ID &gt; App Registrations** and get the Tenant ID value.
    - Audience: `https://securitycenter.onmicrosoft.com/windowsatpservice\`
    - Client ID: Sign-in to https://portal.azure.com and navigate to **Microsoft Entra ID &gt; App Registrations** and get the Client ID value.
    - Credential Type: Select **Secret**.
    - Secret: Sign-in to https://portal.azure.com and navigate to **Microsoft Entra ID &gt; App Registrations** and get the Tenant ID value.

    [![The HTTP conditions](media/http-conditions.png)](media/http-conditions.png#lightbox)
6. Add a new step by selecting **Add new action** then search for **Data Operations** and select **Parse JSON**.

    [![The data operations entry](media/data-operations.png)](media/data-operations.png#lightbox)
7. Add Body in the **Content** field.

    [![The parse JSON section](media/parse-json.png)](media/parse-json.png#lightbox)
8. Select the **Use sample payload to generate schema** link. [![The parse JSON with payload](media/parse-json-schema.png)](media/parse-json-schema.png#lightbox)
9. Copy and paste the following JSON snippet:

    ```json
    {
        "type": "object",
        "properties": {
            "@@odata.context": {
                "type": "string"
            },
            "value": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "type": "string"
                        },
                        "computerDnsName": {
                            "type": "string"
                        },
                        "firstSeen": {
                            "type": "string"
                        },
                        "lastSeen": {
                            "type": "string"
                        },
                        "osPlatform": {
                            "type": "string"
                        },
                        "osVersion": {},
                        "lastIpAddress": {
                            "type": "string"
                        },
                        "lastExternalIpAddress": {
                            "type": "string"
                        },
                        "agentVersion": {
                            "type": "string"
                        },
                        "osBuild": {
                            "type": "integer"
                        },
                        "healthStatus": {
                            "type": "string"
                        },
                        "riskScore": {
                            "type": "string"
                        },
                        "exposureScore": {
                            "type": "string"
                        },
                        "aadDeviceId": {},
                        "machineTags": {
                            "type": "array"
                        }
                    },
                    "required": [
                        "id",
                        "computerDnsName",
                        "firstSeen",
                        "lastSeen",
                        "osPlatform",
                        "osVersion",
                        "lastIpAddress",
                        "lastExternalIpAddress",
                        "agentVersion",
                        "osBuild",
                        "healthStatus",
                        "rbacGroupId",
                        "rbacGroupName",
                        "riskScore",
                        "exposureScore",
                        "aadDeviceId",
                        "machineTags"
                    ]
                }
            }
        }
    }
    
    ```
10. Extract the values from the JSON call and check if the onboarded devices is / are already registered at the SharePoint list as an example:

    - If yes, no notification is triggered
    - If no, will register the newly onboarded devices in the SharePoint list and a notification is sent to the Defender for Endpoint admin

    [![The application of the flow to each element](media/flow-apply.png)](media/flow-apply.png#lightbox)

    [![The application of the flow to the Get items element](media/apply-to-each.png)](media/apply-to-each.png#lightbox)
11. Under **Condition**, add the following expression: "length(body('Get\_items')?['value'])" and set the condition to equal to 0.

    [![The application of the flow to each condition](media/apply-to-each-value.png)](media/apply-to-each-value.png#lightbox)[![The condition-1](media/conditions-2.png)](media/conditions-2.png#lightbox)[![The condition-2](media/condition3.png)](media/condition3.png#lightbox)[![The Send an email section](media/send-email.png)](media/send-email.png#lightbox)

## Review the alert notification email

The following image is an example of an email notification.

[![The email notification screen](media/alert-notification.png)](media/alert-notification.png#lightbox)

## Tips for filtering and reducing duplicate alerts

Use the following tips when configuring the notification flow:

- In the device query, you can filter by using the lastSeen property only:

    - Every 60 min:
        - Take all devices last seen in the past seven days.
- For each device:

    - If last seen property is on the one hour interval of [-7 days, -7days + 60 minutes] -&gt; Alert for offboarding possibility.
    - If first seen is on the past hour -&gt; Alert for onboarding.

With this filtering approach, duplicate alerts are not generated.

There are tenants that have numerous devices. Getting all those devices might require paging.

You can split the device lookup into two queries:

1. For offboarding, take only the one-hour interval of [-7 days, -7 days + 60 minutes] using the OData $filter and only notify if the conditions are met.
2. Take all devices last seen in the past hour and check first seen property for them (if the first seen property is within the past hour, the last seen must also be within the same past-hour window).