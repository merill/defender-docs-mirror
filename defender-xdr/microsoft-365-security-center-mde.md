---
layout: Conceptual
title: Microsoft Defender for Endpoint in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-365-security-center-mde
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Get an overview of what to expect when running Microsoft Defender for Endpoint in the Microsoft Defender portal
ms.service: defender-xdr
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
ms.date: 2024-10-16T00:00:00.0000000Z
audience: ITPro
ms.topic: article
search.appverid:
- MOE150
- MET150
ms.collection:
- m365-security
- tier2
ms.custom: admindeeplinkDEFENDER
locale: en-us
document_id: 564dac6b-81d3-ffdf-1054-5aeebbe4f14c
document_version_independent_id: 564dac6b-81d3-ffdf-1054-5aeebbe4f14c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-365-security-center-mde.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-365-security-center-mde
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-365-security-center-mde.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 910afe62-bb75-01ae-4e97-150f6500bfa8
---

# Microsoft Defender for Endpoint in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

[Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) is part of the Microsoft Defender portal, delivering a unified experience for security teams to manage incidents and alerts, hunt for threats, and automate investigations and responses. The Microsoft Defender portal (https://security.microsoft.com) combines security capabilities that protect assets, and detect, investigate, and respond to threats.

Endpoints like laptops, phones, tablets, routers, and firewalls are the entry points to your network. Microsoft Defender for Endpoint helps you secure these endpoints by providing visibility into the activities on your network, and by detecting and responding to advanced threats.

This guide shows you what to expect when running Microsoft Defender for Endpoint in the Microsoft Defender portal.

## Know before you begin

To use Microsoft Defender for Endpoint in the Microsoft Defender portal, you need to have a Microsoft Defender for Endpoint license. For more information, see [Microsoft Defender for Endpoint licensing](/en-us/defender-endpoint/minimum-requirements#licensing-requirements).

In addition, confirm that you have the requirements on hardware and software, browser, network connectivity, and compatibility with Microsoft Defender Antivirus. For more information, see [Microsoft Defender for Endpoint minimum requirements](/en-us/defender-endpoint/minimum-requirements).

You also need to have the required permissions to access the Microsoft Defender portal. For more information, see [Use basic permissions to access the portal](/en-us/defender-endpoint/basic-permissions).

## What to expect

### Investigation and response

Investigation and response capabilities in the Microsoft Defender portal help you investigate and respond to incidents and alerts. Incidents are groups of alerts that are related to each other.

#### Incidents and alerts

Devices involved in incidents are shown in an incident's page [attack story](investigate-incidents#attack-story), incident graph, and [assets](investigate-incidents#assets) tab. You can view the details of the incident, including the devices involved, the alerts that triggered the incident, and the actions taken. You can apply actions to the incident, like isolating devices, collecting investigation packages, and more.

[![Screenshot of the Assets tab highlighting the devices involved in an incident.](media/microsoft-365-security-center-mde/incident-assets-devices-small.png)](media/microsoft-365-security-center-mde/incident-assets-devices.png#lightbox)

Individual alerts are shown in the Alerts page. You can view the details of the alert, including the devices involved, the incident that the alert is part of, and the actions taken. You can also apply actions to the alert in the alert page.

#### Hunting

Proactively search for threats, malware, and malicious activity across your endpoints, Office 365 mailboxes, and more by using [advanced hunting queries](advanced-hunting-overview). These powerful queries can be used to locate and review threat indicators and entities for both known and potential threats.

[Custom detection rules](custom-detection-rules) can be built from advanced hunting queries to help you proactively watch for events that might be indicative of breach activity and misconfigured devices.

#### Action center and submissions

The [Action center](m365d-action-center) shows you the investigations created by automated investigation and response capabilities. This automated self-healing in the Microsoft Defender portal can help security teams by automatically responding to specific events. You can view actions applied to devices, the status of the actions, and approve or reject the automated actions. Navigate to the Action center page under **Investigation & response &gt; Actions & submissions &gt; Action center**.

[![Screenshot of the Action center in the Microsoft Defender portal.](media/microsoft-365-security-center-mde/action-center-mde-small.png)](media/microsoft-365-security-center-mde/action-center-mde.png#lightbox)

You can submit files, email attachments, and URLs to Microsoft Defender for analysis in the [Submission portal](/en-us/defender-endpoint/admin-submissions-mde). You can also view the status of the submissions and the results of the analysis. Navigate to the submissions page under **Investigation & response &gt; Actions & submissions &gt; Submissions**.

### Threat intelligence

You can view emerging threats, new attack techniques, prevalent malware, and information about threat actors and campaigns in the **Threat intelligence** page. Access the [threat analytics](/en-us/defender-endpoint/threat-analytics) dashboard to view the latest threat intelligence and insights. You can also view read and understand how to protect from certain threats through the [analyst report](/en-us/defender-endpoint/threat-analytics-analyst-reports).

Navigate to the threat analytics page under **Threat intelligence &gt; Threat analytics**.

### Device inventory

The **Assets &gt; Devices** page contains the [device inventory](/en-us/defender-endpoint/machines-view-overview), which lists all the devices in your organization where alerts were generated. You can view the details of the devices, including the IP address, criticality level, device category, and device type.

[![Screenshot of the Device inventory page in the Microsoft Defender portal.](media/microsoft-365-security-center-mde/device-inventory-mde-small.png)](media/microsoft-365-security-center-mde/device-inventory-mde.png#lightbox)

### Microsoft Defender for Vulnerability Management and endpoint configuration management

You can find [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management) dashboard under **Endpoints &gt; Vulnerability management**. Defender for Vulnerability Management helps you discover, prioritize, and remediate vulnerabilities in your network. Know more about [prerequisites and permissions](/en-us/defender-vulnerability-management/tvm-prerequisites) and how to [onboard devices to Defender Vulnerability Management](/en-us/defender-vulnerability-management/mdvm-onboard-devices).

The device configuration dashboard is found in **Endpoints &gt; Configuration management &gt; Dashboard**. You can view device security, onboarding via Microsoft Intune and Microsoft Defender for Endpoint, web protection coverage, and attack surface management at a glance.

Security administrators can deploy endpoint security policies to devices in your organization under **Endpoints &gt; Configuration management &gt; Endpoint security policies**. Know more about [endpoint security policies](/en-us/defender-endpoint/endpoint-security-policies-configure).

### Reports

You can view device health, vulnerable devices, monthly security summary, web protection, firewall, device control, and attack surface reduction rules reports in the **Reports** page.

[![Screenshot of the Reports page highlighting the endpoint-related reports in the Microsoft Defender portal.](media/microsoft-365-security-center-mde/reports-mde-small.png)](media/microsoft-365-security-center-mde/reports-mde.png#lightbox)

### General settings

#### Device discovery

In the **Settings &gt; Device discovery** page, you can configure device discovery settings, including the discovery method, exclusions, enabling Enterprise IOT (access dependent), and configure authenticated scan schedules. For more information, see [Device discovery](/en-us/defender-endpoint/device-discovery).

[![Screenshot of the Device discovery page in the Microsoft Defender portal.](media/microsoft-365-security-center-mde/device-discovery-mde-small.png)](media/microsoft-365-security-center-mde/device-discovery-mde.png#lightbox)

#### Endpoint settings

Navigate to the **Settings &gt; Endpoints** page to configure settings for Microsoft Defender for Endpoint, including [advanced features](/en-us/defender-endpoint/advanced-features), email notifications, permissions, and more.

[![Screenshot of the Settings page in the Microsoft Defender portal where endpoint settings are highlighted.](media/microsoft-365-security-center-mde/settings-mde-small.png)](media/microsoft-365-security-center-mde/settings-mde.png#lightbox)

#### Email notifications

You can create rules for specific devices, alert severities, and vulnerabilities to send email notifications to specific users or groups. For more information, see the following information:

- [Configure email notifications for alerts](configure-email-notifications)
- [Configure email notifications for vulnerabilities](/en-us/defender-endpoint/configure-vulnerability-email-notifications)

#### Permissions and roles

To manage roles, permissions, and device groups for endpoints, navigate to *Permissions* under **Settings &gt; Endpoints**. You can create and define role and assign permissions under *Roles* and create and organize devices into groups under *Device groups*.

Alternately, you can navigate to *Endpoints roles & groups* in the **System &gt; Permissions** page.

#### APIs and MSSPs

The Microsoft Defender XDR alerts API is the official API that enables customers to work with alerts across all Defender products using a single integration. For more information, see [Migrate from the MDE SIEM API to the Microsoft Defender XDR alerts API](/en-us/defender-endpoint/configure-siem).

To authorize a managed security service provider (MSSP) to access receive alerts, you need to provide the application and tenant IDs of the MSSP. For more information, see [MSSP integration](/en-us/defender-endpoint/configure-mssp-support#mssp-integration).

#### Rules

You can create rules and policies to manage indicators, filter web content, manage automation uploads and automation folder exclusions, and more. To create these rules, navigate to *Rules* under **Settings &gt; Endpoints**. More information on managing these rules can be found in the following links:

- [Manage indicators](/en-us/defender-endpoint/indicator-manage)
- [Manage automation uploads](/en-us/defender-endpoint/manage-automation-file-uploads)
- [Manage automation folder exclusions](/en-us/defender-endpoint/automation-folder-exclusions-configure)
- [Filter web content](/en-us/defender-endpoint/web-content-filtering)

#### Security setting management

In **Settings &gt; Endpoints &gt; Configuration management &gt; Enforcement scope**, you can allow Microsoft Intune security settings to be enforced by Microsoft Defender for Endpoint. For more information, see [Use Microsoft Intune to configure and manage Microsoft Defender Antivirus](/en-us/defender-endpoint/use-intune-config-manager-microsoft-defender-antivirus).

#### Device management

You can onboard or offboard devices and run a device detection test in the **Settings &gt; Endpoints &gt; Device management** page. See [Onboard to Microsoft Defender for Endpoint](/en-us/defender-endpoint/onboarding) to know the steps to onboard devices. To offboard devices, see [Offboard devices](/en-us/defender-endpoint/offboard-machines).

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).