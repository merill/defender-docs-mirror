---
layout: Conceptual
title: Migrate to Microsoft Defender for Endpoint from non-Microsoft endpoint protection - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/switch-to-mde-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Move to Microsoft Defender for Endpoint, which includes Microsoft Defender Antivirus for your endpoint protection solution.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365solution-migratetomdatp
- m365solution-overview
- m365initiative-defender-endpoint
- highpri
- tier1
ms.topic: solution-overview
ms.custom: migrationguides
ms.date: 2024-09-21T00:00:00.0000000Z
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho, yongrhee
ms.subservice: onboard
locale: en-us
document_id: 290fa19d-0f14-5cea-180b-45d2c3699968
document_version_independent_id: 290fa19d-0f14-5cea-180b-45d2c3699968
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/switch-to-mde-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: switch-to-mde-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/switch-to-mde-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9172448a-be6e-828e-87bb-50e98fc86ec2
---

# Migrate to Microsoft Defender for Endpoint from non-Microsoft endpoint protection - Microsoft Defender for Endpoint | Microsoft Learn

If you're ready to move from a non-Microsoft endpoint protection solution to [Microsoft Defender for Endpoint](microsoft-defender-endpoint), or you're interested in what all is involved in the process, use this article as a guide. This article describes the overall process of moving to [Defender for Endpoint Plan 1 or Plan 2](microsoft-defender-endpoint). The following image depicts the migration process at a high level:

[![Diagram depicting the process of migrating to Defender for Endpoint](media/nonms-mde-migration.png)](media/nonms-mde-migration.png#lightbox)

When you migrate to Defender for Endpoint, you begin with your non-Microsoft antivirus/antimalware protection in active mode. Then, you configure Microsoft Defender Antivirus in passive mode, and configure Defender for Endpoint features. Then, you onboard your organization's devices, and verify that everything is working correctly. Finally, you remove the non-Microsoft solution from your devices.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## The migration process

[![The MDE migration process](media/phase-diagrams/migration-phases.png)](media/phase-diagrams/migration-phases.png#lightbox)

The process of migrating to Defender for Endpoint can be divided into three phases, as described in the following table:

| Phase | Description |
| --- | --- |
| [Prepare for your migration](switch-to-mde-phase-1) | During [the **Prepare** phase](switch-to-mde-phase-1): 1. Update your organization's devices.2. Get Defender for Endpoint Plan 1 or Plan 2.3. Plan roles and permissions for your security team, and grant them access to the Microsoft Defender portal.4. Configure your device proxy and internet settings to enable communication between your organization's devices and Defender for Endpoint.5. Get baseline performance data for the devices that are onboarded to Defender for Endpoint. |
| [Set up Defender for Endpoint](switch-to-mde-phase-2) | During [the **Setup** phase](switch-to-mde-phase-2): 1. Enable/reinstall Microsoft Defender Antivirus, and make sure it's in passive mode on devices.2. Configure your Defender for Endpoint Plan 1 or Plan 2 capabilities.3. Add Defender for Endpoint to the exclusion list for your existing solution.4. Add your existing solution to the exclusion list for Microsoft Defender Antivirus.5. Set up your device groups, collections, and organizational units. |
| [Onboard to Defender for Endpoint](switch-to-mde-phase-3) | During [the **Onboard** phase](switch-to-mde-phase-3): 1. Onboard your devices to Defender for Endpoint.2. Run a detection test to confirm that onboarding was successful.3. Confirm that Microsoft Defender Antivirus is running in passive mode.4. Get updates for Microsoft Defender Antivirus.5. Uninstall your existing endpoint protection solution.6. Make sure that Defender for Endpoint working correctly. |