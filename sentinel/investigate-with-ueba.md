---
layout: Conceptual
title: Investigate Incidents with UEBA Data | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/investigate-with-ueba
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how to use UEBA data while investigating to gain greater context to potentially malicious activity occurring in your organization.
ms.author: guywild
author: guywi-ms
ms.reviewer: mshechter
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f4c9a593-9875-51f8-972c-889cbd446eff
document_version_independent_id: 0ad50cea-a570-bf90-b9e1-c0c965a6d986
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/investigate-with-ueba.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/investigate-with-ueba
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/investigate-with-ueba.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c0607d10-b8f6-f3ba-9bfe-0bdc9ca55412
---

# Investigate Incidents with UEBA Data | Microsoft Learn

This article describes common methods and sample procedures for using [user entity behavior analytics (UEBA)](identify-threats-with-entity-behavior-analytics) in your regular investigation workflows.

Important

Noted features in this article are currently in *preview*. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Prerequisites

Before you can use UEBA data in your investigations, you must [enable User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel](enable-entity-behavior-analytics).

Start looking for machine powered insights about one week after enabling UEBA.

## Find and investigate user anomalies in the Defender portal (Preview)

In the Defender portal, a **UEBA Anomalies** tag identifies users with anomalies, making it easier to prioritize investigations.

The **Top UEBA anomalies** section, which appears on the User side panel and the **Overview** tab of the User entity page, displays the user's top three anomalies from the last 30 days. Select the links at the bottom of the **Top UEBA anomalies** section to hunt for all of the user's anomalies and view the Sentinel events timeline.

