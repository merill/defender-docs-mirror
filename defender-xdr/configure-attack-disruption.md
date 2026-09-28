---
layout: Conceptual
title: Configure automatic attack disruption in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/configure-attack-disruption
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to configure automatic attack disruption prerequisites in Microsoft Defender XDR, including Defender for Endpoint, Identity, Cloud Apps, and Sentinel integration.
ms.author: guywild
author: guywi-ms
ms.topic: how-to
ms.service: defender-xdr
ms.localizationpriority: medium
ms.date: 2026-08-07T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1015
- autoir
- admindeeplinkDEFENDER
- sfi-ga-nochange
ms.reviewer: Ofer Shreiber
ai-usage: ai-assisted
locale: en-us
document_id: 79289c42-5893-0a9f-108c-fb2662393457
document_version_independent_id: 79289c42-5893-0a9f-108c-fb2662393457
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/configure-attack-disruption.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-attack-disruption
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/configure-attack-disruption.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 05f1d62c-4066-e315-af70-d82eba401f4a
---

# Configure automatic attack disruption in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender XDR includes powerful [automated attack disruption](automatic-attack-disruption) capabilities that can protect your environment from sophisticated, high-impact attacks.

Configure automatic attack disruption capabilities in [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139). Before you begin, review the prerequisites for licensing, permissions, and product-specific setup requirements. After you're all set up, you can view and manage containment actions in Incidents and the Action center. And, if necessary, you can make changes to automatic attack disruption settings.

