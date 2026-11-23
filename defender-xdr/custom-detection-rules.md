---
layout: Conceptual
title: Create custom detection rules in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/custom-detection-rules
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create custom detection rules based on advanced hunting queries to proactively monitor events and take automated response actions.
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier2
ms.custom:
- msecd-doc-authoring-1014
- sfi-ga-nochange
- cx-ti
- cx-ah
- sfi-image-nochange
ms.topic: how-to
ms.date: 2026-11-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 889233db-f43a-794c-5a31-24ee96a226be
document_version_independent_id: 889233db-f43a-794c-5a31-24ee96a226be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/custom-detection-rules.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: custom-detection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/custom-detection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 07966987-9838-b2f6-59e1-a5ccbc17abd4
---

# Create custom detection rules in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Custom detection rules are [advanced hunting](advanced-hunting-overview) queries you design and tweak to proactively monitor various events and system states, including suspected breach activity and misconfigured endpoints. You can set them to run at regular intervals, generating alerts and taking response actions whenever there are matches.

This article walks you through creating and configuring a custom detection rule, including preparing the query, setting alert details, specifying automated response actions, and defining the rule scope.

## Required permissions for managing custom detections

To manage custom detections, you need roles with permissions for the data these detections target. For example, to manage custom detections on multiple data sources (Microsoft Defender and Microsoft Sentinel, or multiple Defender workloads), you need all the applicable Defender and Sentinel roles. For more information, see Microsoft Defender XDR and Microsoft Sentinel.

### Required permissions in Microsoft Defender XDR

To manage custom detections on Microsoft Defender data, you need to be assigned one of these roles:

