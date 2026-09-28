---
layout: Conceptual
title: Alert classification for suspicious IP address related to password spraying activity - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/alert-classification-suspicious-ip-password-spray
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate and review alerts related to suspicious IP address related to password spraying activity and take recommended actions to protect your network.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1014
- admindeeplinkDEFENDER
- sfi-ropc-nochange
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 42ff1a75-f7e1-2abb-aae2-3585c0111b38
document_version_independent_id: 42ff1a75-f7e1-2abb-aae2-3585c0111b38
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/alert-classification-suspicious-ip-password-spray.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: alert-classification-suspicious-ip-password-spray
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/alert-classification-suspicious-ip-password-spray.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: f123aed4-3e83-5685-0c83-e09701e1acdb
---

# Alert classification for suspicious IP address related to password spraying activity - Microsoft Defender XDR | Microsoft Learn

Threat actors use password guessing techniques to gain access to user accounts. In a password spray attack, the threat actor might resort to a few of the most used passwords against many different accounts. Attackers successfully compromise accounts using password spraying since many users still utilize default and weak passwords.

This playbook helps you investigate instances where IP addresses have been labeled risky or associated with a password spray attack, or suspicious unexplained activities were detected, such as a user signing in from an unfamiliar location or a user getting unexpected multi-factor authentication (MFA) prompts. This guide is for security teams like the security operations center (SOC) and IT administrators who review, handle/manage, and classify the alerts. This guide helps in quickly classifying the alerts as either [true positive (TP) or false positive (FP)](investigate-alerts) and, in the case of TP, take recommended actions to remediate the attack and mitigate the security risks.

The intended results of using this guide are:

- You've identified the alerts associated with password-spray IP addresses as malicious (TP) or false positive (FP) activities.
- You've taken the necessary action if IP addresses have been performing password spray attacks.

## Investigate the alert

This playbook provides step-by-step guidance to investigate password spray IP alerts and take recommended actions to protect your organization from further attacks.

### 1. Review the alert

Here's an example of a password spray alert in the alert queue:

