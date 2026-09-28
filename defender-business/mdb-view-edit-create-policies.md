---
layout: Conceptual
title: View or edit policies in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-view-edit-create-policies
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to view, edit, create, and delete cybersecurity policies in Defender for Business. Protect your devices with security policies.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-06-10T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
locale: en-us
document_id: 172e7a90-cf87-080e-e065-a7ed1ff14785
document_version_independent_id: 172e7a90-cf87-080e-e065-a7ed1ff14785
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-view-edit-create-policies.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-view-edit-create-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-view-edit-create-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 14f8ab5f-daa1-3904-150b-a74786c98073
---

# View or edit policies in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

In Defender for Business, security settings are configured through policies that are applied to devices. To help simplify your setup and configuration experience, Defender for Business includes several preconfigured policies to help protect your company's devices as soon as they're onboarded. There are other types of policies you can create as well (see [Set up, review, and edit your security policies and settings in Microsoft Defender for Business](mdb-configure-security-settings)).

This article describes how to view, edit, and create security policies in Defender for Business.

**This article includes**:

- A list of default policies that are included in Defender for Business (Next-generation protection and firewall)
- Extra policies that can be set up in Defender for Business (Web content filtering, controlled folder access, and attack surface reduction rules)
- How to view existing policies
- How to edit an existing policy
- How to create a new policy

## Default policies in Defender for Business

In Defender for Business, there are two main types of default policies that are designed to protect your company's devices as soon as they're onboarded:

- **Next-generation protection policies**, which determine how Microsoft Defender Antivirus and other threat protection features are configured; and
- **Firewall policies**, which determine what network traffic is permitted to flow to and from your company's devices.

[Next-generation protection](mdb-next-generation-protection) includes robust antivirus and anti-malware protection for computers and mobile devices. The default policies are designed to protect your devices and users without hindering productivity. However, you can customize your policies to suit your business needs. For more information, see [Review or edit your next-generation protection policies](mdb-next-generation-protection).

[Firewall policies](mdb-firewall) help secure devices by establishing rules that determine what network traffic is permitted to flow to and from devices. You can use firewall protection to specify whether to allow or to block connections on devices in various locations. For example, your firewall settings can allow inbound connections on devices that are connected to your company's internal network, but prevent connections when the device is on a network with untrusted devices. For more information, see [Firewall](mdb-firewall).

## Policies to set up in Defender for Business

In addition to next-generation protection and firewall policies, there are three other types of policies to configure for the best protection with Defender for Business:

