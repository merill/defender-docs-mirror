---
layout: Conceptual
title: Integration FAQ for Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/integration-faq
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
description: Frequently asked questions about integrating and using Microsoft Defender for Cloud in the Defender portal, including migration, compatibility, and feature questions.
ms.topic: faq
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9f9181fa-9c39-bee7-58c0-a59834dfa266
document_version_independent_id: 4d345b33-2e90-78ae-8433-27b5464409ee
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/integration-faq.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/integration-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/integration-faq.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/970f20f1-2f12-4aa9-9c95-c00fe1f5e722
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/432c4950-b799-4ed5-93d5-b9b2934edf7d
platformId: 5c6a485f-e27e-241a-d386-b163da6cb054
---

# Integration FAQ for Defender portal - Microsoft Defender for Cloud | Microsoft Learn

This article answers frequently asked questions about using Microsoft Defender for Cloud in the Defender portal, including integration, migration, and compatibility topics.

## Overview

### Who is eligible to test the new MDC capabilities in the Defender portal?

The expansion of MDC into the Defender portal is available for billed MDC customers with at least one Defender for Cloud plan enabled. Note: Once the opt-in is selected, it takes up to 24 hours for the data to populate.

Note

The new cloud features in the Defender portal are currently only supported in public/commercial clouds.

### Which environments are supported in the Defender portal?

Cloud security data experiences in the Defender portal support Azure, AWS, and GCP environments.

Onboarding and plan management in the Defender portal currently support Azure commercial environments only. Continue to use the Azure portal to onboard and configure AWS, GCP, and Azure national or sovereign cloud environments. GitHub is supported separately in public preview. For setup instructions, see [Create a GitHub connector](/en-us/security-exposure-management/create-github-connector).

### What are the risks associated with this move?

Viewing Defender for Cloud data in the Defender portal doesn't change your existing plan configuration.

Before moving plan management for an Azure environment to the Defender portal, review [what changes when managing cloud security plans in the Defender portal](plan-management-changes-defender-portal) and the [known limitations](known-limitations). Resource-level plan configurations aren't preserved during migration and are replaced by settings applied at the management-group or subscription scope.

### What happens to MDC in the Azure portal? Is MDC being deprecated from the Azure portal?

Defender for Cloud isn't being deprecated from the Azure portal. The Azure and Defender portals continue to work in parallel.

For Azure commercial environments, you can now connect environments and manage Defender for Cloud plans in the Defender portal. Continue to use the Azure portal for AWS, GCP, unsupported Azure environments, and management capabilities that aren't yet available in the Defender portal, including security policy configuration, continuous export, and workflow automation.

After an Azure environment moves to Defender-based plan management, its plan configuration becomes view-only in the Azure portal.

### Does using Defender for Cloud in the Defender portal change my existing configuration?

Viewing cloud security data in the Defender portal doesn't change your Defender for Cloud plans.

For more information, see [What changes when managing cloud security plans in the Defender portal](plan-management-changes-defender-portal). Existing resource-level plan configurations aren't preserved, and billing for the migrated subscription uses Defender Workload Units.

### Is there a feature parity list for all the features expanding into the Defender portal?

Yes, a feature parity list is available in the official Defender for Cloud documentation on Microsoft Learn here: [Azure portal vs Defender portal feature comparison](../azure-portal-vs-defender-portal-comparison).

### What if I only use the Azure portal and not the Defender portal?

You can continue to use the Azure portal. Azure environments that haven't moved to Defender-based plan management continue to use their existing Azure portal configuration and billing model during the transition period.

After an environment moves to Defender-based plan management, plan settings for that environment are managed in the Defender portal and appear as view-only in the Azure portal.

## Billing implications

### Is there any billing impact from using the Defender portal?

When an Azure subscription moves to Defender-based plan management, its billing uses [Defender Workload Units](estimate-track-costs). Subscriptions that haven't moved continue to use their existing billing model during the transition period.

### What is a Defender Workload Unit?

A Defender Workload Unit (DWU) is a unified unit for measuring Defender for Cloud usage across supported protected workloads. Workload types use defined counting models, and the resulting DWU usage is used to estimate costs, calculate billing, and report cloud security costs.

For more information, see [Estimate and track Cloud security cost](estimate-track-costs).

### Is moving to Defender Workload Unit billing mandatory?

Not at the start of the transition. The move is performed per Azure subscription. Subscriptions that haven't moved to Defender-based plan management can continue to use their existing billing model during the transition period.

