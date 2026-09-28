---
layout: Conceptual
title: Create and manage custom data collection rules in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/create-custom-data-collection-rules
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to create and manage custom data collection rules in Microsoft Defender for Endpoint to enhance your threat hunting capabilities.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- usx-security
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 98073f10-1060-343f-0c52-487023aef239
document_version_independent_id: 98073f10-1060-343f-0c52-487023aef239
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/create-custom-data-collection-rules.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: create-custom-data-collection-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/create-custom-data-collection-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d7f1a5bc-0a51-2315-f086-ebadcd077229
---

# Create and manage custom data collection rules in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Custom data collection rules let you capture specific endpoint events beyond default telemetry and send them to Microsoft Sentinel for advanced hunting and investigation. This article walks you through creating, editing, monitoring, and deleting these rules in the Microsoft Defender portal.

Tip

Before creating custom collection rules, review [Custom data collection](custom-data-collection) to understand when and why to use this feature.

## Prerequisites

Ensure you have:

| Requirement | Details |
| --- | --- |
| **License** | Microsoft Defender for Endpoint Plan 2 |
| **Microsoft Sentinel workspace** | Connected Microsoft Sentinel workspace (required for custom data storage and querying); currently limited to one Sentinel workspace per tenant for custom data collection |
| **Dynamic tags** | Configured in [Asset Rule Management](/en-us/defender-xdr/configure-asset-rules) and run at least once; manual (static) tags aren't supported |
| **Supported operating systems** | • Windows 10 and 11 (minimum client version 10.8805; Windows 10 requires ESU enrollment)• Windows Server 2019 and later |
| **Cost considerations** | Custom data collection is included with Defender for Endpoint Plan 2; data ingestion into Microsoft Sentinel incurs charges based on your Sentinel billing |

Important

Even if you have a connected Microsoft Sentinel workspace, you must select the workspace when creating custom data collection rules.

### Performance and limits

The following limits and operational characteristics apply to custom data collection rules:

- Each rule can capture up to **75,000 events per device per 24-hour rolling window**
- When a device reaches the threshold, telemetry for that rule stops until the window resets
- Rule deployment typically takes 20 minutes to 1 hour
- Custom collection operates alongside default configuration without interference

### Security considerations

Consider these security implications before creating rules:

| Consideration | Details | Recommendation |
| --- | --- | --- |
| **Rule scope impact** | Overly broad rules generate large data volumes, increasing costs and making analysis difficult | Balance specificity with coverage by iterating and refining rules based on initial results |
| **Too narrow rules** | May miss important security events | Test with pilot groups and monitor for gaps in coverage |
| **Performance considerations** | Each device has a 75,000 event per rule per day limit | Use multiple focused rules rather than one overly broad rule; target rules carefully to devices where monitoring is essential |
| **Testing strategy** | Deploying rules without testing can lead to unexpected costs or missed events | 1. Start with a small pilot group (5-10 devices)2. Monitor data volume and event quality for 24-48 hours3. Refine conditions based on results4. Gradually expand to larger device groups5. Review cost and performance metrics regularly |

### Create rules

