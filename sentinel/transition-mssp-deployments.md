---
layout: Conceptual
title: Transition MSSP-managed deployments to Microsoft Defender | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-mssp-deployments
breadcrumb_path: breadcrumb/toc.json
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
description: Learn how managed security service providers can update content deployments, delegated access, and permissions when transitioning from Microsoft Sentinel to ISOC in Microsoft Defender.
author: mberdugo
ms.author: monaberdugo
ms.localizationpriority: high
ms.collection:
- m365-security
- m365solution-getstarted
- highpri
- tier1
- usx-security
- msftsolution-secops
ms.topic: how-to
ai-usage: ai-assisted
ms.date: 2026-11-16T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1032
locale: en-us
document_id: 2ca0f647-cd9a-4c13-e2e6-83ed4b04ff1a
document_version_independent_id: 02cd359a-c7af-81e7-adfe-31750949bcc6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-mssp-deployments.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-mssp-deployments
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-mssp-deployments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 956c4e0a-ae22-00b7-a23c-72800c52e399
---

# Transition MSSP-managed deployments to Microsoft Defender | Microsoft Learn

Managed security service providers (MSSPs) often manage detections, workbooks, automation, and access across multiple customer tenants.

When transitioning existing Microsoft Sentinel deployments to Integrated Security Operations Center (ISOC) in Microsoft Defender, MSSPs must update their content deployment processes and validate access to ensure that security operations continue to function across customer environments.

This article describes the operational considerations and validation steps for transitioning MSSP-managed deployments.

Note

ISOC is in preview. Capabilities and availability might change during the preview period.

## Prerequisites

Before transitioning MSSP-managed deployments:

- Ensure that each customer tenant is [eligible for ISOC](/en-us/defender-xdr/isoc-overview).
- Identify existing Microsoft Sentinel analytics rules, workbooks, automation, and other content managed by the MSSP.
- Identify the content distribution profiles, CI/CD pipelines, and deployment definitions used across customer tenants.
- Verify that the MSSP has the required delegated access and permissions in each customer tenant.
- Identify any content managed jointly by the MSSP and the customer.
- If you use [Tenant Governance (GDAP)](/en-us/defender-xdr/governance-relationships), ensure that you've adopted Unified RBAC.

## Update content deployment processes

Review and update the processes used to deploy and manage content across customer tenants.

### Update content distribution profiles

Update content distribution profiles to deploy content that uses Microsoft Defender Advanced Hunting instead of Microsoft Sentinel workspace-based content.

Ensure that the updated profiles deploy:

- Custom detections instead of Microsoft Sentinel analytics rules.
- Workbooks that use Advanced Hunting data sources.
- Updated automation and Logic App playbooks.

For more information, see:

- [Convert analytics rules to custom detections](transition-custom-detections)
- [Update workbooks to use Advanced Hunting data](update-workbooks-advanced-hunting-data)
- [Update Logic App playbook automation](transition-logic-app-playbooks)

### Update CI/CD pipelines and deployment definitions

If you use CI/CD pipelines or infrastructure as code to deploy content across customer tenants, update the repositories, deployment pipelines, and automation processes.

Ensure that deployment definitions use the converted detections and Advanced Hunting-based content model consistently across customer tenants.

Validate that the updated deployment processes deploy the expected content before reducing ingestion into Microsoft Sentinel.

## Validate delegated access and permissions

MSSPs must have the required delegated access and permissions in each customer tenant to manage and validate the transitioned content.

Before beginning migration activities:

1. Review the delegated access configured for each customer tenant.

    Note

    If you use Tenant Governance (GDAP) and assign permissions through ARM, migrate to Unified RBAC.
2. Verify that the MSSP has the required permissions for the Defender workloads and data used by the transitioned content.
3. Review user and group access to identify any permissions that must be updated.
4. Use SOC Optimization recommendations to identify potential access gaps.
5. Resolve identified access gaps and confirm that analysts can access the required data after the transition.

For more information about updating permissions, see [Update permissions and roles with Unified RBAC](transition-unified-rbac).

Important

Unified RBAC is mandatory when you enable ISOC. MDE device groups aren't currently supported with Tenant Governance (GDAP).

## Define shared content ownership

In some customer environments, both the MSSP and the customer manage detections, workbooks, or automation.

Before transitioning these environments, establish ownership and change-control processes to avoid conflicting updates.

Review the following considerations:

- **Content ownership**: Identify whether the MSSP or customer is responsible for managing each detection, workbook, and automation resource.
- **Change control**: Establish how changes to shared content are reviewed and applied.
- **Deployment responsibilities**: Determine who is responsible for updating and validating content deployments.
- **Ongoing management**: Confirm how the MSSP and customer coordinate changes after the transition.

## Validate MSSP-managed deployments

Before reducing data ingestion into Microsoft Sentinel for a customer tenant, verify that the transitioned content and access configurations work as expected.

Complete the following validation steps for each customer tenant:

1. **Validate content distribution profiles.**

    Confirm that content distribution profiles deploy the converted custom detections, Advanced Hunting-based workbooks, and updated automation.
2. **Validate CI/CD pipelines and deployment definitions.**

    Confirm that repositories, pipelines, and deployment definitions have been updated to deploy content that uses the Advanced Hunting data model.
3. **Validate delegated access and permissions.**

    Verify that the MSSP has the required delegated access and Defender workload permissions in the customer tenant.
4. **Validate shared content ownership.**

    Confirm that ownership and change-control responsibilities are defined for content managed jointly by the MSSP and customer.
5. **Validate user and group access.**

    Confirm that access reviews are complete, identified gaps are resolved, and analysts retain access to the data required for security operations.

Important

Complete the applicable content migration and validation steps before reducing ingestion into Microsoft Sentinel. Ensure that all resources dependent on a table have been updated to use the corresponding Advanced Hunting data and validated.