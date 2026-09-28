---
layout: Conceptual
title: Migrate to the Microsoft Sentinel agentless SAP data connector | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-agent-migrate
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Migrate from the retired containerized SAP agent to the supported agentless data connector so SAP logs continue flowing to Microsoft Sentinel.
ms.author: monaberdugo
author: mberdugo
ms.topic: how-to
ms.date: 2026-09-17T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: d729b194-d586-8b48-e3e4-e6c42d1f0d71
document_version_independent_id: 55ed8a19-42cf-381e-d517-916d9c2cd6a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-agent-migrate.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-agent-migrate
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-agent-migrate.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 6566de2e-bdb6-ce40-b4ed-67f8d0b70a8b
---

# Migrate to the Microsoft Sentinel agentless SAP data connector | Microsoft Learn

Follow this guide to migrate from the containerized SAP agent to the agentless data connector for the Microsoft Sentinel solution for SAP applications.

The containerized data connector agent for SAP [retired on September 14, 2026](https://azure.microsoft.com/updates?id=571342), and is unsupported and unmaintained. Existing TLS-compliant agents might continue sending logs through the retired HTTP Data Collector API. On October 14, 2026, container images will be removed, preventing new pulls, installation, redeployment, scaling, replacement, and disaster recovery. Customers must migrate to the supported SAP agentless connector. Customers who use the agentless data connector aren't affected.

## Why move to the agentless data connector?

The agentless connector offers these advantages:

- Simplified deployment with zero footprint on SAP NetWeaver.
- Reduced maintenance overhead without container management and standard SAP updates.
- Future-proof architecture based on SAP Integration Suite and SAP Cloud Connector.
- Improved scalability.

The migration process involves deploying the agentless connector side by side with the existing containerized agent, validating log retrieval from the agentless connector, and then decommissioning the containerized agent.

Existing analytics rules, workbooks, and playbooks for the Microsoft Sentinel solution for SAP applications remain functional with the agentless data connector. Enhancements to the [KQL functions](sap-solution-function-reference) support both data ingestion methods side by side. The functions use the fuzzy union operator to combine data from both sources when available.

## Migration path

Creation of new containerized agents is disabled. Use the agentless data connector when you onboard new SAP systems, and migrate existing containerized agents as soon as possible. Complete migration before container images are removed on October 14, 2026.

1. **Assess**: Review your existing containerized SAP agent deployment to identify monitored SAP systems, log types collected, and any custom configurations.
2. **Review**: Compare the configuration options and capabilities of the containerized agent and the agentless data connector.
3. **Deploy**: Set up the agentless data connector by following [Deploy the Microsoft Sentinel solution for SAP applications](deploy-sap-security-content).
4. **Validate**: Confirm that all required SAP tables and log types are being collected correctly from your SAP systems by the agentless data connector. Use KQL queries to verify log ingestion. 

    ```kql
    let startTime = ago(1h);
    let endTime = now();
    ABAPAuditLog
    | where TimeGenerated between (startTime .. endTime)
    | summarize Count = count() by SourceSystem, bin(TimeGenerated, 5m)
    | order by TimeGenerated desc
    ```
5. **Monitor**: Run both the containerized agent and the agentless data connector in parallel for a defined period to ensure stable and complete log collection. Confirm that analytics rules, workbooks, hunting queries, and playbooks return the expected results with logs ingested by the agentless connector.
6. **Decommission**: After you validate the agentless data connector, decommission the containerized SAP agent by following [Stop SAP data collection](stop-collection).

Tip

Follow the [agentless migration video playlist](https://www.youtube.com/playlist?list=PLmAptfqzxVEV69k9hwfI4zVOb_o6LgfDV) for latest insights for a smooth transition.

Important

Review the authorizations of the Sentinel user and role on your SAP systems used with the containerized agent. The agentless data connector requires less but different authorizations compared to the containerized SAP agent. Refer to the [configuration guide](/en-us/azure/sentinel/sap/preparing-sap#configure-the-microsoft-sentinel-role) for details and SAP role sample for minimum authorizations.

Warning

The retirement doesn't change pricing or billing meters. However, the agentless data connector uses different identification methods than the containerized data connector. Review billing exclusions for selected SAP SIDs, and contact your account representative before you migrate.

## Feature parity

The agentless data connector provides built-in feature parity with the containerized SAP agent for most important use cases regarding analytic rules and workbooks. See the [content reference](sap-solution-security-content) for details.

All [analytics rules and workbooks](sap-solution-security-content#built-in-analytics-rules) built on the underlying SAP sources mentioned on the [table reference](sap-solution-log-reference#logs-collected-by-the-agentless-data-connector) remain functional without any changes.

These sources include but are not limited to the following logs:

- Security Audit Log (ABAPAuditLog\_CL vs. ABAPAuditLog)
- Change Documents Log (ABAPChangeDocsLog\_CL vs. ABAPChangeDocsLog)
- User and User Authorization Details (multiple ABAPUser tables vs. ABAPUserDetails and ABAPAuthorizationDetails)

The solution scope can be extended through [extensions patterns](https://github.com/Azure-Samples/Sentinel-For-SAP-Community) available for the agentless data connector. Watchlists and Playbooks remain fully functional without any changes.

The "SAPCon" prefix was from analytic rules dropped for clarity.

SAP HANA database or OS-level detections are out of scope for the comparison because they are covered by their own connectors in Microsoft Sentinel.

Note

The cross-workspace deployment option (installing SAP data and SOC data on separate workspaces) is no longer needed with the unified workspace in the Microsoft Defender portal and has been removed from the portal experience. If you still need a split deployment, the underlying ARM APIs continue to support it - the option is only removed from the UI.