1. In the Microsoft Defender portal, navigate to **Settings** &gt; **Endpoints** &gt; **Rules** &gt; **Custom Data Collection**.
2. To onboard your Microsoft Sentinel workspace, on the top right, select the Microsoft Sentinel workspace name.

    [![Screenshot of selecting a Microsoft Sentinel workspace.](media/create-custom-data-collection-rules/select-workspace.png)](media/create-custom-data-collection-rules/select-workspace.png#lightbox)
3. In the **Workspace scope** page, select your workspace.

    ![Screenshot of selecting a Microsoft Sentinel workspace scope.](media/create-custom-data-collection-rules/select-workspace-scope.png)

    Note

    You need to select the workspace at this stage, even if you already have a connected Microsoft Sentinel workspace.
4. Select **Create rule**. In the **General Information** section, type a rule name and description, and select **Next**.

    [![Screenshot of creating a rule: General Information page.](media/create-custom-data-collection-rules/create-custom-data-collection-rule-general.png)](media/create-custom-data-collection-rules/create-custom-data-collection-rule-general.png#lightbox)
5. In the **Create rule** section:

    1. Select which table you want to collect data from. For more information, see [Supported event tables](custom-data-collection#supported-event-tables).
    2. Select the action for which you want to collect data.
    3. Add rule conditions to filter the data even further. You can add multiple conditions to refine the data collection. Rule conditions are based on the selected table. For more information, see the respective table link under [Supported event tables](custom-data-collection#supported-event-tables).

    [![Screenshot of creating a rule: Create rule page.](media/create-custom-data-collection-rules/create-custom-data-collection-rule.png)](media/create-custom-data-collection-rules/create-custom-data-collection-rule.png#lightbox)
6. Select **Next**.
7. In the **Define rule scope** section, select whether you want to collect data from all applicable client devices or from specific devices that include dynamic tags. For more information, see [Create dynamic rules for devices in asset rule management](/en-us/defender-xdr/configure-asset-rules).

    [![Screenshot of creating a rule: Define scope page.](media/create-custom-data-collection-rules/create-custom-data-collection-rule-define-scope.png)](media/create-custom-data-collection-rules/create-custom-data-collection-rule-define-scope.png#lightbox)

    Note

    Custom data collection only supports dynamic tags.
8. In the **Review and finish** section, review your rule settings, and select **Submit**.

    [![Screenshot of creating a rule: Review and finish page.](media/create-custom-data-collection-rules/create-custom-data-collection-rule-review.png)](media/create-custom-data-collection-rules/create-custom-data-collection-rule-review.png#lightbox)

It can take up to an hour for the rule to be deployed to the targeted devices.

## Monitor and troubleshoot

After you deploy custom data collection rules, check how they perform and fix any issues.

### Verify rule deployment

To check if a rule is collecting data from a specific device, use the following KQL query to search all custom event tables in [advanced hunting](/en-us/defender-xdr/advanced-hunting-overview), the query-based tool in Microsoft Defender for investigating device data, and verify that the rule is generating events:

```kusto
search in (DeviceCustomFileEvents, DeviceCustomScriptEvents, DeviceCustomNetworkEvents, DeviceCustomProcessEvents, DeviceCustomImageLoadEvents) "your_device_id"
| where DeviceId == "your_device_id"
| summarize EventCount = count() by RuleName, RuleLastModificationTime, $table
| order by RuleLastModificationTime desc
```

### Common issues and solutions

The following table lists common issues with custom data collection rules and how to resolve them:

| Issue | Possible cause | Solution |
| --- | --- | --- |
| No events collected | Rule not yet deployed | Wait up to 1 hour for deployment; check rule status in the portal |
| No events collected | Device not targeted correctly | Verify dynamic tag is applied to device and tag rule has run in Asset Rule Management |
| Events stopped collecting | 75,000 event limit reached | Review rule conditions to make them more specific; wait for 24-hour window to reset |
| Unexpected devices collecting data | Dynamic tag applied broadly | Review tag rules in Asset Rule Management; refine targeting criteria |
| Rule not visible on device | Device doesn't meet OS requirements | Check client version and OS version meet minimum requirements (Windows 10/11 version 10.8805+, Windows Server 2019+) |
| Custom collection not initializing | EDR exclusions may prevent collection | Check for EDR exclusions on target paths or processes; device reboots may be required if custom collection isn't initializing |
| Tags not updating | Dynamic tags haven't run recently | Dynamic tags update approximately every hour—check **Last run time** in Asset Rule Management |

### Monitor rule performance

Use the following checks to monitor rule performance:

- **Check event volume**: Query custom event tables to see how many events each rule is collecting
- **Review collection status**: Monitor whether devices are approaching the 75,000 event per rule per day limit
- **Validate targeting**: Ensure rules are deploying to the correct devices based on your dynamic tags

### Collect all events for testing

To collect all events from a specific table (for testing or comprehensive monitoring):

1. Create a rule with the desired table
2. Select all available actions
3. Add a condition that's always true, such as:
    - For network events: `RemotePort not equals 0`
    - For file events: `FileName not equals ""`
    - For process events: `ProcessCommandLine not equals ""`
4. Target to a small pilot group first due to high data volume

Warning

Collecting all events generates very large data volumes and can quickly reach the 75,000 event per device limit. Use comprehensive collection only for testing or specific investigative purposes on a small number of devices.

## Manage rules

### Edit a rule

To edit an existing custom data collection rule:

1. Navigate to **Settings** &gt; **Endpoints** &gt; **Rules** &gt; **Custom Data Collection**
2. Select the rule you want to edit
3. Select **Edit**
4. Modify rule settings as needed (name, description, table, actions, conditions, or device targeting)
5. Select **Submit**

Changes take effect on targeted devices within 20 minutes to 1 hour.

### Enable or disable a rule

To enable or disable a custom data collection rule:

1. In **Custom Data Collection**, select the rule
2. Select or clear the **Enable** checkbox under the rule description

When you disable a rule, data collection stops on all targeted devices within the next agent check-in (typically within minutes to 1 hour).

### Delete a rule

Important

Deleting a rule is permanent and cannot be undone. Historical data in Microsoft Sentinel remains available, but new collection stops immediately.

Use the following steps to permanently delete a custom data collection rule:

1. In **Custom Data Collection**, select the rule
2. Select **Delete**
3. Confirm deletion