---
layout: Conceptual
title: Identify SQL Servers protected by Microsoft Monitoring Agent - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/identify-sql-servers-protected-by-monitor-agent
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to identify SQL Server instances still using the legacy Microsoft Monitoring Agent (MMA) so you can deploy Azure Arc and migrate to the updated agent.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: a3f709bd-79a3-a57a-8f8c-c3756ed607c9
document_version_independent_id: 3ddfb898-1c51-5fc9-74f3-19b0714c1efc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/identify-sql-servers-protected-by-monitor-agent.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/identify-sql-servers-protected-by-monitor-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/identify-sql-servers-protected-by-monitor-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: af64b92c-605a-cbd6-781a-adbeb40aa2e2
---

# Identify SQL Servers protected by Microsoft Monitoring Agent - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's Defender for SQL Server on Machines plan provides database security to protect SQL Server instances hosted on Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and on-premises machines. With the retirement of the Microsoft Monitoring Agent (MMA) on August 1, 2024, the Defender for SQL Server on Machines plan requires that you meet prerequisites and deploy Azure Arc on all non-Azure SQL Server instances. For prerequisites, see [Defender for SQL prerequisites](defender-for-sql-usage#prerequisites).

Once Azure Arc is deployed and following the [release on the updated agent](release-notes-archive#update-to-defender-for-sql-servers-on-machines-plan), your SQL Server instances migrate automatically to the updated agent. To ensure your SQL servers are correctly protected, install Azure Arc. For setup steps, see [Connect on-premises machines by using Azure Arc](quickstart-onboard-machines#connect-on-premises-machines-by-using-azure-arc).

Note

Migrating to the updated agent might affect your pricing. For information regarding the plan pricing, review [Microsoft Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

## Determine which SQL servers are protected by the legacy MMA

You can identify SQL servers onboarded to the Defender for SQL Server on Machines plan with the legacy MMA in your environment without Azure Arc installed.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Azure Resource Graph Explorer**.
3. Copy and paste the following query into the query window:

    ```kusto
    securityresources 
    | where type == "microsoft.security/assessments/subassessments" 
    | extend assessmentKey = extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) 
    | where assessmentKey == "f97aa83c-9b63-4f9a-99f6-b22c4398f936" 
    | where tostring(properties.resourceDetails.source) == "OnPremiseSql" 
    | extend lastScanTime = todatetime(properties.timeGenerated) 
    | where lastScanTime > ago(30d) 
    | extend machineName = tostring(properties.resourceDetails.machineName) 
    | extend machineUuid = tostring(properties.resourceDetails.vmuuid) 
    | distinct machineName, machineUuid
    ```
4. Select **Run query**.

    [![Screenshot that shows the pasted query and where to find the Run query button.](media/identify-sql-servers-protected-by-mma/run-query.png)](media/identify-sql-servers-protected-by-mma/run-query.png#lightbox)
5. For any results returned, [connect hybrid machines with Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm).

## Learn more

- [Upcoming changes to Defender for SQL servers on Machines plan](release-notes-archive#update-to-defender-for-sql-servers-on-machines-plan)
- [Verify SQL machine protection](verify-machine-protection)
- [Verify SQL machine protection in government cloud](verify-machine-protection-gov)
- [Troubleshoot Defender for SQL on Machines configuration](troubleshoot-sql-machines-guide)