[![Screenshot of Microsoft Defender 365 alert.](media/alert-grading-playbook-password-spray/fig1-password-spray-alert.png)](media/alert-grading-playbook-password-spray/fig1-password-spray-alert.png#lightbox)

The password spray alert means there's suspicious user activity originating from an IP address that might be associated with a brute-force or password spray attempt according to threat intelligence sources.

### 2. Investigate the IP address

Review activity from the suspicious IP address to determine whether the pattern matches password spray behavior.

- Look at the [activity filters in Defender for Cloud Apps](/en-us/defender-cloud-apps/activity-filters) that originated from the IP:

    - **Is it mostly failed attempts to sign in?**
    - **Does the interval between attempts to sign in look suspicious?** Automated password spray attacks tend to have a regular time interval between attempts.
    - **Are there successful attempts of a user/several users signing in with [multi-factor authentication (MFA)](/en-us/microsoft-365/admin/security-and-compliance/multi-factor-authentication-microsoft-365) prompts?** The existence of these attempts might indicate that the IP isn't malicious.
    - **Are legacy protocols used?** Using protocols like POP3, IMAP, and SMTP might indicate an attempt to perform a password spray attack. Finding `Unknown(BAV2ROPC)` in the user agent (Device type) in the [Activity log](/en-us/defender-cloud-apps/activity-filters#ip-address-insights) indicates use of legacy protocols. When looking at the Activity log, look for `Unknown(BAV2ROPC)` in the **Device type** field, as shown in the following screenshot. Legacy-protocol sign-in activity must be further correlated with other suspicious activities.

        [![Screenshot of Microsoft Defender 365 interface showing the Device type.](media/alert-grading-playbook-password-spray/fig2-password-spray-alert.png)](media/alert-grading-playbook-password-spray/fig2-password-spray-alert.png#lightbox)

        *Figure 1. The Device type field shows `Unknown(BAV2ROPC)` user agent in Microsoft Defender XDR.*
    - **Check the use of anonymous proxies or the Tor network.** Threat actors often use these alternative proxies to hide their information, making them difficult to trace. However, not all use of said proxies correlate with malicious activities. You must investigate other suspicious activities that might provide better attack indicators.
    - Is the IP address coming from a virtual private network (VPN)? Is the VPN trustworthy? **Check if the IP originated from a VPN and review the organization behind it by using tools** like [RiskIQ Enterprise threat intelligence](https://community.riskiq.com/learn-more/enterprise).
    - **Check other IPs with the same subnet/ISP.** Sometimes password spray attacks originate from many different IPs within the same subnet/ISP.
- **Is the IP address common for the tenant?** Check the Activity log to see if the tenant has seen the IP address in the past 30 days.
- **Search for other suspicious activities or alerts that originated from the IP in the tenant.** Examples of activities to look out for might include email deletion, forwarding rules creation, or file downloads after a successful attempt to sign in.
- **Check the IP address' risk score** by using tools like RiskIQ.

### 3. Investigate suspicious user activity after signing in

Once you've identified the alert IP address as suspicious, review the accounts that signed in from that IP. It's possible that a group of accounts were compromised and successfully used to sign in from the IP or other similar IPs.

Filter all successful attempts to sign in from the IP address around and shortly after the time of the alerts. Then search for malicious or unusual activities in such accounts after signing in.

- User account activities

    **Validate that the activity in the account preceding the password spray activity is not suspicious.** For example, check if there's anomalous activity based on common location or ISP, if the account is utilizing a user-agent that it didn't use before, if any other guest accounts were created, if any other credentials were created after the account signed in from a malicious IP, among others.
- Alerts

    **Check whether the user received other alerts preceding the password spray activity.** Having these alerts indicate that the user account might be compromised. Examples include impossible travel alert, activity from infrequent country/region, and suspicious email deletion activity, among others.
- Incident

    **Check whether the alert is associated with other alerts that indicate an incident.** If so, then check whether the incident contains other true positive alerts.

## Advanced hunting queries

[Advanced hunting](advanced-hunting-overview) is a query-based threat hunting tool that lets you inspect events in your network and locate threat indicators.

Use the following query to find accounts with sign-in attempts that have the highest risk scores from the malicious IP. Before running the query, set the `ip_address` variable to the suspicious IP you want to investigate. The query also filters all successful sign-in attempts with their corresponding risk scores.

```kusto
let start_date = now(-7d);
let end_date = now();
let ip_address = ""; // enter here the IP address
AADSignInEventsBeta
| where Timestamp between (start_date .. end_date)
| where IPAddress == ip_address
| where isnotempty(RiskLevelDuringSignIn)
| project Timestamp, IPAddress, AccountObjectId, RiskLevelDuringSignIn, Application, ResourceDisplayName, ErrorCode
| sort by Timestamp asc
| sort by AccountObjectId, RiskLevelDuringSignIn
| partition by AccountObjectId ( top 1 by RiskLevelDuringSignIn ) // remove line to view all successful logins risk scores
```

Use the following query to check whether the suspicious IP used legacy protocols in sign-in attempts over the last eight hours. The query summarizes sign-in events by user agent, so you can identify legacy protocol indicators such as `Unknown(BAV2ROPC)`.

```kusto
let start_date = now(-8h);
let end_date = now();
let ip_address = ""; // enter here the IP address
AADSignInEventsBeta
| where Timestamp between (start_date .. end_date)
| where IPAddress == ip_address
| summarize count() by UserAgent
```

Use this query to review all alerts in the last seven days associated with the suspicious IP.

```kusto
let start_date = now(-7d);
let end_date = now();
let ip_address = ""; // enter here the IP address
let ip_alert_ids = materialize ( 
        AlertEvidence
            | where Timestamp between (start_date .. end_date)
            | where RemoteIP == ip_address
            | project AlertId);
AlertInfo
| where Timestamp between (start_date .. end_date)
| where AlertId in (ip_alert_ids)
```

Use the following query to review cloud app activity for accounts that successfully signed in from the suspicious IP in the last eight hours. The query identifies compromised accounts by filtering for successful sign-ins from the specified IP, then summarizes their cloud application activity by type.

```kusto
let start_date = now(-8h);
let end_date = now();
let ip_address = ""; // enter here the IP address
let compromise_users = 
    materialize ( AADSignInEventsBeta
                    | where Timestamp between (start_date .. end_date)
                    | where IPAddress == ip_address
                    | where ErrorCode == 0
                    | distinct AccountObjectId);
CloudAppEvents
    | where Timestamp between (start_date .. end_date)
    | where AccountObjectId in (compromise_users)
    | summarize ActivityCount = count() by AccountObjectId, ActivityType
    | extend ActivityPack = pack(ActivityType, ActivityCount)
    | summarize AccountActivities = make_bag(ActivityPack) by AccountObjectId
```

Use this query to review all alerts for suspected compromised accounts.

```kusto
let start_date = now(-8h); // change time range
let end_date = now();
let ip_address = ""; // enter here the IP address
let compromise_users = 
    materialize ( AADSignInEventsBeta
                    | where Timestamp between (start_date .. end_date)
                    | where IPAddress == ip_address
                    | where ErrorCode == 0
                    | distinct AccountObjectId);
let ip_alert_ids = materialize ( AlertEvidence
    | where Timestamp between (start_date .. end_date)
    | where AccountObjectId in (compromise_users)
    | project AlertId, AccountObjectId);
AlertInfo
| where Timestamp between (start_date .. end_date)
| where AlertId in (ip_alert_ids)
| join kind=innerunique ip_alert_ids on AlertId
| project Timestamp, AccountObjectId, AlertId, Title, Category, Severity, ServiceSource, DetectionSource, AttackTechniques
| sort by AccountObjectId, Timestamp
```

## Recommended Actions

After confirming a true positive password spray attack, take the following actions to remediate the threat and protect your organization:

1. [Block the attacker's IP address.](/en-us/azure/active-directory/conditional-access/block-legacy-authentication)
2. Reset user accounts' credentials.
3. Revoke access tokens of compromised accounts.
4. [Block legacy authentication.](/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-block-legacy)
5. [Require MFA for users](/en-us/microsoft-365/admin/security-and-compliance/multi-factor-authentication-microsoft-365) if possible to [enable Azure MFA](/en-us/azure/active-directory/authentication/tutorial-enable-azure-mfa) and make account compromise by a password spray attack difficult for the attacker.
6. Block the compromised user account from signing in if needed.