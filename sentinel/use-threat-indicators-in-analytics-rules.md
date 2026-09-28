---
layout: Conceptual
title: Use Threat Indicators in Analytics Rules - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/use-threat-indicators-in-analytics-rules
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
description: This article explains how to generate alerts and incidents with threat intelligence indicators in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 4dbb4f23-0b58-939a-97d3-70cece6418e2
document_version_independent_id: 0b01fd7e-ad3e-8a90-d7be-086dcf2790f5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/use-threat-indicators-in-analytics-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/use-threat-indicators-in-analytics-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/use-threat-indicators-in-analytics-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0a6385ac-9e03-1dc7-1d95-ad2ed8a99b5c
---

# Use Threat Indicators in Analytics Rules - Microsoft Sentinel | Microsoft Learn

You can use TI map analytics rules in Microsoft Sentinel to detect threats. These rules match your imported threat indicators against events from connected data sources. When a match is found, the rules generate alerts and incidents for your team to review.

## Prerequisites

- Threat indicators. These indicators can be from threat intelligence feeds, threat intelligence platforms, bulk import from a flat file, or manual input.
- Data sources. Events from your data connectors must be flowing to your Microsoft Sentinel workspace.
- An analytics rule of the format `TI map...`. The analytics rule must use this format so that it can map your threat indicators to the events you ingested.

## Configure a rule to generate security alerts

The following example shows how to enable and configure a rule that generates security alerts from your imported threat indicators. This example uses the rule template called **TI map IP entity to AzureActivity**. This rule matches any IP address threat indicator with your Azure Activity events. When a match is found, it generates an alert and a related incident for your security operations team to investigate.

This particular analytics rule requires the Azure Activity data connector (to import your Azure subscription-level events). It also requires one or both of the Threat Intelligence data connectors (to import threat indicators). The **TI map IP entity to AzureActivity** rule also triggers from imported indicators or manually created ones.

1. In the [Azure portal](https://portal.azure.com/), go to **Microsoft Sentinel**.
2. Choose the workspace to which you imported threat indicators by using the Threat Intelligence data connectors and Azure Activity data by using the Azure Activity data connector.
3. On the Microsoft Sentinel menu, under the **Configuration** section, select **Analytics**.
4. Select the **Rule templates** tab to see the list of available analytics rule templates.
5. Find the rule titled **TI map IP entity to AzureActivity**, and ensure that you connected all the required data sources.

    ![Screenshot that shows required data sources for the TI map IP entity to AzureActivity analytics rule.](media/work-with-threat-indicators/threat-intel-required-data-sources.png)
6. Select the **TI map IP entity to AzureActivity** rule. Then select **Create rule** to open a rule configuration wizard. Configure the settings in the wizard, and then select **Next: Set rule logic &gt;**.

    ![Screenshot that shows the Create analytics rule configuration wizard.](media/work-with-threat-indicators/threat-intel-create-analytics-rule.png)
7. The rule logic portion of the wizard is prepopulated with the following items:

    - The query that's used in the rule.
    - Entity mappings, which tell Microsoft Sentinel how to recognize entities like accounts, IP addresses, and URLs. Incidents and investigations can then understand how to work with the data in any security alerts that were generated by this rule.
    - The schedule to run this rule.
    - The number of query results needed before a security alert is generated.

    The default settings in the template are:

    - Run once an hour.
    - Match any IP address threat indicators from the `ThreatIntelligenceIndicator` table with any IP address found in the last one hour of events from the `AzureActivity` table.
    - Generate a security alert if the query results are greater than zero to indicate that matches were found.
    - Ensure that the rule is enabled.

    You can leave the default settings or change them to meet your requirements. You can define incident-generation settings on the **Incident settings** tab. For more information, see [Create custom analytics rules to detect threats](detect-threats-custom). When you're finished, select the **Automated response** tab.
8. Configure any automation you want to trigger when a security alert is generated from this analytics rule. Automation in Microsoft Sentinel uses combinations of automation rules and playbooks powered by Azure Logic Apps. To learn more, see [Tutorial: Use playbooks with automation rules in Microsoft Sentinel](tutorial-respond-threats-playbook). When you're finished, select **Next: Review &gt;** to continue.
9. When you see a message stating that the rule validation passed, select **Create**.

## Review your rules

Find your enabled rules on the **Active rules** tab of the **Analytics** section of Microsoft Sentinel. On the **Active rules** tab, you can edit, enable, disable, duplicate, or delete the active rule. The new rule runs immediately upon activation and then runs on its defined schedule.

According to the default settings, each time the rule runs on its schedule, any results that are found generate a security alert. Microsoft Sentinel stores these alerts in a log table called `SecurityAlert`. To view them, go to the **Logs** section of Microsoft Sentinel, and under the **Microsoft Sentinel** group, query the `SecurityAlert` table.

In Microsoft Sentinel, the alerts generated from analytics rules also generate security incidents. On the Microsoft Sentinel menu, under **Threat Management**, select **Incidents**. Incidents are what your security operations teams triage and investigate to determine the appropriate response actions. For more information, see [Tutorial: Investigate incidents with Microsoft Sentinel](investigate-cases).

Note

Analytic rules can look back only 14 days, so Microsoft Sentinel refreshes indicators every seven to 10 days to keep them available for matching.