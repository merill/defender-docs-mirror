---
layout: Conceptual
title: Troubleshoot the Defender for Identity sensor using logs - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/troubleshooting-using-logs
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
description: Use Microsoft Defender for Identity sensor logs to diagnose component behavior and investigate installation or runtime issues. Includes log locations and guidance for troubleshooting.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: abf7e026-af87-85e8-27e1-8d61013e4053
document_version_independent_id: abf7e026-af87-85e8-27e1-8d61013e4053
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/troubleshooting-using-logs.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshooting-using-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/troubleshooting-using-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/00675be6-8413-445a-927c-01fdfb06925d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/3f4c9937-0bf4-403a-90e9-153dbfe1b4c3
platformId: d55f0e7c-cd47-77ce-cda8-421763fbbd3a
---

# Troubleshoot the Defender for Identity sensor using logs - Microsoft Defender for Identity | Microsoft Learn

The Defender for Identity logs provide insight into sensor activity and status at any given point in time.

The Defender for Identity sensor logs are located in the **Logs** subfolder under the sensor installation directory. By default, the sensor is installed in `C:\Program Files\Azure Advanced Threat Protection Sensor`, and the Logs folder can be found at: `C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs`.

## Defender for Identity sensor logs

The Defender for Identity sensor has the following logs:

- **Microsoft.Tri.Sensor.log** – This log contains everything that happens in the Defender for Identity sensor (including resolution and errors). Its main use is getting the overall status of all operations in the chronological order in which they occurred.
- **Microsoft.Tri.Sensor-Errors.log** – This log contains just the errors that are caught by the Defender for Identity sensor. Its main use is performing health checks and investigating issues that need to be correlated to specific times.
- **Microsoft.Tri.Sensor.Updater.log** - This log is used for the sensor updater process, which is responsible for updating the Defender for Identity sensor if configured to do so automatically.
- **Microsoft.Tri.Sensor.Updater-Errors.log** – This log contains just the errors that are caught by the Defender for Identity sensor updater. Its main use is performing health checks and investigating issues that need to be correlated to specific times.

Note

The log files have a maximum size of up to 50 MB. When a log file reaches 50 MB, a new log file is opened and the previous one is renamed to "&lt;original file name&gt;-Archived-00000" where the number increments each time it is renamed. By default, if more than 10 archived files already exist for that specific log file name, the oldest archived files are deleted.

## Defender for Identity deployment logs

The Defender for Identity deployment logs are located in the temp directory of the user who installed the product. Typically, you can find these logs at `%USERPROFILE%\AppData\Local\Temp`. If the deployment was performed by a service, the deployment logs might be located in `C:\Windows\Temp` or `C:\Windows\SystemTemp`, depending on your Windows version and patch level.

Defender for Identity sensor deployment logs:

- **Azure Advanced Threat Protection Microsoft.Tri.Sensor.Deployment.Deployer\_YYYYMMDDHHMMSS.log** - This log file provides the entire process of sensor deployment and can be found in the user's temp folder (`%USERPROFILE%\AppData\Local\Temp`), or in `C:\Windows\Temp` or `C:\Windows\SystemTemp` when deployed by a service.
- **Azure Advanced Threat Protection Sensor\_YYYYMMDDHHMMSS.log** - This log lists the steps in the process of the deployment of the Defender for Identity sensor. Its main use is tracking the Defender for Identity sensor deployment process.
- **Azure Advanced Threat Protection Sensor\_YYYYMMDDHHMMSS\_001\_MsiPackage.log** - This log file lists the steps in the process of the deployment of the Defender for Identity sensor binaries. Its main use is tracking the deployment of the Defender for Identity sensor binaries.

Note

In addition to the deployment logs listed in this section, other logs whose names begin with "Azure Advanced Threat Protection" can also provide information about the deployment process.