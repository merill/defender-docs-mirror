---
layout: Conceptual
title: Hunt for threats across devices, emails, apps, and identities with advanced hunting - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-emails-devices
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Study common hunting scenarios and sample queries that cover devices, emails, apps, and identities.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b3574dd1-607d-f4ea-0cb8-590732944718
document_version_independent_id: b3574dd1-607d-f4ea-0cb8-590732944718
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-emails-devices.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-emails-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-emails-devices.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9953d284-79fb-554d-ac33-bb83dcb07010
---

# Hunt for threats across devices, emails, apps, and identities with advanced hunting - Microsoft Defender XDR | Microsoft Learn

[Advanced hunting](advanced-hunting-overview) in Microsoft Defender allows you to proactively hunt for threats in:

- Devices managed by Microsoft Defender for Endpoint
- Emails processed by Microsoft 365
- Cloud app activities, authentication events, and domain controller activities tracked by Microsoft Defender for Cloud Apps and Microsoft Defender for Identity

With visibility across devices, email, cloud apps, authentication events, and domain controller activities, you can quickly hunt for threats that traverse sections of your network, including sophisticated intrusions that arrive on email or the web, elevate local privileges, acquire privileged domain credentials, and move laterally across your devices.

Here are general techniques and sample queries based on various hunting scenarios that can help you explore how you might construct queries when hunting for such sophisticated threats.

## Get entity information

Use these queries to learn how you can quickly get information about user accounts, devices, and files.

### Obtain user accounts from email addresses

When constructing queries across [tables that cover devices and emails](advanced-hunting-schema-tables), you will likely need to obtain user account names from sender or recipient email addresses. You can generally do this for either recipient or sender address using the *local-host* from the email address.

In the snippet below, we use the [tostring()](/en-us/azure/data-explorer/kusto/query/tostringfunction) Kusto function to extract the local-host right before the `@` from recipient email addresses in the column `RecipientEmailAddress`. This snippet extracts the account name from `RecipientEmailAddress` so you can reuse it in joins with identity or device data:

```kusto
//Query snippet showing how to extract the account name from an email address
AccountName = tostring(split(RecipientEmailAddress, "@")[0])
```

The following example query uses this account-name extraction snippet in an `EmailEvents` query:

```kusto
EmailEvents
| where Timestamp > ago(7d)
| project RecipientEmailAddress, AccountName = tostring(split(RecipientEmailAddress, "@")[0]);
```

### Merge the IdentityInfo table

You can get account names and other account information by merging or joining the [IdentityInfo table](advanced-hunting-identityinfo-table). The query below obtains the list of phishing and malware detections from the [EmailEvents table](advanced-hunting-emailevents-table) and then joins that information with the `IdentityInfo` table to get detailed information about each recipient.

```kusto
EmailEvents
| where Timestamp > ago(7d)
//Get email processing events where the messages were identified as either phishing or malware
| where ThreatTypes has "Malware" or ThreatTypes has "Phish"
//Merge email events with identity info to get recipient details
| join (IdentityInfo | distinct AccountUpn, AccountDisplayName, JobTitle,
Department, City, Country) on $left.RecipientEmailAddress == $right.AccountUpn
//Show important message and recipient details
| project Timestamp, NetworkMessageId, Subject, ThreatTypes,
SenderFromAddress, RecipientEmailAddress, AccountDisplayName, JobTitle,
Department, City, Country
```

