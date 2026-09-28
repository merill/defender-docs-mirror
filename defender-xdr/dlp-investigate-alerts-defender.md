---
layout: Conceptual
title: Investigate data loss alerts with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/dlp-investigate-alerts-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate Microsoft Purview Data Loss Prevention (DLP) alerts and incidents in Microsoft Defender XDR. Learn how to view correlated incidents, hunt across compliance and security data, and take remediation actions.
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2b9c3701-f583-b439-fb75-5d9530c56964
document_version_independent_id: 2b9c3701-f583-b439-fb75-5d9530c56964
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/dlp-investigate-alerts-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: dlp-investigate-alerts-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/dlp-investigate-alerts-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 80e069d9-bde8-cfd5-c801-8833ee9ac3ff
---

# Investigate data loss alerts with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Note

A built-in alert tuning rule for DLP signals will take effect in early October 2026. In Microsoft Defender XDR, the rule sets these signals as behaviors instead of alerts, so they don't generate alerts or appear in the incident queue. The signals remain available for advanced hunting in the [`BehaviorInfo`](advanced-hunting-behaviorinfo-table) and [`BehaviorEntities`](advanced-hunting-behaviorentities-table) tables. To continue seeing DLP signals as alerts in Microsoft Defender XDR, disable the rule in **Settings** &gt; **Microsoft Defender XDR** &gt; **Alert tuning**. For more information, see [Built-in alert tuning rules](investigate-alerts#built-in-alert-tuning-rules).

When the built-in DLP alert tuning rule is disabled, you can manage and respond to Microsoft Purview Data Loss Prevention (DLP) alerts and incidents in the Microsoft Defender portal. Open **Incidents & alerts** &gt; **Incidents** on the quick launch of the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139). From this page, you can:

- View all your DLP alerts grouped under incidents in the Microsoft Defender XDR incident queue.
- View DLP alerts correlated with other DLP alerts, or with alerts from other solutions (Defender for Endpoint, Defender for Office 365, Microsoft Sentinel, and so on), under a single incident.
- Hunt for security threats, using queries combining compliance logs with security logs, under Advanced Hunting.
- Take remediation actions in-place on users, files, and devices.
- Associate custom tags to DLP incidents and filter by them.
- Filter the unified incident queue by DLP policy name, tag, date, service source, incident status, and user.

## Prerequisites

Review the following licensing, role, and setup requirements before investigating DLP alerts.

### Licensing requirements

To investigate Microsoft Purview Data Loss Prevention incidents in the Microsoft Defender portal, you need a license from one of the following subscriptions:

- Microsoft Office 365 E5/A5
- Microsoft 365 E5/A5
- Microsoft 365 E5/A5 Compliance
- Microsoft 365 E5/A5 Information Protection and Governance

### Roles

It's best practice to only grant minimal permissions to alerts in the Microsoft Defender portal. You can create a custom role with these roles and assign it to the users who need to investigate DLP alerts.

| Permission | Defender Alert Access |
| --- | --- |
| Manage Alerts | DLP + Security |
| View-Only Manage Alerts | DLP + Security |
| Information Protection Analyst | DLP only |
| DLP Compliance Management | DLP only |
| View-Only DLP Compliance Management | DLP only |

## Prepare to investigate DLP alerts

