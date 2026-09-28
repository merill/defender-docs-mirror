---
layout: Conceptual
title: Investigate CIS benchmark recommendation - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-investigate-cis-benchmark
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
description: Investigate CIS benchmark recommendation results in Microsoft Defender for IoT using basic portal analysis and advanced Log Analytics queries for OS baseline findings.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 54870086-cbd3-0b89-221b-08dd3e17c267
document_version_independent_id: 2d9c98be-9cb1-19f9-f1bd-8916099cf85d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-investigate-cis-benchmark.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-investigate-cis-benchmark
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-investigate-cis-benchmark.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: dce1a93e-4808-ce99-354b-5a7a01f5b9b9
---

# Investigate CIS benchmark recommendation - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT evaluates OS configurations against CIS benchmarks and raises recommendations when a device doesn't meet baseline security checks. This article walks you through two investigation approaches: a basic investigation using the Defender for IoT portal, and an advanced investigation that uses Azure Log Analytics to query OS baseline test results, identify failed checks, and pinpoint affected devices across your fleet. The advanced investigation requires a Log Analytics workspace connected to Defender for IoT. For details, see Prerequisites for advanced OS baseline investigation.

## Basic OS baseline security recommendation investigation

You can investigate OS baseline recommendations by navigating to [Defender for IoT in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started). For more information, see how to [Investigate security recommendations](quickstart-investigate-security-recommendations).

## Advanced OS baseline security recommendation investigation

The advanced investigation workflow helps you understand OS baseline test results and query related events in Azure Log Analytics.

**Prerequisites**:

The advanced OS baseline security recommendation investigation is only supported by using Azure Log Analytics and you must connect Defender for IoT to a Log Analytics workspace before continuing.

For more information, see [Configure Microsoft Defender for IoT agent-based solution](tutorial-configure-agent-based-solution).

**To query your IoT security events in Log Analytics for alerts**:

1. In your Log Analytics workspace, go to **Logs** &gt; **AzureSecurityOfThings** &gt; **SecurityAlert**.
2. In the query editor on the right, enter a KQL query to display the alerts you want to see.
3. Select **Run** to display the alerts that match your query.

For example:

[![Screenshot of the Log Analytics workspace with a Defender for I o T alert query.](media/how-to-investigate-cis-benchmark/log-analytics.png)](media/how-to-investigate-cis-benchmark/log-analytics.png#lightbox)

Note

In addition to alerts, you can also use this same procedure to query for recommendations or raw event data.

## Useful queries to investigate the OS baseline resources

Use the following Kusto queries in your Log Analytics workspace to retrieve the latest OS baseline check results for your devices.

Note

Make sure to replace `<device-id>` with the name(s) you gave your device in each of the following queries.

### Retrieve the latest information

- **Device fleet failure**: Run this query to retrieve the latest information about checks that failed across the device fleet:

    ```kusto
    let lastDates = SecurityIoTRawEvent |
    where RawEventName == "Baseline" |
    summarize TimeStamp=max(TimeStamp) by DeviceId;
    lastDates | join kind=inner (SecurityIoTRawEvent) on TimeStamp, DeviceId |
    extend event = parse_json(EventDetails) |
    where event.BaselineCheckResult == "FAIL" |
    project DeviceId, event.BaselineCheckId, event.BaselineCheckDescription
    ```
- **Specific device failure** - Run this query to retrieve the latest information about checks that failed on a specific device:

    ```kusto
    let id = SecurityIoTRawEvent | 
    extend IoTRawEventId = extractjson("$.EventId", EventDetails, typeof(string)) |
    where TimeGenerated <= now() |
    where RawEventName == "Baseline" |
    where DeviceId == "<device-id>" |
    summarize arg_max(TimeGenerated, IoTRawEventId) |
    project IoTRawEventId;
    SecurityIoTRawEvent |
    extend IoTRawEventId = extractjson("$.EventId", EventDetails, typeof(string)), extraDetails = todynamic(EventDetails) |
    where IoTRawEventId == toscalar(id) |
    where extraDetails.BaselineCheckResult == "FAIL" |
    project DeviceId, CceId = extraDetails.BaselineCheckId, Description = extraDetails.BaselineCheckDescription
    ```
- **Specific device error** - Run this query to retrieve the latest information about checks that have an error on a specific device:

    ```kusto
    let id = SecurityIoTRawEvent |
    extend IoTRawEventId = extractjson("$.EventId", EventDetails, typeof(string)) |
    where TimeGenerated <= now() |
    where RawEventName == "Baseline" |
    where DeviceId == "<device-id>" |
    summarize arg_max(TimeGenerated, IoTRawEventId) |
    project IoTRawEventId;
    SecurityIoTRawEvent |
    extend IoTRawEventId = extractjson("$.EventId", EventDetails, typeof(string)), extraDetails = todynamic(EventDetails) |
    where IoTRawEventId == toscalar(id) |
    where extraDetails.BaselineCheckResult == "ERROR" |
    project DeviceId, CceId = extraDetails.BaselineCheckId, Description = extraDetails.BaselineCheckDescription
    ```
- **Update device list for device fleet that failed a specific check** - Run this query to retrieve updated list of devices (across the device fleet) that failed a specific check: 

    ```kusto
    let lastDates = SecurityIoTRawEvent |
    where RawEventName == "Baseline" |
    summarize TimeStamp=max(TimeStamp) by DeviceId;
    lastDates | join kind=inner (SecurityIoTRawEvent) on TimeStamp, DeviceId |
    extend event = parse_json(EventDetails) |
    where event.BaselineCheckResult == "FAIL" |
    where event.BaselineCheckId contains "6.2.8" |
    project DeviceId;
    ```