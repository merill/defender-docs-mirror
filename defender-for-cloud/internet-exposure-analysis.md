---
layout: Conceptual
title: Internet exposure analysis - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/internet-exposure-analysis
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
description: Learn how Defender for Cloud detects, assesses, and mitigates internet exposure for your multicloud resources to enhance security.
ms.topic: concept-article
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: template-concept
ai-usage: ai-assisted
locale: en-us
document_id: ee657ce6-a067-7302-1e43-b5e6f47baf35
document_version_independent_id: 8d21e064-5549-d4a6-334e-5fe9a03e3bae
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/internet-exposure-analysis.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/internet-exposure-analysis
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/internet-exposure-analysis.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: ed706ec3-1b6f-83ab-4b67-14632edd15bf
---

# Internet exposure analysis - Microsoft Defender for Cloud | Microsoft Learn

Internet Exposure Analysis is a key capability that helps organizations identify which cloud resources are exposed to the public internet, both intentionally or unintentionally, and prioritize remediation based on the risk and scope of that exposure.

Defender for Cloud uses internet exposure to determine the risk level of your misconfigurations enabling high quality posture insights across attack paths, risk-based posture assessments, and signal prioritization across Defender for Cloud posture.

## How Defender for Cloud detects internet exposure

Defender for Cloud determines if a resource is exposed to the internet by analyzing both:

1. Control-plane configuration (e.g., public IPs, load balancers)
2. Network-path reachability (analyzing routing, security and firewall rules)

Detecting internet exposure can be as simple as checking if a virtual machine (VM) has a public IP address. However, the process can be more complex. Defender for Cloud attempts to locate internet-exposed resources in complex multicloud architectures. For example, a VM might not be directly exposed to the internet but could be behind a load balancer, which distributes network traffic across multiple servers to ensure no single server becomes overwhelmed.

The following table lists the resources that Defender for Cloud assesses for internet exposure:

| Category | Services/Resources |
| --- | --- |
| Virtual machines | Azure VM  Amazon Web Service (AWS) EC2  Google Cloud Platform (GCP) compute instance |
| Virtual machine clusters | Azure Virtual Machine Scale Set  GCP instance groups |
| Databases (DB) | Azure SQL  Azure PostgreSQL  Azure MySQL  Azure SQL Managed Instance  Azure Cosmos DB  Azure Synapse  AWS Relational Database Service (RDS) DB  GCP SQL admin instance |
| Storage | Azure Storage  AWS S3 buckets  GCP storage buckets |
| AI | Azure OpenAI Service  Azure AI Services  Azure Cognitive Search |
| Containers | Azure Kubernetes Service (AKS)  AWS EKS  GCP GKE |
| API | Azure API Management Operations |

The following table lists the network components that Defender for Cloud assesses for internet exposure:

| Category | Services/Resources |
| --- | --- |
| Azure | Application gateway  Load Balancer  Azure Firewall  Network Security Groups  vNet/Subnets |
| AWS | Elastic load balancer |
| GCP | Load balancer |

## Trusted Exposure (Preview)

Note

Trusted Exposure currently supports multicloud virtual machines only including Azure VMs/VMSS, AWS EC2, and GCP compute instance.

Trusted Exposure, now available in Preview, allows organizations to define CIDRs (IP ranges/blocks) and individual IP addresses that are known and trusted. If a resource is exposed only to these trusted IPs, it is not considered internet-facing. In Defender CSPM, such resources are treated as having no internet exposure risk, equivalent to internal-only cloud resources.

When Trusted IPs are configured, Defender for Cloud will:

- **Suppress attack paths** originating from machines that are exposed only to trusted IPs (e.g., internal scanners, VPNs, allow-listed IPs)
- **Priority of security recommendations** will now exclude all trusted sources helping reduce noise.

### How it Works

- Define and apply IP addresses that are trusted using [Azure Policy](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Policy/Define%20MDC%20Trusted%20IPs) applied across your tenant scope.
- The new policy creates an IP group that contains the CIDR/IP addresses.
- Defender for Cloud reads the policy and applies it across supported resource types (currently: multicloud virtual machines).
- Attack Paths will not be created for exposures that originate from virtual machines exposed only to IP addresses that are “Trusted”.
- Security recommendations are deprioritized if a resource is exposed only to Trusted IPs.
- A new "Trusted Exposure" insight is available on the Cloud Security Explorer, allowing users to query all supported resources flagged as Trusted.

## Internet Exposure Width

Note

Internet Exposure Width including the risk factors are applied to only multicloud compute instances that include - Azure VMs/VMSS, AWS EC2, and GCP compute instance.

Internet Exposure Width represents the risks based on how broadly a resource (e.g. virtual machine) is exposed to the public internet. It plays a critical role in helping security teams understand not just whether a resource is internet-exposed, but how wide or narrow that exposure is, influencing the criticality and prioritization of security insights presented in attack paths and security recommendations.

### How It Works

Defender for cloud automatically analyzes your internet-facing resources and tags them as **wide exposure** or **narrow exposure** according to the networking rules. The output is tagged either as wide exposure and

- Attack paths that involve widely exposed resources now clearly indicate this in the title, such as "Widely internet exposed virtual machines has high permissions to storage account".
- The exposure width calculated is then used to determine the attack path generation and risk based recommendation that helps you to rightly prioritize the severity of the findings by adding specific labels to the following experiences.
- A new "Exposure width" insight is available on the Cloud Security Explorer, allowing users to query all supported resources that are widely exposed.

## How to view internet exposed resources

Defender for Cloud offers a few different ways to view internet facing resources.

- [Cloud Security Explorer](how-to-manage-cloud-security-explorer) - The Cloud Security Explorer allows you to run graph-based queries. From the Cloud Security Explorer page, you can run a query to identify resources exposed to the internet. The query returns all attached resources with internet exposure and provides their associated details for review.
- [Attack Path Analysis](how-to-manage-attack-path) - The Attack Path Analysis page lets you view attack paths that an attacker could take to reach a specific resource. With Attack Path Analysis, you can view a visual representation of the attack path and see which resources are exposed to the internet. Internet exposure often serves as an entry point for attack paths, especially when the resource has vulnerabilities. Internet facing resources often lead to targets with sensitive data.
- [Recommendations](review-security-recommendations) - Defender for Cloud prioritizes recommendations based on their exposure to the internet.

## Defender External Attack Surface Management integration

Defender for Cloud also integrates with Defender External Attack Surface Management to assess resources for internet exposure by attempting to contact them from an external source and seeing if they respond.

Learn more about the [Defender External Attack Surface Management integration](concept-easm).