When Microsoft Defender for Endpoint is deployed, automatic attack disruption can contain unmanaged devices and users or automatically isolate a compromised workstation from the network. Automatic device isolation is currently in preview. For details about each response action, see [Automated response actions](automatic-attack-disruption#automated-response-actions).

## Prerequisites

The following are prerequisites for configuring automatic attack disruption in Microsoft Defender:

| Requirement | Details |
| --- | --- |
| Subscription requirements | One of these subscriptions: <br>- Microsoft 365 E5 or A5<br>- Microsoft 365 E3 with the Microsoft Defender Suite add-on<br>- Microsoft 365 E3 with the Enterprise Mobility + Security E5 add-on<br>- Microsoft 365 A3 with the Microsoft 365 A5 Security add-on<br>- Windows 10 Enterprise E5 or A5<br>- Windows 11 Enterprise E5 or A5<br>- Enterprise Mobility + Security (EMS) E5 or A5<br>- Office 365 E5 or A5<br>- Microsoft Defender for Endpoint (Plan 2)<br>- Microsoft Defender for Identity<br>- Microsoft Defender for Cloud Apps<br>- Defender for Office 365 (Plan 2)<br>- Microsoft Defender for Business<br><br><br> See [Microsoft Defender XDR licensing requirements](prerequisites#licensing-requirements). |
| Deployment requirements | - Deployment of Defender products (for example, Defender for Endpoint, Defender for Office 365, Defender for Identity, and Defender for Cloud Apps)<br>    - The wider the deployment, the greater the protection coverage is. For example, if a Microsoft Defender for Cloud Apps signal is used in a certain detection, then this product is required to detect the relevant specific attack scenario.<br>    - Similarly, each Defender product must be deployed to execute its automated response actions. For example, Microsoft Defender for Endpoint is required to contain an unmanaged device or isolate an onboarded workstation.<br>- Microsoft Defender for Endpoint device discovery is set to **Standard discovery** for the automatic **Contain device** action.<br>- For attack disruption actions in external platforms such as Okta or AWS (preview): Microsoft Sentinel analytic workspace connected to the unified security operations portal with the relevant provider connector deployed. |
| Permissions | To configure automatic attack disruption capabilities, you must have one of the following roles assigned in either Microsoft Entra ID (https://portal.azure.com) or in the Microsoft 365 admin center (https://admin.microsoft.com): <br>- Global Administrator<br>- Security Administrator<br>- User Administrator<br>- Authentication Administrator<br>- Privileged Authentication Administrator<br>- Directory Writers<br>- Helpdesk Administrator<br>- Security Operator<br><br>To work with automated investigation and response capabilities, such as by reviewing, approving, or rejecting pending actions, see [Required permissions for Action center tasks](m365d-action-center#required-permissions-for-action-center-tasks). |

### Microsoft Defender for Endpoint prerequisites

To support automatic attack disruption, Microsoft Defender for Endpoint requires a minimum Sense client version and proper automation settings for your device groups.

#### Automatic device isolation prerequisites and safeguards (preview)

Automatic device isolation works only on end-user workstations that are onboarded and managed by Microsoft Defender for Endpoint. Isolation blocks most network traffic while maintaining connectivity to required Defender for Endpoint security services. The action is scoped to devices involved in the incident and is automatically undone after a defined time window. Security operators can release the device earlier.

If isolated devices need access to specific processes or destinations, configure [selective isolation exclusions](/en-us/defender-endpoint/network-isolation-exclusions). To prevent automatic attack disruption from isolating selected devices, configure [automatic attack disruption exclusions](automatic-attack-disruption-exclusions).

#### Minimum Sense Client version (MDE client)

The Sense Agent is the Microsoft Defender for Endpoint sensor component that runs on each device. The minimum Sense Agent version required for the **Contain User** action to work is v10.8470. You can identify the Sense Agent version on a device by running the following PowerShell commands.

To verify that Microsoft Defender for Endpoint is installed and determine its installation path, query the registry:

```powershell
Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Advanced Threat Protection\' -Name "InstallLocation"
```

Alternatively, to confirm the installed sensor version by reading the MsSense DLL version from the registry, run the following command:

```powershell
Get-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Advanced Threat Protection\Status' -Name "MsSenseDllVersion"
```

#### Automation setting for your organization's devices

Review the automation settings for your device group policies to determine whether automated investigations run and whether remediation actions are taken automatically or only after approval. You must be a global administrator or security administrator to perform the following procedure:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to **System** &gt; **Settings** &gt; **Endpoints** &gt; **Device groups** under **Permissions**.
3. Review your device group policies and look at the **Remediation level** column. **Full - remediate threats automatically** is the recommended setting.

You can also create or edit your device groups to set the appropriate remediation level for each group. Selecting the **Semi automation** level allows triggering of automatic attack disruption without the need for manual approval. To exclude a device group from automated containment, you can set its automation level to **no automated response**. This setting isn't highly recommended and should only be done for a limited number of devices.

Note

Attack disruption can act on devices independent of a device's Microsoft Defender Antivirus operating state. The Microsoft Defender Antivirus operating state can be Active, Passive, or EDR Block Mode.

### Microsoft Defender for Identity prerequisites

To support automatic attack disruption, Microsoft Defender for Identity requires domain controller auditing and properly configured action accounts.

#### Set up auditing in domain controllers

To set up auditing on domain controllers, see [Configure audit policies for Windows event logs](/en-us/defender-for-identity/deploy/configure-windows-event-collection). Ensure required audit events are configured on domain controllers where the Defender for Identity sensor is deployed.

#### Validate action accounts

Defender for Identity allows you to take remediation actions targeting on-premises Active Directory accounts when an identity is compromised. To take these actions, Defender for Identity needs to have the required permissions to do so. By default, the Defender for Identity sensor impersonates the LocalSystem account of the domain controller and performs the actions. Since this default LocalSystem account impersonation can be changed, validate that Defender for Identity has the required permissions or uses the default LocalSystem account.

You can find more information on the action accounts in [Configure Microsoft Defender for Identity action accounts](/en-us/defender-for-identity/deploy/manage-action-accounts).

The Defender for Identity sensor needs to be deployed on the domain controller where the Active Directory account is to be turned off.

Note

If you have automation in place to activate or block a user, check if the automation can interfere with disruption. For example, if there's an automation in place to regularly check and enforce that all active employees have enabled accounts, this could unintentionally activate accounts that were deactivated by attack disruption while an attack is detected.

### Microsoft Defender for Cloud Apps prerequisites

To support automatic attack disruption, Microsoft Defender for Cloud Apps requires a properly configured Microsoft Office 365 connector.

#### Microsoft Office 365 connector

Microsoft Defender for Cloud Apps must be connected to Microsoft Office 365 through the connector. To connect Defender for Cloud Apps, see [Connect Microsoft 365 to Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/protect-office-365#connect-microsoft-365-to-microsoft-defender-for-cloud-apps).

Important

To ensure full functionality of the capability, it is mandatory to properly configure the Microsoft 365 connector. When configuring the Microsoft 365 connector in Defender for Cloud Apps, all checkboxes must be selected, including the option to enable Microsoft Entra ID apps. Failure to select all required options may result in:

- Partial or degraded functionality
- Inability to perform critical actions (such as app governance or disruption flows)
- Increased likelihood of operation failures

### Microsoft Defender for Office 365 prerequisites

To support automatic attack disruption, Microsoft Defender for Office 365 requires mailboxes hosted in Exchange Online and specific mailbox audit logging events.

#### Mailboxes location

Mailboxes are required to be hosted in Exchange Online.

#### Mailbox audit logging

At minimum, audit these mailbox events: MailItemsAccessed, UpdateInboxRules, MoveToDeletedItems, SoftDelete, and HardDelete.

Review [manage mailbox auditing](/en-us/purview/audit-mailboxes) to learn about managing mailbox auditing.

### Microsoft Sentinel prerequisites for external platforms (preview)

Your Microsoft Sentinel analytic workspace must be connected to the unified security operations portal to enable attack disruption actions for Okta and AWS.

- For Okta integration and setup steps, see [Enable attack disruption actions in Okta with Microsoft Sentinel](okta-attack-disruption).
- For AWS integration and setup steps, see [Enable attack disruption actions on AWS with Microsoft Sentinel](/en-us/azure/sentinel/aws-disruption?toc=/defender-xdr/toc.json&amp;bc=/defender-xdr/breadcrumb/toc.json).