- [Web content filtering](mdb-web-content-filtering), which enables your security team to track and regulate access to websites based on content categories. Examples of categories include adult content, high bandwidth content, and legal liability content. When you set up your web content filtering policy, you enable web protection for your organization. For more information, see [Web content filtering](mdb-web-content-filtering).
- [Controlled folder access (CFA)](/en-us/defender-endpoint/controlled-folder-access-overview) allows only trusted apps to access protected folders on Windows devices. Think of this capability as ransomware mitigation. For more information, see [Deployment and configuration methods for CFA](/en-us/defender-endpoint/controlled-folder-access-overview#deployment-and-configuration-methods-for-cfa).
- [Attack surface reduction (ASR) rules](/en-us/defender-endpoint/attack-surface-reduction-rules-overview) target certain software behaviors that are often considered risky because attackers commonly abuse these behaviors through malware. Examples of such behaviors include launching executable files and scripts that attempt to download or run files. Attack surface reduction rules can constrain software-based risky behaviors, and help keep your organization safe. At a minimum, we recommend configuring the [standard protection rules](/en-us/defender-endpoint/attack-surface-reduction-rules-overview#asr-rules) to help protect your network without causing disruption for users. For more information, see [Deployment and configuration methods for ASR rules](/en-us/defender-endpoint/attack-surface-reduction-rules-overview#deployment-and-configuration-methods-for-asr-rules).

## View your existing policies

You can view your existing policies in either Microsoft Defender portal (https://security.microsoft.com) or the Intune admin center (https://intune.microsoft.com) (if you're using Intune).

# [Microsoft Defender portal](#tab/M365D)
1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Configuration management** &gt; **Device configuration**. Policies are organized by operating system (such as **Windows client**) and policy type (such as **Next-generation protection** and **Firewall**).
3. Select an operating system tab (for example, **Windows clients**), and then review the list of policies under each category (such as **Next-generation protection** and **Firewall**).
4. To view more details about a policy, select its name. A side pane opens that provides more information about that policy, such as which devices are protected by that policy.

# [Intune admin center](#tab/intune)
1. On the **Endpoint security | Overview** page of the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), select the policy type from the **Manage** section of the navigation pane (for example, **Antivirus**, **Firewall**, or **Attack surface reduction**).
2. Any existing policies are listed for the policy type you selected. To view more details about a policy, select its name.

---

## Edit an existing policy

You can edit your existing policies in either Microsoft Defender portal (https://security.microsoft.com) or the Intune admin center (https://intune.microsoft.com) (if you're using Intune).

# [Microsoft Defender portal](#tab/M365D)
1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Device configuration**. Policies are organized by operating system (such as **Windows client**) and policy type (such as **Next-generation protection** and **Firewall**).
3. Select an operating system tab (for example, **Windows clients**), and then review the list of policies under the **Next-generation protection** and **Firewall** categories.
4. To edit a policy, select its name, and then choose **Edit**.
5. On the **General information** tab, review the information. If necessary, you can edit the description. Then choose **Next**.
6. On the **Device groups** tab, determine which device groups should receive this policy.

    - To keep the selected device group as it is, choose **Next**.
    - To remove a device group from the policy, select **Remove**.
    - To set up a new device group, select **Create new group**, and then set up your device group. (To get help with this task, see [Device groups](mdb-create-edit-device-groups).)
    - To apply the policy to another device group, select **Use existing group**.

    After you specify which device groups should receive the policy, choose **Next**.
7. On the **Configuration settings** tab, review the settings. If necessary, you can edit the settings for your policy. To get help with this task, see the following articles:

    - [Understand next-generation configuration settings](mdb-next-generation-protection)
    - [Firewall settings](mdb-firewall)

    After you specify your next-generation protection settings, choose **Next**.
8. On the **Review your policy** tab, review the general information, targeted devices, and configuration settings.

    - Make any needed changes by selecting **Edit**.
    - When you're ready to proceed, choose **Update policy**.

# [Intune admin center](#tab/intune)
To edit an existing endpoint security policy (for example, **Antivirus**, **Firewall**, or **Attack surface reduction**) in the Intune admin center, see [Modify existing policies](/en-us/intune/intune-service/protect/endpoint-security-policy#modify-existing-policies) (opens in a new tab in the Intune documentation).

---

## Create a new policy

# [Microsoft Defender portal](#tab/M365D)
1. Go to the Microsoft Defender portal (https://security.microsoft.com), and sign in.
2. In the navigation pane, choose **Device configuration**. Policies are organized by operating system (such as **Windows client**) and policy type (such as **Next-generation protection** and **Firewall**).
3. Select an operating system tab (for example, **Windows clients**), and then review the list of **Next-generation protection** policies.
4. Under **Next-generation protection** or **Firewall**, select **+ Add**.
5. On the **General information** tab, take the following steps:

    1. Specify a name and description. This information helps you and your team identify the policy later on.
    2. Review the policy order, and edit it if necessary. (For more information, see [Policy order](mdb-policy-order).)
    3. Choose **Next**.
6. On the **Device groups** tab, either create a new device group, or use an existing group. Policies are assigned to devices through device groups. Here are some things to keep in mind:

    - Initially, you might only have your default device group, which includes the devices people in your company are using to access company data and email. You can keep and use your default device group.
    - Create a new device group to apply a policy with specific settings that are different from the default policy.
    - When you set up your device group, you specify certain criteria, such as the operating system version. Devices that meet the criteria are included in that device group, unless you exclude them.
    - All device groups, including the default and custom device groups that you define, are stored in Microsoft Entra ID.

    To learn more about device groups, see [Device groups](mdb-create-edit-device-groups).
7. On the **Configuration settings** tab, specify the settings for your policy, and then choose **Next**. For more information about the individual settings, see [Configuration settings for Defender for Business](mdb-next-generation-protection).
8. On the **Review your policy** tab, review the general information, targeted devices, and configuration settings.

    - Make any needed changes by selecting **Edit**.
    - When you're ready to proceed, choose **Create policy**.

# [Intune admin center](#tab/intune)
To configure a policy by using Microsoft Intune endpoint security policies, see [Create an endpoint security policy](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) (opens in a new tab in the Intune documentation). When you create the policy, select the **Policy type**, **Platform**, and **Profile** for the protection you want to configure. For the full list of policy types, supported platforms, and available profiles, see [Available endpoint security policy types](/en-us/intune/intune-service/protect/endpoint-security-policy#available-endpoint-security-policy-types).

Important

Microsoft Defender for Endpoint management supports device objects only. Targeting users isn't supported. Assign the policy to Microsoft Entra device groups, not user groups.

The following profiles are the most relevant for Defender for Business:

- **Antivirus**: Set up your [next-generation protection policy](mdb-next-generation-protection), define [exclusions for Microsoft Defender Antivirus](/en-us/defender-endpoint/configure-exclusions-microsoft-defender-antivirus), or turn on [tamper protection](/en-us/defender-endpoint/tamper-protection-overview).
- **Firewall**: Set up your [firewall protection policy](mdb-firewall), including [custom rules](mdb-firewall#manage-your-custom-rules-for-firewall-policies-in-microsoft-defender-for-business).
- **Attack surface reduction**: Set up [attack surface reduction (ASR) rules](/en-us/defender-endpoint/attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-intune-using-endpoint-security-policies) or [controlled folder access (CFA)](/en-us/defender-endpoint/controlled-folder-access-configure#configure-cfa-in-intune-using-endpoint-security-policies).

---