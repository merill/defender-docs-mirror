---
layout: Conceptual
title: Alert classification for suspicious inbox manipulation rules - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/alert-grading-playbook-inbox-manipulation-rules
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate alerts for suspicious inbox manipulation rules, determine whether they are true or false positives, and follow recommended remediation steps for compromised accounts.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c9a2989e-bfe7-34f4-5126-519afa839699
document_version_independent_id: c9a2989e-bfe7-34f4-5126-519afa839699
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/alert-grading-playbook-inbox-manipulation-rules.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: alert-grading-playbook-inbox-manipulation-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/alert-grading-playbook-inbox-manipulation-rules.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: eaf96056-0517-fb5b-05ab-56b479688669
---

# Alert classification for suspicious inbox manipulation rules - Microsoft Defender XDR | Microsoft Learn

Threat actors can use compromised user accounts for many malicious purposes including reading emails in a user's inbox, creating inbox rules to forward emails to external accounts, deleting traces, and sending phishing mails. Malicious inbox rules are common during business email compromise (BEC) and phishing campaigns and it's important to monitor for them consistently.

This playbook helps you investigate any incident related to suspicious inbox manipulation rules configured by attackers and take recommended actions to remediate the attack and protect your network. This playbook is for security teams, including security operations center (SOC) analysts and IT administrators who review, investigate, and grade the alerts. You can quickly grade alerts as either a true positive (TP) or a false positive (FP) and take recommended actions for the TP alerts to remediate the attack.

The results of using this playbook are:

- You identify the alerts associated with inbox manipulation rules as malicious (TP) or benign (FP) activities.

    If malicious, you remove malicious inbox manipulation rules.
- You take the necessary action if emails were forwarded to a malicious email address.

## Overview of inbox manipulation rules

Inbox rules are set to automatically manage email messages based on predefined criteria. For example, you can create an inbox rule to move all messages from your manager into another folder, or forward messages you receive to another email address.

### How attackers use malicious inbox manipulation rules

Attackers might set up email rules to hide incoming emails in the compromised user mailbox to obscure their malicious activities from the user. They might also set rules in the compromised user mailbox to delete emails, move the emails into another less noticeable folder (like RSS), or forward mails to an external account. Some rules might move all the emails to another folder and mark them as "read", while some rules might move only mails that contain specific keywords in the email message or subject.

For example, the inbox rule might be set to look for keywords like "invoice," "phish," "do not reply," "suspicious email," or "spam," among others, and move them to an external email account. Attackers might also use the compromised user mailbox to distribute spam, phishing emails, or malware.

## Investigation workflow for suspicious inbox manipulation rules

Here's the workflow to identify suspicious inbox manipulation rule activities.

