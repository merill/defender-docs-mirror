---
layout: Conceptual
title: Integrate Qradar with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-qradar
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
description: In this tutorial, learn how to integrate Qradar with Microsoft Defender for IoT.
ms.topic: tutorial
ms.date: 2022-06-20T00:00:00.0000000Z
locale: en-us
document_id: b71a0e23-cf1a-da25-29c2-1dfed7f53a5f
document_version_independent_id: 169bf4ea-7f98-dbad-2160-1ef7b4f6ea62
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-qradar.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-qradar
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-qradar.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: e13c3452-e9e0-81f4-d672-d841ae9ff716
---

# Integrate Qradar with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how to integrate Microsoft Defender for IoT with QRadar.

Integrating with QRadar supports:

- Forwarding Defender for IoT alerts to IBM QRadar for unified IT and OT security monitoring and governance.
- An overview of both IT and OT environments, allowing you to detect and respond to multi-stage attacks that often cross IT and OT boundaries.
- Integrating with existing SOC workflows.

## Prerequisites

- Access to a Defender for IoT OT sensor as an Admin user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).
- Access to the QRadar Admin area.

## Configure Syslog listener for QRadar

**To configure the Syslog listener to work with QRadar**:

1. Sign in to QRadar and select **Admin** &gt; **Data Sources**.
2. In the Data Sources window, select **Log Sources**.
3. In the **Modal** window, select **Add**.
4. In the **Add a log source** dialog box, define the following parameters:

    | Parameter | Description |
    | --- | --- |
    | **Log Source Name** | `<Sensor name>` |
    | **Log Source Description** | `<Sensor name>` |
    | **Log Source Type** | `Universal LEEF` |
    | **Protocol Configuration** | `Syslog` |
    | **Log Source Identifier** | `<Sensor name>` |

    Note

    The Log Source Identifier name must not include white spaces. We recommend replacing any white spaces with an underscore.
5. Select **Save**, and then **Deploy Changes**.

## Deploy a Defender for IoT QID

A **QID** is a QRadar event identifier. Since all Defender for IoT reports are tagged under the same, **Sensor Alert** event, you can use the same QID for these events in QRadar.

**To deploy a Defender for IoT QID**:

1. Sign in to the QRadar console.
2. Create a file named `xsense_qids`.
3. In the file, use the following command: `,XSense Alert,XSense Alert Report From <XSense Name>,5,7001`.
4. Run: `sudo /opt/qradar/bin/qidmap_cli.sh -i -f <path>/xsense_qids`.

    A confirmation message appears, indicating that the QID was deployed successfully.

## Create QRadar forwarding rules

Create a forwarding rule from your OT sensor to forward alerts to QRadar.

Forwarding alert rules run only on alerts triggered after the forwarding rule is created. The rule doesn't affect any alerts already in the system from before the forwarding rule was created.

The following code is an example of a payload sent to QRadar:

```sample
<9>May 5 12:29:23 sensor_Agent LEEF:1.0|CyberX|CyberX platform|2.5.0|CyberX platform Alert|devTime=May 05 2019 15:28:54 devTimeFormat=MMM dd yyyy HH:mm:ss sev=2 cat=XSense Alerts title=Device is Suspected to be Disconnected (Unresponsive) score=81 reporter=192.168.219.50 rta=0 alertId=6 engine=Operational senderName=sensor Agent UUID=5-1557059334000 site=Site zone=Zone actions=handle dst=192.168.2.2 dstName=192.168.2.2 msg=Device 192.168.2.2 is suspected to be disconnected (unresponsive).
```

When configuring the forwarding rule:

1. In the **Actions** area, select **Qradar**.
2. Enter details for the QRadar host, port, and timezone.
3. Optionally, select to enable encryption, and then configure encryption, and/or select to manage alerts externally.

For more information, see [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners).

## Map notifications to QRadar

1. Sign into your QRadar console, and select **QRadar**&gt; **Log Activity** .
2. Select **Add Filter**, and define the following parameters:

    | Parameter | Description |
    | --- | --- |
    | **Parameter** | `Log Sources [Indexed]` |
    | **Operator** | `Equals` |
    | **Log Source Group** | `Other` |
    | **Log Source** | `<Xsense Name>` |
3. Locate an unknown report detected from your Defender for IoT sensor and double-click it.
4. Select **Map Event**.
5. In the **Modal Log Source Event** page, select:

    - **High-Level Category**: Suspicious Activity + Low-Level Category - Unknown Suspicious Event + Log
    - **Source Type**: Any
6. Select **Search**.
7. From the results, select the line in which the name XSense appears, and select **OK**.

All of the sensor reports from now on are tagged as Sensor Alerts.

The following new fields appear in QRadar:

- **UUID**: Unique alert identifier, such as 1-1555245116250.
- **Site**: The site where the alert was discovered.
- **Zone**: The zone where the alert was discovered.

For example:

```rest
<9>May 5 12:29:23 sensor_Agent LEEF:1.0|CyberX|CyberX platform|2.5.0|CyberX platform Alert|devTime=May 05 2019 15:28:54 devTimeFormat=MMM dd yyyy HH:mm:ss sev=2 cat=XSense Alerts title=Device is Suspected to be Disconnected (Unresponsive) score=81 reporter=192.168.219.50 rta=0 alertId=6 engine=Operational senderName=sensor Agent UUID=5-1557059334000 site=Site zone=Zone actions=handle dst=192.168.2.2 dstName=192.168.2.2 msg=Device 192.168.2.2 is suspected to be disconnected (unresponsive).
```

Note

The forwarding rule you create for QRadar uses the `UUID` API from the OT sensor. For more information, see [UUID (Manage alerts based on the UUID)](api/management-alert-apis#uuid-manage-alerts-based-on-the-uuid).

## Add custom fields to the alerts

**To add custom fields to alerts**:

1. Select **Extract Property**.
2. Select **Regex Based**.
3. Configure the following fields:

    | Parameter | Description |
    | --- | --- |
    | **New Property** | One of the following:  - Sensor Alert Description  - Sensor Alert ID  - Sensor Alert Score  - Sensor Alert Title  - Sensor Destination Name  - Sensor Direct Redirect  - Sensor Sender IP  - Sensor Sender Name  - Sensor Alert Engine  - Sensor Source Device Name |
    | **Optimize Parsing** | Check on. |
    | **Field Type** | `AlphaNumeric` |
    | **Enabled** | Check on. |
    | **Log Source Type** | `Universal LEAF` |
    | **Log Source** | `<Sensor Name>` |
    | **Event Name** | Should be already set as *Sensor Alert* |
    | Capture Group | 1 |
    | Regex | Define the following:  - Sensor Alert Description RegEx: `msg=(.*)(?=\t)` - Sensor Alert ID RegEx: `alertId=(.*)(?=\t)` - Sensor Alert Score RegEx: `Detected score=(.*)(?=\t)` - Sensor Alert Title RegEx: `title=(.*)(?=\t)` - Sensor Destination Name RegEx: `dstName=(.*)(?=\t)` - Sensor Direct Redirect RegEx: `rta=(.*)(?=\t)` - Sensor Sender IP: RegEx: `reporter=(.*)(?=\t)` - Sensor Sender Name RegEx: `senderName=(.*)(?=\t)` - Sensor Alert Engine RegEx: `engine =(.*)(?=\t)` - Sensor Source Device Name RegEx: `src` |