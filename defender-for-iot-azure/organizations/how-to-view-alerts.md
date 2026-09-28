---
layout: Conceptual
title: View and Manage Alerts on your OT Sensor - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-view-alerts
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
description: Learn about viewing and managing alerts on an OT network sensor.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: a0401595-f3b2-6300-3877-ac0a9526ee86
document_version_independent_id: a563a721-3cc6-8232-55bf-d42fc9249d3a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-view-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-view-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-view-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a4a4ee1c-8e02-995a-7bbb-30443b9d4ce0
---

# View and Manage Alerts on your OT Sensor - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT alerts enhance your network security and operations with real-time details about events logged in your network. OT alerts are triggered when OT network sensors detect changes or suspicious activity in network traffic that needs your attention.

The following sections explain how to view Defender for IoT alerts directly on an OT network sensor. You can also [view and manage Defender for IoT alerts in the Azure portal](how-to-manage-cloud-alerts).

For more information, see [Defender for IoT alerts overview](alerts).

## Prerequisites

- **To have alerts on your OT sensor**, you must have a SPAN port configured for your sensor and Defender for IoT monitoring software installed. For more information, see [Install OT agentless monitoring software](how-to-install-software).
- **To view alerts on the OT sensor**, sign into your sensor as an *Admin*, *Security Analyst*, or *Viewer* user.
- **To manage alerts on an OT sensor**, sign into your sensor as an *Admin* or *Security Analyst* user. Alert management activities include modifying their statuses or severities, *learning* or *muting* an alert, accessing PCAP data, or adding pre-defined comments to an alert.

For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

## View alerts on an OT sensor

Note