[![Alert investigation workflow for inbox manipulation rules](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-workflow.png)](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-workflow.png#lightbox)

## Investigation steps

The following investigation steps provide detailed step-by-step guidance to respond to the incident and take the recommended steps to protect your organization from further attacks.

### 1. Review the alerts

Here's an example of an inbox manipulation rule alert in the alert queue.

[![Example of an inbox manipulation rule](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-alert-queue.png)](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-alert-queue.png#lightbox)

Here's an example of the details of an alert that was triggered by a malicious inbox manipulation rule.

[![Details of alert that was triggered by a malicious inbox manipulation rule](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-alert-description.png)](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-alert-description.png#lightbox)

### 2. Investigate inbox manipulation rule parameters

Determine if the rules look suspicious according to the following rule parameters or criteria:

- Keywords

    The attacker might apply the manipulation rule only to emails that contains certain words. You can find these keywords under certain attributes such as: "BodyContainsWords," "SubjectContainsWords," or "SubjectOrBodyContainsWords."

    If there are filtering by keywords, then check whether the keywords seem suspicious to you (common scenarios are to filter emails related to the attacker activities, such as "phish," "spam," and "do not reply," among others).

    If there is no filter at all, a rule with no filter might be suspicious as well.
- Destination folder

    To evade security detection, the attacker might move the emails to a less noticeable folder and mark the emails as read (for example, "RSS" folder). If the attacker applies "MoveToFolder" and "MarkAsRead" action, check whether the destination folder is somehow related to the keywords in the rule to decide if it seems suspicious or not.
- Delete all

    Some attackers will just delete all the incoming emails to hide their activity. Mostly, a rule of "delete all incoming emails" without filtering them with keywords is an indicator of malicious activity.

Here's an example of a "delete all incoming emails" rule configuration (as seen on RawEventData.Parameters) of the relevant event log.

[![Example of a delete all incoming emails rule configuration](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-delete-log.png)](media/alert-grading-playbook-inbox-manipulation-rules/alert-grading-playbook-inbox-manipulation-rules-delete-log.png#lightbox)

### 3. Investigate the IP address

Review the attributes of the IP address that performed the relevant event of rule creation:

- Search for other suspicious cloud activities that originated from the same IP in the tenant. For instance, suspicious activity might be multiple failed login attempts.
- Is the internet service provider (ISP) common and reasonable for this user?
- Is the location common and reasonable for this user?

### 4. Investigate suspicious activity by the user prior to creating the rules

You can review all user activities before the suspicious inbox rules were created, check for indicators of compromise, and investigate user actions that seem suspicious.

For instance, for multiple failed logins, examine:

- Login activity

    Validate that the login activity prior to the rule creation is not suspicious. (common location / ISP / user-agent).
- Alerts

    Check whether the user received alerts prior to creating the rules. This could indicate that the user account might be compromised. For example, impossible travel alert, infrequent country/region, multiple failed logins, among others.)
- Incident

    Check whether the investigated alert is associated with other alerts that indicate an incident. If so, then check whether the incident contains other true positive alerts.

## Advanced hunting queries

[Advanced Hunting](advanced-hunting-overview) is a query-based threat hunting tool that lets you inspect events in your network to locate threat indicators.

Use the following query to find all new inbox rule events for a specific user during a given time window. Replace the `user_id` variable with the affected user's account ID before running the query.

```kusto
let start_date = now(-10h);
let end_date = now();
let user_id = ""; // enter here the user id
CloudAppEvents
| where Timestamp between (start_date .. end_date)
| where AccountObjectId == user_id
| where Application == @"Microsoft Exchange Online"
| where ActionType in ("Set-Mailbox", "New-InboxRule", "Set-InboxRule", "UpdateInboxRules") //set new inbox rule related operations
| project Timestamp, ActionType, CountryCode, City, ISP, IPAddress, RuleConfig = RawEventData.Parameters, RawEventData
```

The *RuleConfig* column will provide the new inbox rule configuration.

Use the following query to determine whether the ISP associated with the alert is common for the user. The query examines the user's activity over the previous 60 days leading up to the alert to establish a baseline of typical ISP usage. An unfamiliar ISP might indicate unauthorized access.

```kusto
let alert_date = now(); //enter alert date
let timeback = 60d;
let userid = ""; //enter here user id
CloudAppEvents
| where Timestamp between ((alert_date-timeback)..(alert_date-1h))
| where AccountObjectId == userid
| make-series ActivityCount = count() default = 0 on Timestamp  from (alert_date-timeback) to (alert_date-1h) step 12h by ISP
```

Use the following query to check whether the country/region associated with the alert activity is common for the user. The query reviews the user's sign-in history over the previous 60 days to establish a baseline. Activity from an unfamiliar country/region can indicate that the account was accessed by an unauthorized party.

```kusto
let alert_date = now(); //enter alert date
let timeback = 60d;
let userid = ""; //enter here user id
CloudAppEvents
| where Timestamp between ((alert_date-timeback)..(alert_date-1h))
| where AccountObjectId == userid
| make-series ActivityCount = count() default = 0 on Timestamp  from (alert_date-timeback) to (alert_date-1h) step 12h by CountryCode
```

Use the following query to check whether the user agent string associated with the alert activity is common for the user. The query reviews the user's activity over the previous 60 days to establish a baseline. An unusual or unexpected user agent can indicate that the account was accessed by an attacker using a different browser or automation tool.

```kusto
let alert_date = now(); //enter alert date
let timeback = 60d;
let userid = ""; //enter here user id
CloudAppEvents
| where Timestamp between ((alert_date-timeback)..(alert_date-1h))
| where AccountObjectId == userid
| make-series ActivityCount = count() default = 0 on Timestamp  from (alert_date-timeback) to (alert_date-1h) step 12h by UserAgent
```

## Recommended actions

After confirming a true positive alert, take the following actions to remediate the attack:

1. Disable the malicious inbox rule.
2. Reset the user account's credentials. You can also verify if the user account has been compromised with Microsoft Defender for Cloud Apps, which gets security signals from Microsoft Entra ID Protection.
3. Search for other malicious activities performed by the impacted user account.
4. Check for other suspicious activity in the tenant that originated from the same IP or from the same ISP (if the ISP is uncommon) to find other compromised user accounts.