## Azure plan management

### What changes when I move an Azure environment to Defender-based plan management?

After an Azure environment moves:

- Plan configuration is managed in the Defender portal.
- Plan configuration becomes view-only in the Azure portal.
- Resource-level plan configurations aren't preserved.
- The migrated subscription uses Defender Workload Unit billing.
- Cloud security cost becomes available in the Defender portal, in addition to the Azure portal.

For the complete procedure, see [Manage Defender for Cloud plans in the Defender portal](manage-plans-defender-portal).

## Customer impact & experience

### What specific customer workflows are being affected by this move? (for example, threat detection, incident response, reporting or all)

The expansion of Defender for Cloud into the Defender portal enhances and unifies existing workflows. For example, SOC teams can now access all the cloud information they need to investigate cloud-related incidents, end to end. Vulnerability management admins can view vulnerabilities from cloud resources such as virtual machines and containers in parallel with the endpoint data. Information security architects now have a comprehensive view of their cloud security posture, alongside devices, SaaS apps, and data, enabling faster remediation of security recommendations and a complete picture of their organization's overall posture.

### Are there any known limitations to this expansion?

Yes, while Defender for Cloud is expanding in the Defender portal for an improved security experience, there are known limitations during the public preview phase. These are covered in a dedicated article on the Microsoft Learn platform, here: [Known limitations](known-limitations).

## Technical integration & operations

### Access & permissions

#### Will existing Azure MDC role-based access control permissions carry over to the new experience in the Defender portal, or do we need to reassign access?

Defender for Cloud in Azure and Defender portals operate with different role-based access control models: Defender for Cloud in Azure utilizes Azure role-based access control, while the Defender portal employs a combination of Entra ID global roles and Unified role-based access control. Here's the difference between the two:

- Azure role-based access control manages access controls at the Azure resource level, including subscriptions and resource groups.
- Unified role-based access control enables more granular permissions within the Defender portal, allowing assignment of roles specific to security tasks and cloud scopes across Defender solutions.

With the enhanced experience in the Defender portal, security teams can now access critical security data without requiring extensive permissions to underlying cloud resources. This eliminates a long-standing challenge in the Azure portal, where broad Azure access was necessary just to view security information—often causing friction with cloud operations teams. In addition, we can now group together cloud accounts into scopes and use them to grant access to relevant security teams so your relevant teams can review and act on security findings without requiring full platform access. This also enables non-Azure users—such as AWS or GCP admins—to manage their security content in Defender without needing Azure subscription rights, making multicloud operations easier and more secure.

Defender uses its own permission model called Unified role-based access control, designed specifically for security tasks. It doesn't rely on Azure role-based access control roles. If users need access to both the Azure portal and the Defender portal, they'll require two permissions: their existing Azure role-based access control role and a new Unified role-based access control role for Defender. For organizations that want to align permissions across systems, public APIs are available to automate role assignments. This approach ensures least-privilege access, improves governance, and streamlines security operations across multicloud environments.

### Multitenant & environment handling

#### If I have an MDC multitenant environment with Azure Lighthouse, how will this environment surface in the new Defender portal?

Microsoft Defender for Cloud expands within the Defender portal to provide incident detection and response for multitenant environments through the existing multitenant Organizations (MTO) experience. At this stage, posture management features—such as recommendations, attack paths, and cloud inventory—aren't yet available for multitenant scenarios in the Defender portal.

**Customers can continue to use Azure Lighthouse for multi-tenant posture management and operations, in parallel with the Defender portal.** This approach ensures that organizations retain full posture management capabilities while benefiting from the unified incident management and response features available in the Defender portal.

As we build and enhance MTO capabilities in future releases, customers see expanded support for multitenant posture management and additional experiences directly within the Defender portal.

### Synchronization & data consistency

#### After enabling the preview, how quickly can customers start seeing their data?

The initial synchronization can take up to 24-hours.

#### If I remediate recommendations in the Defender portal, will those changes immediately reflect in the Azure portal or is there a delay? If there is, how long will it take to show up in Azure portal?

In the short term, security recommendations resolved in the Azure portal will be reflected as resolved in the Defender portal within 2 hours. We're working to improve this time so that users don't experience any delay

#### Will the count of healthy and unhealthy resources be consistent across the Azure and the Defender portal? If not, what explains the difference?

