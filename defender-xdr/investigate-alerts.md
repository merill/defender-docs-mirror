---
layout: Conceptual
title: Investigate alerts in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/investigate-alerts
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate alerts seen across devices, users, and mailboxes.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
ms.custom:
- msecd-doc-authoring-1028
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c06e410c-40c7-f5bb-fa10-81a72443b6f6
document_version_independent_id: c06e410c-40c7-f5bb-fa10-81a72443b6f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/investigate-alerts.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/investigate-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 5fd9b229-f196-2531-6e05-3a48a81aac9a
---

# Investigate alerts in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Note

This article describes security alerts in Microsoft Defender XDR. However, you can use alert policies to send email notifications to yourself or other admins when users perform specific activities in Microsoft 365. For more information, see [Alert policies in the Microsoft Defender portal](alert-policies).

Note

While this article is specific to Defender XDR, you don't necessarily need an XDR license to access these alerts. For example, if you have Microsoft Defender for Office 365, you get alerts in the locations mentioned in this article. Depending on your license level, you have access to some Defender XDR settings in the Defender settings catalog. For more information on Defender for 365, see the [Microsoft Defender for Office 365 documentation](/en-us/defender-office-365/).

Alerts are signals that result from various threat detection activities. These signals are produced by the many security services that reside in the Microsoft Defender portal, and they indicate the occurrence of malicious or suspicious events in your environment.

These suspicious events are typically part of a broader attack story. In the Microsoft Defender portal, alerts represent individual pieces of evidence that Defender XDR correlates together to form [incidents](incidents-overview) (see [Incidents overview](incidents-overview)). Incidents tell the whole attack story; however, analyzing alerts can be valuable when deeper analysis is required.

The **Alerts queue** shows the current set of alerts. You can view the entire alerts queue from **Incidents & alerts &gt; Alerts** on the quick launch of the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139). You can also see the alerts for each incident on the [Incidents queue](incidents-overview), and on each individual incident's page, on the **Alerts** tab.

