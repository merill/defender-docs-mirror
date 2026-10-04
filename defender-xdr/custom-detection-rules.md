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
- msecd-doc-authoring-1030
- sfi-ga-nochange
- cx-ti
- cx-ah
- sfi-image-nochange
ms.topic: how-to
ms.date: 2026-10-04T00:00:00.0000000Z
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

Regardless of which entry point you use, follow these steps to configure the rule:

1. Prepare the query
2. Create new rule and provide alert details
3. Define alert enrichment details
4. Specify actions
5. Set the rule scope
6. Review and turn on the rule

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
    - Account:
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

For better query performance, set a time filter that matches the configured lookback period for the rule.

#### Custom column for Microsoft Sentinel scoping

If you configured [Microsoft Sentinel scoping](/en-us/azure/sentinel/scoping), the `SentinelScope_CF` custom field is available for use in queries and detection rules to reference scope in your analytics.

When you create custom detections and analytics rules, you must project the `SentinelScope_CF` column in your queries to make the triggered alerts visible to scoped analysts. If you don't project this column, alerts are unscoped and hidden from scoped users.

### 2. Create new rule and provide alert details

In the query editor, select **Create detection rule** and specify the following alert details:

- **Detection name** - Name of the detection rule; make it unique.
- **Frequency** - Interval for running the query and taking action. Custom frequency for all supported data sources is in public preview and supports intervals from 5 minutes to 14 days. For more information, see Rule frequency.
- **Lookback** - Amount of historical data that the query evaluates each time it runs. Configurable lookback for all supported data sources is in public preview and supports periods from 5 minutes to 30 days. For more information, see Custom frequency and lookback.
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

When you save a new rule, it runs and checks for matches from the past 30 days of data. The rule then runs again at the configured interval:

- **Every 24 hours**
- **Every 12 hours**
- **Every 3 hours**
- **Every hour**
- **Continuous (NRT)** - Runs continuously, checking data from events as they're collected and processed in near real-time (NRT). For more information, see [Continuous (NRT) frequency](custom-detection-rules#continuous-nrt-frequency).
- **Custom (public preview)** - Runs at an interval that you configure, from 5 minutes to 14 days. For more information, see Custom frequency and lookback.

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

##### Custom frequency and lookback (public preview)

Flexible frequency and lookback for custom detections are in public preview. You can configure these settings independently for rules that use any supported data source, including Microsoft Defender XDR and Microsoft Sentinel data.

Use these settings to:

- Run a rule as frequently as every 5 minutes.
- Set the frequency from 5 minutes to 14 days.
- Set the lookback from 5 minutes to 30 days.
- Use a longer lookback while keeping the frequency needed for time-sensitive detections.

To configure the schedule, select **Custom** frequency. In **Run query every**, enter the frequency, and then select minutes, hours, or days. In **Lookup data from the last**, configure the lookback period.

