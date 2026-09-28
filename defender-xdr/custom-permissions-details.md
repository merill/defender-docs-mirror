---
layout: Conceptual
title: Permissions in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/custom-permissions-details
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the custom permissions available in Microsoft Defender Security role-based access control (RBAC)
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom: 
ms.topic: concept-article
ms.date: 2026-05-25T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: 
locale: en-us
document_id: e48f7595-2127-b0ca-fd24-d9fcaac9f91b
document_version_independent_id: e48f7595-2127-b0ca-fd24-d9fcaac9f91b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/custom-permissions-details.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: custom-permissions-details
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/custom-permissions-details.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 6ff0415e-f9d4-591f-4ed6-880ed939b8d6
---

# Permissions in Microsoft Defender unified role-based access control (RBAC) - Microsoft Defender XDR | Microsoft Learn

Use Microsoft Defender unified role-based access control (RBAC) to manage permissions for users and groups in your organization. Unified RBAC supports selecting permissions from each permission group to customize a role.

This article provides details about the permissions available to configure for your users, based on the tasks they need to do.

Unless otherwise stated, all permissions are applicable to all supported workloads and will be applied to the data scope selected during the data source and assignment stage.

## Security operations – Security data

Permissions for managing day-to-day operations and responding to incidents and advisories.

| Permission name | Level | Description |
| --- | --- | --- |
| Security data basics | Read | View info about incidents, alerts, investigations, advanced hunting, devices, submissions, evaluation lab, and reports. View data lake data and experiences (Preview). |
| Alerts | Manage | Manage alerts, start automated investigations, run scans, collect investigation packages, and manage device tags. |
| Response | Manage | Take response actions, approve or dismiss pending remediation actions, and manage blocked and allowed lists for automation. |
| Basic live response | Manage | Initiate a live response session, download files, and perform read-only actions on devices remotely. |
| Advanced live response | Manage | Create live response sessions and perform advanced actions, including uploading files and running scripts on devices remotely. |
| File collection | Manage | Collect or download relevant files for analysis, including executable files. |
| Email & collaboration quarantine | Manage | View and release email from quarantine. |
| Email & collaboration advanced actions | Manage | Move or Delete email to the junk email folder, deleted items or inbox, including soft and hard delete of email. |

## Security operations – Raw data (Email & collaboration)

| Permission name | Level | Description |
| --- | --- | --- |
| Email & collaboration metadata | Read | View email and collaboration data in hunting scenarios, including advanced hunting, threat explorer, campaigns, and email entity. |
| Email & collaboration content | Read | View and download email content and attachments. |
| Email & collaboration content: Emails associated with alerts | Read | View and download email content associated with security alerts **Email reported by user as malware or phish** and **Email reported by user as junk**. |
| Email & collaboration content: Quarantine Emails | Read | View and download quarantined messages for all users. |

## Security posture – Posture management

Permissions for managing the organization's security posture and performing vulnerability management.

| Permission name | Level | Description |
| --- | --- | --- |
| Vulnerability management | Read | View Defender Vulnerability Management data for the following: software and software inventory, weaknesses, missing KBs, advanced hunting, security baselines assessment, and devices. |
| Exception handling | Manage | Create security recommendation exceptions and manage active exceptions in Defender Vulnerability Management. |
| Remediation handling | Manage | Create remediation tickets, submit new requests, and manage remediation activities in Defender Vulnerability Management. |
| Application handling | Manage | Manage vulnerable applications and software, including blocking and unblocking them in Defender Vulnerability Management. |
| Security baseline assessment | Manage | Create and manage profiles so you can assess if your devices comply with security industry baselines. |
| Exposure Management | Read / Manage | View or manage Exposure Management insights, including Microsoft Secure Score recommendations from all products that are covered by Secure Score. |

## Security posture – AI code scan

Permissions for running AI code scans and managing scan results.

| Permission name | Level | Description |
| --- | --- | --- |
| Run scan | Manage | Allows users to run AI code scans. |
| Upload results | Manage | Allows users to upload AI code scan results to Defender. |
| Scan results | Read | View AI code scan results. |
| Scan results | Manage | Manage AI code scan results. |

## Authorization and settings

Permissions to manage the security and system settings and to create and assign roles.

| Permission name | Level | Description |
| --- | --- | --- |
| Authorization | Read / Manage | View or manage device groups, and custom and built-in roles. |
| Core security settings | Read / Manage | View or manage core security settings for the Microsoft Defender portal. |
| Detection tuning | Manage | Manage tasks related to detections in the Microsoft Defender portal including Custom detections, Alerts Tuning and Threat Indicators of compromise. |
| System settings | Read / Manage | View or manage general systems settings for the Microsoft Defender portal. |

## Data operations (Preview)

Permissions for managing the organization's security data and controlling advanced analytics permissions, supported for Microsoft Sentinel workspaces [onboarded to the Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard) and the [Microsoft Sentinel data lake](https://aka.ms/data-lake-overview).

The following permissions can be assigned for both Microsoft Sentinel SIEM and data lake capabilities, which includes data lake data stored in the default data lake workspace.

| Permission name | Level | Description |
| --- | --- | --- |
| Data | Manage | Manage data retention, move data between tiers, create data lake tables, and manage connectors for the Microsoft Sentinel data lake. |
| Analytics Jobs Schedule | Read / Manage | Schedule and manage analytics jobs within the Microsoft Sentinel data lake using Lake Exploration, Azure Data Explorer, or Notebooks. |