[![The Alerts section in the Microsoft Defender portal](media/investigate-alerts/alerts-page-defender-small.png)](media/investigate-alerts/alerts-page-defender.png#lightbox)

Alerts from different Microsoft security solutions like Microsoft Defender for Endpoint, Defender for Office 365, Microsoft Sentinel, Defender for Cloud, Defender for Identity, Defender for Cloud Apps, Defender XDR, App Governance, Microsoft Entra ID Protection, and Microsoft Data Loss Prevention appear in the Alerts queue.

By default, the alerts queue in the Microsoft Defender portal displays the new and in progress alerts from the last seven days. The most recent alert is at the top of the list so you can see it first. You can also find the **total number of alerts** in the queue indicated beside the Search bar. The total number of alerts varies depending on the filters used in the queue.

From the default alerts queue, you can select **Filter** to see all available filters from which you can specify a subset of the alerts. Here's an example.

[![All the filters available in the Alerts queue in the Microsoft Defender portal](media/investigate-alerts/alert-filters-small.png)](media/investigate-alerts/alert-filters.png#lightbox)

You can filter alerts according to these criteria:

- Severity
- Status
- Categories
- Service/detection sources
- Tags
- Policy/Policy rule
- Alert type
- Product name
- Alert subscription ID
- Entities (the impacted assets)
- Automated investigation state
- Workspace
- Data stream (workload or location)
- Sensitivity label

Note

Microsoft Defender XDR customers can now filter incidents with alerts where a compromised device communicated with operational technology (OT) devices connected to the enterprise network through the [device discovery integration of Microsoft Defender for IoT and Microsoft Defender for Endpoint](/en-us/defender-endpoint/device-discovery#device-discovery-integration). To filter these incidents, select **Any** in the Service/detection sources, then select **Microsoft Defender for IoT** in the Product name or see [Investigate incidents and alerts in Microsoft Defender for IoT in the Defender portal](/en-us/defender-for-iot/investigate-threats/). You can also use device groups to filter for site-specific alerts. For more information about Defender for IoT prerequisites, see [Get started with enterprise IoT monitoring in Microsoft Defender XDR](/en-us/azure/defender-for-iot/organizations/eiot-defender-for-endpoint/).

An alert can have system tags and/or custom tags with white, red, or black backgrounds. Custom tags use the white background while system tags typically use red or black background colors. System tags identify the following in an incident:

- A **type of attack**, like ransomware or credential phishing
- **Automatic actions**, like automatic investigation and response and automatic attack disruption
- **Defender Experts** handling an incident
- **Critical assets** involved in the incident

Tip

Microsoft's Security Exposure Management, based on predefined classifications, automatically tags devices, identities, and cloud resources as a **critical asset**. This out-of-the-box capability ensures the protection of an organization's valuable and most important assets. It also helps security operations teams to prioritize investigation and remediation. Know more about [critical asset management](/en-us/security-exposure-management/critical-asset-management).

Important

Some information in this article relates to a prereleased product, which may be substantially modified before it’s commercially released. Microsoft makes no warranties expressed or implied, with respect to the information provided here.

You can search for alerts using a custom date and time range or by using the search bar to search for specific alerts. To search for alerts within a specific date or time range, select **Custom range** in the date picker and then specify the start and end dates and times.

![Highlighting the custom range option in the date and time picker in the Alerts queue.](media/investigate-alerts/alerts-custom-range.png)

To search for specific alerts, enter the search term in the search bar. You can search for alerts based on the alert title or alert ID.

[![Highlighting the search bar in the Alerts queue](media/investigate-alerts/alerts-search-bar-small.png)](media/investigate-alerts/alerts-search-bar.png#lightbox)

## Required permissions to investigate alerts

Access to alerts in the Microsoft Defender portal is controlled by Microsoft Defender permissions and role assignments.

### Required role assignments

You can receive the permissions required to view alerts through these role assignments:

- Microsoft Entra roles, such as Security Reader, Security Operator, or Security Administrator.
- Microsoft Defender custom roles that include permissions to access security data, such as Security data basics (read).

For more information, see [Permissions in Microsoft Defender unified role-based access control (RBAC)](manage-rbac).

Note

Microsoft Sentinel data continues to use Microsoft Sentinel workspace permissions. To view alerts that contain Microsoft Sentinel data, you need the appropriate Azure RBAC permissions on the corresponding Sentinel workspace. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).

## Analyze an alert

To see the main alert page, select the name of the alert. Here's an example.

[![Screenshot showing the details of an alert in the Microsoft Defender portal](media/investigate-alerts/alerts-ss-alerts-main.png)](media/investigate-alerts/alerts-ss-alerts-main.png#lightbox)

You can also select the **Open the main alert page** action from the **Manage alert** pane.

An alert page is composed of these sections:

- Alert story, which is the chain of events and alerts related to this alert in chronological order
- Summary details

Throughout an alert page, you can select the ellipses (**...**) beside any entity to see available actions, such as linking the alert to another incident. The list of available actions depends on the selected alert's type.

### Alert sources

Microsoft Defender XDR alerts come from solutions like Microsoft Defender for Endpoint, Defender for Office 365, Defender for Identity, Defender for Cloud Apps, the app governance add-on for Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection, and Microsoft Data Loss Prevention. You might notice prepended characters in the alert ID. The following table provides guidance to help you understand the mapping of alert sources based on the prepended character on the alert.

Note

- The prepended GUIDs are specific only to unified experiences such as unified alerts queue, unified alerts page, unified investigation, and unified incident.
- The prepended character does not change the GUID of the alert. The only change to the GUID is the prepended component.

| Alert source | Alert ID with prepended characters |
| --- | --- |
| Microsoft Defender XDR | `ra{GUID}``ta{GUID}` for alerts from ThreatExperts `ea{GUID}` for alerts from custom detections |
| Microsoft Defender for Office 365 | `fa{GUID}` Example: `fa123a456b-c789-1d2e-12f1g33h445h6i` |
| Microsoft Defender for Endpoint | `da{GUID}``ed{GUID}` for alerts from custom detections |
| Microsoft Defender for Identity | `aa{GUID}``ri{GUID}` for alerts from XDR detection engine  Example: `aa123a456b-c789-1d2e-12f1g33h445h6i`, `ri001122334455667788_-0123456789` |
| Microsoft Defender for Cloud Apps | `ca{GUID}``ma{GUID}` for alerts from App Governance detections and policies `rm{GUID}` for alerts from XDR detection engine  Example: `ca123a456b-c789-1d2e-12f1g33h445h6i` |
| Microsoft Entra ID Protection | `ad{GUID}` |
| App Governance | `ma{GUID}` |
| Microsoft Data Loss Prevention | `dl{GUID}` |
| Microsoft Defender for Cloud | `dc{GUID}` |
| Microsoft Sentinel | `sn{GUID}` |
| Microsoft Purview Insider Risk Management | `ir{GUID}` |
| Microsoft Security Copilot | `sc{GUID}` |

Note

If you have provisioned access to Microsoft Purview Insider Risk Management, you can view and manage insider risk management alerts and hunt for insider risk management events in the Microsoft Defender portal. For more information, see [Investigate insider risk threats in the Microsoft Defender portal](irm-investigate-alerts-defender).

### Alert promotion (preview)

Alert promotion automatically creates Microsoft Defender XDR alerts from alerts ingested from supported third-party security products. Promotion requires a Microsoft Sentinel workspace [onboarded to the Microsoft Defender portal](/en-us/unified-secops/microsoft-sentinel-onboard).

Supported sources are listed in the following table. Ingest data through the connector listed for each source.

| Source | Alerts promoted | Connector |
| --- | --- | --- |
| CrowdStrike | High, Critical, and CrowdStrike OverWatch alerts. | [CrowdStrike API Data Connector (via Codeless Connector Framework)](/en-us/azure/sentinel/data-connectors-reference#crowdstrike-api-data-connector-via-codeless-connector-framework) |

Promoted alerts include extracted entities and enrichment and can be correlated into incidents with other alerts. To find promoted alerts and their incidents, filter the **Alerts** and **Incidents** pages by the source product, such as **CrowdStrike**.

If you already use analytics rules to create alerts from the same data, you might see duplicate alerts. Review overlapping rules before changing them. To manage unwanted promoted alerts, use alert tuning.

### Configure alert service settings

To configure alert service settings in Microsoft Defender XDR:

1. Go to the Microsoft Defender portal (https://security.microsoft.com), select **Settings** &gt; **Microsoft Defender XDR**.
2. From the list, select **Alert service settings**, and then configure the alert settings for the service.

    Important

    Starting December 11, 2025, Microsoft Defender XDR is rolling out enhanced configuration options for Entra ID Protection alerts in public preview. These updates give you more granular control over risk-based alerting. The new default setting is **High-risk detections only**. Change the default setting to **High + Medium** or **All detections** based on your organization’s needs.

    [![Screenshot of Microsoft Entra ID Protection alerts setting in the Microsoft Defender portal.](media/investigate-alerts/alert-service-settings-entra.png)](media/investigate-alerts/alert-service-settings-entra.png#lightbox)

You can access **Alert service settings** from the **Incidents** page in the Microsoft Defender portal.

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

### Analyze affected assets

On an alert details page, the **Actions taken** section lists impacted assets, such as mailboxes, devices, and users affected by the alert.

You can also select **View in action center** to view the **History** tab of the **Action center** in the Microsoft Defender portal.

### Trace an alert's role in the alert story

The alert story displays all assets or entities related to the alert in a process tree view. On the alert details page, the alert named in the page title is the one initially in focus. Assets in the alert story are expandable and clickable. They provide additional information and expedite your response by allowing you to take action right in the context of the alert page.

Note

The alert story section may contain more than one alert, with additional alerts related to the same execution tree appearing before or after the alert you've selected.

### View more alert information on the details page

The details page shows the details of the selected alert, with details and actions related to it. If you select any of the affected assets or entities in the alert story, the details page changes to provide contextual information and actions for the selected object.

Once you've selected an entity of interest, the details page changes to display information about the selected entity type, historic information when it's available, and options to take action on this entity directly from the alert page.

## Manage alert status and classification

To manage an alert, select **Manage alert** in the summary details section of the alert page. For a single alert, here's an example of the **Manage alert** pane.

[![Screenshot of the Manage alert section in the Microsoft Defender portal](media/investigate-alerts/alerts-ss-alerts-manage.png)](media/investigate-alerts/alerts-ss-alerts-manage.png#lightbox)

The **Manage alert** pane allows you to view or specify:

- The alert status (New, Resolved, In progress).
- The user account that has been assigned the alert.
- The alert's classification:
    - **Not Set** (default).
    - **True positive** with a type of threat. Use this classification for alerts that accurately indicate a real threat. Specifying this threat type alerts your security team see threat patterns and act to defend your organization from them.
    - **Informational, expected activity** with a type of activity. Use this option for alerts that are technically accurate, but represent normal behavior or simulated threat activity. You generally want to ignore these alerts but expect them for similar activities in the future where the activities are triggered by actual attackers or malware. Use the options in this category to classify alerts for security tests, red team activity, and expected unusual behavior from trusted apps and users.
    - **False positive** for types of alerts that were created even when there's no malicious activity or for a false alarm. Use the options in this category to classify alerts that are mistakenly identified as normal events or activities as malicious or suspicious. Unlike alerts for 'Informational, expected activity', which can also be useful for catching real threats, you generally don't want to see these alerts again. Classifying alerts as false positive helps Microsoft Defender XDR improve its detection quality.
- A comment on the alert.

Note

- In August 2022, previously supported alert determination values (`Apt` and `SecurityPersonnel`) were deprecated and are no longer available via the API.
- One way of managing alerts is through the use of tags. The tagging capability for Microsoft Defender for Office 365 is currently in preview, rolling out incrementally.

Currently, modified tag names are only applied to alerts created *after* the update. Alerts that were generated before the modification will not reflect the updated tag name.

To manage a *set of alerts similar to a specific alert*, select **View similar alerts** in the **INSIGHT** box in the summary details section of the alert page.

[![Screenshot of selecting an alert in the Microsoft Defender portal](media/investigate-alerts/alerts-ss-alerts-manage-select.png)](media/investigate-alerts/alerts-ss-alerts-manage-select.png#lightbox)

From the **Manage alerts** pane, you can then classify all of the related alerts at the same time. Here's an example.

[![Screenshot of managing related alerts in the Microsoft Defender portal](media/investigate-alerts/alerts-ss-alerts-select-related.png)](media/investigate-alerts/alerts-ss-alerts-select-related.png#lightbox)

If similar alerts were already classified in the past, you can save time by using Microsoft Defender XDR recommendations to learn how previously classified similar alerts were resolved. From the summary details section, select **Recommendations**.

[![Screenshot of an example of selecting recommendations for an alert](media/investigate-alerts/alerts-ss-alerts-recommendations.png)](media/investigate-alerts/alerts-ss-alerts-recommendations.png#lightbox)

The **Recommendations** tab provides next-step actions and advice for investigation, remediation, and prevention. Here's an example.

[![Screenshot of an example of alert recommendations](media/investigate-alerts/alerts-ss-alerts-recommendations-example.png)](media/investigate-alerts/alerts-ss-alerts-recommendations-example.png#lightbox)

## Built-in alert tuning rules

Microsoft Defender includes built-in alert tuning rules that help reduce reporting noise from common benign activity. These built-in rules suppress alerts without affecting other features like AIR investigations and email notifications. If the AIR investigation detects malicious or suspicious activity, the new alert is reactivated.

To see the built-in alert tuning rules in the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Microsoft Defender XDR** &gt; **Rules** section &gt; **Alert tuning** or directly on the **Alert tuning** page at https://security.microsoft.com/securitysettings/defender/alert_suppression.

Be sure to review these rules to understand how they might affect which alerts appear in the Microsoft Defender portal.

Important

Built-in alert tuning rules don't apply to alerts from [custom detection rules](/en-us/defender-xdr/custom-detections-overview) and [Custom TI](/en-us/defender-endpoint/indicators-overview).

Note

The [Microsoft Security Copilot Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) doesn't classify alerts suppressed by [alert tuning](/en-us/defender-xdr/investigate-alerts#tune-an-alert). Be sure to disable the **Auto-Resolve - Email reported by user as malware or phish** built-in alert tuning rule and any custom tuning rules that suppress this alert.

## Tune an alert

As a security operations center (SOC) analyst, one of the top issues is triaging the sheer number of alerts that are triggered daily. While wanting to focus only on high severity and high priority alerts, analysts are also required to triage and resolve lower priority alerts, which tend to be a manual process. Alert tuning (previously *alert suppression*) lets you hide or resolve alerts automatically when expected organizational behavior occurs and rule conditions are met. This streamlines your alert queue and saves triage time.

Alert tuning rules support conditions based on *evidence types* such as files, processes, scheduled tasks, and other types of evidence that trigger alerts. After creating an alert tuning rule, apply it to the selected alert or any alert type that meets the defined conditions to tune the alert.

Microsoft Defender XDR includes built-in alert tuning rules that help reduce reporting noise from common benign activity. These built-in rules suppress alerts without affecting other features like AIR investigations and email notifications. If the AIR investigation detects malicious or suspicious activity, Defender XDR reactivates the suppressed alert.

You can also create your own custom alert tuning rules to perform one of the following actions when specific conditions are met:

- **Hide alert**: Suppresses the alert and prevents incident creation. Hidden alerts remain in *AlertInfo* and *AlertEvidence* tables. The **Hide alert** action is only applicable for Defender for Endpoint alerts.
- **Resolve alert**: Automatically resolves the alert and related incidents. Matching alerts and their associated incidents are triggered with resolved status.
- **Set as behavior**: Converts matching signals into behaviors. They won’t appear in the alert queue or trigger incidents. Data remains in *BehaviorInfo* and *BehaviorEntities* tables for hunting. This action isn't supported for Defender for Cloud or Microsoft Defender for Office 365 alerts.

Caution

Use alert tuning with caution, for scenarios where known, internal business applications or security tests trigger expected activity.

### Create rule conditions to tune alerts

Create alert tuning rules from the Microsoft Defender XDR **Settings** area or from an alert details page. Select one of the following tabs to continue.

# [Create a rule from the Settings page](#tab/settings)
To create an alert tuning rule from the Settings page, follow these steps:

1. In the Microsoft Defender portal, select **Settings &gt; Microsoft Defender XDR &gt; Alert tuning**.

    [![Screenshot of Alert tuning option in Microsoft Defender XDR's Settings page.](media/investigate-alerts/alert-tuning-settings.png)](media/investigate-alerts/alert-tuning-settings.png#lightbox)
2. Select **Add new rule** to tune a new alert, or select an existing rule row to make changes. Selecting the rule title opens a rule details page, where you can view a list of associated alerts, edit conditions, or turn the rule on and off.
3. In the **Tune alert** pane, under **Select service sources**, select the service sources where you want to the rule to apply. Only services where you have permissions are shown in the list. For example:

    [![Screenshot of service source dropdown menu in Tune an alert page.](media/investigate-alerts/alert-tuning-select-service.png)](media/investigate-alerts/alert-tuning-select-service.png#lightbox)
4. In the **Conditions** area, add a condition for the alert's triggers. For example, if you want to prevent an alert from being triggered when a specific file is created, define a condition for the **File:Custom** trigger, and define the file details:

    [![Screenshot of the IOC menu in Tune an alert page.](media/investigate-alerts/alert-tuning-choose-ioc2.png)](media/investigate-alerts/alert-tuning-choose-ioc2.png#lightbox)

    - Listed triggers differ, depending on the service sources you selected. Triggers are all indicators of compromise (IOCs), such as files, processes, scheduled tasks, and other evidence types that might trigger an alert, including AntiMalware Scan Interface (AMSI) scripts, Windows Management Instrumentation (WMI) events, or scheduled tasks.
    - To set multiple rule conditions, select **Add filter** and use **AND**, **OR**, and grouping options to define the relationships between the multiple evidence types that trigger the alert. Further evidence properties are automatically populated as a new subgroup, where you can define your condition values. Condition values aren't case sensitive, and some properties support wildcards.
5. In the **Action** area of the **Tune alert** pane, select the relevant action you want the rule to take. Choose from **Hide alert**, **Resolve alert**, or **Set as behavior**.
6. Enter a meaningful name for your alert and a comment to describe the alert, and then select **Save**.

# [Create a rule from the Alerts page](#tab/alerts)
To create an alert tuning rule from an alert details page, follow these steps:

1. In the Microsoft Defender portal, go to the **Alerts** page or an alert details page. If you're on the **Alerts** page, first select the alert you want to tune, and then select **Tune alert**. Depending on your screen resolution, you might need to select the ellipsis (**...**) to see the **Tune alert** option. For example:

    ![Screenshot of the Tune alert option from an alert details pane.](media/investigate-alerts/tune-alert-alert-details.png)

    The **Tune alert** pane opens on the side, where you can define conditions for the alert. For example:

    ![Screenshot of the Tune alert pane from the Alerts page.](media/investigate-alerts/tune-alert-pane-alert-details.png)
2. In the **Alert types** area, select to apply the alert tuning rule only to alerts of the selected type, or any alert type based on the same conditions. If you select **Any alert type based on certain conditions**, also select the service sources where you want the rule to apply. Only services where you have permissions are shown in the list. For example:

    ![Screenshot of the Service sources area showing in the Tune alert pane.](media/investigate-alerts/alert-tuning-alert-details-service-sources.png)
3. In the **Conditions** area, add a condition for the alert's triggers. For example, if you want to prevent an alert from being triggered when a specific file is created, define a condition for the **File:Custom** trigger, and define the file details:

    ![Screenshot of the Conditions area in the Alert tuning pane.](media/investigate-alerts/alert-tuning-alert-details-conditions.png)

    - Listed triggers differ, depending on the service sources you selected. Triggers are all indicators of compromise (IOCs), such as files, processes, scheduled tasks, and other evidence types that might trigger an alert, including AntiMalware Scan Interface (AMSI) scripts, Windows Management Instrumentation (WMI) events, or scheduled tasks.
    - To set multiple rule conditions, select **Add filter** and use **AND**, **OR**, and grouping options to define the relationships between the multiple evidence types that trigger the alert. Further evidence properties are automatically populated as a new subgroup, where you can define your condition values. Condition values aren't case sensitive, and some properties support wildcards.
4. In the **Action** area of the **Tune alert** pane, select the relevant action you want the rule to take. Choose from **Hide alert**, **Resolve alert**, or **Set as behavior**.
5. Enter a meaningful name for your alert and a comment to describe the alert.
6. Select **Save**

---

Note

The **alert title (Name)** is based on the **alert type (IoaDefinitionId)**, which decides the alert title. Two alerts that have the same alert type can change to a different alert title. The *Hide alert* feature is only available in Defender for Endpoint alerts.

Note

Alert suppression is not compatible for custom detections. Make sure to fine-tune your custom detections to avoid false positives.

After creating your alert tuning rule from an alert details page, in the **Successful rule creation** page that appears, add any of the alert-related IOCs as indicators to an *allow list* to prevent them from being blocked in the future. IOCs that are configured as part of the alert tuning rule are selected by default. For example:

1. Add a file to the **Select evidence (IOC) to allow** list. By default, the file that triggered the alert is already selected.
2. Define a scope for the **Select scope to apply to** value. By default, the scope that applies to your alert is selected.
3. Select **Save** to add the file to an allow list and prevent it from being blocked.

## Resolve an alert

Once you're done analyzing an alert and it can be resolved, go to the **Manage alert** pane for the alert or similar alerts and mark the status as **Resolved** and then classify it as a **True positive** with a type of threat, an **Informational, expected activity** with a type of activity, or a **False positive**.

Classifying alerts helps Microsoft Defender XDR improve its detection quality.

## Use Power Automate to triage alerts

Modern security operations (SecOps) teams need automation to work effectively. To focus on hunting and investigating real threats, SecOps teams use Power Automate to triage through the list of alerts and eliminate the ones that aren't threats.

### Criteria for resolving alerts

In this Power Automate example, the flow checks the following criteria to decide whether to resolve the alert automatically:

- User has Out-of-office message turned on
- User isn't tagged as high risk

If the user has an Out-of-office message turned on and isn't tagged as high risk, SecOps marks the alert as legitimate travel and resolves it. A notification is posted in Microsoft Teams after the alert is resolved.

### Connect Power Automate to Microsoft Defender for Cloud Apps

To create the automation, you'll need an API token before you can connect Power Automate to Microsoft Defender for Cloud Apps.

1. Open the [Microsoft Defender portal](https://security.microsoft.com/) and select **Settings** &gt; **Cloud Apps** &gt; **API token**, and then select **Add token** in the **API tokens** tab.
2. Provide a name for your token, and then select **Generate**. Save the token as you'll need it later.

### Create an automated flow

Watch the following video to learn how to connect Power Automate to Defender for Cloud Apps and create an automated alert triage workflow.

## Use Dynamic Threat Detection Agent to triage alerts

[Microsoft Security Copilot in Microsoft Defender](security-copilot-in-microsoft-365-defender) includes the Dynamic Threat Detection Agent, an always on, adaptive backend service that uncovers hidden threats across Defender and Microsoft Sentinel environments. It uses AI to identify gaps and uncover false negatives by correlating alerts, events, anomalies, and threat intelligence. When the agent identifies a gap, it generates a dynamic alert with the full context in the alert details, including natural language explanations, mapped [MITRE ATT&CK techniques](https://attack.mitre.org/), and tailored remediation steps.

For more information, see [Microsoft Security Copilot Dynamic Threat Detection Agent](dynamic-threat-detection-agent).