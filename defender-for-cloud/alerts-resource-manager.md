---
layout: Conceptual
title: Microsoft Defender for Resource Manager Detections Overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-resource-manager
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: CESANU
ms.author: cesanu
manager: orspodek
ms.service: defender-for-cloud
description: Learn about the types of threats Microsoft Defender for Resource Manager detects in suspicious Azure resource management activity.
ms.topic: overview
ms.custom: linux-related-content, msecd-doc-authoring-1032
ms.date: 2026-11-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fe4e7eaa-2f77-1a3e-dd52-66cb427caa8e
document_version_independent_id: 38711941-7cec-ecdc-9a0e-2d11de297ef8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-resource-manager.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-resource-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-resource-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: e38b9880-83d3-9ab8-ae4b-3ccdec7de7c6
---

# Microsoft Defender for Resource Manager Detections Overview - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Resource Manager is a threat protection plan in Microsoft Defender for Cloud that detects suspicious Azure control plane activity. It monitors management operations performed through the Azure portal, Azure REST APIs, Azure CLI, and other Azure programmatic clients. Detections use specific rules and behavioral analysis.

Security analysts can use this overview to understand detection families and assess coverage. The alerts you receive depend on the resources and services you protect and your environment's configuration.

## Resource management detection

Defender for Resource Manager analyzes Azure control plane operations to identify possible account compromise or resource misuse. The detection families below group suspicious activity by what an attacker might try to accomplish.

Some detections identify activity associated with known exploitation toolkits, such as MicroBurst and PowerZure.

These categories summarize detection coverage. They aren't a complete inventory of alerts or a guarantee that every activity in a category generates an alert.

### Suspicious access and reconnaissance

Management operations from suspicious sources and reconnaissance tools can indicate attempts to explore an Azure environment. These operations might indicate that an attacker is using a compromised identity to identify resources and access opportunities.

Examples include:

- **Suspicious IP addresses:** Management operations from addresses identified as suspicious by threat intelligence feeds.
- **Proxy services:** Operations from IP addresses associated with proxy services that attackers might use to hide their source.
- **Resource discovery:** Toolkit activity that enumerates resources, permissions, and network structures.

### Credential access and data collection

Suspicious management operations can indicate attempts to retrieve credentials or collect sensitive resource data. An attacker might use retrieved keys or secrets to access sensitive resources or move to other resources.

Examples include:

- **Keys and secrets:** Detections include suspicious recovery of a soft-deleted key vault and suspicious operations that might indicate credential access or data collection.
- **Automation credentials:** Attempts to extract Azure Automation account credentials.
- **Automation content:** Toolkit activity that extracts runbook content.

### Code execution through management operations

Suspicious use of management operations to execute code on virtual machines or through Azure Automation might indicate a compromised identity. An attacker might use these operations to run malicious code.

Examples include:

- **Virtual machine operations:** Behavioral detections identify suspicious execution of scripts or commands on one or more virtual machines, including suspicious scripts in virtual machine extensions.
- **Azure Automation operations:** Toolkit activity that executes runbooks or runs arbitrary code through automation accounts.

### Privilege escalation and persistent access

Suspicious changes to roles and access can indicate attempts to gain permissions or maintain access to an Azure environment.

Examples include:

- **Role changes:** Behavioral detections identify suspicious creation of privileged custom roles or unusual role assignments.
- **Access elevation:** Suspicious operations that elevate an identity's access to Azure resources.

### Defense evasion and resource abuse

Behavioral detections identify suspicious operations that can indicate attempts to evade defenses, change resource configurations, or abuse compute resources.

Examples include:

- **Defense evasion:** Suspicious operations that might help an attacker avoid detection, such as disabling antimalware.
- **Resource configuration changes:** Suspicious high-risk operations that might indicate attempts to change resource configurations.
- **Compute resource abuse:** Unusual creation of virtual machines or scale sets that might indicate crypto mining.

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Alert investigation context

Suspicious management activity can also be legitimate administration. Use the activity and resource context in each alert to determine whether the behavior was expected.

Note

Alerts with a **delegated access** indication are triggered due to activity of third-party service providers. For more information, see [service providers activity indications](defender-for-resource-manager-usage).

These alerts include a customized description and remediation guidance to support investigation.

For investigation and containment guidance, see [Respond to Defender for Resource Manager alerts](defender-for-resource-manager-usage).