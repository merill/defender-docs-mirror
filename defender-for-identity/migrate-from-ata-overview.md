---
layout: Conceptual
title: Migrate from Advanced Threat Analytics - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/migrate-from-ata-overview
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to move an existing Advanced Threat Analytics installation to Microsoft Defender for Identity.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d8193840-fc29-b20f-94f9-eed077bc2615
document_version_independent_id: d8193840-fc29-b20f-94f9-eed077bc2615
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/migrate-from-ata-overview.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: migrate-from-ata-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/migrate-from-ata-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/58f888a4-3847-4473-ba35-882e789f0dbe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/314a9abc-91dd-4683-8691-43005e929bb8
platformId: df580881-1dac-e9b7-d5c2-5f6c5533dfe8
---

# Migrate from Advanced Threat Analytics - Microsoft Defender for Identity | Microsoft Learn

Important

Advanced Threat Analytics (ATA) has reached end of life. Mainstream support ended on January 12, 2021, and extended support ended on January 13, 2026. ATA no longer receives updates of any kind, including security updates, and is no longer supported by Microsoft. For more information, see [Advanced Threat Analytics 1.X lifecycle](/en-us/lifecycle/products/advanced-threat-analytics-1x).

We strongly recommend migrating to Microsoft Defender for Identity as soon as possible. For migration guidance, see [Migrate from Advanced Threat Analytics (ATA) to Microsoft Defender for Identity](/en-us/defender-for-identity/migrate-from-ata-overview).

This article describes how to migrate from an existing ATA installation to a Microsoft Defender for Identity sensor. Before you begin, make sure your environment meets the [Defender for Identity prerequisites](prerequisites). The migration includes the following steps:

- Review and confirm Defender for Identity service prerequisites
- Document your existing ATA configuration
- Plan your migration
- Set up and configure your Defender for Identity service
- Perform post-migration checks and verifications
- Decommission ATA

ATA is a standalone on-premises solution with multiple components, such as the ATA Center that requires dedicated hardware on-premises.

Defender for Identity is a cloud-based security solution that uses your on-premises Active Directory signals. Defender for Identity is highly scalable and is frequently updated.

In contrast to the ATA Lightweight Gateway, the Defender for Identity sensor also uses data sources such as Event Tracing for Windows (ETW) enabling Defender for Identity to deliver extra detections. Defender for Identity also provides:

- Support for [multi-forest environments](deploy/multi-forest)
- [Microsoft Secure Score posture assessments](/en-us/defender-for-identity/security-assessment)
- Direct integrations with other services like Microsoft Defender for Cloud Apps and Microsoft Entra for a hybrid view of what's taking place in both on-premises and hybrid environments
- And more

Defender for Identity also uses the Microsoft 365 security portfolio to automatically analyze cross-domain threat data, building a complete picture of each attack in a single dashboard.

Important

This migration guide is designed for Defender for Identity sensors only, and not standalone sensors.

While you can migrate to Defender for Identity from any ATA version, your ATA data isn't migrated. Therefore, we recommend that you plan to retain your ATA Data Center and any alerts required for ongoing investigations until all ATA alerts are closed or remediated.

Note

The final release of ATA is [Update 3 for Microsoft Advanced Threat Analytics 1.9](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). ATA ended Mainstream Support on January 12, 2021. Extended Support will continue until January 2026. For more information, read [End of mainstream support for Advanced Threat Analytics](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

## Prerequisites

To migrate from ATA to Defender for Identity, you must have an environment and domain controllers that meet Defender for Identity sensor requirements. For more information, see [Microsoft Defender for Identity prerequisites](prerequisites).

Make sure that all the domain controllers you plan to use have sufficient internet access to the Defender for Identity service. For more information, see [Configure endpoint proxy and internet connectivity settings](configure-proxy).

## Plan your migration

Before starting the migration, gather all of the following information:

- **Account details for your [Directory Services](directory-service-accounts) account**.
- **Syslog [notification settings](/en-us/defender-for-identity/notifications)**.
- **Email [notification settings](notifications)**.
- **All [ATA role group memberships](/en-us/advanced-threat-analytics/ata-role-groups)**.
- **[VPN integration details](vpn-integration)**.
- **Alert exclusions**: Exclusions are not transferable from ATA to Defender for Identity, so details of each exclusion are required to [replicate the exclusions as Defender for Identity](exclusions) in Microsoft Defender.
- **Account details for entity tags**: If you don't already have dedicated entity tags, create new ones for use with Defender for Identity. For more information, see [Defender for Identity entity tags in Microsoft Defender](entity-tags).
- **A complete list of all entities, such as computers, groups, or users, that you want to manually tag as *Sensitive* entities**: For more information, see [Defender for Identity entity tags in Microsoft Defender](entity-tags).
- **[Report scheduling and classic reports](/en-us/defender-for-identity/classic-reports)**: Including a list of all reports and scheduled timing.

Caution

Don't uninstall the ATA Center until all ATA Gateways are removed. Uninstalling the ATA Center with ATA Gateways still running leaves your organization exposed with no threat protection.

## Move to Defender for Identity

Use the following steps to migrate to Defender for Identity:

1. [Create your new Defender for Identity workspace](deploy-defender-identity#start-using-microsoft-defender-xdr).
2. Uninstall the ATA Lightweight Gateway on all domain controllers.
3. Install the Defender for Identity Sensor on all domain controllers:

    1. [Download and install the Defender for Identity sensor](deploy/install-sensor) on your domain controllers.
4. [Configure the your Defender for Identity sensor](configure-sensor-settings).

After the migration is complete, allow two hours for the Defender for Identity sensor initial synchronization to complete before starting validation tasks.

## Validate your migration

In Microsoft Defender, check the following areas to validate your migration:

- Review any [Defender for Identity health alerts](health-alerts) for signs of service issues.
- Review Defender for Identity [sensor error logs](troubleshooting-using-logs) for any unusual errors.

## Post-migration activities

After completing your migration to Defender for Identity, do the following to clean up your legacy ATA resources:

1. Make sure that you've recorded or remediated all existing ATA alerts. Existing ATA security alerts aren't imported to Defender for Identity with the migration.
2. Do one or both of the following:

    - **Decommission the ATA Center**: We recommend keeping ATA data online for a period of time.
    - **Back up Mongo DB**: If you want to keep the ATA data indefinitely. For more information, see [Backing up the ATA database](/en-us/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).