---
layout: Conceptual
title: Create Custom Alerts - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/quickstart-create-custom-alerts
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
ms.subservice: device-builders
description: Understand, create, and assign custom device alerts for the Microsoft Defender for IoT security service.
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: ebf0d39c-5d0f-fcee-4445-0dcf50cccdf0
document_version_independent_id: 2279f33a-cba1-b7f1-77bc-6fc44d16d215
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/quickstart-create-custom-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/quickstart-create-custom-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/quickstart-create-custom-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 90ec7e18-bda9-fe4d-8f06-22cfa0f29952
---

# Create Custom Alerts - Microsoft Defender for IoT | Microsoft Learn

By using custom security groups and alerts, Defender for IoT takes full advantage of end-to-end security information and categorical device knowledge to improve security across your IoT solution.

## Why use custom alerts?

You know your IoT devices best.

For customers who fully understand their expected device behavior, Defender for IoT allows you to translate this understanding into a device behavior policy and alert on any deviation from expected, normal behavior.

## Use security groups for custom alerts

Security groups enable you to define logical groups of devices, and manage their security state in a centralized way.

Security groups can represent devices with specific hardware, devices deployed in a certain location, or any other grouping suitable to your specific needs.

Security groups are defined by a device twin tag property named **SecurityGroup**. By default, each IoT solution on IoT Hub has one security group named **default**. Change the value of the **SecurityGroup** property to change the security group of a device.

The following JSON example shows a device twin with the **SecurityGroup** tag set to the default security group:

```json
{
  "deviceId": "VM-Contoso12",
  "etag": "AAAAAAAAAAM=",
  "deviceEtag": "ODA1BzA5QjM2",
  "status": "enabled",
  "statusUpdateTime": "0001-01-01T00:00:00",
  "connectionState": "Disconnected",
  "lastActivityTime": "0001-01-01T00:00:00",
  "cloudToDeviceMessageCount": 0,
  "authenticationType": "sas",
  "x509Thumbprint": {
    "primaryThumbprint": null,
    "secondaryThumbprint": null
  },
  "version": 4,
  "tags": {
    "SecurityGroup": "default"
  },
```

Use security groups to group your devices into logical categories. After creating the groups, assign them to the custom alerts of your choice, for the most effective end-to-end IoT security solution.

## Configure custom alert settings

1. Open your IoT Hub and select **Settings** from the **Security** menu.
2. Select on **Custom alerts**.
3. Choose a security group to which you wish to apply the customization.
4. Select **Add a custom alert**.
5. Select a custom alert from the drop-down list.
6. Edit the required properties and select **OK**.
7. Make sure to select **Save**. Without saving the new alert, the alert is deleted the next time you close IoT Hub.

## Alerts available for customization

Defender for IoT offers a large number of alerts, which can be customized according to your specific needs. Review the [customizable alert table](concept-customizable-security-alerts) for alert severity, data source, description, and our suggested remediation steps if and when each alert is received.