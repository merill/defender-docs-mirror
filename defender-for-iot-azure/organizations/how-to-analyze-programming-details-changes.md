---
layout: Conceptual
title: Analyze programming details and changes on an OT sensor - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-analyze-programming-details-changes
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
description: Discover suspicious programming activity by investigating programming events occurring on your network devices.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 5bc0bea3-da76-87c3-1edd-40e9c0562a69
document_version_independent_id: 23a778c0-e43d-b409-6043-5ba609db5692
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-analyze-programming-details-changes.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-analyze-programming-details-changes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-analyze-programming-details-changes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 340aa187-d49c-8546-014a-8a1a9565614e
---

# Analyze programming details and changes on an OT sensor - Microsoft Defender for IoT | Microsoft Learn

Enhance forensics by displaying programming events occurring on your network devices and analyzing any code changes using the OT sensor. Watching for programming events helps you investigate suspicious programming activity, such as:

- **Human error**: An engineer programming the wrong device.
- **Corrupted programming automation**: Programming errors due to automation failures.
- **Hacked systems**: Unauthorized users logged into a programming device.

Use the **Programming Timeline** tab on your OT network sensor to review programming data, such as when investigating an alert about unauthorized programming, after a planned controller update, or when a process or machine isn't working correctly and you want to understand who made the last update and when.

Programming activity shown on OT sensors include both *authorized* and *unauthorized* events. Authorized events are performed by devices that are either learned or manually defined as programming devices. Unauthorized events are performed by devices that haven't been learned or manually defined as programming devices.

Note

Programming data is available for devices using text based programming protocols, such as DeltaV.

## Prerequisites

To perform the procedures in this article, make sure that you have:

- An OT sensor installed and configured, with text based programming protocol traffic.
- Access to the sensor as a **Viewer**, **Security analyst** or **Admin** user.

## Access programming data

The **Programming Timeline** tab can be accessed from the **Device map**, **Device inventory**, and **Event timeline** pages in the sensor console.

### Access programming data from the device map

To open programming data from the device map:

1. Sign into the OT sensor console and select **Device map**.
2. In the **Groups** area to the left of the map, select **Filter** &gt; **OT Protocols** &gt; select a text based programming protocol, such as DeltaV.
3. In the map, right-click on the device you want to analyze, and select **Programming timeline**.

    [![Screenshot of the programming timeline option from the device map.](media/analyze-programming/select-programming-timeline-from-device-map.png)](media/analyze-programming/select-programming-timeline-from-device-map.png#lightbox)

    The device details page opens with the **Programming Timeline** tab open.

### Access programming data from the device inventory

To access programming data from the device inventory:

1. Sign into the OT sensor console and select **Device inventory**.
2. Filter the device inventory to show devices using text based programming protocols, such as DeltaV.
3. Select the device you want to analyze, and then select **View full details** to open the device details page.
4. On the device details page, select the **Programming Timeline** tab.

    For example:

    [![Screenshot of programming timeline tab on device details page.](media/analyze-programming/programming-timeline-window-device-inventory.png)](media/analyze-programming/programming-timeline-window-device-inventory.png#lightbox)

### Access programming data from the event timeline

Use the event timeline to display a timeline of events in which programming changes were detected.

1. Sign into the OT sensor console and select **Event timeline**.
2. Filter the event timeline for devices using text based programming protocols, such as **DeltaV**.
3. Select the event you want to analyze to open the event details pane on the right, and then select **Programming timeline**.

## View programming details

The **Programming Timeline** tab shows details about each device that was programmed. Select an event and a file to view full programming details on the right. In the **Programming Timeline** tab:

- The **Recent Events** area lists the 50 most recent events detected by the OT sensor. Hover over an event period select the star to mark the event as an **Important** event.
- The **Files** area lists programming files detected for the selected device. The OT sensor can display a maximum of 300 files per device, where each file has a maximum size of 15 MB. The **Files** area lists each file's name and size, and one of the following statuses to indicate the programming event that occurred:

    - **Added**: The programming file was added to the endpoint
    - **Updated**: The programming file was updated on the endpoint
    - **Deleted**: The programming file was removed from the endpoint
    - **Unknown**: No changes were detected for the programming file
- When a programming file is opened on the right, the device that was programmed is listed as the *programmed asset*. Multiple devices may have made programming changes on the device. Devices that made changes are listed as the *programming assets*, and details include the hostname, when the change was made, and the user that was signed in to the device at the time.

Tip

Select the ![](media/analyze-programming/download-icon.png) download button to download a copy of the currently displayed programming file.

For example:

[![Screenshot of viewing programming details in programming timeline.](media/analyze-programming/programming-timeline-2.png)](media/analyze-programming/programming-timeline-2.png#lightbox)

## Compare OT device programming files

Compare multiple programming detail files to identify discrepancies or investigate suspicious activity.

**To compare files:**

1. Open a programming file from an alert or from the **Device map** or **Device inventory** pages.
2. With your first file open, select the compare ![](media/analyze-programming/compare-icon.png) button.
3. In the **Compare** pane, select a file for comparison by selecting the scale icon under **Action** next to the file. For example:

    [![Screenshot of compare files pane.](media/analyze-programming/compare-file-pane.png)](media/analyze-programming/compare-file-pane.png#lightbox)

    The selected file opens up in a new pane for side-by-side comparison with the first file. The current file installed on the programmed device is labeled *Current* at the top of the file.

    [![Screenshot of programming file comparison side by side.](media/analyze-programming/compare-files-side-by-side.png)](media/analyze-programming/compare-files-side-by-side.png#lightbox)

    Scroll through the files to see the programming details and any differences between the files. Differences between the two files are highlighted in green and red.