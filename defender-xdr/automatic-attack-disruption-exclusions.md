---
layout: Conceptual
title: Exclude assets from automated response in attack disruption - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/automatic-attack-disruption-exclusions
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Exclude identities and devices from automatic attack disruption responses in Microsoft Defender XDR to prevent automated containment of selected assets.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- usx-security
- usx-security
ms.topic: how-to
ms.date: 2026-10-04T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1028
locale: en-us
document_id: f3006777-871c-e28b-7788-ece7737856a9
document_version_independent_id: f3006777-871c-e28b-7788-ece7737856a9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/automatic-attack-disruption-exclusions.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: automatic-attack-disruption-exclusions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/automatic-attack-disruption-exclusions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ca9fc181-07e2-5872-d1d7-6b63d5b4e7db
---

# Exclude assets from automated response in attack disruption - Microsoft Defender XDR | Microsoft Learn

Use exclusion policies to prevent [automatic attack disruption](automatic-attack-disruption) in Microsoft Defender XDR from applying selected responses to specific assets.

Automatic attack disruption and exclusion policies work together to contain active cyber threats. Automatic attack disruption is a built-in, AI-powered capability that analyzes attacker intent and identifies compromised assets. It can isolate devices or disable user accounts to stop an ongoing attack. Exclusion policies let security teams exempt specific assets or actions from these responses. For example, you can prevent critical servers from being isolated or critical accounts from being disabled to avoid unintended business disruption. You can remove exclusions at any time to include assets in automated responses again.

Caution

Excluding assets from automated responses isn't recommended. It can reduce the effectiveness of automatic attack disruption in protecting your environment from sophisticated, high-impact attacks.

## Prerequisites

The permissions required to manage attack disruption exclusions depend on whether [Microsoft Defender XDR Unified role-based access control (RBAC)](manage-rbac) is enabled for the relevant product.

### Device exclusions

The following table lists the permissions required to manage device exclusions.

