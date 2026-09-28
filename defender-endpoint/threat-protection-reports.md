---
layout: Conceptual
title: Microsoft Defender for Endpoint reports - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/threat-protection-reports
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Access the various reports for devices, protection features, and more in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: article
ms.date: 2025-02-04T00:00:00.0000000Z
locale: en-us
document_id: c5f5936a-4fd9-8cb1-6aab-5c2edd5949ed
document_version_independent_id: c5f5936a-4fd9-8cb1-6aab-5c2edd5949ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/threat-protection-reports.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-protection-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/threat-protection-reports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: a9d70e22-33a1-c8e7-44ea-9e921c3e9fe3
---

# Microsoft Defender for Endpoint reports - Microsoft Defender for Endpoint | Microsoft Learn

This article provides an overview of the reports available to Microsoft Defender for Endpoint users. It offers information on various reports that can be used to collect data, summarize findings, and obtain recommended actions when applicable.

## Monthly security summary

The **monthly security summary** report helps organizations get a visual summary of key findings and overall preventative actions taken to enhance the organization's overall security posture completed in the last 30 or 90 days. It helps you identify areas of strength and improvement, track your progress over time, and prioritize your actions based on risk and impact.

To access this report, navigate to **Reports &gt; Endpoints &gt; Monthly Security Summary**. The monthly security summary report contains the following sections:

| Section | Description |
| --- | --- |
| [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score) | Microsoft Secure Score is a measurement of an organization's security posture and how well you have implemented security best practices and recommendations across the devices in your organization. The secure score card shows how the overall cybersecurity strength of an organization has improved in the past month and how it compares to other companies with similar number of managed devices. |
| Secure score compared to other organizations | This score is an evaluation of an organization's security score in relation to organizations of a similar size. It's a way to benchmark an organization's performance in implementing security measures compared to other organizations of an equivalent size. |
| Devices onboarded | The devices card provides information on the number of devices that were onboarded in the last month as well as devices still not onboarded. Onboarding devices are essential for enabling protection and detection capabilities. |
| Protection against specific threats | This card shows how effective your defenses are against common attack vectors such as phishing and ransomware. A higher number indicates better defense in place against phishing and ransomware. The report shows how many threats were blocked or mitigated in the last month and how your protection level has increased. |
| Web content monitoring and filtering | Shows the number of malicious URLs that were blocked by Microsoft Defender for Endpoint in the last month. The report also shows the categories of URLs that were blocked and the number of clicks for each category. |
| Suspicious or malicious activities | Track how many incidents and alerts were resolved in the past month using the incidents card. The card also shows all active incidents and alerts that require attention. You'll also be able to see a list of the top 10 severe incidents, their status, number of alerts, and the impacted devices and users. |

You can generate a PDF report of the summary, by selecting **Generate PDF report**. The generated report is a summary of the last 30 days.

## Threat protection report

To gather data on Defender for Endpoint threat protection information, you can use the Microsoft Defender portal's alerts queue or create advanced hunting queries. The following sections provide guidance on how to use these tools to find the information you need.

### Use the alert queue filter in the Microsoft Defender portal

You can use the Microsoft Defender portal alerts view, using Defender for Endpoint as the **detection source**, to see the current status of alerts for protected devices. Use the **Status** filter to see *New*, *In progress*, and *Resolved* alerts. [Learn more about the alerts queue](/en-us/defender-xdr/investigate-alerts).

### Use advanced hunting queries

You can also use advanced hunting queries to find Defender for Endpoint threat protection information. [Learn more about advanced hunting in Defender XDR](/en-us/defender-xdr/advanced-hunting-overview). The following sample advanced hunting queries show alert-related information.

#### Alert information by severity, detection source, and category

```kusto
// Severity
AlertInfo
| where Timestamp > startofday(now()) // Today
| summarize count() by Severity
| render columnchart

// Detection source
AlertInfo
| where Timestamp > startofday(now()) // Today
| summarize count() by DetectionSource
| render columnchart

// Detection category
AlertInfo
| where Timestamp > startofday(now()) // Today
| summarize count() by Category
| render columnchart
```

#### Alert trends by severity, detection source, and category

```kusto
// Severity
AlertInfo
| where Timestamp > ago(30d)
| summarize count() by Severity , bin(Timestamp, 1d)
| render timechart

// Detection source
AlertInfo
| where Timestamp > ago(30d)
| summarize count() by DetectionSource , bin(Timestamp, 1d)
| render timechart

// Detection category
AlertInfo
| where Timestamp > ago(30d)
| summarize count() by Category , bin(Timestamp, 1d)
| render timechart
```

## Reports about Defender for Endpoint capabilities

The following reports provide in-depth information about events and actions related to Defender for Endpoint capabilities:

- [Device health reports](device-health-reports)
    - [Microsoft Defender Antivirus health report](device-health-microsoft-defender-antivirus-health)
    - [Sensor health & OS report](device-health-sensor-health-os)
- [Host firewall reporting](host-firewall-reporting)
- [Web protection monitoring report](web-protection-monitoring)
- [Attack surface reduction (ASR) rules report](attack-surface-reduction-rules-report)
- [Device control report](device-control-report)

## Create custom reports using Power BI

You can also create customized reports using Power BI. To create your own report, see [Create custom reports using Power BI](api/api-power-bi).

## Aggregated reporting

You can review all signals collected by Defender for Endpoint by turning on aggregated reporting.

To turn aggregated reporting on, go to **Settings &gt; Endpoints &gt; Advanced features**. Toggle on the **Aggregated reporting** feature. Learn more about [aggregated reporting in Defender for Endpoint](aggregated-reporting).