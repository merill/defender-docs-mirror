---
layout: Conceptual
title: Maintain Threat Intelligence Packages on OT Network Sensors - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-work-with-threat-intelligence-packages
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
description: Learn how to maintain threat intelligence packages on OT network sensors.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 99f06dce-2686-f10c-90db-44b6427b7b15
document_version_independent_id: 05a18dcc-83fe-08e8-e2be-d385f0ce0a6b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-work-with-threat-intelligence-packages.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-work-with-threat-intelligence-packages
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-work-with-threat-intelligence-packages.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0e0226c6-953b-cc45-2339-4c8699a59299
---

# Maintain Threat Intelligence Packages on OT Network Sensors - Microsoft Defender for IoT | Microsoft Learn

Microsoft security teams continually run proprietary ICS threat intelligence and vulnerability research. Security research provides security detection, analytics, and response to Microsoft's cloud infrastructure and services, traditional products and devices, and internal corporate resources.

Microsoft Defender for IoT regularly delivers threat intelligence package updates for OT network sensors, providing increased protection from known and relevant threats and insights that can help your teams triage and prioritize alerts.

Threat intelligence packages contain signatures, such as malware signatures, CVEs, and other security content.

CVE scores shown are aligned with the [National Vulnerability Database (NVD)](https://nvd.nist.gov/vuln-metrics/cvss), and CVSS v3 scores are shown if they're relevant. If there's no CVSS v3 score relevant, the CVSS v2 score is shown instead.

Tip

We recommend ensuring that your OT network sensors always have the latest threat intelligence package installed so that you always have the full context of a threat before an environment is affected, and increased relevancy, accuracy, and actionable recommendations.

Announcements about new packages are available from the [Defender for IoT TechCommunity blog](https://techcommunity.microsoft.com/t5/azure-defender-for-iot/bd-p/AzureDefenderIoT).

## Permissions required to manage threat intelligence packages

To manage threat intelligence packages on OT network sensors, make sure that you have:

- One or more OT sensors onboarded to Defender for IoT. For onboarding steps, see [Onboard OT sensors to Defender for IoT](onboard-sensors).
- Relevant permissions on the Azure portal and any OT network sensors you want to update.

    - **To download threat intelligence packages from the Azure portal**, you need access to the Azure portal as a [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader), [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role.
    - **To push threat intelligence updates to cloud-connected OT sensors from the Azure portal**, you need access to the Azure portal as a [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role.
    - **To manually upload threat intelligence packages to OT sensors**, you need access to the OT sensor as an **Admin** user.

For more information, see [Azure user roles and permissions for Defender for IoT](roles-azure) and [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

## View the most recent threat intelligence package

**To view the most recent package available from Defender for IoT**:

In the Azure portal, select **Sites and sensors** &gt; **Threat intelligence update (Preview)** &gt; **Local update**. The **Sensor TI update** pane shows details about the most recent package. For example:

[![Screenshot of the Sensor TI update pane with the most recent threat intelligence package.](media/how-to-work-with-threat-intelligence-packages/ti-local-update.png)](media/how-to-work-with-threat-intelligence-packages/ti-local-update.png#lightbox)

## Update threat intelligence packages

Defender for IoT supports two update modes: *Automatic* (packages install on sensors as soon as they're released) and *Manual* (you push packages to sensors when needed).

Update threat intelligence packages on your OT sensors using any of the following methods:

- Automatically push updates to cloud-connected OT sensors as they're released.
- Manually push updates to cloud-connected OT sensors.
- Download and manually upload an update package to locally managed OT sensors.

### Automatically push updates to cloud-connected sensors

Threat intelligence packages can be automatically updated to cloud-connected sensors as the packages are released by Defender for IoT.

Ensure automatic threat intelligence package updates by onboarding your cloud-connected sensor with the **Automatic Threat Intelligence Updates** option enabled. For more information, see [Onboard OT sensors to Defender for IoT](onboard-sensors).

To change the update mode after you've onboarded your OT sensor:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors**, and then locate the sensor you want to change.
2. Select the options (**...**) menu for the selected OT sensor &gt; **Edit**.
3. Toggle on or toggle off the **Automatic Threat Intelligence Updates** option as needed.

### Manually push updates to cloud-connected sensors

Your cloud-connected sensors can be automatically updated with threat intelligence packages. However, if you would like to take a more conservative approach, you can push packages from Defender for IoT to sensors only when you feel it's required. Pushing updates manually gives you the ability to control when a package is installed, without the need to download and then upload it to your sensors.

To manually push updates to a single OT sensor:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors**, and locate the OT sensor you want to update.
2. Select the options (**...**) menu for the selected sensor and then select **Push Threat Intelligence update**.

The **Threat Intelligence update status** field displays the update progress.

**To manually push updates to multiple OT sensors**:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors**. Locate and select the OT sensors you want to update.
2. Select **Threat intelligence updates (Preview)** &gt; **Remote update**.

The **Threat Intelligence update status** field displays the update progress for each selected sensor.

### Manually update locally managed sensors

If you're working with locally managed OT sensors, you need to download the updated threat intelligence packages and upload them manually on your sensors.

Tip

The manual download-and-upload method can also be used for cloud-connected sensors if you don't want to push the updates from the Azure portal.

To download threat intelligence packages:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Threat intelligence update (Preview)** &gt; **Local update**.
2. In the **Sensor TI update** pane, select **Download** to download the latest threat intelligence file.

All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

**To update a single sensor:**

1. Sign into your OT sensor and then select **System settings** &gt; **Threat intelligence**.
2. In the **Threat intelligence** pane, select **Upload file**. For example:

    [![Screenshot of where you can upload Threat Intelligence package to a single sensor.](media/how-to-work-with-threat-intelligence-packages/update-threat-intelligence-single-sensor.png)](media/how-to-work-with-threat-intelligence-packages/update-threat-intelligence-single-sensor.png#lightbox)
3. Browse to and select the package you'd downloaded from the Azure portal and upload it to the sensor.

## Review threat intelligence update statuses

On each OT sensor, the threat intelligence update status and version information are shown in the sensor's **System settings &gt; Threat intelligence** settings.

For cloud-connected OT sensors, threat intelligence data is also shown on the [**Sites and sensors** page](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) in the Azure portal. To view threat intelligence statuses from the Azure portal:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Site and sensors**.
2. Locate the OT sensors where you want to check the threat intelligence statues.
3. Note the values of the following columns for your OT sensors:

    | Column name | Description |
    | --- | --- |
    | **Threat Intelligence version** | Version naming is based on the day the package was built by Defender for IoT. |
    | **Threat Intelligence mode** | *Automatic* indicates that newly available packages will be automatically installed on sensors as they're released by Defender for IoT. *Manual* indicates that you can push newly available packages directly to sensors as needed. |
    | **Threat Intelligence update status** | Shows one of the following statuses:  - **Failed** - **In Progress** - **Update Available** - **Ok** |

Tip

If a cloud-connected OT sensor shows that a threat intelligence update has failed, we recommend that your check your sensor connection details. On the **Sites and sensors** page, check the **Sensor status** and **Last connected UTC** columns.