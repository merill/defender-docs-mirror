---
layout: Conceptual
title: Protecting VM secrets with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/secrets-scanning-servers
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
description: Learn how to protect VM secrets with Defender for Server's agentless secrets scanning in Microsoft Defender for Cloud.
ms.topic: overview
ms.date: 2025-02-26T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 60365b3f-3ef5-6a45-cea3-d8283ea113e1
document_version_independent_id: 58b46033-373c-776e-29e3-bd4e2f381b4b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/secrets-scanning-servers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/secrets-scanning-servers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/secrets-scanning-servers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: efa6e365-3da1-91d2-af4a-ba55f767f969
---

# Protecting VM secrets with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud provides [secrets scanning](secrets-scanning) in a number of scenarios, including scanning for machine secrets.

Machine secrets scanning is one of Defender for Cloud's [agentless scanning features](concept-agentless-data-collection) that improve machine security posture. Agentless scanning doesn't need any installed agents or network connectivity, and doesn't affect machine performance.

- Agentless machine secrets scanning helps you quickly detect, prioritize, and remediate exposed plaintext secrets in your environment.
- If secrets are detected, findings help security teams prioritize actions and remediate to minimize the risk of lateral movement.
- Scanning machines for [supported secrets](secrets-scanning#secrets-support) is available when Defender for Servers Plan 2 or the Defender Cloud Security Posture Management (CSPM) plan is enabled.
- Machine secrets scanning can scan Azure VMs and AWS/GCP instances connected to Defender for Cloud.

## Reducing security risk

Secrets scanning helps reduce risk by:

- Eliminating secrets that aren’t needed.
- Applying the principle of least privilege.
- Strengthening secrets security by using secrets management systems such as Azure Key Vault.
- Using short-lived secrets such as substituting Azure Storage connection strings with SAS tokens that possess shorter validity periods.

## How machine secrets scanning works

Secrets scanning for VMs is agentless and uses cloud APIs. Here's how it works:

1. Secrets scanning captures disk snapshots and analyzes them, with no impact on VM performance.
2. After the Microsoft secrets scanning engine collects secrets metadata from disk, it sends the data to Defender for Cloud.
3. The secrets scanning engine verifies if SSH private keys can be used to move laterally in your network.
    - SSH keys that aren't successfully verified are categorized as unverified on the Defender for Cloud **Recommendations** page.
    - Directories containing test-related content are excluded from scanning.

## Machine secrets recommendations

The following machine secrets security recommendations are available:

- Azure resources: Machines should have secrets findings resolved
- AWS resources: EC2 instances should have secrets findings resolved
- GCP resources: VM instances should have secrets findings resolved

## Machine secrets attack paths

The table summarizes supported attack paths.

| **VM** | **Attack paths** |
| --- | --- |
| Azure | Exposed Vulnerable VM has an insecure SSH private key that is used to authenticate to a VM.Exposed Vulnerable VM has insecure secrets that are used to authenticate to a storage account.Vulnerable VM has insecure secrets that are used to authenticate to a storage account.Exposed Vulnerable VM has insecure secrets that are used to authenticate to an SQL server. |
| AWS | Exposed Vulnerable EC2 instance has an insecure SSH private key that is used to authenticate to an EC2 instance.Exposed Vulnerable EC2 instance has an insecure secret that is used to authenticate to a storage account.Exposed Vulnerable EC2 instance has insecure secrets that are used to authenticate to an AWS RDS server.Vulnerable EC2 instance has insecure secrets that are used to authenticate to an AWS RDS server. |
| GCP | Exposed Vulnerable GCP VM instance has an insecure SSH private key that is used to authenticate to a GCP VM instance. |

## Predefined cloud security explorer queries

Defender for Cloud provides these predefined queries for investigating secrets security issues:

- VM with plaintext secret that can authenticate to another VM - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access other VMs or EC2s.
- VM with plaintext secret that can authenticate to a storage account - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access storage accounts
- VM with plaintext secret that can authenticate to an SQL database - Returns all Azure VMs, AWS EC2 instances, or GCP VM instances with plaintext secret that can access SQL databases.

## Investigating and remediating machine secrets

You can investigate machine secrets findings in Defender for Cloud using several methods. Not all methods are available for all secrets. [Review supported methods](secrets-scanning#secrets-support) for different types of secrets.