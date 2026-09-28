---
layout: Conceptual
title: Monitored activities - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/monitored-activities
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
description: Describes each activity type monitored by Microsoft Defender for Identity
ms.date: 2024-02-12T00:00:00.0000000Z
ms.topic: article
ms.reviewer: rlitinsky
locale: en-us
document_id: 888882ce-80ac-7945-57e3-9c03eedc0929
document_version_independent_id: 888882ce-80ac-7945-57e3-9c03eedc0929
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/monitored-activities.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitored-activities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/monitored-activities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 2d32fc6f-63bb-8f7a-a6d7-e857b5f8d1ca
---

# Monitored activities - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity monitors information generated from your organization's Active Directory, network activities and event activities to detect suspicious activity. The monitored activity information enables Defender for Identity to help you determine the validity of each potential threat and correctly triage and respond.

In the case of a valid threat, or **true positive**, Defender for Identity enables you to discover the scope of the breach for each incident, investigate which entities are involved, and determine how to remediate them.

The information monitored by Defender for Identity is presented in the form of activities. Defender for Identity currently supports monitoring of the following activity types:

Note

- This article is relevant for all Defender for Identity sensor types.
- Defender for Identity monitored activities appear on both the user and machine profile page.
- Defender for Identity monitored activities are also available in [Microsoft Defender's Advanced Hunting](/en-us/defender-xdr/advanced-hunting-overview) page.

Tip

For detailed information on all supported event types (`ActionType` values) in Advanced Hunting Identity-related tables, use the built-in schema reference available in Microsoft Defender XDR.

## Monitored user activities: User account AD attribute changes

| Monitored activity | Description |
| --- | --- |
| Account Constrained Delegation State Changed | The account state is now enabled or disabled for delegation. |
| Account Constrained Delegation SPNs Changed | Constrained delegation restricts the services to which the specified server can act on behalf of the user. |
| Account Delegation Changed | Changes to the account delegation settings. |
| Account Disabled Changed | Indicates whether an account is disabled or enabled. |
| Account Expired | Date when the account expires. |
| Account Expiry Time Changed | Change to the date when the account expires. |
| Account Locked Changed | Changes to the account lock settings. |
| Account Password Changed | User changed their password. |
| Account Password Expired | User's password expired. |
| Account Password Never Expires Changed | User's password changed to never expire. |
| Account Password Not Required Changed | User account was changed to allow logging in with a blank password. |
| Account Smartcard Required Changed | Account changes to require users to log on to a device using a smart card. |
| Account Supported Encryption Types Changed | Kerberos supported encryption types were changed (types: Des, AES 129, AES 256). |
| Account Unlock changed | Changes to the account unlock settings. |
| Account UPN Name Changed | User's principal name was changed. |
| Group Membership Changed | User was added/removed, to/from a group, by another user or by themselves. |
| User Mail Changed | Users email attribute was changed. |
| User Manager Changed | User's manager attribute was changed. |
| User Phone Number Changed | User's phone number attribute was changed. |
| User Title Changed | User's title attribute was changed. |

## Monitored user activities: AD security principal operations

| Monitored activity | Description |
| --- | --- |
| User Account Created | User account was created. |
| Computer Account Created | Computer account was created. |
| Security Principal Deleted Changed | Account was deleted/restored (both user and computer). |
| Security Principal Display Name Changed | Account display name was changed from X to Y. |
| Security Principal Name Changed | Account name attribute was changed. |
| Security Principal Path Changed | Account Distinguished name was changed from X to Y. |
| Security Principal Sam Name Changed | SAM name changed (SAM is the logon name used to support clients and servers running earlier versions of the operating system). |

## Monitored user activities: Domain controller based user operations

| Monitored activity | Description |
| --- | --- |
| Directory Service Replication | User tried to replicate the directory service. |
| DNS Query | Type of query user performed against the domain controller (**AXFR**,**TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**). |
| gMSA Password retrieval | gMSA account password was retrieved by a user.  To monitor this activity, event 4662 must be collected. For more information, see [Configure Windows Event collection](configure-windows-event-collection). |
| LDAP Query | User performed an LDAP query. |
| Potential lateral movement | A lateral movement was identified. |
| PowerShell execution | User attempted to remotely execute a PowerShell method. |
| Private Data Retrieval | User attempted/succeeded to query private data using LSARPC protocol. |
| Service Creation | User attempted to remotely create a specific service to a remote machine. |
| SMB Session Enumeration | User attempted to enumerate all users with open SMB sessions on the domain controllers. |
| SMB file copy | User copied files using SMB. |
| SAMR Query | User performed a SAMR query. |
| Task Scheduling | User tried to remotely schedule X task to a remote machine. |
| Wmi Execution | User attempted to remotely execute a WMI method. |

## Monitored user activities: Login operations

For more information, see [Supported logon types](/en-us/microsoft-365/security/defender/advanced-hunting-identitylogonevents-table#supported-logon-types) for the `IdentityLogonEvents` table.

## Monitored machine activities: Machine account

| Monitored activity | Description |
| --- | --- |
| Computer Operating System Changed | Change to the computer OS. |
| SID-History changed | Changes to the computer SID history. |