| Unified RBAC for endpoints | Required permission |
| --- | --- |
| **Disabled** | Security Administrator or Global Administrator role in [Microsoft Entra ID](https://entra.microsoft.com) or the [Microsoft 365 admin center](https://admin.microsoft.com). |
| **Enabled** | Security Operator (or higher) global Microsoft Entra role, **or** the [Core security settings (manage)](custom-permissions-details) permission in Unified RBAC. |

For information about enabling Unified RBAC, see [Activate Microsoft Defender XDR Unified RBAC](activate-defender-rbac).

### Identity exclusions

Identity exclusions affect automated response actions in both Defender for Identity and Defender for Endpoint. The following table lists the permissions required to manage identity exclusions for each deployed product.

| Unified RBAC for identities and endpoints | Required permission |
| --- | --- |
| **Disabled for identities and endpoints** | Security Administrator or Global Administrator role in [Microsoft Entra ID](https://entra.microsoft.com) or the [Microsoft 365 admin center](https://admin.microsoft.com). |
| **Enabled** | Security Operator (or higher) global Microsoft Entra role, **or** the [Core security settings (manage)](custom-permissions-details) permission in Unified RBAC for the **Microsoft Defender for Endpoint** and **Microsoft Defender for Identity** data sources. If either product isn't deployed, permission for its data source isn't required. |

For information about role assignments and data-source scope, see [Create a custom role](create-custom-rbac-roles#create-a-custom-role).

Note

A Security Reader can view exclusions and tags but can't edit them.

## Exclusion types and approaches

You can exclude specific assets, or you can configure broad policy-driven rules based on your operational needs.

### Exclude assets

**User account exclusions** prevent specific user identities from being automatically disabled when an attack is detected. Use this for service accounts, emergency admin accounts, or identities that support critical business processes.

**Device group exclusions** allow you to set automation levels for groups of devices, controlling whether and how devices respond to detected threats. Use this to balance security with business continuity for critical infrastructure, legacy systems, or devices running mission-critical applications.

**IP exclusions** prevent specific IP addresses or ranges from being automatically contained. Use this for critical infrastructure IP ranges, legacy systems, or external services that your organization relies on.

#### Exclude user accounts

Exclude user accounts to prevent critical service accounts, emergency admin accounts, or identities supporting critical business processes from being automatically disabled during an attack. This helps maintain business continuity for essential functions while disruption actions continue against other compromised accounts.

To exclude a user account from automated responses:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to **Settings** &gt; **Microsoft Defender XDR**.

To exclude one or more user accounts from automated responses, follow these steps:

1. Under **Automated response**, select **Identities**.
2. Select **Add user exclusion**. A flyout pane appears.

    [![Screenshot of the Identities page in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-identity-add-small.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-identity-add.png#lightbox)
3. In the flyout pane, enter the user account names in the **Select users** box and select the user accounts you want to exclude.

    [![Screenshot of the flyout pane for adding and selecting user exclusions](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-identity-flyout-small.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-identity-flyout.png#lightbox)
4. Select **Exclude users** to save the exclusion.

#### Exclude device groups

Exclude device groups to protect critical infrastructure, legacy systems, or devices running mission-critical applications from automatic containment or isolation. This approach lets you keep disruption enabled for most of your environment while carving out specific device groups that require different handling due to operational dependencies.

Caution

Excluding device groups from automated responses also impacts [automated investigation and response](m365d-autoir) actions.

To exclude a device group from automated responses:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to **Settings** &gt; **Microsoft Defender XDR**.
3. Under **Automated responses**, select **Devices**.
4. In the **Device groups** tab, choose a device group by selecting the checkbox next to the group name from the list to configure attack disruption automation settings.

    [![Screenshot of the Device groups tab in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-device-select-small.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-device-select.png#lightbox)
5. In the flyout pane, select the appropriate automation level for the device group. You can choose from any of the following automation levels appropriate for your device group:

    - **Full - remediate threats automatically**: Automatically contain devices when a threat is detected.
    - **Semi - require approval for core folders**: Automatically investigate devices when an alert is received and apply remediation actions except to items within core system folders. Remediation actions for the core folders require approval.
    - **Semi - require approval for non-temp folders**: Automatically investigate and apply remediation to actions within temp and download folders when an alert is received. All other remediation actions require approval.
    - **Semi - require approval for all folders**: Automatically investigate devices when an alert is received. All remediation actions require approval.
    - **No automated response**: No automated investigation or response is taken for devices in this group.

    [![Screenshot of the flyout pane for configuring device group automation levels](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-device-flyout-small.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-device-flyout.png#lightbox)
6. Select **Save** to save the automation level for the device group.

#### Exclude IP addresses

Exclude IP addresses to prevent critical infrastructure IP ranges, legacy systems, or external services from being automatically blocked. This approach is useful for protecting network resources that your organization depends on but might not have the flexibility to respond to automated containment.

To exclude an IP address from automated responses:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to **Settings** &gt; **Microsoft Defender XDR**.
3. Under **Automated responses**, select **Devices**.

    [![Screenshot of the Devices page in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/attack-disrupt-devices-tab.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-devices-tab.png#lightbox)
4. In the **Policy application** tab, select **Exclude IP** to exclude an IP address.

    [![Screenshot of the IPs tab in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-ip-add.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-ip-add-big.png#lightbox)
5. In the flyout pane, enter the IP address/IP range/IP subnet you want to exclude. You can add multiple IP addresses and IP subnets by separating them with a comma.

    [![Screenshot of the flyout pane for adding IP address exclusions](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-ip-flyout-small.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-ip-flyout.png#lightbox)
6. Add a name and note for the exclusion. Select **Create** to save the exclusion.

### Policy applications and exclusions (Preview)

When automatic attack disruption detects with high confidence that a user or device is compromised, it automatically applies containment policies to managed devices in your organization. These policies help contain the threat and stop it from spreading across your environment.

Policy application exclusions give you granular control over how automatic attack disruption enforcement policies are applied in your environment. They let you define devices that shouldn't receive specific disruption policies. This flexibility protects sensitive, operationally critical, or exception-based systems without fully disabling automatic attack disruption.

Policy applications and exclusions allow you to:

- Manage protections for multiple devices as a group using dynamic tags
- Keep most disruption controls active while selectively disabling specific protections
- Maintain centralized control over which disruption policy controls are enabled or excluded for each tagged group of devices

First create a tag or use an existing tag to define the devices. Then create a rule that applies to that tag. For example, you might create a tag for all servers in a specific department and then create a policy application that applies to that tag. By default, all policy controls are enabled. By configuring a policy application for tagged devices, you can keep disruption enabled and exclude only specific controls for that group.

#### Create a tag

Create a tag to group devices together for a policy application.

To create a tag go to Asset rule management in the Microsoft Defender portal and select **Create tag**. Provide a name and description for the tag, then define dynamic rules to automatically include devices in the tag based on device properties such as device type, operating system, or other attributes.

#### Create a policy application

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to **Settings** &gt; **Microsoft Defender XDR**.

To create a policy application rule for tagged devices, follow these steps:

1. Under **Automated responses**, select **Devices**.

    [![Screenshot of the Devices page in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/attack-disrupt-devices-tab.png)](media/automatic-attack-disruption-exclusions/attack-disrupt-devices-tab.png#lightbox)
2. In the **Policy application** tab, select **Create rule**.

    [![Screenshot of the Policy application tab in automated response settings for attack disruption](media/automatic-attack-disruption-exclusions/policy-application-create-rule.png)](media/automatic-attack-disruption-exclusions/policy-application-create-rule.png#lightbox)
3. Provide a name and description for the policy and select **Next**.

    [![Screenshot of the policy application creation page in automated response settings](media/automatic-attack-disruption-exclusions/create-new-exclusion.png)](media/automatic-attack-disruption-exclusions/create-new-exclusion.png#lightbox)
4. Select a tag to apply the policy to, and then select **Next**.
5. Configure the disruption controls you want to disable for the tagged devices, and then select **Next**.

    [![Screenshot of selecting controls to disable for a policy application rule](media/automatic-attack-disruption-exclusions/policy-application-select-controls.png)](media/automatic-attack-disruption-exclusions/policy-application-select-controls.png#lightbox)
6. Review and submit the policy application.

## Remove exclusions

Removing an exclusion allows the asset to be included in automated responses for attack disruption again. When an exclusion is removed, the asset is no longer excluded from automated responses and can be automatically contained if it's involved in an attack that triggers attack disruption.

In the Microsoft Defender portal, go to **Settings** &gt; **Microsoft Defender XDR** &gt; **Automated response**. Then use the appropriate tab to remove an exclusion:

- Go to the **Identities** page. Select the user account you want to remove from the list and then select **Remove**.

![Screenshot of the remove option for an excluded user on the Identities page](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-user-remove.png)

- Go to the **Devices** page and navigate to the **IPs** tab. Select the IP address you want to remove from the list and then select **Remove exclusion**.

![Screenshot of the remove exclusion option for an IP in the IPs tab](media/automatic-attack-disruption-exclusions/attack-disrupt-exclude-ip-remove.png)

- Device group exclusions can be configured in the **Device groups** tab. Select the device group you want to configure from the list and choose the appropriate exclusion from the flyout pane. Select **Save** to save the exclusion.

To edit or remove a policy application, go to the **Policy application** tab and select the tag with the policy application you want to remove. Select **Edit** or **Delete**.

## Opting out of automatic attack disruption

Opting out of attack disruption can greatly increase security risk. Instead of opting out entirely, consider [excluding specific entities](automatic-attack-disruption-exclusions#exclude-user-accounts) to limit automated responses only for selected assets.

If you must opt out of attack disruption, open a support case in the Microsoft Defender portal with the subject *Attack disruption opt-out*. In your request, specify that you wish to opt out of attack disruption and include a brief explanation about your decision. This feedback helps us improve the feature and better understand customer needs. By opting out, you still receive alerts related to attack disruption but no automated actions are taken.