- **Security settings (manage)** - Users with this [Microsoft Defender permission](manage-rbac) can manage security settings in the Microsoft Defender portal.
- **Security Administrator** - Users with this [Microsoft Entra role](/en-us/azure/active-directory/roles/permissions-reference#security-administrator) can manage security settings in the Microsoft Defender portal and other portals and services.
- **Security Operator** - Users with this [Microsoft Entra role](/en-us/azure/active-directory/roles/permissions-reference#security-operator) can manage alerts and have global read-only access to security-related features, including all information in the Microsoft Defender portal. This role is sufficient for managing custom detections only if role-based access control (RBAC) is turned off in Microsoft Defender for Endpoint. If you have RBAC configured, you also need the **Manage Security Settings** permission for Defender for Endpoint.

You can manage custom detections that apply to data from specific Defender solutions if you have the right permissions for them. For example, if you only have manage permissions for Microsoft Defender for Office 365, you can create custom detections using `Email*` tables but not `Identity*` tables.

Likewise, since the `IdentityLogonEvents` table holds authentication activity information from both Microsoft Defender for Cloud Apps and Defender for Identity, you need to have manage permissions for both services to manage custom detections querying that table.

Note

To manage custom detections, Security Operators must have the Manage Security Settings permission in Microsoft Defender for Endpoint if RBAC is turned on.

### Required permissions in Microsoft Sentinel

To manage custom detections on Microsoft Sentinel data, you need to be assigned the **Microsoft Sentinel Contributor** role or higher. Users with this [Azure role](/en-us/azure/role-based-access-control/built-in-roles/security#microsoft-sentinel-contributor) can manage Microsoft Sentinel SIEM workspace data, including alerts and detections. You can assign this role on a specific primary workspace, Azure resource group, or an entire subscription.

### Manage required permissions

To manage required permissions, a Global Administrator can:

- Assign the Security Administrator or Security Operator role in [Microsoft 365 admin center](https://admin.microsoft.com/) under **Roles** &gt; **Security Administrator**.
- Check RBAC settings for Microsoft Defender for Endpoint in [Microsoft Defender XDR](https://security.microsoft.com/) under **Settings** &gt; **Permissions** &gt; **Roles**. Select the corresponding role to assign the **manage security settings** permission.

Important

Use roles with the fewest permissions to help improve security for your organization. Global Administrator is a highly privileged role. Limit its use to emergency scenarios when you can't use an existing role.

Note

A user also needs the appropriate permissions for the devices in the device scope of a custom detection rule that they're creating or editing. A user can't edit a custom detection rule that is scoped to run on all devices if the user doesn't have permissions for all devices.

## Create a custom detection rule

You can create a custom detection rule from either of the following entry points:

- **From Advanced hunting** — Go to **Advanced hunting**, prepare and run your query, then select **Create detection rule**. This approach lets you validate your query results before creating the rule.
- **From the custom detections list** — Go to **Custom detection rules** and select **+ Create detection rule**. This approach opens the rule wizard directly, where you can write or paste a query and configure all rule settings in one place.

Regardless of which entry point you use, prepare the query, then configure the wizard steps in this order:

1. **General**
2. **Alert settings**
3. **Incident settings** (preview)
4. **Automated actions**
5. **Scope**
6. **Review and create**

### 1. Prepare the query

In the Microsoft Defender portal, go to **Advanced hunting** and select an existing query or create a new query. When you use a new query, run the query to identify errors and understand possible results. If you started from the custom detections list by selecting **+ Create detection rule**, you can write or paste your query directly in the rule wizard.

Important

To prevent the service from returning too many alerts, each rule can generate only 150 alerts each time it runs. Before creating a rule, tweak your query to avoid alerting for normal, day-to-day activity.

#### Required columns in the query results

To create a custom detection rule by using Defender data, we recommend that the query returns the following columns:

1. `Timestamp` or `TimeGenerated` - This column sets the timestamp for generated alerts. If these columns aren't projected from the KQL, the first and last event time for the generated alert is set according to the lookback window of the detection.
2. **For Microsoft Defender for Endpoint tables**, include `DeviceId` and `ReportId`columns to ensure that:
    - Alerts are tagged with the correct device group scope.
    - Process tree view is built successfully.
3. **For all other Defender tables**, project `Timestamp` and `ReportId`from the same event to ensure Defender identifies the original event that triggered the alert so that:
    - Alerts are tagged with the correct entity scope (only relevant for organizations that use Defender XDR scopes)
    - Alert timeline view is fully enriched with relevant data.
4. To map an impacted asset automatically in the wizard, project one of the following columns that contain a strong identifier for an impacted asset:
    - Device:
        - `DeviceId`
        - `DeviceName`
        - `RemoteDeviceName`
    - Mailbox:
        - `RecipientEmailAddress`
        - `SenderFromAddress` (envelope sender or Return-Path address)
        - `SenderMailFromAddress` (sender address displayed by email client)
        - `SenderObjectId`
        - `RecipientObjectId`
    - User:
        - `AccountObjectId`
        - `AccountSid`
        - `AccountUpn`
        - `InitiatingProcessAccountSid`
        - `InitiatingProcessAccountUpn`

Simple queries, such as those that don't use the `project` or `summarize` operator to customize or aggregate results, typically return these recommended columns.

There are various ways to ensure more complex queries return these columns. For example, if you prefer to aggregate and count by entity under a column such as `AccountObjectId`, you can still return `Timestamp` and `ReportId` by getting them from the most recent event involving each unique `AccountObjectId`.

Important

Avoid filtering custom detections by using the `Timestamp` or `TimeGenerated` column. The service prefilters data for custom detections based on the detection lookback. Filter the results by `Timestamp` or `TimeGenerated` columns only if you want to add additional filtering to ensure a specific sunset of the lookback window is evaluated.

The following sample query shows how to return the recommended columns in a more complex query. It counts the number of unique devices (`DeviceId`) with antivirus detections and finds only devices with more than five detections. To return the latest `Timestamp` and the corresponding `ReportId`, it uses the `summarize` operator with the `arg_max` function. This query references a single table and uses only supported operators, which also makes it compatible with Continuous (NRT) frequency.

```kusto
DeviceEvents
| where ingestion_time() > ago(1d)
| where ActionType == "AntivirusDetection"
| summarize (Timestamp, ReportId)=arg_max(Timestamp, ReportId), count() by DeviceId
| where count_ > 5
```

Tip

For better query performance, set a time filter that matches your intended run frequency for the rule. Since the least frequent run is *every 24 hours*, filtering for the past day covers all new data.

#### Custom column for Microsoft Sentinel scoping

If you configured [Microsoft Sentinel scoping](/en-us/azure/sentinel/scoping), the `SentinelScope_CF` custom field is available for use in queries and detection rules to reference scope in your analytics.

When you create custom detections and analytics rules, you must project the `SentinelScope_CF` column in your queries to make the triggered alerts visible to scoped analysts. If you don't project this column, alerts are unscoped and hidden from scoped users.

### 2. Create new rule and provide alert details

In the query editor, select **Create detection rule**. In the wizard, configure **General** and **Alert settings** with the following rule and alert details:

- **Detection name** - Name of the detection rule; make it unique.
- **Frequency** - Interval for running the query and taking action. For more information, see Rule frequency.
- **Lookback** - The time period covered by the query when the custom detection targets data from Microsoft Sentinel only. For more information, see Lookback.
- **Alert title** - Title displayed with alerts triggered by the rule; make it unique and use plaintext. Strings are sanitized for security purposes, so HTML, Markdown, and other code don't work. Any URLs included in the title should follow the [percent-encoding format](https://en.m.wikipedia.org/wiki/Percent-encoding) for them to display properly.
- **Severity** - Potential risk of the component or activity identified by the rule.
- **Category** - Threat component or activity identified by the rule.
- **Tactic** - MITRE ATT&CK tactic identified by the rule as documented in the [MITRE ATT&CK framework](https://attack.mitre.org/).
- **Techniques** - One or more attack techniques identified by the rule as documented in the MITRE ATT&CK framework.
- **Sub-techniques** - One or more attack sub-techniques identified by the rule as documented in the MITRE ATT&CK framework.
- **Threat analytics report** - Link the generated alert to an existing threat analytics report so that it appears in the [Related incidents](threat-analytics#set-up-custom-detections-and-link-them-to-threat-analytics-reports) tab in threat analytics.
- **Description** - More information about the component or activity identified by the rule. Strings are sanitized for security purposes, so HTML, Markdown, and other code don't work. Any URLs included in the description should follow the percent-encoding format for them to display properly.
- **Recommended actions** - Additional actions that responders might take in response to an alert.

#### Rule frequency

When you save a new rule, it runs and checks for matches from the past 30 days of data. The rule then runs again at fixed intervals, applying a lookback period based on the frequency you choose:

- **Every 24 hours**
- **Every 12 hours**
- **Every 3 hours**
- **Every hour**
- **Continuous (NRT)** - Runs continuously, checking data from events as they're collected and processed in near real-time (NRT). For more information, see [Continuous (NRT) frequency](custom-detection-rules#continuous-nrt-frequency).
- **Custom** - Runs according to the frequency you selected. This option is available if the rule is based only on data that is ingested to Microsoft Sentinel. For more information, see Custom frequency for Microsoft Sentinel data.

Tip

Match the time filters in your query with the lookback period. Results outside of the lookback period are ignored.

When you edit a rule, the next run time scheduled according to the frequency you set applies the changes. The rule frequency is based on the event timestamp and not the ingestion time. Small delays might occur in specific runs, so the configured frequency isn't 100% accurate.

##### Continuous (NRT) frequency

Setting a custom detection to run in Continuous (NRT) frequency increases your organization's ability to identify threats faster. Using the Continuous (NRT) frequency has minimal to no impact on your resource usage. Consider using it for any qualified custom detection rule in your organization.

From the custom detection rules page, you can migrate custom detections rules that fit the Continuous (NRT) frequency by selecting **Migrate now**:

[![Screenshot of the Migrate now button in advanced hunting.](media/custom-detection-rules/custom-detection-migrate-now.png)](media/custom-detection-rules/custom-detection-migrate-now.png#lightbox)

When you select **Migrate now**, you see a list of all compatible rules according to their KQL query. You can choose to migrate all or selected rules only:

[![Screenshot of the continuous frequency compatible queries in advanced hunting.](media/custom-detection-rules/custom-detection-compatible-queries.png)](media/custom-detection-rules/custom-detection-compatible-queries.png#lightbox)

When you select **Save**, the selected rules' frequency is updated to Continuous (NRT) frequency.

###### Queries you can run continuously

You can run a query continuously as long as:

- The query references one table only.
- The query uses an operator from the list of **[Supported KQL features](/en-us/azure/azure-monitor/essentials/data-collection-transformations-structure#supported-kql-features)**. For the `matches regex` operator, regular expressions must be encoded as string literals and follow the string quoting rules. For example, the regular expression `\A` is represented in KQL as `"\\A"`. The extra backslash indicates that the other backslash is part of the regular expression `\A`.
- The query doesn't use joins, unions, or the `externaldata` operator.
- The query doesn't include any comments line or information.

###### Tables that support Continuous (NRT) frequency

Near real-time detections support the following tables:

| Microsoft Defender XDR | Microsoft Sentinel |
| --- | --- |
| - `AlertEvidence`<br>- `CloudAppEvents`<br>- `DeviceEvents`<br>- `DeviceFileCertificateInfo`<br>- `DeviceFileEvents`<br>- `DeviceImageLoadEvents`<br>- `DeviceLogonEvents`<br>- `DeviceNetworkEvents`<br>- `DeviceNetworkInfo`<br>- `DeviceInfo`<br>- `DeviceProcessEvents`<br>- `DeviceRegistryEvents`<br>- `EmailAttachmentInfo`<br>- `EmailEvents` (except `LatestDeliveryLocation` and `LatestDeliveryAction` columns)<br>- `EmailPostDeliveryEvents`<br>- `EmailUrlInfo`<br>- `IdentityDirectoryEvents`<br>- `IdentityLogonEvents`<br>- `IdentityQueryEvents`<br>- `UrlClickEvents` | - `ABAPAuditLog_C`<br>- `ABAPChangeDocsLog_CL`<br>- `AuditLogs`<br>- `AWSCloudTrail`<br>- `AWSGuardDuty`<br>- `AzureActivity`<br>- `CommonSecurityLog`<br>- `GCPAuditLogs`<br>- `MicrosoftGraphActivityLogs`<br>- `OfficeActivity`<br>- `Okta_CL`<br>- `OktaV2_CL`<br>- `ProofpointPOD`<br>- `ProofPointTAPClicksPermitted_CL`<br>- `ProofPointTAPMessagesDelivered_CL`<br>- `SecurityAlert`<br>- `SecurityEvent`<br>- `SigninLogs` |

Note

Only generally available columns support **Continuous (NRT)** frequency.

###### Custom frequency for Microsoft Sentinel data

Microsoft Sentinel customers who onboard to Microsoft Defender can select **Custom** frequency when the rule is based only on data that Microsoft Sentinel ingests.

When you select this frequency option, the **Run query every input** component appears. Type the desired frequency for the rule and use the dropdown to select the units: minutes, hours, or days. The supported range is any value from 5 minutes to 14 days.

[![Screenshot that shows the Custom frequency option in the Custom detections setup guide.](media/custom-detection-rules/ah-custom-frequency.png)](media/custom-detection-rules/ah-custom-frequency.png#lightbox)

Important

When you select a custom frequency, Defender fetches your data from Microsoft Sentinel. This condition means that:

1. You must have data available in Microsoft Sentinel.
2. Defender data doesn't support scoping, since Microsoft Sentinel doesn't support scoping.

#### Lookback

The lookback period of your custom detections can range from five minutes to 30 days, depending on the target data and frequency of your query.

If your custom detections include Defender XDR data, a fixed lookback period is applied depending on the rule frequency that you choose:

- For detections set to run **every 24 hours**, the lookback period is **30 days**.
- For detections set to run **every 12 hours**, the lookback period is **48 hours**.
- For detections set to run **every three hours**, the lookback period is **12 hours**.
- For detections set to run **hourly**, the lookback period is **four hours**.

If your custom detections target Microsoft Sentinel data only, you can customize the lookback period depending on the rule frequency that you set:

- For detections set to run in frequencies **higher (more frequent) than one hour**, the lookback period is limited to **less than 48 hours**.
- For detections set to run in frequencies **higher than one day**, the lookback can be set **up to 14 days**.
- For detections set to run in frequencies of **one day or less**, the lookback can be set **up to 30 days**.

Important

Custom detections evaluate `ingestion_time()` to account for ingestion delays. Because custom detections evaluate `ingestion_time()` instead of event timestamps, events with `Timestamp` or `TimeGenerated` values older than the configured lookback period might still be included in the rule evaluation.

When the lookback period is longer than the frequency, duplicate events might occur. However, custom detections group and deduplicate them automatically to reduce alert noise and fatigue.

### 3. Define alert enrichment details

In **Alert settings**, you can enrich alerts by providing and defining more details. When you enrich alerts, you can:

- Create a dynamic alert title and description
- Add custom details to display in the alert side panel
- Link entities

#### Create a dynamic alert title and description

You can dynamically craft your alert’s title and description by using the results of your query to make them accurate and indicative. This feature can boost SOC analysts’ efficiency when triaging alerts and incidents, and when trying to quickly understand the essence of an alert.

To dynamically configure the alert’s title or description, integrate them into the **Alert details** section by using the free text names of columns that are available in your query results and surrounding them with double curly brackets.

For example: `User {{AccountName}} unexpectedly signed in from {{Location}}`

Note

You can reference up to three columns in each field.

[![Screenshot that shows the dynamic alert title and description fields in the Custom detections wizard.](media/custom-detection-rules/ah-dynamic-alert.png)](media/custom-detection-rules/ah-dynamic-alert.png#lightbox)

To help you decide on the exact column names you want to reference, select **Explore query and results**. This selection opens the Advanced hunting context pane on top of the rule creation wizard, where you can examine your query logic and its results.

#### Add custom details

You can further enhance your SOC analysts’ productivity by showing important details in the alert side panel. You can surface events’ data in alerts that are constructed from those events. This feature gives your SOC analysts immediate event content visibility of their incidents, enabling them to triage, investigate, and draw conclusions faster.

In the **Custom details** section, add key-value pairs corresponding to the details you want to surface:

- In the **Key** field, enter a name of your choosing that appears as the field name in alerts.
- In the **Parameter** field, choose the event parameter you wish to surface in the alerts from the dropdown list. This list is populated by values corresponding to the column names that your KQL query outputs.

[![Screenshot that shows the Custom details option in the Custom detections wizard.](media/custom-detection-rules/ah-custom-details.png)](media/custom-detection-rules/ah-custom-details.png#lightbox)

The following screenshot shows how the custom details surface in the alert side panel:

[![Screenshot that shows the custom details as they appear in the alert side panel of the Defender portal.](media/custom-detection-rules/ah-custom-details-panel.png)](media/custom-detection-rules/ah-custom-details-panel.png#lightbox)

Important

Custom details have the following limitations:

1. Each rule is limited to up to 20 key-value pairs of custom details.
2. The combined size limit for all custom details and their values in a single alert is 4 KB. If the custom details array exceeds this limit, the whole custom details array is dropped from the alert.

#### Link entities

Note

Mapping up to four identifiers per entity, adding the same entity type more than once, and the newly supported identifiers are in preview.

Identify the columns in your query results where you expect to find the main affected or impacted entity. For example, a query might return sender (`SenderFromAddress` or `SenderMailFromAddress`) and recipient (`RecipientEmailAddress`) addresses. Identifying which of these columns represent the main impacted entity helps the service aggregate relevant alerts, correlate incidents, and target response actions.

You can add the same entity type more than once and map up to four identifier and column pairs to each entity. For example, map one **Device** entity to `DeviceName` and another **Device** entity to `RemoteDeviceName`, or map several **IP** entities to `IPAddress`, `LocalIP`, and `RemoteIP`. You can't select columns that aren't returned by your query.

##### Expanded entity mapping

Note

Mapping up to four identifiers per entity, adding the same entity type more than once, and the newly supported identifiers are in preview.

You can link a wide range of entity types to your alerts. Linking more entities helps the correlation engine group alerts to the same incidents and to correlate incidents together. If you're a Microsoft Sentinel customer, this also means that you can map any entity from your third-party data sources that are ingested into Microsoft Sentinel.

For Microsoft Defender XDR data, the entities are automatically selected. If the data is from Microsoft Sentinel, you need to select the entities manually.

Note

Identified entities determine how alerts are grouped into incidents. Make sure to carefully review the entities to ensure a high quality of incident correlation. For more information, see [Alert correlation and incident merging in the Microsoft Defender portal](alerts-incidents-correlation).

In the **Alert settings** step, the **Entity mapping** section follows **Alert details** and **Custom details**. It has two parts:

- **Impacted Assets** - Select **Add assets**to add impacted assets that appear in the selected events. You can add the following types of assets:
    - User
    - Device
    - Mailbox
    - Cloud Application
    - Azure resource
    - Amazon Web Services resource
    - Google Cloud Platform resource
- **Related Evidence** - Select **Add entities**to add nonassets that appear in the selected events. The supported entity types are:
    - Process
    - File
    - Registry value
    - IP
    - OAuth Application
    - DNS
    - Security group
    - URL
    - Mail cluster
    - Mail message

Note

You can currently map only assets as impacted entities.

[![Screenshot of Impacted Assets with one Device entity mapped to three identifiers and query result columns.](media/custom-detection-rules/custom-detection-impacted-assets.png)](media/custom-detection-rules/custom-detection-impacted-assets.png#lightbox)

[![Screenshot of Related Evidence with a Process entity mapping and the Add identifier and Add entities controls.](media/custom-detection-rules/custom-detection-related-evidence.png)](media/custom-detection-rules/custom-detection-related-evidence.png#lightbox)

For each entity, use the following steps in either **Impacted Assets** or **Related Evidence**:

1. Choose the entity type under **Entity**.
2. Choose an **Identifier** and the query result **Column** that contains it. Both fields are required.
3. To map more identifiers to the same entity, select **Add identifier**. Each entity supports up to four identifier and column pairs.
4. To remove an identifier row or a whole entity, select the delete (trash) icon next to it.

For example, map a **Registry value** entity by **Key** to `RegistryKey` and by **ValueName** to `RegistryValueName`.

Each entity type has a list of supported identifiers in the **Identifier** dropdown. To better understand an identifier, read its description when you hover over it.

##### Newly supported identifiers (preview)

The following identifiers are available in preview for existing entity types:

| Entity | Newly supported identifiers |
| --- | --- |
| User | `ObjectGuid`, `AadTenantId`, `PUID`, `IsDomainJoined`, `DisplayName` |
| Device | `AzureID`, `OMSAgentID`, `OSFamily`, `OSVersion`, `IsDomainJoined` |
| Cloud Application | `InstanceName`, `SaasId` |
| File | `Directory` |
| Process | `ElevationToken`, `CreationTimeUtc` |
| Registry value | `Value`, `ValueType` |
| Mailbox | `DisplayName`, `Upn`, `ExternalDirectoryObjectId`, `RiskLevel` |
| Mail Cluster | `NetworkMessageIds`, `CountByDeliveryStatus`, `CountByThreatType`, `CountByProtectionStatus`, `MailCount`, `QueryTime`, `IsVolumeAnomaly`, `ClusterSourceIdentifier`, `ClusterSourceType`, `ClusterQueryStartTime`, `ClusterQueryEndTime`, `ClusterGroup` |
| Mail Message | `P1Sender`, `P1SenderDisplayName`, `P1SenderDomain`, `P2SenderDisplayName`, `P2SenderDomain`, `InternetMessageId`, `Threats`, `ReceivedDate`, `BodyFingerprintBin1`, `BodyFingerprintBin2`, `BodyFingerprintBin3`, `BodyFingerprintBin4`, `BodyFingerprintBin5`, `AntispamDirection`, `DeliveryAction`, `DeliveryLocation`, `Language`, `ThreatDetectionMethods` |

The supported identifiers for IP, URL, Azure resource, and Security Group are unchanged; these entity types already support the same identifiers in custom detection rules and Microsoft Sentinel analytics rules.

After selecting the identifier, select a column from the query results that contains the selected identifier. Select **Explore query and results** to open the advanced hunting context panel. This option allows you to explore your query and results to make sure you choose the right column for the selected identifier.

### 4. Incident settings (preview)

Note

Alert grouping for custom detection rules is in preview.

In **Incident settings**, use **Alert grouping** to combine related alerts from the same custom detection rule into a single incident instead of creating one incident per alert. As with alert grouping in Microsoft Sentinel analytics rules, this gives analysts one place to investigate recurring or related activity.

#### Alert grouping (preview)

Configure alert grouping in the custom detection rule wizard:

1. In **Incident settings**, expand **Alert grouping**.
2. Turn on **Group related alerts, triggered by this custom detection rule, into incidents**. The default is **Disabled**. The remaining alert grouping settings are unavailable until you turn it on.
3. Under **Limit the group to alerts created within the selected time frame**, enter a number and choose a unit. This setting is required and defaults to **5 Hours**. Only alerts created within this time frame are grouped together.
4. Under **Group alerts triggered by this custom detection rule into a single incident by**, choose one option:
    - **Grouping alerts into a single incident if all the entities match (recommended).** This option is selected by default.
    - **Grouping all alerts triggered by this rule into a single incident.**
    - **Grouping alerts into a single incident if the selected entity types and details match.** Select the entities and details to match in the **Select entities** and **Select details** dropdowns, which become available when you choose this option.

[![Screenshot of the custom detection wizard with alert grouping enabled, a five-hour time frame, and all entities matching.](media/custom-detection-rules/custom-detection-alert-grouping.png)](media/custom-detection-rules/custom-detection-alert-grouping.png#lightbox)

Alert grouping has the following behavior and limits:

- **Up to 150 alerts per incident.** After an incident reaches this limit, a new incident is created with the same incident details, and additional alerts are grouped into it. This limit is separate from the 150-alert limit per rule run, which limits how many alerts a rule can generate each time it runs.
- **Closed incidents aren't reopened.** Unlike Microsoft Sentinel analytics rules, custom detection rules don't have a **Re-open closed matching incidents** option. If a new alert matches a closed incident, a new incident is created.
- **Defender correlation still applies.** Alert grouping doesn't prevent Defender from linking other alerts or merging existing incidents.

Note

Microsoft Defender correlation activities can link other alerts or merge existing incidents to the generated incident, regardless of the alert grouping settings defined in the custom detection rule.

### 5. Specify actions

In **Automated actions**, if your custom detection rule uses Defender data, it can automatically take actions on devices, files, users, or emails that the query returns.

[![Screenshot that shows actions for custom detections in the Microsoft Defender portal.](media/custom-detection-rules/ah-custom-actions.png)](media/custom-detection-rules/ah-custom-actions.png#lightbox)

#### Actions on devices

Apply these actions to devices in the `DeviceId` column of the query results:

- **Isolate device** - Uses Microsoft Defender for Endpoint to apply full network isolation, preventing the device from connecting to any application or service. For more information, see [Microsoft Defender for Endpoint machine isolation](/en-us/windows/security/threat-protection/microsoft-defender-atp/respond-machine-alerts#isolate-devices-from-the-network).
- **Collect investigation package** - Collects device information in a ZIP file. For more information, see [Collect investigation package from devices](/en-us/windows/security/threat-protection/microsoft-defender-atp/respond-machine-alerts#collect-investigation-package-from-devices).
- **Run antivirus scan** - Performs a full Microsoft Defender Antivirus scan on the device.
- **Initiate investigation** - Initiates an [automated investigation](m365d-autoir) on the device.
- **Restrict app execution** - Sets restrictions on device to allow only files that are signed with a Microsoft-issued certificate to run. For more information, see [App restrictions in Microsoft Defender for Endpoint](/en-us/defender-endpoint/respond-machine-alerts#restrict-app-execution).

#### Actions on files

- When selected, the **Allow/Block** action can be applied to the file. Blocking files is only allowed if you have *Remediate* permissions for files and if the query results identify a file ID, such as a SHA-1 hash. Once a file is blocked, other instances of the same file on all devices are also blocked. You can control which device group the blocking applies to, but not specific devices.
- When selected, the **Quarantine file** action can be applied to files in the `SHA1`, `InitiatingProcessSHA1`, `SHA256`, or `InitiatingProcessSHA256` column of the query results. This action deletes the file from its current location and places a copy in quarantine.

#### Actions on users

- When selected, the **Mark user as compromised** action takes on users in the `AccountObjectId`, `InitiatingProcessAccountObjectId`, or `RecipientObjectId` column of the query results. This action sets the user's risk level to "high" in Microsoft Entra ID, triggering corresponding [identity protection policies](/en-us/azure/active-directory/identity-protection/overview-identity-protection).
- Select **Disable user** to temporarily prevent a user from signing in.
- Select **Reset user authentication** to prompt the user to either change their password on their next sign-in session (for on-premises identities) or require them to sign in again (for Microsoft Entra identities).
- Both the **Disable user** and **Reset user authentication** options require the user security identifier (SID), which are in the columns `AccountSid`, `InitiatingProcessAccountSid`, `RequestAccountSid`, and `OnPremSid`.
- For Microsoft Entra identities, `AccountObjectId` parameter is needed for all actions.
- Custom detection rules can apply governance actions to supported SaaS identities returned by queries that use the `CloudAppEvents` table. This capability is in preview.
- To apply SaaS actions, the query results must include `AccountObjectId`, `InstanceId`, `ApplicationId`, and `AppInstanceId`, along with other required columns such as `Timestamp`. You can use joins as long as the required columns are present in the query results.

Important

If the selected governance action or SaaS service isn't supported, the rule doesn't take an action.

The following table lists the supported governance actions for SaaS identities:

| SaaS service | Supported governance actions |
| --- | --- |
| Box | **Disable user** |
| Google Workspace | **Disable user**, **Force password reset** |
| Salesforce | **Disable user** |

For more information on user actions, see [Remediation actions in Microsoft Defender for Identity](/en-us/defender-for-identity/remediation-actions) and [Remediation actions in Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/governance-actions).

#### Actions on emails

- If the custom detection yields email messages, you can select **Move to mailbox folder** to move the email to a selected folder (any of **Junk**, **Inbox**, or **Deleted items** folders). Specifically, you can move email results from quarantined items (for instance, in the case of false positives) by selecting the **Inbox** option.

    [![Screenshot of the Inbox option under custom detections in the Microsoft Defender portal.](media/custom-detection-rules/advanced-hunting-custom-quarantine-results.png)](media/custom-detection-rules/advanced-hunting-custom-quarantine-results.png#lightbox)
- Alternatively, you can select **Delete email** and then choose to either move the emails to Deleted Items (**Soft delete**) or delete the selected emails permanently (**Hard delete**).

The columns `NetworkMessageId` and `RecipientEmailAddress` must be present in the output results of the query to apply actions to email messages.

### 6. Set the rule scope

In **Scope**, specify which devices the rule covers. The scope influences rules that check devices and doesn't affect rules that check only mailboxes and user accounts or identities.

When setting the scope, select:

- All devices
- Specific device groups

The rule queries data only from devices in the scope. It takes actions only on those devices.

Note

Users can create or edit a custom detection rule only if they have the corresponding permissions for the devices included in the scope of the rule. For example, admins can only create or edit rules that are scoped to all device groups if they have permissions for all device groups.

### 7. Review and turn on the rule

In **Review and create**, review the rule, then select **Create** to save it. The custom detection rule runs immediately. It runs again based on the configured frequency to check for matches, generate alerts, and take response actions.

Important

Regularly review custom detections for efficiency and effectiveness. For guidance on how to optimize your queries, see **[Advanced hunting query best practices](advanced-hunting-best-practices)**. To make sure you're creating detections that trigger true alerts, take time to review your existing custom detections by following the steps in **[Manage existing custom detection rules](custom-detection-manage)**.

You maintain control over the broadness or specificity of your custom detections. Any false alerts generated by custom detections might indicate a need to modify certain parameters of the rules.

#### How custom detections handle duplicate alerts

An important consideration when creating and reviewing custom detection rules is alert noise and fatigue. Custom detections group and deduplicate events into a single alert. If a custom detection rule runs twice on an event that contains the same entities, custom details, and dynamic details, it creates one alert for both events. If the detection rule recognizes that the events are identical, it logs one of the events on the created alert and takes care of the duplicates. Duplicates can occur when the lookback period is longer than the frequency. If the events are different, the custom detection logs both events on the alert.

This event-to-alert deduplication is separate from alert-to-incident grouping.