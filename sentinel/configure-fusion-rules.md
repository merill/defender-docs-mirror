---
layout: Conceptual
title: Configure multistage attack detection (Fusion) rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-fusion-rules
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
description: Create and configure attack detection rules based on Fusion technology in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f343f56e-d254-fab8-d4fb-1a63f282e64a
document_version_independent_id: 4d7f0f9e-fbc3-2105-5652-fdb11b0dacbb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-fusion-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-fusion-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-fusion-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 95655348-b5d1-de5d-5154-3cf325388762
---

# Configure multistage attack detection (Fusion) rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Important

The new version of the Fusion analytics rule is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

Microsoft Sentinel uses Fusion, a correlation engine based on scalable machine learning algorithms, to automatically detect multistage attacks by identifying combinations of anomalous behaviors and suspicious activities that are observed at various stages of the attack chain. Based on these detected attack patterns, Microsoft Sentinel generates incidents that would otherwise be difficult to catch. These incidents comprise two or more alerts or activities. By design, these incidents are low-volume, high-fidelity, and high-severity.

Customized for your environment, this detection technology not only reduces [false positive](false-positives) rates but can also detect attacks with limited or missing information.

## Configure Fusion rules

The Fusion analytics rule is enabled by default in Microsoft Sentinel. To check or change its status, use the following instructions:

1. Sign in to the [Azure portal](https://portal.azure.com) and enter **Microsoft Sentinel**.
2. From the Microsoft Sentinel navigation menu, select **Analytics**.
3. Select the **Active rules** tab, and then locate **Advanced Multistage Attack Detection** in the **NAME** column by filtering the list for the **Fusion** rule type. Check the **STATUS** column to confirm whether this detection is enabled or disabled.

    [![Screenshot of Fusion analytics rule.](media/configure-fusion-rules/selecting-fusion-rule-type.png)](media/configure-fusion-rules/selecting-fusion-rule-type.png#lightbox)
4. To change the status, select the **Advanced Multistage Attack Detection** entry. On the **Advanced Multistage Attack Detection** preview pane, select **Edit**.
5. In the **General** tab of the **Analytics rule wizard**, note the status (Enabled/Disabled), or change it if you want.

    If you change the status but have no further changes to make, select the **Review and update** tab and select **Save**.

    To further configure the Fusion detection rule, select **Next: Configure Fusion**.

    [![Screenshot of Fusion rule configuration.](media/configure-fusion-rules/configure-fusion-rule.png)](media/configure-fusion-rules/configure-fusion-rule.png#lightbox)
6. **Configure source signals for Fusion detection**: we recommend you include all the listed source signals, with all severity levels, for the best result. By default, they're already all included, but you have the option to make changes in the following ways:

    Note

    If you exclude a particular source signal or an alert severity level, any Fusion detections that rely on signals from that source, or on alerts matching that severity level, won't be triggered.

    - **Exclude signals from Fusion detections**, including anomalies, alerts from various providers, and raw logs.

        *Use case:* If you're testing a specific signal source known to produce noisy alerts, you can temporarily turn off the signals from that particular signal source for Fusion detections.
    - **Configure alert severity for each provider**: By design, the Fusion ML model correlates low fidelity signals into a single high severity incident based on anomalous signals across the kill-chain from multiple data sources. Alerts included in Fusion are lower severity (medium, low, informational), but occasionally relevant high severity alerts are included.

        *Use case:* If you have a separate process for triaging and investigating high severity alerts and prefer not to have these alerts included in Fusion, you can configure the source signals to exclude high severity alerts from Fusion detections.
    - **Exclude specific detection patterns from Fusion detection**. Certain Fusion detections might not be applicable to your environment, or might be prone to generating false positives. If you want to exclude a specific Fusion detection pattern, follow the instructions below:

        1. Locate and open a Fusion incident of the kind you want to exclude.
        2. In the **Description** section, select **Show more**.
        3. Under **Exclude this specific detection pattern**, select **exclusion link**, which redirects you to the **Configure Fusion** tab in the analytics rule wizard.

            ![Screenshot of Fusion incident. Select the exclusion link.](media/configure-fusion-rules/exclude-fusion-incident.png)

        On the **Configure Fusion** tab, you see that the detection pattern—a combination of alerts and anomalies in a Fusion incident—has been added to the exclusion list, along with the time when the detection pattern was added.

        You can remove an excluded detection pattern at any time by selecting the trashcan icon on that detection pattern.

        ![Screenshot of list of excluded detection patterns.](media/configure-fusion-rules/exclusion-patterns-list.png)

        Incidents that match excluded detection patterns still trigger, but they **don't show up in your active incidents queue**. They're autopopulated with the following values:

        - **Status**: "Closed"
        - **Closing classification**: “Undetermined”
        - **Comment**: “Auto closed, excluded Fusion detection pattern”
        - **Tag**: “ExcludedFusionDetectionPattern” - you can query on this tag to view all incidents matching this detection pattern.

            ![Screenshot of auto closed, excluded Fusion incident.](media/configure-fusion-rules/auto-closed-incident.png)

Note

Microsoft Sentinel currently uses 30 days of historical data to train the machine learning systems. This data is always encrypted with Microsoft’s keys as it passes through the machine learning pipeline. However, the training data isn't encrypted with [customer-managed keys (CMK)](customer-managed-keys), which are encryption keys that you create and manage in Azure Key Vault, even if you enable CMK in your Microsoft Sentinel workspace. To opt out of Fusion, go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Analytics &gt; Active rules**, right-click on the **Advanced Multistage Attack Detection** rule, and select **Disable.**

## Configure scheduled analytics rules for Fusion detections

Important

Fusion-based detection using analytics rule alerts is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

**Fusion** detects scenario-based multistage attacks and emerging threats by using alerts generated by [scheduled analytics rules](detect-threats-custom). To get the most out of Microsoft Sentinel's Fusion capabilities, take the following steps to configure and enable these rules.

1. Fusion for emerging threats uses alerts generated by any [scheduled analytics rules](scheduled-rules-overview) that contain kill-chain (tactics) and entity mapping information. To ensure that Fusion can use alerts from a scheduled analytics rule to detect emerging threats, verify the rule's entity mapping and tactics configuration:

    - Review **entity mapping** for these scheduled rules. Use the [entity mapping configuration section](map-data-fields-to-entities) to map parameters from your query results to Microsoft Sentinel-recognized entities. Because Fusion correlates alerts based on entities (such as *user account* or *IP address*), its ML algorithms can't perform alert matching without the entity information.
    - Review the **tactics and techniques** in your analytics rule details. The Fusion ML algorithm uses [MITRE ATT&CK](https://attack.mitre.org/) information for detecting multistage attacks, and the tactics and techniques you label the analytics rules with show up in the resulting incidents. Fusion calculations might be affected if incoming alerts are missing tactic information.
2. Fusion can also detect scenario-based threats by using rules based on the following **scheduled analytics rule templates**.

    To enable the queries available as templates in the **Analytics** page, go to the **Rule templates** tab, select the rule name in the templates gallery, and select **Create rule** in the details pane.

    - [Cisco - firewall block but success logon to Microsoft Entra ID](https://github.com/Azure/Azure-Sentinel/blob/60e7aa065b196a6ed113c748a6e7ae3566f8c89c/Detections/MultipleDataSources/SigninFirewallCorrelation.yaml)
    - [Fortinet - Beacon pattern detected](https://github.com/Azure/Azure-Sentinel/blob/83c6d8c7f65a5f209f39f3e06eb2f7374fd8439c/Detections/CommonSecurityLog/Fortinet-NetworkBeaconPattern.yaml)
    - [IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN](https://github.com/Azure/Azure-Sentinel/blob/60e7aa065b196a6ed113c748a6e7ae3566f8c89c/Detections/MultipleDataSources/HostAADCorrelation.yaml)
    - [Multiple Password Reset by user](https://github.com/Azure/Azure-Sentinel/blob/83c6d8c7f65a5f209f39f3e06eb2f7374fd8439c/Detections/MultipleDataSources/MultiplePasswordresetsbyUser.yaml)
    - [Rare application consent](https://github.com/Azure/Azure-Sentinel/blob/83c6d8c7f65a5f209f39f3e06eb2f7374fd8439c/Detections/AuditLogs/RareApplicationConsent.yaml)
    - [SharePointFileOperation via previously unseen IPs](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/OfficeActivity/SharePoint_Downloads_byNewIP.yaml)
    - [Suspicious Resource deployment](https://github.com/Azure/Azure-Sentinel/blob/83c6d8c7f65a5f209f39f3e06eb2f7374fd8439c/Detections/AzureActivity/NewResourceGroupsDeployedTo.yaml)
    - [Palo Alto Threat signatures from Unusual IP addresses](https://github.com/Azure/Azure-Sentinel/blob/master/Solutions/PaloAlto-PAN-OS/Analytic%20Rules/PaloAlto-UnusualThreatSignatures.yaml)

    To add queries that aren't available in the **Rule templates** gallery, see [Create a custom analytics rule from scratch](detect-threats-custom).

    - [New Admin account activity seen which wasn't seen historically](https://github.com/Azure/Azure-Sentinel/blob/83c6d8c7f65a5f209f39f3e06eb2f7374fd8439c/Hunting%20Queries/OfficeActivity/new_adminaccountactivity.yaml)

    For more information, see [Fusion Advanced Multistage Attack Detection Scenarios with Scheduled Analytics Rules](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/what-s-new-fusion-advanced-multistage-attack-detection-scenarios/ba-p/2337497).

    Note

    For the set of scheduled analytics rules used by Fusion, the ML algorithm does fuzzy matching for the KQL queries provided in the templates. Renaming the templates doesn't impact Fusion detections.