Customers might notice differences when using Defender for Cloud in the Defender portal. With this expansion, we're exposing customers with the discovery of their complete environment and hence, the count can be different. This applies to the Secure Score, security recommendations, and the number of discovered resources in the environment.

## Feature availability & roadmap

### If I only use Foundational CSPM and have other Defender Plans enabled, such as Defender for Storage, will I be able to see Foundational CSPM data in the new portal?

Yes, security recommendations provided by the Foundational CSPM plan appears for any subscription with at least one paid plan.

### I can see recommendation ownership via Governance feature. Will the Governance feature be available in the Defender portal?

Governance assignments created manually or automatic will continue to work, and the assignment status including the relevant owner and due date will appear in the Defender portal. However, editing operations such as owner and due date changes will still be done via the Azure portal. In the future, we plan to introduce improved mobilization capabilities to allow security teams to operate and delegate the remediation effort directly to the Defender portal.

## Operations

### How will the transition impact ongoing investigation, alerts or integrations?

With cloud security posture data now integrated into the Defender portal, SOC teams gain a unified experience for investigating and responding to cloud-related alerts and incidents. Previously, investigations required switching to the Azure portal to gather resource details, creating inefficiencies, and gaps in visibility. Now, all posture signals and metadata are available directly within Defender, eliminating tool-hopping and enabling faster, more informed decisions. The new cloud asset inventory provides complete visibility into resources and their posture, while exposure insights—such as the exposure graph—deliver a 360-degree view of each asset. This integration empowers SOC teams to correlate alerts with posture data instantly, streamline workflows, and strengthen incident response.

## Extracting identifiers for support cases

When working with Microsoft Defender for Cloud support cases, you often need to provide specific identifiers for assets, vulnerabilities, initiatives, and environments. Without proper resource identifiers, support teams can't effectively troubleshoot or escalate customer issues.

### What identifiers do I need for support cases?

You might need to extract the following types of identifiers from the Defender portal:

- **Asset IDs** - for specific cloud resources
- **Vulnerability IDs** - for security vulnerabilities (CVEs, Microsoft vulnerability IDs)
- **Initiative IDs** - for compliance initiatives and standards
- **Environment IDs** - for cloud scope and environment identification

### How do I extract Asset IDs from recommendations?

**Method 1: From Cloud Assets Recommendations**

1. Navigate to **Microsoft Defender portal** &gt; **Exposure Management** &gt; **Recommendations** &gt; **Cloud Assets** tab.
2. Locate the recommendation containing the asset you need to identify.
3. Select the **exposed asset** in the recommendation panel.
4. In the asset details, look for the **Asset ID** field.
5. Copy the identifier using the copy button.

**Method 2: From Cloud Infrastructure Asset Inventory**

1. Navigate to **Microsoft Defender portal** &gt; **Assets** &gt; **Cloud infrastructure**.
2. Use filters to locate the specific asset (environment, workload type, or search by name).
3. Select the asset name to open detailed information.
4. In the asset details panel, locate and copy the **Asset ID**.

Note

If you're referring to an Azure resource be sure to include the listed **Native ID**

### How do I extract Vulnerability IDs?

1. Navigate to **Microsoft Defender portal** &gt; **Exposure Management** &gt; **Recommendations**
2. In the Cloud Assets tab, filter by **Vulnerabilities** category on the left navigation.
3. Select a vulnerability-related recommendation.
4. In the recommendation side panel, look for:
    - **Associated CVEs** tab or section
    - **Vulnerability details** with specific identifiers
    - **CVSS scores** and vulnerability classifications
5. Select individual vulnerabilities to get detailed information including:
    - Full CVE identifier (for example, CVE-2023-1234)
    - Microsoft vulnerability ID (if applicable)
    - Package-specific vulnerability identifiers

### How do I extract Initiative IDs?

1. Navigate to **Exposure Management** &gt; **Recommendations**.
2. Select any recommendation.
3. In the recommendation side panel, go to **Related initiatives**.
4. This shows, which initiatives the recommendation belongs to.
5. Each initiative displays its name and identifier.
6. Copy the initiative ID associated with the specific recommendation.

### How do I find Environment IDs for Cloud Scopes (preview)?

1. Navigate to **Microsoft Defender portal** &gt; **Assets** &gt; **Cloud**.
2. Check the scope filter dropdown - the environment filter lists all environment identifiers.
3. Select a scope and then choose the environment filter to see detailed information including all environment IDs within that scope.