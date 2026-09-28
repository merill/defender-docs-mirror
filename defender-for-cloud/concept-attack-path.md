---
layout: Conceptual
title: Security explorer and attack paths in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-attack-path
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
description: Learn how Security explorer and attack paths in Microsoft Defender for Cloud help you prioritize high-risk exposures and reduce exploitable paths across multicloud environments.
ms.topic: concept-article
ms.date: 2026-05-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 17398fed-bd3c-6c51-d4fe-5b7caa2f0b74
document_version_independent_id: bb41b184-4427-fc6c-222a-8e1586a59d13
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-attack-path.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-attack-path
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-attack-path.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 4c2adfc8-73ca-2efa-d43a-3b606ebcaba4
---

# Security explorer and attack paths in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

One of the biggest challenges for security teams today is the number of daily security issues. Numerous security issues need resolution, but resources are insufficient.

Defender for Cloud's contextual security capabilities help security teams assess the risk behind each security issue and identify the highest-risk issues that need immediate resolution. Defender for Cloud helps security teams reduce the risk of impactful breaches effectively.

All of these capabilities are available as part of the [Defender Cloud Security Posture Management (Defender CSPM) plan](concept-cloud-security-posture-management). They require you to enable either [agentless scanning for virtual machines (VMs)](concept-agentless-data-collection) or the [vulnerability assessment capability](deploy-vulnerability-assessment-vm) on the [Defender for Servers plan](apply-security-baseline).

## Access attack paths and security explorer

In the Azure portal, you can access these capabilities through:

- **Attack path analysis**: Navigate to **Microsoft Defender for Cloud** &gt; **Attack path analysis**
- **Cloud security explorer**: Navigate to **Microsoft Defender for Cloud** &gt; **Cloud security explorer**

## What is the cloud security graph?

The cloud security graph is a graph-based context engine within Defender for Cloud. The cloud security graph collects data from your multicloud environment and other sources. For example, it includes cloud assets inventory, connections, lateral movement possibilities, internet exposure, permissions, network connections, vulnerabilities, and more. The collected data builds a graph representing your multicloud environment.

Defender for Cloud uses the generated graph to perform an attack path analysis and find the highest-risk issues in your environment. You can also query the graph using the cloud security explorer.

Learn more about how [Defender for Cloud collects and protects your data](data-security).

[![Screenshot of a conceptualized graph that shows the complexity of security graphing.](media/concept-cloud-map/security-map.png)](media/concept-cloud-map/security-map.png#lightbox)

## What is an attack path?

An attack path is a series of steps a potential attacker uses to breach your environment and access your assets. Attack paths focus on real, externally-driven and exploitable threats that adversaries could use to compromise your organization. An attack path starts at an external entry point, such as an internet-exposed vulnerable resource. The attack path follows available lateral movement within your multicloud environment, such as using attached identities with permissions to other resources. The attack path continues until the attacker reaches a critical target, such as databases containing sensitive data.

Defender for Cloud's attack path analysis feature uses the cloud security graph and a proprietary algorithm to find exploitable entry points that begin outside your organization and the steps an attacker can take to reach your vital assets. This helps you cut through the noise and act faster by emphasizing only the most urgent, externally initiated, and exploitable threats. The algorithm exposes attack paths and suggests recommendations to fix issues, breaking the attack path and preventing a breach.

Attack path analysis expands cloud threat detection to cover a broad range of cloud resources, including storage accounts, containers, serverless environments, unprotected repositories, unmanaged application programming interfaces (APIs), and artificial intelligence (AI) agents. Each attack path is built from a real, exploitable weakness such as exposed endpoints, misconfigured access settings, or leaked credentials. This helps ensure identified threats reflect genuine risk scenarios. By analyzing cloud configuration data and performing active reachability scans, the system validates whether exposures are accessible from outside the environment. This reduces false positives and emphasizes threats that are both real and actionable.

![Diagram showing a sample attack path from an attacker to sensitive data.](media/concept-cloud-map/attack-path.png)

The attack path analysis feature scans each customer's unique cloud security graph for exploitable entry points. If an entry point is found, the algorithm searches for potential next steps an attacker could take to reach critical assets. These attack paths are presented on the attack path analysis page in Defender for Cloud and in applicable recommendations.

Each customer sees their unique attack paths based on their unique multicloud environment. Using the attack path analysis feature in Defender for Cloud, you can identify issues that might lead to a breach. You can also remediate any found issue based on the highest risk first. Risk is based on factors such as internet exposure, permissions, and lateral movement.

Learn how to use [attack path analysis](how-to-manage-attack-path).

## What is cloud security explorer?

With cloud security explorer, you can run graph-based queries on the cloud security graph to proactively identify security risks in your multicloud environments. Your security team can use the query builder to locate risks based on your organization's specific context.

Cloud security explorer enables proactive exploration. You can search for security risks within your organization by running graph-based path-finding queries on the contextual security data provided by Defender for Cloud, such as cloud misconfigurations, vulnerabilities, resource context, lateral movement possibilities between resources, and more.

Learn how to use the [cloud security explorer](how-to-manage-cloud-security-explorer), or check out the [cloud security graph components list](attack-path-reference#cloud-security-graph-components-list).