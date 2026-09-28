---
layout: Conceptual
title: Microsoft Defender for Cloud Overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction
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
description: Secure your Azure, hybrid, and multicloud resources with Microsoft Defender for Cloud. This cloud-native application protection platform (CNAPP) includes two key capabilities, cloud security posture management (CSPM) and cloud workload protection platform (CWPP). It helps protect your environments across Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and on-premises systems.
ms.topic: overview
ms.date: 2026-08-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: f11148c5-754d-be54-c66e-b2d763a6b739
document_version_independent_id: 42d6c2aa-79a8-dca8-6022-604b043ad3d4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-cloud-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-cloud-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-cloud-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: fdfa193d-3564-b28b-5cd1-867f99b8e3ef
---

# Microsoft Defender for Cloud Overview - Microsoft Defender for Cloud | Microsoft Learn

Important

Microsoft Defender for Cloud is expanding to the Defender portal to provide a unified security experience across cloud and code environments. As part of this expansion, some features are now available in the Microsoft Defender Portal, and additional capabilities will be added to the Defender portal over time.

This change is designed to:

- Unlock new cloud and posture management experiences.
- Provide deep integration with other Microsoft security services.
- Empower security teams with streamlined workflows by bringing all tools together in one portal.

To identify documentation specific for the Defender Portal, look for the portal entry point at the top of the article. This pivot indicates whether the content applies to the Defender portal or the Azure portal.

Our documentation will be continuously updated to reflect these changes, so check back regularly for the latest guidance and feature availability.

Microsoft Defender for Cloud is a Cloud Native Application Protection Platform (CNAPP), which is a unified solution that combines multiple cloud security tools to protect applications across their entire lifecycle. The solution provides a comprehensive view of your security posture across your cloud and on-premises resources. It also helps you secure multicloud and hybrid environments and integrates security into DevOps workflows. It has three core components:

- Cloud Security Posture Management (CSPM) checks and improves the security posture of cloud resources.
- Development Security Operations (DevSecOps) manages code-level security across multicloud and multi-pipeline environments.
- Cloud Workload Protection Platform (CWPP) defends workloads such as virtual machines (VMs), containers, storage, databases, and serverless functions from threats.

Defender for Cloud uses its broader Cloud Native Application Protection Platform (CNAPP) capabilities to unify protections into one experience. Defender for Cloud embeds security early in the development lifecycle. It helps DevOps teams find misconfigurations, apply policies, and fix risks early. Defender for Cloud integrates with the Defender XDR portal and the Microsoft Security ecosystem, offering unified posture management and SOC experiences.

In addition to its core CNAPP capabilities, Defender for Cloud delivers AI security and AI threat protection to safeguard generative AI workloads throughout their lifecycle. These features help you discover AI applications, identify vulnerabilities, reduce risks, and detect threats targeting your generative AI workloads.

![Diagram showing the core functionality of Defender for Cloud.](media/defender-for-cloud-introduction/cloud-security-pillars.png)

Note