[Turn on alerts for all your DLP policies](/en-us/purview/dlp-create-deploy-policy) in the [Microsoft Purview portal](https://purview.microsoft.com).

Note

[Administrative units](/en-us/microsoft-365/compliance/microsoft-365-compliance-center-permissions#administrative-units) restrictions flow from data loss prevention (DLP) into the Defender portal. If you are an administrative unit restricted admin, you'll only see the DLP alerts for your administrative unit.

## Investigate DLP alerts in the Microsoft Defender portal

Perform the following steps to find and review DLP alerts in the Microsoft Defender portal.

1. Go to the Microsoft Defender portal, and select **Incidents** in the left hand navigation menu to open the incidents page.
2. Select **Add filter** on the toolbar, and choose the **Service/detection sources** filter. Then select the **Service/detection sources** filter and choose **Microsoft Data Loss Prevention** to view all incidents with DLP alerts. You can also filter the queue by user and device names (using the **Entities** filter) and by policies, using the **Policy/policy rule** filter, you can search on file names, user, device names, and file paths.

    1. (in preview) In the **Incidents** queue &gt; **Alert policies** &gt; Alert policy title. You can search on the DLP policy name.
3. Search for the DLP policy name of the alerts and incidents you're interested in.
4. To view the incident summary page, select the incident from the queue. Similarly, select the alert to view the DLP alert page. Select **Summarize** (preview) for Security Copilot to generate a summary of the alert. The Security Copilot-generated alert summary will contain the:

- alert severity
- alert title
- the name of the policy that was matched
- the name file involved and a link to the file
- alert status
- the email address of the user who performed the action that matched the policy

1. View the **Alert story** for details about policy and the sensitive information types detected in the alert. Select the event in the **Related Events** section to see the user activity details.
2. View the matched sensitive content in the **Sensitive info types** tab and the file content in the **Source** tab if you have the required permission (see [required roles and permissions](/en-us/microsoft-365/compliance/dlp-alerts-dashboard-get-started#roles)).

### Extend DLP alert investigation with advanced hunting

Advanced hunting is a query-based threat hunting tool that lets you explore up to 30 days of audit logs of user, files and site locations to aid in your investigation. You can proactively inspect events in your network to locate threat indicators and entities. The flexible access to data enables unconstrained hunting for both known and potential threats.

The **CloudAppEvents** table contains all audit logs across all locations like SharePoint, OneDrive, Exchange and Devices.

#### Before you begin

If you're new to Microsoft Defender advanced hunting, review [Get started with advanced hunting](advanced-hunting-overview).

Before you can use advanced hunting you must have [access to the **CloudAppEvents** table](/en-us/defender-cloud-apps/protect-office-365#connect-microsoft-365-to-microsoft-defender-for-cloud-apps) that contains Microsoft Purview DLP audit data.

#### Use built-in advanced hunting queries for DLP investigations

Important

This feature is in preview. Preview features aren't meant for production use and may have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

The Defender portal offers multiple built-in queries you can use to help with your DLP alert investigation.

1. Go to the Microsoft Defender portal, and select **Incidents & alerts** in the left hand navigation menu to open the incidents page. Select **Incidents**.
2. Select **Filters** on the top right, and choose **Service Source : Data Loss Prevention** to view all incidents with DLP alerts.
3. Open a DLP incident.
4. Select on an alert to view its associated events.
5. Select an event.
6. In the event details pane, select the **Go Hunt**control.
    1. Defender shows you a list of built-in queries that are relevant to the source location of the event. For example, if the event is from SharePoint you see
        1. **File shared with**
        2. **File activities**
        3. **Site activity**
        4. **User DLP violations for last 30 days**
7. You can choose to **Run query** immediately, change the time range, edit or save the query for later use.
8. Once you run the query, view the results on the **Results** tab.

If the alert is for an email message, you can download the message by selecting **Actions** &gt; **Download email**.

If the alert is for a file in SharePoint Online or One Drive for Business, you can take the following remediation actions:

- Apply retention label
- Unshare
- Delete
- Apply sensitivity label
- Download ([data classification content viewer role](/en-us/defender-office-365/scc-permissions#role-groups-in-microsoft-defender-for-office-365-and-microsoft-purview-compliance) is required for this action)
- Withdraw feedback

To take remediation actions on the user associated with the alert, select the **User card** on the top of the alert page to open the user details.

For Devices DLP alerts, select the device card on the top of the alert page to view details about the device associated with the alert and take remediation actions.

Go to the incident summary page and select **Manage Incident** to add incident tags, assign, or resolve an incident.