[![Screenshot that shows the overview tab of the User page for a user with UEBA anomalies in the last 30 days.](media/investigate-with-ueba/entity-behavior-analytics-user-investigations.png)](media/investigate-with-ueba/entity-behavior-analytics-user-investigations.png#lightbox)

### Investigate user anomalies from an incident

To investigate a user in an incident, select **Go Hunt &gt; All user anomalies** from the user entity in the incident graph to retrieve all anomalies related to the user from the past 30 days.

[![Screenshot that shows an incident graph, highlighting the Go hunt All user anomalies option, which allows analysts to quickly find all anomalies related to the user.](media/identify-threats-with-entity-behavior-analytics/entity-behavior-analytics-incident-investigations.png)](media/identify-threats-with-entity-behavior-analytics/entity-behavior-analytics-incident-investigations.png#lightbox)

For more information about investigating user anomalies and the user entity page, see [Investigate incidents in the Microsoft Defender portal](https://aka.ms/ueba-go-hunt) and [User entity page in Microsoft Defender](https://aka.ms/ueba-entity-details).

## Run proactive, routine searches on entity data

We recommend running regular, proactive searches through user activity to create leads for further investigation.

Use the Microsoft Sentinel [UEBA Essentials solution](identify-threats-with-entity-behavior-analytics#enable-ueba-to-create-behavior-profiles-and-detect-anomalies) to query your data for a range of insights, such as:

- **Top risky users**, with anomalies or attached incidents.
- **Data on specific users**, to determine whether the user has indeed been compromised, or whether there is an insider threat based on actions that deviate from the user's profile.

Capture non-routine actions in the UEBA workbook, and use them to find anomalous activities and potentially non-compliance practices.

### Investigate an anomalous sign-in

For example, the following steps follow the investigation of a user who connected to a VPN that they'd never used before. This unfamiliar VPN connection is an anomalous activity.

1. In the Sentinel **Workbooks** area, search for and open the **User and Entity Behavior Analytics** workbook.
2. Search for a specific user name to investigate and select their name in the **Top users to investigate** table.
3. Scroll down through the **Incidents Breakdown** and **Anomalies Breakdown** tables to view the incidents and anomalies associated with the selected user.
4. In the anomaly, such as one named **Anomalous Successful Logon**, review the details shown in the table to investigate. For example:

    | Step | Description |
    | --- | --- |
    | **Note the description on the right** | Each anomaly has a description, with a link to learn more in the [MITRE ATT&CK knowledge base](https://attack.mitre.org/). For example: ***Initial Access*** *The adversary is trying to get into your network.* *Initial Access consists of techniques that use various entry vectors to gain their initial foothold within a network. Techniques used to gain a foothold include targeted spear phishing and exploiting weaknesses on public-facing web servers. Footholds gained through initial access may allow for continued access, like valid accounts and use of external remote services, or may be limited-use due to changing passwords.* |
    | **Note the text in the Description column** | In the anomaly row, scroll to the right to view an additional description. Select the link to view the full text. For example: *Adversaries may steal the credentials of a specific user or service account using Credential Access techniques or capture credentials earlier in their reconnaissance process through social engineering for means of gaining Initial Access. APT33, for example, has used valid accounts for initial access. The query below generates an output of successful Sign-in performed by a user from a new geo location he has never connected from before, and none of his peers as well.* |
    | **Note the UsersInsights data** | Scroll further to the right in the anomaly row to view the user insight data, such as the account display name and the account object ID. Select the text to view the full data on the right. |
    | **Note the Evidence data** | Scroll further to the right in the anomaly row to view the evidence data for the anomaly. Select the text view the full data on the right, such as the following fields: - **ActionUncommonlyPerformedByUser**- **UncommonHighVolumeOfActions**- **FirstTimeUserConnectedFromCountry**- **CountryUncommonlyConnectedFromAmongPeers**- **FirstTimeUserConnectedViaISP**- **ISPUncommonlyUsedAmongPeers**- **CountryUncommonlyConnectedFromInTenant**- **ISPUncommonlyUsedInTenant** |

Use the data found in the **User and Entity Behavior Analytics** workbook to determine whether the user activity is suspicious and requires further action.

## Use UEBA data to analyze false positives

Sometimes, an incident captured in an investigation is a false positive.

A common example of a false positive is when impossible travel activity is detected, such as a user who signed into an application or portal from both New York and London within the same hour. While Microsoft Sentinel notes the impossible travel as an anomaly, an investigation with the user might clarify that a VPN was used with an alternative location to where the user actually was.

### Analyze a false positive

For example, for an **Impossible travel** incident, after confirming with the user that a VPN was used, navigate from the incident to the user entity page. Use the data displayed on the user entity page to determine whether the locations captured are included in the user's commonly known locations.

For example:

[![Screenshot of an incident's user entity page showing user details and commonly known locations.](media/ueba/open-entity-pages.png)](media/ueba/open-entity-pages.png#lightbox)

The user entity page is also linked from the [incident page](investigate-cases#how-to-investigate-incidents) and from the [investigation graph](investigate-cases#use-the-investigation-graph-to-deep-dive).

Tip

After confirming the data on the user entity page for the specific user associated with the incident, go to the Microsoft Sentinel **Hunting** area to understand whether the user's peers usually connect from the same locations as well. If so, this knowledge would make an even stronger case for a false positive.

In the **Hunting** area, run the **Anomalous Geo Location Logon** query. For more information, see [Hunt for threats with Microsoft Sentinel](hunting).

### Embed IdentityInfo data in your analytics rules (Public Preview)

As attackers often use the organization's own user and service accounts, data about those user accounts, including the user identification and privileges, are crucial for the analysts in the process of an investigation.

The **IdentityInfo** table is a Microsoft Sentinel UEBA table that stores identity attributes such as user metadata, group memberships, and Microsoft Entra roles, synchronized from your Microsoft Entra workspace. Embed data from the **IdentityInfo** table to fine-tune your analytics rules to fit your use cases, reducing false positives, and possibly speeding up your investigation process.

For example:

- To correlate security events with the **IdentityInfo** table in an alert that's triggered if a server is accessed by someone outside the **IT** department:

    ```kusto
    SecurityEvent
    | where EventID in ("4624","4672")
    | where Computer == "My.High.Value.Asset"
    | join kind=inner  (
        IdentityInfo
        | summarize arg_max(TimeGenerated, *) by AccountObjectId) on $left.SubjectUserSid == $right.AccountSID
    | where Department != "IT"
    ```
- To correlate Microsoft Entra sign-in logs with the **IdentityInfo** table in an alert that's triggered if an application is accessed by someone who isn't a member of a specific security group:

    ```kusto
    SigninLogs
    | where AppDisplayName == "GitHub.Com"
    | join kind=inner  (
        IdentityInfo
        | summarize arg_max(TimeGenerated, *) by AccountObjectId) on $left.UserId == $right.AccountObjectId
    | where GroupMembership !contains "Developers"
    ```

The **IdentityInfo** table synchronizes with your Microsoft Entra workspace to create a snapshot of your user profile data, such as user metadata, group information, and Microsoft Entra roles assigned to each user. For more information, see [IdentityInfo table](ueba-reference#identityinfo-table) in the UEBA enrichments reference.

For details about the operators and functions used in the SecurityEvent and SigninLogs query examples, see the following Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***render*** operator](/en-us/kusto/query/render-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***iff()*** function](/en-us/kusto/query/iff-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***now()*** function](/en-us/kusto/query/now-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***bin()*** function](/en-us/kusto/query/bin-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***startofday()*** function](/en-us/kusto/query/startofday-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***sum()*** aggregation function](/en-us/kusto/query/sum-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

## Identify password spray and spear phishing attempts

Without multifactor authentication (MFA) enabled, user credentials are vulnerable to attackers looking to compromise attacks with [password spraying](https://www.microsoft.com/security/blog/2020/04/23/protecting-organization-password-spray-attacks/) or [spear phishing](https://www.microsoft.com/security/blog/2019/12/02/spear-phishing-campaigns-sharper-than-you-think/) attempts.

### Investigate a password spray incident with UEBA insights

For example, to investigate a password spray incident with UEBA insights, you might do the following to learn more:

1. In the incident, on the bottom left, select **Investigate** to view the accounts, machines, and other data points that were potentially targeted in an attack.

    Browsing through the data, you might see an administrator account with a relatively large number of logon failures. While this is suspicious, you might not want to restrict the account without further confirmation.
2. Select the administrative user entity in the map, and then select **Insights** on the right to find more details, such as the graph of sign-ins over time.
3. Select **Info** on the right, and then select **View full details** to jump to the [user entity page](entity-pages) to drill down further.

    For example, note whether this is the user's first Potential Password spray incident, or watch the user's sign-in history to understand whether the failures were anomalous.

Tip

You can also run the **Anomalous Failed Logon**[hunting query](hunting) to monitor all of an organization's anomalous failed logins. Use the results from the query to start investigations into possible password spray attacks.

## URL detonation (Public preview)

When there are URLs in the logs ingested into Microsoft Sentinel, those URLs are automatically detonated to help accelerate the triage process.

The Investigation graph includes a node for the detonated URL, as well as the following details:

- **DetonationVerdict**: The high-level, Boolean determination from detonation. For example, **Bad** means that the side was classified as hosting malware or phishing content.
- **DetonationFinalURL**: The final, observed landing page URL, after all redirects from the original URL.

For example:

![Screenshot of a sample URL detonation shown in the Investigation graph.](media/investigate-with-ueba/url-detonation-example.png)

Tip

If you don't see URLs in your logs, check that URL logging, also known as threat logging, is enabled for your secure web gateways, web proxies, firewalls, or legacy IDS/IPS.

You can also create custom logs to channel specific URLs of interest into Microsoft Sentinel for further investigation.