For pricing information, check out [the Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

## Cloud Native Application Protection Platform (CNAPP)

[![Conceptual image of CNAPP and how the Defender for Cloud plans protect all of your resources in their environments.](media/defender-for-cloud-introduction/defender-plans.png)](media/defender-for-cloud-introduction/defender-plans.png#lightbox)

After you enable the [Defender for Cloud solution](connect-azure-subscription) on your Azure subscription, the system collects security data from your multicloud and DevOps environments. Defender for Cloud uses the data to provide insights, recommendations, and actions that help you protect your cloud workloads and resources. You can increase your cloud workloads protection and coverage by enabling additional plans that are listed in the following section.

Defender for Cloud's available plans and their CNAPP benefits include:

| Defender for Cloud plan | CNAPP benefits | Relevant links |
| --- | --- | --- |
| **Defender CSPM / Foundational CSPM** | Provides advanced security posture capabilities including agentless vulnerability scanning, data-aware security posture, the cloud security graph, and advanced threat hunting. | Check out the [differences between the CSPM plans](concept-cloud-security-posture-management#plan-availability). [Enable the Defender CSPM plan](tutorial-enable-cspm-plan). |
| **Defender for Servers** | Provides threat detection and advanced defenses for Windows and Linux machines that run in Azure, AWS, GCP, and on-premises environments. | [Plan your Defender for Servers deployment](plan-defender-for-servers) Check out the [differences between the Defender for Servers plans](defender-for-servers-overview#defender-for-servers-plans)[Deploy Defender for Servers](tutorial-enable-servers-plan) |
| **Defender for Containers** | Provides environment hardening, vulnerability assessment, run time protection of Kubernetes nodes and clusters. | [Overview of Container security in Microsoft Defender for Containers](defender-for-containers-introduction)[Defender for Containers architecture](defender-for-containers-architecture) Protect your [Azure](tutorial-enable-containers-azure), [IaaS](defender-for-containers-arc-enable-portal), [AWS](tutorial-enable-container-aws), and [GCP](tutorial-enable-container-gcp) containers with Defender for Containers |
| **Defender for Resource Manager** | Detects unusual and potentially harmful activity by automatically monitoring the resource management operations. | [Overview of Microsoft Defender for Resource Manager](defender-for-resource-manager-introduction)[Protect your resources with Defender for Resource Manager](tutorial-enable-resource-manager-plan) |
| **Defender for Storage** | Protects against malware, storage specific threats, sensitive data leakage, and Shared Access Signature (SAS) token misuse. | [Overview of Microsoft Defender for Storage](defender-for-storage-introduction)[Malware scanning](defender-for-storage-malware-scan)[Detect threats to sensitive data](defender-for-storage-data-sensitivity)[Deploy Microsoft Defender for Storage](tutorial-enable-storage-plan) |
| **Defender for App Service** | Identifies attacks that target applications running over App Service. | [Overview of Defender for App Service to protect your Azure App Service web apps and APIs](defender-for-app-service-introduction)[Protect your applications with Defender for App Service](tutorial-enable-app-service-plan) |
| **Defender for Databases** | Protects your entire database estate with attack detection and threat response for the various database types in Azure. | [Overview of Microsoft Defender for Azure SQL](defender-for-sql-introduction)[Protect your databases with Defender for Databases](tutorial-enable-databases-plan)[What is Microsoft Defender for open-source relational databases](defender-for-databases-introduction)[Overview of Microsoft Defender for Azure Cosmos DB](concept-defender-for-cosmos) |
| **Defender for Key Vault** | Detects unusual and potentially harmful attempts to access or exploit Key Vault accounts. | [Overview of Microsoft Defender for Key Vault](defender-for-key-vault-introduction)[Protect your key vaults with Defender for Key Vault](tutorial-enable-key-vault-plan) |
| **Defender for APIs** | Provides visibility into business critical APIs, improves API security posture, prioritization of vulnerability fixes, and quickly detect active real-time threats. | [About Microsoft Defender for APIs](defender-for-apis-introduction)[Protect your APIs with Defender for APIs](defender-for-apis-deploy) |
| **AI Services** | Identifies threats to generative AI applications in real time and helps respond to security issues. | [AI threat protection](ai-threat-protection)[Enable threat protection for AI services](ai-onboarding) |

You can also check out the E-book ["From plan to deployment: Implementing a Cloud Native Application Protection Platform (CNAPP) strategy"](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Implementing-A-Cloud-Native-Application-Protection-Strategy-Ebook.pdf), to learn more about implementing CNAPP in Defender for Cloud.

## Cloud security posture management (CSPM)

The security of your cloud and on-premises resources depends on proper configuration and deployment. Defender for Cloud recommendations help you secure your environment.

Defender for Cloud includes free Foundational CSPM capabilities. Enable advanced CSPM capabilities by using the Defender CSPM plan.

Note

Defender CSPM provides broad recommendation coverage in Defender for Cloud. Some recommendations are plan-specific and require you to enable specific CWPP plans to access them.

| Capability | What problem does it solve? | Get started | Defender plan |
| --- | --- | --- | --- |
| [Centralized policy management](security-policy-concept) | Define the security conditions that you want to maintain across your environment. The policy translates to recommendations that identify resource configurations that violate your security policy. The [Microsoft cloud security benchmark](concept-regulatory-compliance) is a built-in standard that applies security principles with detailed technical implementation guidance for Azure and other cloud providers (such as Amazon Web Services (AWS) and Google Cloud Platform (GCP). | [Customize a security policy](create-custom-recommendations) | Foundational CSPM (Free) |
| [Secure score](secure-score-security-controls) | Summarize your security posture based on the security recommendations. As you remediate recommendations, your secure score improves. | [Track your secure score](secure-score-access-and-track) | Foundational CSPM (Free) |
| [Multicloud coverage](plan-multicloud-security-get-started) | Connect to your multicloud environments by using agentless methods for CSPM insight and CWPP protection. | Connect your [Amazon AWS](quickstart-onboard-aws) and [Google GCP](quickstart-onboard-gcp) cloud resources to Defender for Cloud | Foundational CSPM (Free) |
| [Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management) | Use the dashboard to see weaknesses in your security posture. | [Enable CSPM tools](connect-azure-subscription) | Foundational CSPM (Free) |
| [Advanced Cloud Security Posture Management](concept-cloud-security-posture-management) | Get advanced tools to identify weaknesses in your security posture, including:- Governance to drive actions to improve your security posture- Regulatory compliance to verify compliance with security standards- Cloud security explorer to build a comprehensive view of your environment | [Enable CSPM tools](connect-azure-subscription) | Defender CSPM |
| [Data Security Posture Management](concept-data-security-posture) | Data security posture management automatically discovers datastores containing sensitive data, and helps reduce risk of data breaches. | [Enable data security posture management](data-security-posture-enable) | Defender CSPM or Defender for Storage |
| [Attack path analysis](concept-attack-path#what-is-an-attack-path) | Model traffic on your network to identify potential risks before you implement changes to your environment. | [Build queries to analyze paths](how-to-manage-attack-path) | Defender CSPM |
| [Cloud Security Explorer](concept-attack-path#what-is-cloud-security-explorer) | A map of your cloud environment that lets you build queries to find security risks. | [Build queries to find security risks](how-to-manage-cloud-security-explorer) | Defender CSPM |
| [Security governance](governance-rules) | Drive security improvements through your organization by assigning tasks to resource owners and tracking progress in aligning your security state with your security policy. | [Define governance rules](governance-rules) | Defender CSPM |
| [AI SPM](identify-ai-workload-model) | Provides a comprehensive view of your organization's AI Bill of Materials (AI BOM) which assesses the security posture of the scanned AI workloads. | [Discover generative AI workloads](identify-ai-workload-model) | Defender CSPM |

## Development security operations (DevSecOps)

Defender for Cloud adds security to the start of development. It helps you secure code pipelines and environments, and monitor your security posture from one place. Defender for Cloud enables security teams to manage DevOps security across multi-pipeline environments.

Applications require security awareness at the code, infrastructure, and runtime levels to ensure that deployed applications are hardened against attacks.

| Capability | What problem does it solve? | Get started | Defender plan |
| --- | --- | --- | --- |
| [Code pipeline insights](defender-for-devops-introduction) | Empowers security teams with the ability to protect applications and resources from code to cloud across multi-pipeline environments, including GitHub, Azure DevOps, and GitLab. DevOps security findings, such as Infrastructure as Code (IaC) misconfigurations and exposed secrets, can then be correlated with other contextual cloud security insights to prioritize remediation in code. | Connect [Azure DevOps](quickstart-onboard-devops), [GitHub](quickstart-onboard-github), and [GitLab](quickstart-onboard-gitlab) repositories to Defender for Cloud | Foundational CSPM (Free) and Defender CSPM |

## Cloud workload protection platform (CWPP)

Proactive security principles require implementing security practices to protect your workloads from threats. Cloud workload protection platforms (CWPP) provide workload-specific recommendations to guide you to the right security controls to protect your workloads.

To compare workload protection coverage for Azure, AWS, and GCP in one place, see the [multicloud workload protection support matrix](multicloud-support-matrix).

When your environment is threatened, security alerts immediately indicate the nature and severity of the threat so you can plan your response. After identifying a threat in your environment, respond quickly to limit the risk to your resources.

| Capability | What problem does it solve? | Get started | Defender plan |
| --- | --- | --- | --- |
| Protect cloud servers | Provide server protections through Microsoft Defender for Endpoint or extended protection with just-in-time network access, file integrity monitoring, vulnerability assessment, and more. | [Secure your multicloud and on-premises servers](defender-for-servers-introduction) | Defender for Servers |
| Identify threats to your storage resources | Detect unusual and potentially harmful attempts to access or exploit your storage accounts by using advanced threat detection capabilities and Microsoft Threat Intelligence data to provide contextual security alerts. | [Protect your cloud storage resources](defender-for-storage-introduction) | Defender for Storage |
| Protect cloud databases | Protect your entire database estate with attack detection and threat response for the most popular database types in Azure to protect the database engines and data types, according to their attack surface and security risks. | [Deploy specialized protections for cloud and on-premises databases](quickstart-enable-database-protections) | - Defender for Azure SQL Databases- Defender for SQL servers on machines- Defender for Open-source relational databases- Defender for Azure Cosmos DB |
| Protect containers | Secure your containers so you can improve, monitor, and maintain the security of your clusters, containers, and their applications with environment hardening, vulnerability assessments, and run-time protection. | [Find security risks in your containers](defender-for-containers-introduction) | Defender for Containers |
| [Infrastructure service insights](asset-inventory) | Diagnose weaknesses in your application infrastructure that can leave your environment susceptible to attack. | - [Identify attacks targeting applications running over App Service](defender-for-app-service-introduction)- [Detect attempts to exploit Key Vault accounts](defender-for-key-vault-introduction)- [Get alerted on suspicious Resource Manager operations](defender-for-resource-manager-introduction)- [Expose anomalous Domain Name System (DNS) activities](defender-for-dns-introduction) | - Defender for App Service- Defender for Key Vault- Defender for Resource Manager- Defender for DNS |
| [Security alerts](alerts-overview) | Get informed of real-time events that threaten the security of your environment. Alerts are categorized and assigned severity levels to indicate proper responses. | [Manage security alerts](manage-respond-alerts) | Any workload protection Defender plan |
| [Security incidents](alerts-overview#what-are-security-incidents) | Identify attack patterns by correlating alerts. Integrate with Security Information and Event Management (SIEM), Security Orchestration, Automation, and Response (SOAR), and traditional IT deployment solutions that respond to threats and reduce risk. | [Export alerts to SIEM, SOAR, or ITSM systems](export-to-siem) | Any workload protection Defender plan |

Important

- As of August 1, 2023, customers with an existing subscription to Defender for DNS can continue to use the service as a standalone plan.
- For new subscriptions, alerts about suspicious DNS activity are included as part of Defender for Servers Plan 2 (P2).
- There's no change to the protection scope: Defender for DNS continues to protect all Azure resources connected to Azure's default DNS resolvers. The change affects how DNS protection is billed and bundled, not what resources are covered.

## AI security and threat protection

Microsoft Defender for Cloud provides AI security posture management and AI threat protection to help you secure your generative AI workloads across their entire lifecycle.

| Type of AI security | Description | Relevant links |
| --- | --- | --- |
| AI security posture management (SPM) | Helps you discover generative AI applications, identify vulnerabilities, and reduce risks by using built-in recommendations and attack path analysis. | Learn more about [AI security posture management](ai-security-posture) |
| AI threat protection | Uses advanced threat detection techniques to identify and respond to threats targeting your generative AI workloads. | [AI threat protection](ai-threat-protection) |

Defender for Cloud also includes a Data and AI security dashboard. This dashboard gives you a central place to monitor and manage your data and AI resources, track risks, and check protection status.

## Managed detection and response for servers

Microsoft Defender Experts for Servers is a managed detection and response service that adds Microsoft analyst expertise to your Defender for Servers deployment. Microsoft analysts and automation work together to detect, investigate, and respond to threats on Windows and Linux servers across Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and on-premises environments. Defender Experts for Servers is sold separately from Defender for Servers Plan 1 and Plan 2, and you opt in when you want Microsoft to operate detection and response on your behalf. To learn more, see [Microsoft Defender Experts for Servers](/en-us/defender-xdr/dex-servers-overview).