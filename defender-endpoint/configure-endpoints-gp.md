---
layout: Conceptual
title: Onboard Windows devices to Microsoft Defender for Endpoint with Group Policy - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-endpoints-gp
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Group Policy to onboard and offboard Windows devices, configure sample collection, and verify Defender for Endpoint deployment.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-09-21T00:00:00.0000000Z
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: c0d7aca6-1b57-e82c-cdac-f2962c6b7de8
document_version_independent_id: c0d7aca6-1b57-e82c-cdac-f2962c6b7de8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-endpoints-gp.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-endpoints-gp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-endpoints-gp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: ae971fb1-e225-fa18-a253-20f032652c11
---

# Onboard Windows devices to Microsoft Defender for Endpoint with Group Policy - Microsoft Defender for Endpoint | Microsoft Learn

You can use Active Directory Domain Services (AD DS) Group Policy to onboard supported Windows client and Windows Server devices to Microsoft Defender for Endpoint at scale. This article explains how to deploy the onboarding package, configure sample collection, verify deployment, and offboard devices. Before you begin, review the deployment prerequisites and confirm that Group Policy is the appropriate deployment method for your environment.

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Prerequisites

- Review the [minimum requirements for Microsoft Defender for Endpoint](minimum-requirements) and [configure device connectivity](configure-device-connectivity).
- To download onboarding and offboarding packages, you need full access to Defender for Endpoint. The Microsoft Entra **Security Administrator** role grants this access. For more information, see [Assign basic permissions](basic-permissions).
- Install the Group Policy Management Console (GPMC), and make sure your account can create and edit Group Policy Objects (GPOs) and link them to the target site, domain, or organizational unit (OU). For more information, see [Group Policy Management Console](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console).
- Use current Windows Administrative Template files in your Central Store. Current templates are especially important for devices running Windows Server 2012 R2 or Windows Server 2016 with the unified Defender for Endpoint solution. For more information, see [Create and manage the Central Store for Group Policy Administrative Templates](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store).

To compare Group Policy with other deployment options, see [Identify Defender for Endpoint architecture and deployment methods](deployment-strategy).

## Onboard devices by using Group Policy

Download the onboarding package, create an immediate scheduled task, and deploy the task to the Windows devices that you want to onboard.

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the package:

    1. **Step 1: Select an operating system to start deployment**: Select the operating-system version group for the target devices. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
    2. If **Connectivity type** is available, select the connectivity method for your environment.
    3. For **Deployment method**, select **Group Policy**.
    4. Select **Download onboarding package**.
2. Extract the downloaded `.zip` file to a shared, read-only location that the target devices can access. The extracted package contains the `WindowsDefenderATPOnboardingScript.cmd` file.
3. Open the GPMC, right-click **Group Policy Objects**, and select **New**. Enter a name for the GPO, and then select **OK**.
4. Right-click the new GPO, and select **Edit**.
5. In the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Preferences** &gt; **Control Panel Settings**.
6. Right-click **Scheduled Tasks**, select **New**, and then select **Immediate Task (At least Windows 7)**.
7. On the **General** tab, configure the task:

    1. Under **Security options**, select **Change User or Group**.
    2. Enter `SYSTEM`, select **Check Names**, and then select **OK**. The account appears as `NT AUTHORITY\SYSTEM`.
    3. Select **Run whether user is logged on or not**.
    4. Select **Run with highest privileges**.
    5. Enter a descriptive task name, such as `Defender for Endpoint onboarding`.

    Note

    On Windows Server 2019 and later, if the Group Policy preference XML contains `NT AUTHORITY\Well-Known-System-Account`, replace that value with `NT AUTHORITY\SYSTEM`.
8. On the **Actions** tab, select **New**, and configure the action:

    1. For **Action**, select **Start a program**.
    2. For **Program/script**, enter the Universal Naming Convention (UNC) path to the shared `WindowsDefenderATPOnboardingScript.cmd` file. Use the file server's fully qualified domain name (FQDN) in the path.
    3. Select **OK**.
9. Select **OK**, and close the **Group Policy Management Editor**.
10. In the GPMC, link the GPO to the site, domain, or OU that contains the target devices. Test the GPO with a limited device group before you deploy it broadly.

For information about linking and validating GPOs, see [Group Policy Management Console](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console).

## Configure sample collection

Defender for Endpoint can collect files from onboarded devices when an analyst requests a file for deep analysis. Configure the sample collection policy to control whether devices can respond to these requests.

1. On the device where you manage Group Policy, copy the Defender for Endpoint administrative template files from the extracted onboarding package:

    - For a local Policy Definitions folder:
        - Copy `AtpConfiguration.admx` to `C:\Windows\PolicyDefinitions`.
        - Copy `AtpConfiguration.adml` to the applicable language folder, such as `C:\Windows\PolicyDefinitions\en-US`.
    - For a Central Store:
        - Copy `AtpConfiguration.admx` to `\\<forest-root>\SYSVOL\<forest-root>\Policies\PolicyDefinitions`.
        - Copy `AtpConfiguration.adml` to the applicable language folder, such as `\\<forest-root>\SYSVOL\<forest-root>\Policies\PolicyDefinitions\en-US`.
2. In the GPMC, right-click the GPO that you use for Defender for Endpoint settings, and select **Edit**.
3. In the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Windows Defender ATP**.

    Note

    **Windows Defender ATP** is the legacy name that appears in this administrative template.
4. Open **Enable or disable Sample collection**, select **Enabled**, select **Enable sample collection on machines**, and then select **OK**.

If you don't configure this policy, sample collection is enabled by default.

## Other recommended configuration settings

Onboarding connects devices to Defender for Endpoint, but it doesn't configure Microsoft Defender Antivirus or other endpoint protection features. Use the same GPO or separate GPOs to configure the security controls required by your organization.

### Update endpoint protection configuration

In Microsoft Defender Antivirus platform version 4.18.2208.0 and later, the **Turn off Windows Defender** policy no longer completely disables Defender Antivirus on onboarded devices running Windows Server 2012 R2 and later. Instead, the policy places Defender Antivirus in passive mode. If the policy is already enabled before you onboard the server, Defender Antivirus remains disabled. This behavior applies only to servers onboarded to Defender for Endpoint.

If you use a non-Microsoft antivirus solution, review [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility) before you configure antivirus mode. Otherwise, in the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus**, and set **Turn off Microsoft Defender Antivirus** to **Disabled** or **Not configured**. For Windows Server mode and `ForceDefenderPassiveMode` guidance, see [Configure Microsoft Defender Antivirus on Windows Server](microsoft-defender-antivirus-windows-server-configure).

Configure and test the following protections according to your organization's requirements:

- [Use Group Policy to configure Microsoft Defender Antivirus](use-group-policy-microsoft-defender-antivirus).
- [Configure cloud-delivered protection](cloud-protection-configure) and [sample submission](cloud-protection-microsoft-antivirus-sample-submission).
- [Configure attack surface reduction rules](attack-surface-reduction-rules-configure). Evaluate rules in audit mode before you enable blocking.
- [Detect and block potentially unwanted applications](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).
- [Schedule Microsoft Defender Antivirus scans](schedule-antivirus-scans).
- [Manage Microsoft Defender Antivirus security intelligence and product updates](manage-protection-updates-microsoft-defender-antivirus).

## Verify device onboarding

Group Policy doesn't report deployment status to Defender for Endpoint. Use Group Policy Results to confirm that the GPO applied, and then verify the device in the Defender portal.

1. On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines?category=all-devices, search for the device.
2. Open the device page, and verify that the device is onboarded and its sensor health state is active.

After the GPO is applied and the scheduled task runs, the device typically appears in the inventory within several minutes. Group Policy replication, policy refresh, and network connectivity can delay reporting.

To generate a test alert and confirm end-to-end reporting, see [Run a detection test on a newly onboarded device](run-detection-test). If the device doesn't appear or report as expected, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](troubleshoot-onboarding).

## Offboard devices using Group Policy

The offboarding package expires seven days after you download it. Defender for Endpoint rejects expired packages, and the expiration date appears in the package file name.

Important

Don't deploy onboarding and offboarding policies to the same device at the same time. Remove or unlink the onboarding GPO from the target devices before you deploy the offboarding GPO.

To offboard devices by using Group Policy, create a separate GPO for the offboarding task:

1. On the **Offboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/offboarding, configure the package:

    1. Select the operating-system version group for the target devices. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
    2. For **Deployment method**, select **Group Policy**.
    3. Select **Download package**, and then select **Download** in the confirmation dialog.
2. Extract the downloaded `.zip` file to a shared, read-only location that the target devices can access. The extracted package contains a file named `WindowsDefenderATPOffboardingScript_valid_until_YYYY-MM-DD.cmd`.
3. In the GPMC, create a GPO for offboarding, and edit the GPO.
4. In the **Group Policy Management Editor**, go to **Computer Configuration** &gt; **Preferences** &gt; **Control Panel Settings**.
5. Right-click **Scheduled Tasks**, select **New**, and then select **Immediate Task (At least Windows 7)**.
6. On the **General** tab, configure the task to:

    - Run as `NT AUTHORITY\SYSTEM`.
    - Run whether the user is logged on or not.
    - Run with highest privileges.
    - Use a descriptive name, such as `Defender for Endpoint offboarding`.
7. On the **Actions** tab, select **New**, and configure the action:

    1. For **Action**, select **Start a program**.
    2. For **Program/script**, enter the UNC path to the shared `WindowsDefenderATPOffboardingScript_valid_until_YYYY-MM-DD.cmd` file. Use the file server's FQDN in the path.
    3. Select **OK**.
8. Select **OK**, close the **Group Policy Management Editor**, and link the offboarding GPO to the target site, domain, or OU.

Offboarding stops the device from sending new detection, vulnerability, and security data to Defender for Endpoint. Historical data remains in the Defender portal until the configured retention period expires. The device profile, without data, remains in the device inventory for up to 180 days. For more information, see [Offboard devices](offboard-machines).