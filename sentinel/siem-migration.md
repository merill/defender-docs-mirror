---
layout: Conceptual
title: Use the SIEM Migration Experience - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/siem-migration
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
description: Migrate security monitoring use cases from other Security Information and Event Management (SIEM) systems to Microsoft Sentinel.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: yohasson
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c50290de-2627-0ba4-a6c5-b7fcaeb8b70b
document_version_independent_id: bfbf3012-9a22-c49c-7ae4-6a8cf3e0ed38
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/siem-migration.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/siem-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/siem-migration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 0d3b0286-a496-07c8-89b6-6074fc648c78
---

# Use the SIEM Migration Experience - Microsoft Sentinel | Microsoft Learn

The SIEM migration tool analyzes Splunk and QRadar detections, including custom detections, and recommends best-fit Microsoft Sentinel detections and Defender XDR native detections. It also provides recommendations for data connectors, both Microsoft and third-party connectors available in Content Hub to enable the recommended detections. You can track migration by assigning the right status to each recommendation card.

The SIEM Migration experience includes the following features:

- The experience focuses on migrating Splunk and QRadar security monitoring to Microsoft Sentinel and mapping out-of-the-box (OOTB) analytics rules wherever possible.
- The experience supports migration of Splunk and QRadar detections to Microsoft Sentinel analytics rules.

## Prerequisites

