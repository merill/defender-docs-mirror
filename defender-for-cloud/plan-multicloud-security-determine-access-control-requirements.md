---
layout: Conceptual
title: Determine Access Control Requirements for Multicloud Security - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-access-control-requirements
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
description: Determine the permissions and access controls you need for multicloud deployment with Microsoft Defender for Cloud for your CSPM and CWPP solution design.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 73249053-9002-05b1-570b-f3731d628a94
document_version_independent_id: 984ff3e5-fee2-d95f-bfe0-4d0b3ea82158
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-access-control-requirements.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-access-control-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-access-control-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b05f9ca9-c317-2322-c764-0ab2360611a5
---

# Determine Access Control Requirements for Multicloud Security - Microsoft Defender for Cloud | Microsoft Learn

This article is part of a series that provides guidance as you design a cloud security posture management (CSPM) and cloud workload protection platform (CWPP) solution for multicloud resources with Microsoft Defender for Cloud. Determine the permissions and access controls required for your multicloud deployment, including identity and access management (IAM) considerations for Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP) resources.

## Define access control objectives

Determine the permissions and access controls you need in your multicloud deployment.

## Assess access control requirements

As part of your multicloud solution design, review access requirements for multicloud resources that users can access. As you plan, answer the following questions, take notes, and document why each answer matters.

- Who should have access to recommendations and alerts for multicloud resources?
- Are your multicloud resources and environments owned by different teams? If so, does each team need the same level of access?
- Do you need to limit access to specific resources for specific users and groups? If so, how can you limit access for Azure, AWS, and GCP resources?
- Does your organization need identity and access management (IAM) permissions to be inherited at the resource group level?
- Do you need to determine any IAM requirements for people who:

    - Implement just-in-time (JIT) virtual machine (VM) access controls for Azure VMs and Amazon Elastic Compute Cloud (Amazon EC2) instances?
    - Perform security operations?

With clear answers available, you can figure out your Defender for Cloud access requirements. Other things to consider:

- Defender for Cloud multicloud capabilities support IAM permission inheritance.
- User permissions at the resource group level where the AWS and GCP connectors reside are inherited automatically for multicloud recommendations and security alerts.