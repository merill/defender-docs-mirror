---
layout: Conceptual
title: Set up automatic sensor disconnection notifications - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/automate-sensor-disconnection-alerts
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
description: This tutorial describes how to create a playbook in Microsoft Sentinel that automatically sends an email notification when a sensor disconnects.
ms.topic: tutorial
ms.date: 2025-01-06T00:00:00.0000000Z
ms.subservice: sentinel-integration
locale: en-us
document_id: 40c4c2d4-08f1-4251-f04a-7b21dbd2a5e2
document_version_independent_id: aab2f88b-453f-ab36-de4e-1fd535269c1c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/automate-sensor-disconnection-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/automate-sensor-disconnection-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/automate-sensor-disconnection-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 758d2e59-0147-c093-58f7-a2d54a9d7d4b
---

# Set up automatic sensor disconnection notifications - Microsoft Defender for IoT | Microsoft Learn

This tutorial shows you how to create a [playbook](/en-us/azure/sentinel/tutorial-respond-threats-playbook) in Microsoft Sentinel that automatically sends an email notification when a sensor disconnects from the cloud.

In this tutorial, you:

- Create a playbook to send automatic sensor disconnection notifications
- Paste the playbook code into the editor and modify fields
- Set up managed identity for your subscription
- Run a query to confirm that the sensor is offline

## Prerequisites

Before you start, make sure you have:

- Completed [Tutorial: Connect Microsoft Defender for IoT with Microsoft Sentinel](iot-solution).
- The subscription ID for the relevant subscription. In the Azure portal **Subscriptions** page, copy the subscription ID and save it for a later stage.
- The resource group for the relevant subscription. Learn more about [resource groups](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal).

## Create the playbook