When you view alerts in the Azure portal **Alerts** page, some alerts may not correlate with alerts on specific sensors. For more information, see [Investigate alerts that don't correlate with specific sensors](respond-ot-alert#investigate-alerts-that-dont-correlate-with-a-specific-sensor).

1. Sign into your OT sensor console and select the **Alerts** page on the left. By default, the following details are shown in the grid:

    | Name | Description |
    | --- | --- |
    | **Severity** | A predefined alert severity assigned by the sensor that you can modify as needed, including: *Critical*, *Major*, *Minor*, *Warning*. |
    | **Name** | The alert title |
    | **Engine** | The [Defender for IoT detection engine](architecture#defender-for-iot-analytics-engines) that detected the activity and triggered the alert. |
    | **Last detection** | The last time the alert was detected. - If an alert's status is **New**, and the same traffic is seen again, the **Last detection** time is updated for the same alert. - If the alert's status is **Closed** and traffic is seen again, the **Last detection** time is *not* updated, and a new alert is triggered.**Note**: While the sensor console displays an alert's **Last detection** field in real-time, Defender for IoT in the Azure portal may take up to one hour to display the updated time. This display delay explains a scenario where the last detection time in the sensor console isn't the same as the last detection time in the Azure portal. |
    | **Status** | The alert status: *New*, *Active*, *Closed*For more information, see [Alert statuses and triaging options](alerts#alert-statuses-and-triaging-options). |
    | **Source Device** | The source device IP address, MAC, or device name. |
    | **Id** | The unique alert ID, aligned with the ID on the Azure portal.**Note:** If the [alert was merged with other alerts](alerts#alert-management-options) from sensors that detected the same alert, the Azure portal displays the alert ID of the first sensor that generated the alerts. |

    To view more details, select the ![](media/how-to-manage-device-inventory-on-the-cloud/edit-columns-icon.png)**Edit Columns** button.
2. In the **Edit Columns** pane on the right, select **Add Column** and any of the following extra columns:

    | Name | Description |
    | --- | --- |
    | **Destination Device** | The destination device IP address. |
    | **First detection** | The first time the alert activity was detected. |
    | **ID** | The alert ID. |
    | **Last activity** | The last time the alert was changed, including manual updates for severity or status, or automated changes for device updates or device/alert de-duplication |

### Filter alerts displayed

Use the **Search** box, **Time range**, and **Add filter** options to filter the alerts displayed by specific parameters or help locate a specific alert.

For example:

![Screenshot of an OT sensor Alerts page being filtered by Groups.](media/how-to-view-alerts/filter-alerts-groups.png)

Filtering alerts by **Groups** uses any custom groups you may have created in the [Device inventory](how-to-investigate-sensor-detections-in-a-device-inventory) or the [Device map](how-to-work-with-the-sensor-device-map) pages.

### Group alerts displayed

Use the **Group by** menu at the top right to collapse the grid into subsections based on *Severity*, *Name*, *Engine*, or *Status*.

For example, while the total number of alerts appears in the alerts summary header, you may want more specific information about alert count breakdown, such as the number of alerts with a specific severity or status.

## View details and remediate a specific alert

1. Sign into the OT sensor and select **Alerts** on the left-hand menu.
2. Select an alert in the grid to display more details in the pane on the right. The alert details pane includes the alert description, traffic source and destination, and more. Select **View full details** to drill down further. For example:

    ![Screenshot of an alert selected from the Alerts page on an OT sensor.](media/alerts/alerts-on-sensor.png)
3. The alert details page provides more details about the alert, and a set of remediation steps on the **Take action** tab.

    Use the following tabs to gain more contextual insight:

    - **Map View**. View the source and destination devices in a map view with other devices connected to your sensor.
    - **Event Timeline**. View the event together with other recent activity on the related devices. Filter options to customize the data displayed. For example:

        ![Screenshot of an event timeline on an alert details page.](media/alerts/event-timeline-alert-sensor.png)

## Manage alert status and triage alerts

Make sure to update your alert status once you've taken remediation steps so that the progress is recorded. You can update status for a single alert or for a selection of alerts in bulk.

*Learn* an alert to indicate to Defender for IoT that the detected network traffic is authorized. Learned alerts won't be triggered again the next time the same traffic is detected on your network. *Mute* an alert when learning isn't available and you want to ignore a specific scenario on your network.

For more information, see [Alert statuses and triaging options](alerts#alert-statuses-and-triaging-options).

- To manage alert status:

    1. Sign into your OT sensor console and select the **Alerts** page on the left.
    2. Select one or more alerts in the grid whose status you want to update.
    3. Use the toolbar ![](media/how-to-manage-sensors-on-the-cloud/status-icon.png)**Change Status** button or the ![](media/how-to-manage-sensors-on-the-cloud/status-icon.png)**Status** option in the details pane on the right to update the alert status.

        The ![](media/how-to-manage-sensors-on-the-cloud/status-icon.png)**Status** option is also available on the alert details page.
- To learn one or more alerts:

    Sign into your OT sensor console and select the **Alerts** page on the left, and then do one of the following:

    - Select one or more learnable alerts in the grid and then select ![](media/how-to-manage-sensors-on-the-cloud/learn-icon.png)**Learn** in the toolbar.
    - On an alert details page, in the **Take Action** tab, select **Learn**.
- To mute an alert:

    1. Sign into your OT sensor console and select the **Alerts** page on the left.
    2. Locate the alert you want to mute and open its alert details page.
    3. On the **Take action** tab, toggle on the **Alert mute** option.
- To unlearn or unmute an alert:

    1. Sign into your OT sensor console and select the **Alerts** page on the left.
    2. Locate the alert you've learned or muted and open its alert details page.
    3. On the **Take action** tab, toggle off the **Alert learn** or **Alert mute** option.

    After you unlearn or unmute an alert, alerts are re-triggered whenever the sensor senses the selected traffic combination.

## Access alert PCAP data

You might want to access raw traffic files, also known as *packet capture files* or *PCAP* files as part of your investigation.

To access raw traffic files for your alert, select **Download PCAP** from the top-left corner of your alert details page:

For example:

![Screenshot of the Download PCAP options on the OT sensor.](media/alerts/download-pcap-sensor.png)

The PCAP file is downloaded and your browser prompts you to open or save it locally.

## Export alerts to CSV or PDF

You may want to export a selection of alerts to a CSV or PDF file for offline sharing and reporting.

- Export alerts to a CSV file from the main **Alerts** page. Export alerts one at a time or in bulk.
- Export alerts to a PDF file one at a time only, either from the main **Alerts** page or an alert details page.

To export alerts to a CSV file:

1. Sign into your OT sensor console and select the **Alerts** page on the left.
2. Use the search box and filter options to show only the alerts you want to export.
3. In the toolbar above the grid, select **Export to CSV**.

The file is generated, and you're prompted to open or save the file locally.

To export an alert to a PDF file:

Sign into your OT sensor console and select the **Alerts** page on the left, and then do one of the following:

- On the **Alerts** page, select an alert and then select **Export to PDF** from the toolbar above the grid.
- On an alerts details page, select **Export to PDF**.

The file is generated, and you're prompted to save the file locally.

## Add alert comments

Alert comments help you accelerate your investigation and remediation process by making communication between team members and recording data more efficient.

If your admin has [created custom alert comments on your OT sensor](how-to-accelerate-alert-incident-response#create-alert-comments-on-an-ot-sensor) for your team to add to alerts, add them from the **Comments** section on an alert details page.

1. Sign into your OT sensor console and select the **Alerts** page on the left.
2. Locate the alert where you want to add a comment and open the alert details page.
3. From the **Choose comment** list, select the comment you want to add, and then select **Add**. For example:

    ![Screenshot of the Comments section on an alert details page on the sensor.](media/alerts/add-comment-sensor.png)

For more information, see [Accelerating OT alert workflows](alerts#accelerating-ot-alert-workflows).

## Remediate aggregated alert violations

To reduce alert fatigue, multiple versions of the same alert violation with identical parameters are listed as one alert item in the Alerts page. As you investigate alerts, an aggregated alert is identified by the *Multiple violations* message that appears under the Source device IP. Use the **Violations** tab to investigate further and the **Take action** tab to remediate the alerts.

1. Sign into your OT sensor console and select the **Alerts** page on the left.

    1. For an aggregated alert the *Multiple violations* message appears underneath the Source device IP address, and the **Violations** tab is displayed.
2. Select the **Violations** tab.

    An inventory table displays the first 10 alerts from this aggregated alert group.
3. Select **Export** to download the CSV data file. Open the file and examine the data.
4. Select the **Take action** tab. Follow the **Remediation steps**.
5. Select **Learn**, if needed. For more information, see [Alert statuses and triaging options](alerts#alert-statuses-and-triaging-options).

Note

An alert with specific violations does not prevent new alerts with different violations from appearing. After you learn an alert, the same alert might be triggered again if the new alert has different violation parameters. To check why the alert was triggered, review the list of violations in the alert list (for the first 10 alerts) or the CSV file you downloaded in step 3.