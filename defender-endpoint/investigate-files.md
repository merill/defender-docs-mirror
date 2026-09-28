---
layout: Conceptual
title: Investigate Microsoft Defender for Endpoint files - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-files
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the investigation options to get details on files associated with alerts, behaviors, or events.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: concept-article
ms.date: 2023-07-10T00:00:00.0000000Z
ms.subservice: edr
locale: en-us
document_id: 3a745444-a843-b9fd-516c-238683b6d00d
document_version_independent_id: 3a745444-a843-b9fd-516c-238683b6d00d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-files.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-files
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-files.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: c4c21225-c51a-7dca-fe4c-a3c38ec452c5
---

# Investigate Microsoft Defender for Endpoint files - Microsoft Defender for Endpoint | Microsoft Learn

Investigate the details of a file associated with a specific alert, behavior, or event to help determine if the file exhibits malicious activities, identify the attack motivation, and understand the potential scope of the breach.

There are many ways to access the detailed profile page of a specific file. For example, you can use the search feature, click on a link from the **Alert process tree**, **Incident graph**, **Artifact timeline**, or select an event listed in the **Device timeline**.

Once on the detailed profile page, you can switch between the new and old page layouts by toggling **new File page**. The rest of this article describes the newer page layout.

You can get information from the following sections in the file view:

- File details and PE metadata (if it exists)
- Incidents and alerts
- Observed in organization
- File names
- File content and capabilities (if a file has been analyzed by Microsoft)

You can also take action on a file from this page.

## File actions

The file actions are above the file information cards at the top of the profile page. Actions you can perform here include:

- Stop and quarantine
- Manage indicator
- Download file
- Ask Defender Experts
- Manual actions
- Go hunt
- Deep analysis

See [take response action on a file](respond-file-alerts) for more information on these actions.

## File page overview

The file page offers an overview of the file's details and attributes, the incidents and alerts where the file is seen, file names used, the number of devices where the file was seen in the last 30 days, including the dates when the file was first and last seen in the organization, Virus Total detection ratio, Microsoft Defender Antivirus detection, the number of cloud apps connected to the file, and the file's prevalence in devices outside of the organization.

Note

Different users may see dissimilar values in the *devices in organization* section of the file prevalence card. This is because the card displays information based on the role-based access control (RBAC) scope that a user has. This means if a user has been granted visibility on a specific set of devices, they will only see the file organizational prevalence on those devices.

[![Screenshot of the File page overview](/en-us/defender/media/investigate-files/investigatefiles-fileoverview.png)](/en-us/defender/media/investigate-files/investigatefiles-fileoverview.png#lightbox)

## Incidents and alerts

The **Incidents and alerts** tab provides a list of incidents that are associated with the file and the alerts the file is linked to. This list covers much of the same information as the incidents queue. You can choose what kind of information is shown by selecting **Customize columns**. You can also filter the list by selecting **Filter**.

![Screenshot showing incidents and alerts.](https://user-images.githubusercontent.com/96785904/200527005-1fd139dc-7483-4e4c-83ad-855cd198f153.png)

## Observed in organization

The **Observed in organization** tab shows you the devices and cloud apps observed with the file. File history related to devices can be shown up to the last six months, whereas cloud apps-related history is up to the last 30 days

### Devices

This section shows all the devices where the file is detected. The section includes a trending report identifying the number of devices where the file has been observed in the past 30 days. Below the trendline, you can find detailed information on the file on each device where it is seen, including file execution status, first and last seen events on each device, initiating process and time, and file names associated with a device.

You can click on a device on the list to explore the full six months file history on each device and pivot to the first seen event in the device timeline.

[![Screenshot of the devices page within a file](/en-us/defender/media/investigate-files/investigatefiles-devices.png)](/en-us/defender/media/investigate-files/investigatefiles-devices.png#lightbox)

### Cloud apps

Note

The Defender for Cloud Apps workload must be enabled to see file information related to cloud apps.

This section shows all the cloud applications where the file is observed. It also includes information like the file's names, the users associated with the app, the number of matches to a specific cloud app policy, associated apps' names, when the file was last modified, and the file's path.

[![Screenshot of the cloud apps page within a file](/en-us/defender/media/investigate-files/investigatefiles-cloudapps.png)](/en-us/defender/media/investigate-files/investigatefiles-cloudapps.png#lightbox)

## File names

The **File names** tab lists all names the file has been observed to use, within your organizations.

[![The File names tab](media/atp-file-names.png)](media/atp-file-names.png#lightbox)

## File content and capabilities

Note

The file content and capabilities views depend on whether Microsoft analyzed the file.

The File content tab lists information about portable executable (PE) files, including process writes, process creation, network activities, file writes, file deletes, registry reads, registry writes, strings, imports, and exports. This tab also lists all the file's capabilities.

[![Screenshot of a file's content](/en-us/defender/media/investigate-files/investigatefiles-filecontent.png)](/en-us/defender/media/investigate-files/investigatefiles-filecontent.png#lightbox)

The file capabilities view lists a file's activities as mapped to the MITRE ATT&CK™ techniques.

[![Screenshot of a file's capabilities](/en-us/defender/media/investigate-files/investigatefiles-filecapabilities.png)](/en-us/defender/media/investigate-files/investigatefiles-filecapabilities.png#lightbox)