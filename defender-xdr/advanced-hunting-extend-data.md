---
layout: Conceptual
title: Extend advanced hunting coverage with the right settings - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-extend-data
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Check auditing settings on Windows devices and other settings to help ensure that you get the most comprehensive data in advanced hunting
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b2a303ff-d185-247f-3fe0-2fc9c85412f5
document_version_independent_id: b2a303ff-d185-247f-3fe0-2fc9c85412f5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-extend-data.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-extend-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-extend-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: b36f2339-89d7-472f-5e6d-fb73748edd7a
---

# Extend advanced hunting coverage with the right settings - Microsoft Defender XDR | Microsoft Learn

## Configure data sources for advanced hunting

[Advanced hunting](advanced-hunting-overview) relies on data from various sources. These sources include your devices, your Office 365 workspaces, Microsoft Entra ID, and Microsoft Defender for Identity. To get the most complete data, make sure you have the correct settings in each data source.

## Enable advanced security auditing on Windows devices

Turn on these advanced auditing settings to ensure you get data about activities on your devices, including local account management, local security group management, and service creation.

| Data | Description | Schema table | How to configure |
| --- | --- | --- | --- |
| Account management | Events captured as various `ActionType` values indicating local account creation, deletion, and other account-related activities | [DeviceEvents](advanced-hunting-deviceevents-table) | - Deploy an advanced security audit policy: [Audit User Account Management](/en-us/windows/security/threat-protection/auditing/audit-user-account-management) - [Learn about advanced security audit policies](/en-us/windows/security/threat-protection/auditing/advanced-security-auditing) |
| Security group management | Events captured as various `ActionType` values indicating local security group creation and other local group management activities | [DeviceEvents](advanced-hunting-deviceevents-table) | - Deploy an advanced security audit policy: [Audit Security Group Management](/en-us/windows/security/threat-protection/auditing/audit-security-group-management) - [Learn about advanced security audit policies](/en-us/windows/security/threat-protection/auditing/advanced-security-auditing) |
| Service installation | Events captured with the `ActionType` value `ServiceInstalled`, indicating that a service has been created | [DeviceEvents](advanced-hunting-deviceevents-table) | - Deploy an advanced security audit policy: [Audit Security System Extension](/en-us/windows/security/threat-protection/auditing/audit-security-system-extension) - [Learn about advanced security audit policies](/en-us/windows/security/threat-protection/auditing/advanced-security-auditing) |

## Install the Microsoft Defender for Identity sensor on the domain controller

If you're running Active Directory on premises, you need to install the Microsoft Defender for Identity sensor on the domain controller to get data for Microsoft Defender for Identity. When installed and properly configured, data from on-premises Active Directory also feeds into advanced hunting through Microsoft Defender for Identity and provides a more holistic picture of identity information and events in your network. Data collected by the Defender for Identity sensor also enhances the ability of Microsoft Defender for Identity to generate relevant alerts that are also covered by advanced hunting.

| Data | Description | Schema table | How to configure |
| --- | --- | --- | --- |
| Domain controller | Data from on-premises Active Directory sent to Microsoft Defender for Identity, enriching identity-related information, such as account details, logon activity, and Active Directory queries | Multiple tables, including [IdentityInfo](advanced-hunting-identityinfo-table), [IdentityLogonEvents](advanced-hunting-identitylogonevents-table), and [IdentityQueryEvents](advanced-hunting-identityqueryevents-table) | - [Install the Microsoft Defender for Identity sensor](/en-us/azure-advanced-threat-protection/install-atp-step4)- [Turn on relevant Windows Events](/en-us/azure-advanced-threat-protection/configure-event-collection) |

Note

Some tables in this article might not be available in Microsoft Defender for Endpoint. [Turn on Microsoft Defender XDR](m365d-enable) to hunt for threats using more data sources. You can move your advanced hunting workflows from Microsoft Defender for Endpoint to Microsoft Defender XDR by following the steps in [Migrate advanced hunting queries from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde).