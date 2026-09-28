---
layout: Conceptual
title: Validate sensor deployment on domain controllers - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/test-sensor
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
description: Validate your Microsoft Defender for Identity sensor deployment by checking the Identity Security dashboard, entity pages, advanced hunting, and alert functionality.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bdbd79cb-a6d9-c992-a681-619c811465fd
document_version_independent_id: bdbd79cb-a6d9-c992-a681-619c811465fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/test-sensor.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/test-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/test-sensor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 958d0c23-8abd-cb0d-deb1-c937e70deb0e
---

# Validate sensor deployment on domain controllers - Microsoft Defender for Identity | Microsoft Learn

Use the following procedures to check that your sensors are working.

Note

The first time you activate the sensor on your domain controller, it might take up to an hour for the sensor to show as **Running** on the **Sensors** page. Subsequent activations show within five minutes.

## Check the Identity Security dashboard

1. In the Defender portal, select **Identities** &gt; **Dashboard**, and review the details shown. Check for expected results from your environment. For more information, see [Identity Security dashboard](../dashboard).

## Confirm entity data in the Defender portal

1. In the Defender portal, select **Assets &gt; Devices**, and select the machine for your new sensor. Confirm that Defender for Identity events appear on the device timeline.
2. Select **Assets &gt; Users** and check for users from a newly onboarded domain. You can also use the global search to find specific users. Confirm that user details pages include **Overview**, **Observed in organization**, and **Timeline** data.
3. Use the global search to find a user group, or pivot from a user or device details page where group details are shown. Confirm group membership details, group users, and group timeline data.

    If no event data is found on the group timeline, you might need to create some manually. For example, add and remove users from the group in Active Directory.

For more information, see [Investigate assets](../investigate-assets).

## Verify data in advanced hunting tables

Use advanced hunting queries to confirm that sensor data is written to the expected tables.

1. In the Defender portal's **Advanced hunting** page, run the following queries to verify that data appears in the expected tables:

    ```kusto
    IdentityDirectoryEvents
    | where TargetDeviceName contains "DC_FQDN" // insert domain controller FQDN
    
    IdentityInfo 
    | where AccountDomain contains "domain" // insert domain
    
    IdentityQueryEvents 
    | where DeviceName contains "DC_FQDN" // insert domain controller FQDN
    ```

For more information, see [Advanced hunting in the Microsoft Defender portal](/en-us/microsoft-365/security/defender/advanced-hunting-microsoft-defender).

## Test Identity Security Posture Management (ISPM) recommendations

We recommend simulating risky behavior in a test environment to trigger supported assessments and verify that the assessments appear as expected. For example:

1. Trigger a new **Resolve unsecure domain configurations** recommendation by setting your Active Directory configuration to a noncompliant state, and then returning it to a compliant state. For example, run the following commands:

    **To set a non-compliant state**

    ```powershell
    Set-ADObject -Identity ((Get-ADDomain).distinguishedname) -Replace @{"ms-DS-MachineAccountQuota"="10"}
    ```

    **To return it to a compliant state**:

    ```powershell
    Set-ADObject -Identity ((Get-ADDomain).distinguishedname) -Replace @{"ms-DS-MachineAccountQuota"="0"}
    ```

    **To check your local configuration**:

    ```powershell
    Get-ADObject -Identity ((Get-ADDomain).distinguishedname) -Properties ms-DS-MachineAccountQuota
    ```
2. In Microsoft Secure Score, select **Recommended Actions** to check for a new **Resolve unsecure domain configurations** recommendation. You might want to filter recommendations by the **Defender for Identity** product.

For more information, see [Microsoft Defender for Identity's security posture assessments](../security-assessment)

## Test alert functionality

Simulate risky activity in a test environment to verify that alerts are triggered as expected. For example:

1. Tag an account as a honeytoken account, and then try signing in to the honeytoken account against the activated domain controller.
2. Create a suspicious service on your domain controller.
3. Run a remote command on your domain controller as an administrator signed in from your workstation.
4. Verify that the expected alerts appear in the Defender portal.

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender](../manage-security-alerts).

## Test remediation actions

Test remediation actions on a test user. For example:

1. In the Defender portal, go to the user details page for a test user.
2. From the **Options** menu, select any of the available remediation actions.
3. Check Active Directory for the expected activity.

For more information, see [Remediation actions in Microsoft Defender for Identity](../remediation-actions).