Watch this [video on joining tables with Kusto Query Language](https://www.youtube.com/watch?v=8qZx7Pp5XgM) to learn more.

### Get device information

The [advanced hunting schema](advanced-hunting-schema-tables) provides extensive device information in various tables. For example, the [DeviceInfo table](advanced-hunting-deviceinfo-table) provides comprehensive device information based on event data aggregated regularly. This query uses the `DeviceInfo` table to check if a potentially compromised user (`<account-name>`) has logged on to any devices and then lists the alerts that have been triggered on the devices that the user has logged on to.

Tip

This query uses `kind=inner` to specify an [inner-join](/en-us/azure/data-explorer/kusto/query/joinoperator?pivots=azuredataexplorer#inner-join-flavor), which prevents deduplication of left side values for `DeviceId`.

```kusto
DeviceInfo
//Query for devices that the potentially compromised account has logged onto
| where LoggedOnUsers contains '<account-name>'
| distinct DeviceId
//Crosscheck devices against alert records in AlertEvidence and AlertInfo tables
| join kind=inner AlertEvidence on DeviceId
| project AlertId
//List all alerts on devices that user has logged on to
| join AlertInfo on AlertId
| project AlertId, Timestamp, Title, Severity, Category
```

### Get file event information

Use the following query to get information on file related events.

```kusto
DeviceInfo
| where Timestamp > ago(1d)
| where ClientVersion startswith "20.1"
| summarize by DeviceId
| join kind=inner (
    DeviceFileEvents
    | where Timestamp > ago(1d)
) on DeviceId
| take 10
```

### Get network event information

Use the following query to get information on network related events.

```kusto
DeviceInfo
| where Timestamp > ago(1d)
| where ClientVersion startswith "20.1"
| summarize by DeviceId
| join kind=inner (
    DeviceNetworkEvents
    | where Timestamp > ago(1d)
) on DeviceId
| take 10
```

### Get device agent version information

Use the following query to get the version of the agent running on a device.

```kusto
DeviceInfo
| where Timestamp > ago(1d)
| where ClientVersion startswith "20.1"
| summarize by DeviceId
| join kind=inner (
    DeviceNetworkEvents
    | where Timestamp > ago(1d)
) on DeviceId
| take 10
```

### Example query for macOS devices

Use the following example query to see all devices running macOS with a version older than Catalina.

```kusto
DeviceInfo
| where Timestamp > ago(1d)
| where OSPlatform == "macOS" and  OSVersion !contains "10.15" and OSVersion !contains "11."
| summarize by DeviceId
| join kind=inner (
    DeviceInfo
    | where Timestamp > ago(1d)
) on DeviceId
| take 10
```

### Get device status info

Use the following query to check whether a device is onboarded by querying the `DeviceInfo` table and filtering on `OnboardingStatus`.

```kusto
DeviceInfo
| where Timestamp > ago(1d)
| where OnboardingStatus != "Onboarded"
| summarize by DeviceId
| join kind=inner (
    DeviceInfo
    | where Timestamp > ago(1d)
) on DeviceId
| take 10
```

## Hunting scenarios

The following example queries address common threat-hunting investigations that span email, identity, and device data.

### List logon activities of users that received emails that were not zapped successfully

[Zero-hour auto purge (ZAP)](/en-us/defender-office-365/zero-hour-auto-purge) addresses malicious emails after they have been received. If ZAP fails, malicious code might eventually run on a recipient's device and leave accounts compromised. This query checks for logon activity made by the recipients of emails that were not successfully addressed by ZAP.

```kusto
EmailPostDeliveryEvents
| where Timestamp > ago(7d)
//List malicious emails that were not zapped successfully
| where ActionType has "ZAP" and ActionResult == "Error"
| project ZapTime = Timestamp, ActionType, NetworkMessageId , RecipientEmailAddress
//Get logon activity of recipients using RecipientEmailAddress and AccountUpn
| join kind=inner IdentityLogonEvents on $left.RecipientEmailAddress == $right.AccountUpn
| where Timestamp between ((ZapTime-24h) .. (ZapTime+24h))
//Show only pertinent info, such as account name, the app or service, protocol, the target device, and type of logon
| project ZapTime, ActionType, NetworkMessageId , RecipientEmailAddress, AccountUpn,
LogonTime = Timestamp, AccountDisplayName, Application, Protocol, DeviceName, LogonType
```

### Get logon attempts by domain accounts targeted by credential theft

This query first identifies all credential access alerts in the `AlertInfo` table. It then merges or joins the `AlertEvidence` table, which it parses for the names of the targeted accounts and filters for domain-joined accounts only. Finally, it checks the `IdentityLogonEvents` table to get all logon activities by the domain-joined targeted accounts.

```kusto
AlertInfo
| where Timestamp > ago(30d)
//Get all credential access alerts
| where Category == "CredentialAccess"
//Get more info from AlertEvidence table to get the SID of the target accounts
| join AlertEvidence on AlertId
| extend IsJoined=(parse_json(AdditionalFields).Account.IsDomainJoined)
| extend TargetAccountSid=tostring(parse_json(AdditionalFields).Account.Sid)
//Filter for domain-joined accounts only
| where IsJoined has "true"
//Merge with IdentityLogonEvents to get all logon attempts by the potentially compromised target accounts
| join kind=inner IdentityLogonEvents on $left.TargetAccountSid == $right.AccountSid
//Show only pertinent info, such as account name, the app or service, protocol, the accessed device, and type of logon
| project AccountDisplayName, TargetAccountSid, Application, Protocol, DeviceName, LogonType
```

### Check if files from a known malicious sender are on your devices

Assuming you know of an email address sending malicious files (`MaliciousSender@example.com`), you can run this query to determine if files from this sender exist on your devices. You can use this query, for example, to identify devices affected by a malware distribution campaign.

```kusto
EmailAttachmentInfo
| where SenderFromAddress =~ "MaliciousSender@example.com"
//Get emails with attachments identified by a SHA-256
| where isnotempty(SHA256)
| join (
//Check devices for any activity involving the attachments
DeviceFileEvents
| project FileName, SHA256, DeviceName, DeviceId
) on SHA256
| project Timestamp, FileName , SHA256, DeviceName, DeviceId,  NetworkMessageId, SenderFromAddress, RecipientEmailAddress
```

### Review logon attempts after receipt of malicious emails

This query finds the 10 latest logons performed by email recipients within 30 minutes after they received known malicious emails. You can use this query to check whether the accounts of the email recipients have been compromised.

```kusto
//Define new table for malicious emails
let MaliciousEmails=EmailEvents
//List emails detected as malware, getting only pertinent columns
| where ThreatTypes has "Malware"
| project TimeEmail = Timestamp, Subject, SenderFromAddress, AccountName = tostring(split(RecipientEmailAddress, "@")[0]);
MaliciousEmails
| join (
//Merge malicious emails with logon events to find logons by recipients
IdentityLogonEvents
| project LogonTime = Timestamp, AccountName, DeviceName
) on AccountName
//Check only logons within 30 minutes of receipt of an email
| where (LogonTime - TimeEmail) between (0min.. 30min)
| take 10
```

### Review PowerShell activities after receipt of emails from known malicious sender

Malicious emails often contain documents and other specially crafted attachments that run PowerShell commands to deliver additional payloads. If you are aware of emails coming from a known malicious sender (`MaliciousSender@example.com`), you can use this query to list and review PowerShell activities that occurred within 30 minutes after an email was received from the sender.

```kusto
//Define new table for emails from specific sender
let EmailsFromBadSender=EmailEvents
| where SenderFromAddress =~ "MaliciousSender@example.com"
| project TimeEmail = Timestamp, Subject, SenderFromAddress, AccountName = tostring(split(RecipientEmailAddress, "@")[0]);
//Merge emails from sender with process-related events on devices
EmailsFromBadSender
| join (
DeviceProcessEvents
//Look for PowerShell activity
| where FileName =~ "powershell.exe"
//Add line below to check only events initiated by Outlook
//| where InitiatingProcessParentFileName =~ "outlook.exe"
| project TimeProc = Timestamp, AccountName, DeviceName, InitiatingProcessParentFileName, InitiatingProcessFileName, FileName, ProcessCommandLine
) on AccountName
//Check only PowerShell activities within 30 minutes of receipt of an email
| where (TimeProc - TimeEmail) between (0min.. 30min)
```