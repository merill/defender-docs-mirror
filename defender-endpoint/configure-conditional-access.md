---
layout: Conceptual
title: Configure Conditional Access with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-conditional-access
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Microsoft Defender for Endpoint device risk with Microsoft Intune compliance policies and Microsoft Entra Conditional Access to protect resources.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-09-21T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e1864276-3a19-b260-e2f7-30baef1a5158
document_version_independent_id: e1864276-3a19-b260-e2f7-30baef1a5158
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-conditional-access.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-conditional-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-conditional-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ecdb6f48-e008-e463-4689-31b237a7e203
---

# Configure Conditional Access with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

You can use Microsoft Defender for Endpoint device-risk signals with Microsoft Intune compliance policies and Microsoft Entra Conditional Access. Devices that exceed your selected risk threshold are marked as noncompliant, and Conditional Access can block them from organizational resources.

The configuration applies to Intune-enrolled Windows devices that are onboarded to Defender for Endpoint. Before you begin, review the licensing, enrollment, and role requirements in Prerequisites.

## Prerequisites

Make sure your environment meets the following requirements:

Warning

Create an Intune compliance policy and confirm that at least one test device reports as compliant before you enable the Conditional Access policy. Without a working compliance policy, Conditional Access can't evaluate device compliance as intended and might block access unexpectedly.

- **Licenses**: A Microsoft Defender for Endpoint subscription, a Microsoft Intune subscription, and a Microsoft Entra ID P1 or P2 license for Conditional Access.
- **Microsoft Intune**: Intune is a separate product that isn't part of Defender for Endpoint and isn't included in all subscriptions. You need a subscription that includes Intune, or you can buy it separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
- **Devices**: Windows 10 or later devices that are registered with Microsoft Entra ID, enrolled in Intune, and onboarded to Defender for Endpoint. Microsoft Entra registered devices are supported when they're enrolled in Intune. To enroll devices, use [Windows automatic enrollment](/en-us/intune/intune-service/enrollment/windows-enroll#enable-windows-automatic-enrollment) or have users [enroll their Windows devices in Intune](/en-us/intune/intune-service/user-help/enroll-windows-10-device). For device identity planning, see [Plan your Microsoft Entra device deployment](/en-us/entra/identity/devices/plan-device-deployment).

Use the following roles or equivalent custom permissions:

- **Microsoft Defender portal**: Security Administrator in Microsoft Entra ID or the **Manage security settings in Windows Security Center** permission in Defender for Endpoint. For more information, see [Permission options](user-roles#permission-options).
- **Microsoft Intune admin center**: Endpoint Security Manager. An equivalent custom role requires the permissions specified in [Configure Microsoft Defender for Endpoint with Intune](/en-us/intune/device-security/microsoft-defender/configure-integration).
- **Microsoft Entra admin center**: [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Configure device risk-based Conditional Access

Complete the following steps to use Defender for Endpoint device risk in Conditional Access:

### Step 1: Turn on the Microsoft Intune Connection

Follow the service-connection instructions in [Connect Defender for Endpoint to Intune](/en-us/intune/device-security/microsoft-defender/configure-integration#connect-defender-for-endpoint-to-intune).

On the **Other options** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, verify that **Microsoft Intune Connection** is ![](media/toggle-on.png)**On**. If you change the setting, select **Save preferences**.

On the **Endpoint security | Defender for Endpoint** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/atp](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/atp), verify that **Connection status** is **Enabled**. The status can take up to 15 minutes to update.

### Step 2: Turn on the Defender for Endpoint integration in Intune

Follow [Configure integration settings](/en-us/intune/device-security/microsoft-defender/configure-integration#configure-integration-settings). On the **Endpoint security | Microsoft Defender for Endpoint** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/atp](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/atp), verify the following settings:

- **Connection status** is **Enabled**.
- In the **Compliance policy evaluation** section, verify **Connect Windows devices to Microsoft Defender for Endpoint** is **On**.

### Step 3: Create and assign the compliance policy in Intune

Follow [Create and assign a compliance policy to set the device risk level](/en-us/intune/device-security/microsoft-defender/configure-integration#create-and-assign-compliance-policy-to-set-device-risk-level). Use the following Defender for Endpoint-specific settings:

- **Platform**: Select **Windows 10 and later**.
- **Profile type**: If this option is available, select **Windows 10/11 compliance policy**.
- **Compliance settings**: Expand **Microsoft Defender for Endpoint**, and set **Require the device to be at or under the machine risk score**to the maximum risk level that your organization permits:
    - **Clear**: This level is the most secure. The device cannot have any existing threats and still access organizational resources. If any threats are found, the device is evaluated as noncompliant.
    - **Low**: The device is compliant if only low-level threats exist. Devices with medium or high threat levels are not compliant.
    - **Medium**: The device is compliant if the threats found on the device are low or medium. If high-level threats are detected, the device is determined as noncompliant.
    - **High**: This level is the least secure and allows all threat levels. Use it only when you want to report risk without making devices noncompliant based on the threat level.
- **Actions for noncompliance**: Configure the timing and actions appropriate for your organization. Intune adds **Mark device noncompliant** by default, but you can change its schedule and add other actions.
- **Assignments**: Start with a test group. After you validate device compliance results, expand the assignment to the intended users or devices.

Create the policy, and confirm that test devices report the expected status before you configure Conditional Access.

### Step 4: Create a Microsoft Entra Conditional Access policy

Tip

Create the policy in **Report-only** mode first. A policy that requires compliance for all users and resources can block access if its scope or exclusions are incorrect.

Follow [Require device compliance with Conditional Access](/en-us/entra/identity/conditional-access/policy-all-users-device-compliance). On the **Conditional Access | Policies** page in the Microsoft Entra admin center at [https://entra.microsoft.com/#view/Microsoft_AAD_ConditionalAccess/ConditionalAccessBlade/~/Policies/menuId//fromNav/Identity](https://entra.microsoft.com/#view/Microsoft_AAD_ConditionalAccess/ConditionalAccessBlade/%7E/Policies/menuId//fromNav/Identity), create a policy with the following settings:

- **Users or workload identities**:
    - **Include**: Select **All users**.
    - **Exclude**: Select your organization's [emergency access accounts](/en-us/entra/identity/role-based-access-control/security-emergency-access). If you use Microsoft Entra Connect or Microsoft Entra Connect Cloud Sync, also exclude the **Directory Synchronization Accounts** directory role.
- **Target resources**: Under **Resources (formerly cloud apps)**, select **All resources (formerly 'All cloud apps')**.
- **Grant**: Select **Grant access**, and then select **Require device to be marked as compliant**.
- **Enable policy**: Select **Report-only**.

Create the policy. After you confirm the expected results in [report-only mode](/en-us/entra/identity/conditional-access/concept-conditional-access-report-only#reviewing-results), edit the policy and change **Enable policy** to **On**.

Note

- The **Require device to be marked as compliant** control doesn't block Intune enrollment.
- You don't need to exclude the Microsoft Defender for Endpoint app for Android and iOS (app ID `dd47d17a-3194-4d86-bfd5-c6ae6f5651e3`) from compliant-device policies. The app can report device security posture to Conditional Access.

For the complete integration workflow, see [Configure Microsoft Defender for Endpoint with Intune](/en-us/intune/device-security/microsoft-defender/configure-integration).