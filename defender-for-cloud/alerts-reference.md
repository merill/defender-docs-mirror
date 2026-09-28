---
layout: Conceptual
title: Reference guide for security alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-reference
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
description: This article links to the various security alerts visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f7ea2039-1ff6-c2a0-5b4e-8b1a2e232bbf
document_version_independent_id: dcc7230a-d5db-1c19-4321-30866a637661
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-reference.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e7e28e63-cf6e-3fa0-eedf-dd75732f440a
---

# Reference guide for security alerts - Microsoft Defender for Cloud | Microsoft Learn

This article provides links to pages listing the security alerts you may receive from Microsoft Defender for Cloud and any enabled Microsoft Defender plans. The alerts displayed in your environment depend on the resources and services you are protecting and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

This page also includes a table describing the Microsoft Defender for Cloud kill chain aligned with version 9 of the [MITRE ATT&CK matrix](https://attack.mitre.org/versions/v9/).

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Security alert pages by category

- [Alerts for Windows machines](alerts-windows-machines)
- [Alerts for Linux machines](alerts-linux-machines)
- [Alerts for DNS](alerts-dns)
- [Alerts for Azure VM extensions](alerts-azure-vm-extensions)
- [Alerts for Azure App Service](alerts-azure-app-service)
- [Alerts for containers - Kubernetes clusters](alerts-containers)
- [Alerts for SQL Database and Azure Synapse Analytics](alerts-sql-database-and-azure-synapse-analytics)
- [Alerts for open-source relational databases](alerts-open-source-relational-databases)
- [Alerts for Resource Manager](alerts-resource-manager)
- [Alerts for Azure Storage](alerts-azure-storage)
- [Alerts for Azure Cosmos DB](alerts-azure-cosmos-db)
- [Alerts for Azure network layer](alerts-azure-network-layer)
- [Alerts for Azure Key Vault](alerts-azure-key-vault)
- [Alerts for Azure DDoS Protection](alerts-azure-ddos-protection)
- [Alerts for Defender for APIs](alerts-defender-for-apis)
- [Alerts for AI workloads](alerts-ai-workloads)
- [Deprecated security alerts](deprecated-alerts)

## MITRE ATT&CK tactics

Understanding the intention of an attack can help you investigate and report the event more easily. To help with these efforts, Microsoft Defender for Cloud alerts include the MITRE tactics with many alerts.

The series of steps that describe the progression of a cyberattack from reconnaissance to data exfiltration is often referred to as a "kill chain".

Defender for Cloud's supported kill chain intents are based on [version 9 of the MITRE ATT&CK matrix](https://attack.mitre.org/versions/v9/) and described in the table below.

| Tactic | ATT&CK Version | Description |
| --- | --- | --- |
| **PreAttack** |  | [PreAttack](https://attack.mitre.org/matrices/enterprise/pre/) could be either an attempt to access a certain resource regardless of a malicious intent, or a failed attempt to gain access to a target system to gather information prior to exploitation. This step is usually detected as an attempt, originating from outside the network, to scan the target system and identify an entry point. |
| **Initial Access** | V7, V9 | Initial Access is the stage where an attacker manages to get a foothold on the attacked resource. This stage is relevant for compute hosts and resources such as user accounts, certificates etc. Threat actors will often be able to control the resource after this stage. |
| **Persistence** | V7, V9 | Persistence is any access, action, or configuration change to a system that gives a threat actor a persistent presence on that system. Threat actors will often need to maintain access to systems through interruptions such as system restarts, loss of credentials, or other failures that would require a remote access tool to restart or provide an alternate backdoor for them to regain access. |
| **Privilege Escalation** | V7, V9 | Privilege escalation is the result of actions that allow an adversary to obtain a higher level of permissions on a system or network. Certain tools or actions require a higher level of privilege to work and are likely necessary at many points throughout an operation. User accounts with permissions to access specific systems or perform specific functions necessary for adversaries to achieve their objective might also be considered an escalation of privilege. |
| **Defense Evasion** | V7, V9 | Defense evasion consists of techniques an adversary might use to evade detection or avoid other defenses. Sometimes these actions are the same as (or variations of) techniques in other categories that have the added benefit of subverting a particular defense or mitigation. |
| **Credential Access** | V7, V9 | Credential access represents techniques resulting in access to or control over system, domain, or service credentials that are used within an enterprise environment. Adversaries will likely attempt to obtain legitimate credentials from users or administrator accounts (local system administrator or domain users with administrator access) to use within the network. With sufficient access within a network, an adversary can create accounts for later use within the environment. |
| **Discovery** | V7, V9 | Discovery consists of techniques that allow the adversary to gain knowledge about the system and internal network. When adversaries gain access to a new system, they must orient themselves to what they now have control of and what benefits operating from that system give to their current objective or overall goals during the intrusion. The operating system provides many native tools that aid in this post-compromise information-gathering phase. |
| **LateralMovement** | V7, V9 | Lateral movement consists of techniques that enable an adversary to access and control remote systems on a network and could, but does not necessarily, include execution of tools on remote systems. The lateral movement techniques could allow an adversary to gather information from a system without needing more tools, such as a remote access tool. An adversary can use lateral movement for many purposes, including remote Execution of tools, pivoting to more systems, access to specific information or files, access to more credentials, or to cause an effect. |
| **Execution** | V7, V9 | The execution tactic represents techniques that result in execution of adversary-controlled code on a local or remote system. This tactic is often used in conjunction with lateral movement to expand access to remote systems on a network. |
| **Collection** | V7, V9 | Collection consists of techniques used to identify and gather information, such as sensitive files, from a target network prior to exfiltration. This category also covers locations on a system or network where the adversary might look for information to exfiltrate. |
| **Command and Control** | V7, V9 | The command and control tactic represents how adversaries communicate with systems under their control within a target network. |
| **Exfiltration** | V7, V9 | Exfiltration refers to techniques and attributes that result or aid in the adversary removing files and information from a target network. This category also covers locations on a system or network where the adversary might look for information to exfiltrate. |
| **Impact** | V7, V9 | Impact events primarily try to directly reduce the availability or integrity of a system, service, or network; including manipulation of data to impact a business or operational process. This would often refer to techniques such as ransomware, defacement, data manipulation, and others. |

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.