[![Screenshot that shows the Custom frequency option in the custom detection rule wizard.](media/custom-detection-rules/ah-custom-frequency.png)](media/custom-detection-rules/ah-custom-frequency.png#lightbox)

The lookback must be at least as long as the frequency to avoid coverage gaps. The frequency also determines the maximum supported lookback:

| Frequency | Supported lookback |
| --- | --- |
| 5 minutes to less than 1 hour | At least the selected frequency and less than 48 hours |
| 1 hour to less than 1 day | At least the selected frequency and up to 14 days |
| 1 day to 14 days | At least the selected frequency and up to 30 days |

Rules that run more frequently have shorter maximum lookback periods to maintain performance.

Important

Custom detections evaluate `ingestion_time()` to account for ingestion delays. Because custom detections evaluate `ingestion_time()` instead of event timestamps, events with `Timestamp` or `TimeGenerated` values older than the configured lookback period might still be included in the rule evaluation.

When the lookback period is longer than the frequency, duplicate events might occur. However, custom detections group and deduplicate them automatically to reduce alert noise and fatigue.

### 3. Define alert enrichment details

You can enrich alerts by providing and defining more details. When you enrich alerts, you can:

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

Identify the columns in your query results where you expect to find the main affected or impacted entity. For example, a query might return sender (`SenderFromAddress` or `SenderMailFromAddress`) and recipient (`RecipientEmailAddress`) addresses. Identifying which of these columns represent the main impacted entity helps the service aggregate relevant alerts, correlate incidents, and target response actions.

You can select only one column for each entity type (mailbox, user, or device). You can't select columns that aren't returned by your query.

##### Expanded entity mapping

You can link a wide range of entity types to your alerts. Linking more entities helps the correlation engine group alerts to the same incidents and to correlate incidents together. If you're a Microsoft Sentinel customer, this also means that you can map any entity from your third-party data sources that are ingested into Microsoft Sentinel.

For Microsoft Defender XDR data, the entities are automatically selected. If the data is from Microsoft Sentinel, you need to select the entities manually.

Note

Entities impact how alerts are grouped into incidents. Make sure to carefully review the entities to ensure high quality of incidents. For more information, see [Alert correlation and incident merging in the Microsoft Defender portal](alerts-incidents-correlation).

The expanded **Entity mapping** section has two sections where you can select entities:

- **Impacted assets**– Add impacted assets that appear in the selected events. You can add the following types of assets:
    - Account
    - Device
    - Mailbox
    - Cloud application
    - Azure resource
    - Amazon Web Services resource
    - Google Cloud Platform resource
- **Related evidence**– Add nonassets that appear in the selected events. The supported entity types are:
    - Process
    - File
    - Registry value
    - IP
    - OAuth application
    - DNS
    - Security group
    - URL
    - Mail cluster
    - Mail message

Note

You can currently map only assets as impacted entities.

[![Screenshot that shows the entity mapping options in the Custom detections wizard.](media/custom-detection-rules/ah-link-entities.png)](media/custom-detection-rules/ah-link-entities.png#lightbox)

After you select an entity type, select an identifier type that exists in the selected query results so you can use it to identify this entity. Each entity type has a list of supported identifiers, as shown in the relevant dropdown menu. To better understand each identifier, read the description displayed when you hover over it.

After selecting the identifier, select a column from the query results that contains the selected identifier. Select **Explore query and results** to open the advanced hunting context panel. This option allows you to explore your query and results to make sure you choose the right column for the selected identifier.

### 4. Specify actions

If your custom detection rule uses Defender data, it can automatically take actions on devices, files, users, or emails that the query returns.

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

### 5. Set the rule scope

Set the scope to specify which devices the rule covers. The scope influences rules that check devices and doesn't affect rules that check only mailboxes and user accounts or identities.

When setting the scope, select:

- All devices
- Specific device groups

The rule queries data only from devices in the scope. It takes actions only on those devices.

Note

Users can create or edit a custom detection rule only if they have the corresponding permissions for the devices included in the scope of the rule. For example, admins can only create or edit rules that are scoped to all device groups if they have permissions for all device groups.

### 6. Review and turn on the rule

After reviewing the rule, select **Create** to save it. The custom detection rule runs immediately. It runs again based on the configured frequency to check for matches, generate alerts, and take response actions.

Important

Regularly review custom detections for efficiency and effectiveness. For guidance on how to optimize your queries, see **[Advanced hunting query best practices](advanced-hunting-best-practices)**. To make sure you're creating detections that trigger true alerts, take time to review your existing custom detections by following the steps in **[Manage existing custom detection rules](custom-detection-manage)**.

You maintain control over the broadness or specificity of your custom detections. Any false alerts generated by custom detections might indicate a need to modify certain parameters of the rules.

#### How custom detections handle duplicate alerts

An important consideration when creating and reviewing custom detection rules is alert noise and fatigue. Custom detections group and deduplicate events into a single alert. If a custom detection rule runs twice on an event that contains the same entities, custom details, and dynamic details, it creates one alert for both events. If the detection rule recognizes that the events are identical, it logs one of the events on the created alert and takes care of the duplicates. Duplicates can occur when the lookback period is longer than the frequency. If the events are different, the custom detection logs both events on the alert.