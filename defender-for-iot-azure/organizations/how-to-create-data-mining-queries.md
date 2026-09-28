---
layout: Conceptual
title: Create data mining queries and reports in Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-create-data-mining-queries
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
description: Create data mining queries and generate detailed reports about OT network devices in Defender for IoT, including connectivity, ports, firmware, programming commands, and device state.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0604ac11-6649-752d-ed01-ce5e0c716176
document_version_independent_id: e2f025ab-c8ad-c085-4801-08219a0f2e30
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-create-data-mining-queries.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-create-data-mining-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-create-data-mining-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 22e5b1d7-df2b-6ca4-6efd-b72d9abbe4e8
---

# Create data mining queries and reports in Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Run data mining queries to view details about the network devices detected by your OT sensor, like internet connectivity, ports and protocols, firmware versions, programming commands, and device state.

Defender for IoT OT network sensors provide a series of out-of-the-box reports for you to use. Both out-of-the-box and custom data mining reports always show information that’s correct for the day you’re viewing the report, rather than the day the report or query was created.

Data mining query data is continuously saved until a device is deleted, and is automatically backed on a daily basis to ensure system continuity.

## Prerequisites

To create data mining reports, you must be able to access the OT network sensor you want to generate data for as an **Admin** or **Security Analyst** user.

For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

## View an OT sensor predefined data mining report

To view current data on a predefined, out-of-the-box data mining report, sign into the OT sensor and select **Data Mining** on the left.

The following out-of-the-box reports are listed in the **Recommended** area, ready for you to use:

| Report | Description |
| --- | --- |
| **Programming Commands** | Lists all detected devices that send industrial programming commands. |
| **Internet Activity** | Lists all detected devices that are connected to the internet. |
| **Excluded CVEs** | Lists all detected devices that have CVEs that were manually excluded from the **CVEs** report. |
| **Active Devices (Last 24 Hours)** | Lists all detective devices that have had active traffic within the last 24 hours. |
| **Remote Access** | Lists all detected devices that communicate through remote session protocols. |
| **CVEs** | Lists all detected devices with known vulnerabilities, along with CVSS risk scores.  Select **Edit** to delete and exclude specific CVEs from the report. **Tip**: Delete CVEs to exclude them from the list to have your attack vector reports to reflect your network more accurately. |
| **Nonactive Devices (Last 7 Days)** | Lists all detected devices that haven't communicated for the past seven days. |

Select a report to view today’s data. Use the ![](media/how-to-generate-reports/refresh-icon.png)**Refresh**, ![](media/how-to-generate-reports/expand-all-icon.png)**Expand all**, and ![](media/how-to-generate-reports/collapse-all-icon.png)**Collapse all** options to update and change your report views.

## Create an OT sensor custom data mining report

Create your own custom data mining report if you have reporting needs not covered by the out-of-the-box reports. Once created, custom data mining reports are visible to all users.

To create a custom data mining report:

1. Sign into the OT sensor and select **Data Mining** &gt; **Create report**.
2. In the **Create new report** pane on the right, enter the following values:

    | Name | Description |
    | --- | --- |
    | **Name** / **Description** | Enter a meaningful name for your report and an optional description. |
    | **Choose category** | Select the categories to include in your report.  For example, select **Internet Domain Allowlist** under **DNS** to create a report of the allowed internet domains and their resolved IP addresses. |
    | **Order by** | Select to sort your data by category or by activity. |
    | **Filter by** | Define a filter for your report using any of the following parameters:  - **Results within the last**: Enter a number and then select **Minutes**, **Hours**, or **Days** - **IP address / MAC address / Port**: Enter one or more IP addresses, MAC addresses, and ports to filter into your report. Enter a value and then select + to add it to the list. - **Device group**: Select one or mode device groups to filter into your report. |
    | **Add filter type** | Select to add any of the following filter types into your report.  - Transport (GENERIC)  - Protocol (GENERIC)  - TAG (GENERIC)  - Maximum value (GENERIC)  - State (GENERIC)  - Minimum value (GENERIC)  Enter a value in the relevant field and then select + to add it to the list. |
3. Select **Save**. Your data mining report is shown in the **My reports** area. For example:

    [![Screenshot of a list of customized data mining reports.](media/how-to-generate-reports/custom-data-mining-reports.png)](media/how-to-generate-reports/custom-data-mining-reports.png#lightbox)

## Manage OT sensor data mining report data

Each data mining report on an OT sensor has the following options for managing your data:

| Option | Description |
| --- | --- |
| ![](media/how-to-generate-reports/export-icon.png)**Export to CSV** | Export the current report data to a CSV file. |
| ![](media/how-to-generate-reports/export-icon.png)**Export to PDF** | Export the current report data to a PDF file. |
| ![](media/how-to-generate-reports/snapshot-icon.png)**Snapshots** | Save the current report data as a snapshot you can return to later. |
| ![](media/how-to-generate-reports/manage-icon.png)**Manage report** | Update the values of an existing custom data mining report. This option is disabled for Recommended reports. |
| ![](media/how-to-generate-reports/edit-icon.png)**Edit mode** | Select to remove specific results from the saved report. |

To update an existing custom data mining report, select **Manage report** and edit the **Name**, **Choose category**, **Order by**, **Filter by**, and **Add filter type** fields.