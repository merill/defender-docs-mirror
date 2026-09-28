---
layout: Conceptual
title: Configure sensor settings in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/configure-sensor-settings
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Configure Microsoft Defender for Identity sensor settings to start collecting data, validate your deployment, and prepare additional integrations for full functionality.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 030e1875-bc29-a69a-0f1f-22afa8879b69
document_version_independent_id: 030e1875-bc29-a69a-0f1f-22afa8879b69
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/configure-sensor-settings.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/configure-sensor-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/configure-sensor-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 13afe88e-daf3-aed8-5946-c16b2539ff91
---

# Configure sensor settings in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

In this article, you'll learn how to correctly configure Microsoft Defender for Identity sensor settings to start seeing data. You'll need to do additional configuration and integration to take advantage of Defender for Identity's full capabilities.

## View and configure sensor settings

After the Defender for Identity sensor is installed, do the following to view and configure Defender for Identity sensor settings:

1. In [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** &gt; **Identities** &gt; **Sensors**. For example:

![Screenshot that shows the sensor page in the Microsoft Defender portal.](../media/download-sensor/sensor-page.png)

The **Sensors** page displays all of your Defender for Identity sensors, listing the following details per sensor:

- Sensor name
- Sensor domain membership
- Sensor version number
- Whether updates should be [delayed (delayed sensor updates)](../sensor-settings#delayed-update-for-sensor-v2x)
- Sensor service status

- Sensor status
- Sensor health status
- The number of health issues
- When the sensor was created

For more information, see [Sensor details](../sensor-settings#sensor-details).

1. Select **Filters** to select the filters you want visible. For example:

    [![Screenshot of the Sensors page filter options for narrowing the sensor list.](../media/sensor-filters.png)](../media/sensor-filters.png#lightbox)
2. Use the displayed filters to determine which sensors to display. For example:

    [![Screenshot of a filtered list of sensors.](../media/filtered-sensor.png)](../media/filtered-sensor.png#lightbox)
3. Select a sensor to show a details pane with more information about the sensor and its health status. For example:

    [![Screenshot of a sensor details pane showing health status and configuration.](../media/sensor-details.png)](../media/sensor-details.png#lightbox)
4. Scroll down and select **Manage sensor** to show a pane where you can configure sensor details. For example:

    [![Screenshot of the Sensors page with the Manage sensor option selected to open sensor configuration settings.](../media/manage-sensor.png)](../media/manage-sensor.png#lightbox)
5. Configure the following sensor details:

    | Name | Description |
    | --- | --- |
    | **Description** | Optional. Enter a description for the Defender for Identity sensor. |
    | **Domain Controllers (FQDN)** | Required for the Defender for Identity [standalone sensors](prerequisites-standalone) and [sensors installed on AD FS / AD CS servers](active-directory-federation-services), and can't be modified for the Defender for Identity sensor. Enter the complete FQDN of your domain controller and select the plus sign to add it to the list. For example, **DC1.domain1.test.local**. For any servers you define in the **Domain Controllers** list:  - All domain controllers whose traffic is being monitored via port mirroring by the Defender for Identity standalone sensor must be listed in the **Domain Controllers** list. If a domain controller isn't listed in the **Domain Controllers** list, detection of suspicious activities might not function as expected.  - At least one domain controller in the list should be a global catalog. This enables Defender for Identity to resolve computer and user objects in other domains in the forest. |
    | **Capture Network adapters** | Required.  - For Defender for Identity sensors, all network adapters that are used for communication with other computers in your organization. - For Defender for Identity standalone sensor on a dedicated server, select the network adapters that are configured as the destination mirror port. These network adapters receive the mirrored domain controller traffic. |
6. On the **Sensors** page, select **Export** to export a list of your sensors to a **.csv** file. For example:

    [![Screenshot of the Sensors page with the Export option for downloading the sensor list as a CSV file.](../media/export-sensors.png)](../media/export-sensors.png#lightbox)

## Validate installations

Use the following procedures to validate your Defender for Identity sensor installation.

Note

If you're installing on an AD FS or AD CS server, you use a different set of validations. For more information, see [Validate successful deployment on AD FS / AD CS servers](active-directory-federation-services#validate-successful-deployment).

### Validate successful deployment

To validate that the Defender for Identity sensor has been successfully deployed:

1. Check that the **Azure Advanced Threat Protection sensor** service is running on your sensor machine. After you save the Defender for Identity sensor settings, it might take a few seconds for the service to start.
2. If the service doesn't start, review the **Microsoft.Tri.sensor-Errors.log** file, located by default at `%programfiles%\Azure Advanced Threat Protection sensor\<sensor version>\Logs`, where `<sensor version>` is the version you deployed.

### Verify security alert functionality

The following procedure describes how to verify that security alerts are triggered as expected.

When using the examples in this validation procedure, make sure to replace `contosodc.contoso.azure` and `contoso.azure` with the fully qualified domain name (FQDN) of your Defender for Identity sensor and your domain name, respectively.

1. On a member-joined device, open a command prompt and enter `nslookup`
2. Enter `server` and the FQDN or IP address of the domain controller where the Defender for Identity sensor is installed. For example: `server contosodc.contoso.azure`
3. Enter `ls -d contoso.azure`
4. Repeat the `server` and `ls -d` commands for each sensor you want to test.
5. Access the device details page for the computer you ran the connectivity test from, such as from the **Devices** page, by searching for device name, or from elsewhere in the Defender portal.
6. On the device details tab, select the **Timeline** tab to view the following activity:

    - **Events**: DNS queries performed to a specified domain name
    - **Action type** MdiDnsQuery

If the domain controller or AD FS / AD CS that you're testing is the first sensor you've deployed, wait at least 15 minutes before verifying any logical activity for that domain controller, allowing the database backend to complete the initial microservice deployments.

### Verify latest available sensor version

The Defender for Identity version is updated frequently. Check for the latest version in the Microsoft Defender **Settings** &gt; **Identities** &gt; **About** page.