- [Microsoft Sentinel in Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard#onboard-microsoft-sentinel)
- At least [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) permissions in the Microsoft Sentinel workspace
- [Security Copilot](/en-us/defender-xdr/security-copilot-in-microsoft-365-defender) enabled in your tenant with at least a [workspace operator role](/en-us/copilot/security/authentication#assign-security-copilot-access) assigned

Note

The SIEM Migration tool is powered by [Security Copilot](https://securitycopilot.microsoft.com/), so you need Security Copilot enabled in your tenant to use the SIEM Migration tool. However, the SIEM Migration tool doesn't consume SCUs or generate any SCU‑based charges no matter how you configure Security Copilot. You can optimize your Security Copilot setup based on your preferences for access and cost management, and workflow remains completely SCU‑free. Any SCU usage would apply only to other Security Copilot features you intentionally use.

![Screenshot of the Security Copilot usage monitoring settings.](media/siem-migration/monitor-usage.png)

## Export detection rules from your current SIEM

Export your existing detection rules from your current SIEM so the SIEM migration experience can analyze them.

# [Splunk](#tab/splunk)
In the **Search and Reporting** app in Splunk, run the following query:

```kusto
| rest splunk_server=local count=0 /servicesNS/-/-/saved/searches | search disabled=0 | search alert_threshold != "" | table title, search, description, cron_schedule, dispatch.earliest_time, alert.severity, alert_comparator, alert_threshold, alert.suppress.period, id, eai:acl.app, actions, action.correlationsearch.annotations, action.correlationsearch.enabled | tojson | table _raw | rename _raw as alertrules | mvcombine delim=", " alertrules | append [ | rest splunk_server=local count=0 /servicesNS/-/-/admin/macros | table title,definition,args,iseval | tojson | table _raw | rename _raw as macros | mvcombine delim=", " macros ] | filldown alertrules |tail 1 
```

You need a Splunk admin role to export all Splunk alerts. For more information, see [Splunk role-based user access](https://docs.splunk.com/Documentation/Splunk/9.1.3/Security/Aboutusersandroles).

# [QRadar](#tab/qradar)
Use the QRadar migration data collector script to export your QRadar detection rules and building blocks to a CSV file that the SIEM migration experience can analyze.

Before you start, make sure you have:

- Python 3 installed on the machine where you'll run the script. The latest stable release is recommended.
- A QRadar authorized service token with Admin privileges. For more information, see [Creating authorized service tokens in IBM QRadar](https://www.ibm.com/docs/qradar-common?topic=configuration-creating-authorized-service-token).
- Network access from the script machine to your QRadar console.

1. In the SIEM migration experience, select **QRadar**, then select **Download script**.
2. Save `qradar_collector.py` to the machine where you'll run it.
3. From a terminal, run the script with your QRadar console hostname or IP address:

    ```bash
    python3 qradar_collector.py --host <qradar-host-or-ip>
    ```

    If `python3` isn't recognized, use the Python command for your environment, such as `python`.
4. When prompted, enter your QRadar authorized service token. The token input is hidden. Don't include the token in the command line.
5. When the script finishes, upload the generated `qradar_rules_YYYYMMDDHHMMSS.csv` file in the SIEM migration experience, then select **Next**.

For more information about the QRadar migration data collector script and its parameters, see the [QRadar migration data collector README](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/QRadarMigration).

#### Troubleshoot QRadar exports

If the script fails and you need a workaround, manually export QRadar rules as a CSV file by using [Exporting rules - IBM Documentation](https://go.microsoft.com/fwlink/?linkid=2332524).

When you export manually:

1. Clear any filter values for *Rule or Building Block(BB)* so the export includes both rules and building blocks.
2. Include only the supported fields:

    "Rule name", "Type", "Rule enabled", "Notes", "Action details", "Response details", "Rule response: Event description", "Is rule", "Rule installed", "Rule response: Event name", "Rule: test definition", "Content extension name", "Content category"

Manual exports can produce less accurate migration results than the collector script because the script enriches and normalizes QRadar data for migration analysis.

---

## Start the SIEM migration experience

After exporting the rules, do the following:

1. Go to `security.microsoft.com`.
2. From the **SOC Optimization** tab, select **Set up your new SIEM**.

    ![Screenshot of the Setup your new SIEM option in the top right corner of the SOC Optimization screen.](media/siem-migration/set-up-new-siem.png)
3. Select **Migrate from your current SIEM**:

    ![Screenshot of the Migrate from current SIEM option.](media/siem-migration/migrate.png)
4. Select the SIEM you're migrating from.

    ![Screenshot of the UI asking the user to select the SIEM they're migrating from.](media/siem-migration/select-siem.png)
5. Upload the configuration data that you exported (see Export detection rules from your current SIEM) and select **Next**.

    The migration tool analyzes the export and identifies the number of data sources and detection rules in the file you provided. Use this information to confirm that you have the right export.

    If the data doesn't look correct, select **Replace file** from the top right corner and upload a new export. When the correct file is uploaded, select **Next**.

    ![Screenshot of the confirmation screen showing the number of data sources and detection rules.](media/siem-migration/confirm-siem.png)
6. Select a workspace, then select **Start Analyzing**.

    ![Screenshot of the UI asking the user to select a workspace.](media/siem-migration/select-workspace.png)

    The migration tool maps the detection rules to Microsoft Sentinel data sources and detection rules. If there are no recommendations in the workspace, recommendations are created. If there are existing recommendations, the SIEM migration tool deletes and replaces them with new ones.

    ![Screenshot of the migration tool getting ready to analyze the rules.](media/siem-migration/getting-ready.png)
7. Refresh the page and select the **SIEM setup analysis status** to view the progress of the analysis:

    ![Screenshot of the SIEM Set-up analysis status showing the progress of the analysis.](media/siem-migration/setup-analysis-status.png)

    The SIEM setup analysis status page doesn't refresh automatically. To see the latest status, close and reopen the page.

    The analysis is complete when all three check marks are green. If the three checkmarks are green but there are no recommendations, it means that no matches were found for your rules.

    ![Screenshot showing all three check marks green indicating analysis is complete.](media/siem-migration/status-complete.png)

    When the SIEM migration analysis completes, the migration tool generates use-case-based recommendations, grouped by Content Hub solutions. You can also download a detailed report of the analysis. The report contains a detailed analysis of recommended migration jobs, including Splunk and QRadar rules that don't have a good match, weren't detected, or aren't applicable.

    [![A screenshot of recommendations generated by the migration tool.](media/siem-migration/recommendations.png)](media/siem-migration/recommendations.png#lightbox)

    Filter *recommendation type* by *SIEM Setup* to see migration recommendations.
8. Select one of the recommendation cards to view the data sources and rules mapped.

    [![A screenshot of a recommendation card.](media/siem-migration/recommendation-card.png)](media/siem-migration/recommendation-card.png#lightbox)

    The SIEM migration tool matches Splunk and QRadar rules to out-of-box Microsoft Sentinel data connectors, out-of-box Microsoft Sentinel detection rules, and Defender XDR native detections. The *connectors* tab shows the data connectors matched to the rules from your SIEM and the status (connected or not disconnected). If the connector you want to use isn't already connected, you can connect from the connector tab. If a connector isn't installed, go to the Microsoft Sentinel Content hub and install the solution that contains the connector you want to use.

    ![Screenshot of Microsoft Sentinel data connectors matched to Splunk or QRadar rules.](media/siem-migration/connectors.png)

    The *detections* tab shows the following information:

    - Recommendations from the SIEM migration tool.
    - The current Splunk or QRadar detection rule from your uploaded file.
    - The product, which indicates whether the matched detection is a Microsoft Sentinel detection rule or a Defender XDR native detection.
    - The status of the detection rule in Microsoft Sentinel. The status can be:
        - *Enabled*: The detection rule is created from the rule template, enabled, and active (from a previous action)
        - *Disabled*: The detection rule is installed from the Content Hub but not enabled in the Microsoft Sentinel workspace
        - *Not in use*: The detection rule was installed from Content Hub and is available as a template to be enabled
        - *Not installed*: The detection rule wasn't installed from the Content Hub
    - The required connectors that need to be configured to bring the logs required for the recommended detection rule. If a required connector isn't available, there's a side panel with a wizard to install it from the Content Hub. If all required connectors are connected, a green check mark appears.

    [![Screenshot of Microsoft Sentinel detection rules matched to Splunk or QRadar rules.](media/siem-migration/detection.png)](media/siem-migration/detection.png#lightbox)

## Enable detection rules

After reviewing the matched results, you can enable the recommended Microsoft Sentinel detection rules or review Defender XDR native detections.

# [Microsoft Sentinel detection rules](#tab/sentinel-detection-rules)
When you select a recommended detection rule, the rule details side panel opens and you can view the rule template details.

[![Screenshot of the rule details side panel.](media/siem-migration/rule-details.png)](media/siem-migration/rule-details.png#lightbox)

- If the associated data connector is installed and configured, select **Enable detection** to enable the detection rule.

    [![Screenshot of the Enable detection button in the rule details side panel.](media/siem-migration/enable-detection.png)](media/siem-migration/enable-detection.png#lightbox)
- Select **More actions** &gt; **Create manually** to open the analytics rules wizard so you can review and edit the rule before enabling it.
- If the rule is already enabled, select **Edit** to open the analytics rules wizard to review and edit the rule.

    ![Screenshot of the More actions button in the rules wizard.](media/siem-migration/more-actions.png)

    The wizard shows the Splunk SPL rule and you can compare it with the Microsoft Sentinel KQL.

    ![Screenshot of the comparison between Splunk SPL rule and Microsoft Sentinel KQL.](media/siem-migration/compare-rules.png)

Tip

Instead of creating rules manually from scratch, consider enabling the rule from the template and then editing the rule as needed.

*Enable detection* is only enabled if the data connector is installed and configured to stream logs.

- You can enable several rules at once by selecting the check boxes next to each rule you want to enable and then selecting **Enable selected detections** at the top of the page.

    [![Screenshot of the list of rules in the detection tab with checkboxes next to them.](media/siem-migration/enable-multiple-rules.png)](media/siem-migration/enable-multiple-rules.png#lightbox)

The SIEM migration tool doesn't explicitly install any connectors or enable detection rules.

# [Defender XDR native detections](#tab/defender-xdr-native-detections)
Defender XDR native detections are built-in detection logic that generate alerts, which are then correlated into incidents. The SIEM migration tool maps Splunk and QRadar rules to these native detections. Matched Defender XDR native detections are in active status. Defender XDR native detections don't require Microsoft Sentinel data connectors to be installed, configured, and connected.

[![Screenshot of the list of matched Defender XDR native detections.](media/siem-migration/defender-detections.png)](media/siem-migration/defender-detections.png#lightbox)

Select a matched Defender XDR rule to view full details. You won't see matching KQL because Defender XDR native detections use built-in detection logic.

[![Screenshot of the details side panel for a Defender XDR native detection.](media/siem-migration/defender-matched-rules.png)](media/siem-migration/defender-matched-rules.png#lightbox)

---

## Limitations

The migration tool maps the rules export to out-of-the-box Microsoft Sentinel data connectors and detection rules.