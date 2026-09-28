---
layout: Conceptual
title: Create risk assessment reports on an OT sensor - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-create-risk-assessment-reports
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
description: Gain insight into network risks detected by individual Defender for IoT OT sensors or an aggregate view of risks detected by all OT sensors.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 6e4e6ade-ab7a-11be-7f20-9ddd7329cca1
document_version_independent_id: 5982d0bf-8e55-372e-d9d2-18473e7293a4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-create-risk-assessment-reports.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-create-risk-assessment-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-create-risk-assessment-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: da0eba0b-cc3a-899a-dd38-12d58f6b7641
---

# Create risk assessment reports on an OT sensor - Microsoft Defender for IoT | Microsoft Learn

Risk assessment reports provide details about security scores, vulnerabilities, and operational issues for devices that a specific OT network sensor detects. These reports also cover risks from imported firewall rules.

Each Defender for IoT network sensor can generate a risk assessment report. This article explains how to generate, view, and enrich risk assessment reports from individual OT sensors or across multiple sensors.

## Prerequisites

To create risk assessment reports, you must be able to access the OT network sensor you want to generate data for:

- You must be an **Admin** user to import firewall rules to an OT sensor or add backup and anti-virus server addresses.
- You must be an **Admin** or **Security Analyst** user to create or view risk assessment reports on the OT sensor.

For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises)

## Generate risk assessment reports from an OT sensor

Use an individual OT sensor to view reports generated only for the selected sensor.

**To generate a report**:

1. Sign in to the sensor console and select **Risk assessment** &gt; **Generate report**. The report appears in the **Reports list** with the timestamp and report size.

    For example:

    [![Screenshot of a list of risk assessment reports.](media/how-to-generate-reports/risk-assessment-reports-list.png)](media/how-to-generate-reports/risk-assessment-reports-list.png#lightbox)

    Reports are automatically named `risk-assessment-report-<integer>`, where the `<integer>` is incremented automatically.
2. Select the report name to download it and open it in your browser.

## Risk assessment report contents

Risk assessment reports include the following details:

| Details | Description |
| --- | --- |
| **Security scores** | An overall security score for all detected devices, and a security score for each individual device.  Security scores are based on data learned from packet inspection, behavioral modeling engines, and a SCADA-specific state machine design, and are categorized as follows:  - **Secure Devices** are devices with a security score above 90%.  - **Devices Needing Improvement** are devices with a security score between 70 percent and 89%.  - **Vulnerable Devices** are devices with a security score below 70%. |
| **Security and operational issues** | Insight into any of the following security and operational issues:  - Configuration issues  - Device vulnerability, prioritized by security level  - Network security issues  - Network operational issues  - Connections to ICS networks  - Internet connections  - Industrial malware indicators  - Protocol issues  - Attack vectors |
| **Firewall rule risk** | The Risk Assessment report highlights if a rule isn't secure, or if there's a mismatch between the rule and the monitored network. |

## Enrich the risk assessment report

Enrich your sensor with extra data to provide fuller risk assessment reports:

- Import firewall rules to have them assessed for risks in the report
- Lower your risk by defining addresses for your backup and anti-virus server

### Import firewall rules to an OT sensor

Import firewall rules to your OT sensor for analysis in **Risk assessment** reports. Importing firewall rules is supported for the following firewalls:

| Name | Description | File type |
| --- | --- | --- |
| **Check Point** | Firewall export to R77 | .ZIP |
| **Fortinet** | Configuration backup | .CONF |
| **Juniper** | ScreenOS CLI configuration | .TXT |

To import firewall rules:

1. Sign in to your sensor as an **Admin** user and elect **System Settings** &gt; **Import settings** &gt; **Firewall rules**.
2. In the **Firewall rules** pane:

    - Select a firewall type from the dropdown menu
    - Select **+ Import file** to browse to and select the file you want to import.

For example:

[![Screenshot of how to import firewall rules.](media/how-to-generate-reports/import-firewall-rules.png)](media/how-to-generate-reports/import-firewall-rules.png#lightbox)

### Define backup and anti-virus servers on an OT sensor

Backup and anti-virus servers aren't set up on your sensor by default. Define these addresses on your sensor to keep your risk assessment score low.

To add backup and anti-virus server addresses:

1. Sign into your OT sensor and select **System Settings** &gt; **System Properties** &gt; **Vulnerability Assessment**.
2. Add your backup and anti-virus server addresses to the **backup\_servers** and **AV\_addresses** fields, respectively. Use commas to separate multiple addresses.
3. Select **Save** to save your changes.

## View risk assessment reports for multiple sensors

Use an OT sensor to view risk assessment reports for all OT sensors connected to the same management console.

To generate a report:

1. Sign in to your OT sensor and select **Risk assessment**.
2. From the **Select Sensor** drop-down menu, select the sensor for which you want to generate the report, and then select **Generate Report**.

    The new report appears in the **Archived Reports** area. It shows the date, time, security score, and report size.

    For example:

    [![Screenshot of a list of archived reports.](media/how-to-generate-reports/risk-assessment-report-for-multiple-sensors.png)](media/how-to-generate-reports/risk-assessment-report-for-multiple-sensors.png#lightbox)
3. Select **Download** to download a report and open it in your browser.