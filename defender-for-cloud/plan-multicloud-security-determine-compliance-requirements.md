---
layout: Conceptual
title: Determine Multicloud Compliance Requirements for AWS and GCP - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-compliance-requirements
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
description: Learn about determining compliance requirements in multicloud environment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 1f9e02c2-46bd-0a59-37c3-0ce537bcb933
document_version_independent_id: aaab5043-5319-3d81-02a8-070b63d540e4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-compliance-requirements.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-compliance-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-compliance-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f165d140-854a-c858-a6e5-80c6aa153a3e
---

# Determine Multicloud Compliance Requirements for AWS and GCP - Microsoft Defender for Cloud | Microsoft Learn

## Overview

This article is part of a series that provides guidance as you design a cloud security posture management (CSPM) and cloud workload protection platform (CWPP) solution for multicloud resources with Microsoft Defender for Cloud. Identify and assess compliance requirements for Amazon Web Services (AWS) and Google Cloud Platform (GCP) environments, including default standards, available benchmarks, and custom assessments.

## Compliance planning goals

Identify compliance requirements in your organization as you design your multicloud solution.

## Get started with compliance requirements assessment

Defender for Cloud continually assesses your resource configuration against compliance controls and best practices in the standards and benchmarks applied in your subscriptions.

- By default, every subscription has the [Microsoft cloud security benchmark](/en-us/security/benchmark/azure/introduction) assigned. This benchmark contains Microsoft Azure security and compliance best practices based on common compliance frameworks.
- Amazon Web Services (AWS) standards include AWS Foundational Security Best Practices, the Center for Internet Security (CIS) AWS Foundations Benchmark v1.2.0, and the Payment Card Industry Data Security Standard (PCI DSS) v3.2.1.
- Google Cloud Platform (GCP) standards include GCP Default, GCP CIS benchmarks v1.1.0 and v1.2.0, GCP International Organization for Standardization (ISO) 27001, GCP National Institute of Standards and Technology (NIST) SP 800-53, and PCI DSS v3.2.1.
- By default, every subscription that contains the AWS connector has the AWS Foundational Security Best Practices assigned.
- Every subscription with the GCP connector has the GCP Default benchmark assigned.
- For AWS and GCP, the compliance monitoring freshness interval is 4 hours.

After you enable [security features](defender-for-cloud-introduction) in a Defender plan, you can add other compliance standards to the dashboard. Regulatory compliance is available when you enable at least one Defender plan on the subscription where the multicloud connector is located.

You can also create custom standards and assessments to align with your organizational requirements. For guidance, see [Custom standards and assessments for AWS](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/custom-assessments-and-standards-in-microsoft-defender-for-cloud/ba-p/3066575) and [Custom standards and assessments for GCP](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/custom-assessments-and-standards-in-microsoft-defender-for-cloud/ba-p/3251252).