1. In Microsoft Sentinel, select **Automation**.
2. In the **Automation** page, select **Create &gt; Playbook with alert trigger**.

    [![Screenshot of creating a playbook for Defender for IoT sensor disconnection.](media/automate-sensor-disconnection-alerts/sentinel-create-playbook.png)](media/automate-sensor-disconnection-alerts/sentinel-create-playbook.png#lightbox)
3. In the **Create playbook** page **Basics** tab, select the subscription and resource group running Microsoft Sentinel, and give the playbook a name.
4. Select **Next: Connections**.
5. In the **Connections** tab, select **Microsoft Sentinel &gt; Connect with managed identity**.
6. Review the playbook information and select **Create playbook**.

    ![Screenshot of reviewing a playbook for Defender for IoT sensor disconnection.](media/automate-sensor-disconnection-alerts/sentinel-save-playbook.png)

    When the playbook is ready, Microsoft Sentinel displays a **Deployment successful** message and navigates to the **Logic app designer** page.

    ![Screenshot of a Deployment successful message for a playbook that sends Defender for IoT sensor disconnection alerts.](media/automate-sensor-disconnection-alerts/sentinel-playbook-successful-message.png)

## Paste the playbook code and modify fields

1. Select **Logic app code view**, and paste the playbook code into the editor.
2. Modify these fields in the code:

    - Under the `post` body, in the `To` field, type the email to which you want to receive the notifications.
    - Under the `office365` parameter:

        - Under the `id` field, replace `Replace with subscription` with the ID of the subscription running Microsoft Sentinel, for example:

        ```json
        "id": "/subscriptions/exampleID/providers/Microsoft.Web/locations/eastus/managedApis/office365"
        ```

        - Under the `connectionId` field, replace `Replace with subscription` with your subscription ID, and replace `Replace with RG name` with your resource group name, for example:

        ```json
         "connectionId": "/subscriptions/exampleID/resourceGroups/ExampleResourceGroup/providers/Microsoft.Web/connections/office365"
        ```
3. Select **Save**.
4. Go back to the **Logic app designer** to view the logic that the playbook follows.

## Set up a managed identity for your subscription

To give the playbook permission to run Keyword Query Language (KQL) queries and get relevant sensor data:

1. In the Azure portal, select **Subscriptions**.
2. Select the subscription running Microsoft Sentinel and select **Access Control (IAM)**.
3. Select **Add &gt; Add Role Assignment**.
4. Search for the **Reader** role.
5. In the **Role** tab, select **Next**.
6. In the **Members** tab, under **Assign access to**, select **Managed Identity**.
7. In the **Select Managed identities** window:

    - Under **Subscription**, select the subscription running Microsoft Sentinel.
    - The **Managed identity** field is automatically selected.
    - Under **Select**, select the name of the playbook you created.

    [![Screenshot showing setting up members for a managed identity while creating a Defender for IoT sensor disconnection alerts playbook.](media/automate-sensor-disconnection-alerts/playbook-permissions-managed-identity-members.png)](media/automate-sensor-disconnection-alerts/playbook-permissions-managed-identity-members.png#lightbox)
8. In the editor, select **HTTP2** and verify that the **Authentication Type** is set to **Managed Identity**.

## Run a query to confirm that the sensor is offline

If you can't create the playbook successfully, run a KQL query in Azure Resource Graph to confirm that the sensor is offline.

1. In the Azure portal, search for *Azure resource graph explorer*.
2. Run the following query:

    ```kusto
    iotsecurityresources  
    
    | where type =='microsoft.iotsecurity/locations/sites/sensors'  
    
    |extend Status=properties.sensorStatus  
    
    |extend LastConnectivityTime=properties.connectivityTime  
    
    |extend Status=iif(LastConnectivityTime<ago(5m),'Disconnected',Status)  
    
    |project SensorName=name, Status, LastConnectivityTime  
    
    |where Status == 'Disconnected' 
    ```

If the sensor has been offline for at least five minutes, the sensor status is **Disconnected**.

Note

It takes up to 15 minutes for the sensor to synchronize the status update with the cloud. This means that the sensor needs to be offline for at least 15 minutes before the status is updated.

### Playbook code

Copy this code and return to the paste the playbook code step.

```json
        { 

    "definition": { 

        "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#", 

        "contentVersion": "1.0.0.0", 

        "triggers": { 

            "Recurrence": { 

                "type": "Recurrence", 

                "recurrence": { 

                    "frequency": "Minute", 

                    "interval": 5, 

                    "startTime": "2024-11-12T19:00:00Z" 

                } 

            } 

        }, 

        "actions": { 

            "For_each": { 

                "type": "Foreach", 

                "foreach": "@body('Parse_JSON_2')", 

                "actions": { 

                    "Condition": { 

                        "type": "If", 

                        "expression": { 

                            "and": [ 

                                { 

                                    "equals": [ 

                                        "@items('For_each')['Status']", 

                                        "Disconnected" 

                                    ] 

                                }, 

                                { 

                                    "less": [ 

                                        "@items('For_each')['LastConnectivityTime']", 

                                        "@getPastTime(5, 'Minute')" 

                                    ] 

                                } 

                            ] 

                        }, 

                        "actions": { 

                            "Send_an_email_(V2)-copy": { 

                                "type": "ApiConnection", 

                                "inputs": { 

                                    "host": { 

                                        "connection": { 

                                            "name": "@parameters('$connections')['office365']['connectionId']" 

                                        } 

                                    }, 

                                    "method": "post", 

                                    "body": { 

                                        "To": [Please add your email], 

                                        "Subject": "Sensor disconnected - True", 

                                        "Body": "<p class=\"editor-paragraph\"><br>True</p>", 

                                        "Importance": "Normal" 

                                    }, 

                                    "path": "/v2/Mail" 

                                } 

                            } 

                        }, 

                        "else": { 

                            "actions": {} 

                        } 

                    } 

                }, 

                "runAfter": { 

                    "Parse_JSON_2": [ 

                        "Succeeded" 

                    ] 

                } 

            }, 

            "HTTP_2": { 

                "type": "Http", 

                "inputs": { 

                    "uri": "https://management.azure.com/providers/Microsoft.ResourceGraph/resources", 

                    "method": "POST", 

                    "headers": { 

                        "Content-Type": "application/json" 

                    }, 

                    "queries": { 

                        "api-version": "2021-03-01" 

                    }, 

                    "body": { 

                        "query": "iotsecurityresources | where type =='microsoft.iotsecurity/locations/sites/sensors' |extend Status=properties.sensorStatus |extend LastConnectivityTime=properties.connectivityTime |extend Status=iif(LastConnectivityTime<ago(5m),'Disconnected',Status) |project SensorName=name, Status, LastConnectivityTime | where Status == 'Disconnected'" 

                    }, 

                    "authentication": { 

                        "type": "ManagedServiceIdentity" 

                    } 

                }, 

                "runAfter": {} 

            }, 

            "Parse_JSON": { 

                "type": "ParseJson", 

                "inputs": { 

                    "content": "@body('HTTP_2')", 

                    "schema": { 

                        "properties": { 

                            "count": { 

                                "type": "integer" 

                            }, 

                            "data": { 

                                "items": { 

                                    "properties": { 

                                        "LastConnectivityTime": { 

                                            "type": "string" 

                                        }, 

                                        "SensorName": { 

                                            "type": "string" 

                                        }, 

                                        "Status": { 

                                            "type": "string" 

                                        } 

                                    }, 

                                    "required": [ 

                                        "SensorName", 

                                        "Status", 

                                        "LastConnectivityTime" 

                                    ], 

                                    "type": "object" 

                                }, 

                                "type": "array" 

                            }, 

                            "facets": { 

                                "type": "array" 

                            }, 

                            "resultTruncated": { 

                                "type": "string" 

                            }, 

                            "totalRecords": { 

                                "type": "integer" 

                            } 

                        }, 

                        "type": "object" 

                    } 

                }, 

                "runAfter": { 

                    "HTTP_2": [ 

                        "Succeeded" 

                    ] 

                } 

            }, 

            "Parse_JSON_2": { 

                "type": "ParseJson", 

                "inputs": { 

                    "content": "@body('Parse_JSON')?['data']", 

                    "schema": { 

                        "items": { 

                            "properties": { 

                                "LastConnectivityTime": { 

                                    "type": "string" 

                                }, 

                                "SensorName": { 

                                    "type": "string" 

                                }, 

                                "Status": { 

                                    "type": "string" 

                                } 

                            }, 

                            "required": [ 

                                "SensorName", 

                                "Status", 

                                "LastConnectivityTime" 

                            ], 

                            "type": "object" 

                        }, 

                        "type": "array" 

                    } 

                }, 

                "runAfter": { 

                    "Parse_JSON": [ 

                        "Succeeded" 

                    ] 

                } 

            } 

        }, 

        "outputs": {}, 

        "parameters": { 

            "$connections": { 

                "type": "Object", 

                "defaultValue": {} 

            } 

        } 

    }, 

    "parameters": { 

        "$connections": { 

            "value": { 

                "office365": { 

                    "id": "/subscriptions/[Replace with Subscription ID]/providers/Microsoft.Web/locations/eastus/managedApis/office365", 

                    "connectionId": "/subscriptions/[Replace with Subscription ID]/resourceGroups/[replace with RG name]/providers/Microsoft.Web/connections/office365", 

                    "connectionName": "office365" 

                } 

            } 

        } 

    } 

} 
```