---
layout: Conceptual
title: Set up AI agent runtime protection with Microsoft Defender for Endpoint (Preview) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-ai-agent-runtime-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure Microsoft Defender for Endpoint AI agent runtime protection to detect, audit, and block prompt injection on Windows devices.
author: j0shbregman
ms.author: joshbregman
ms.service: defender-endpoint
ms.topic: how-to
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: df1c9385-412d-7f1c-0080-21466c20b26c
document_version_independent_id: df1c9385-412d-7f1c-0080-21466c20b26c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-ai-agent-runtime-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-ai-agent-runtime-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-ai-agent-runtime-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: e109d355-caac-bd16-3663-619ad9e9dd83
---

# Set up AI agent runtime protection with Microsoft Defender for Endpoint (Preview) - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Local AI agents run with the user's privileges on the endpoints they operate on, where they can read files, invoke tools, and run commands. Malicious instructions hidden in the content an agent reads can hijack the agent through prompt injection. AI agent runtime protection helps you detect prompt injection at the device level and block or audit the agent's action before it acts on those instructions.

This article explains how to enable runtime protection in Microsoft Defender for Endpoint, deploy it throughout your organization, and investigate detections.

For an overview of how runtime protection works, see [AI agent runtime protection with Microsoft Defender for Endpoint](ai-agent-runtime-protection-overview).

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

## Prerequisites

Before you configure runtime protection, review the following requirements:

- Your organization has a Microsoft Defender for Endpoint Plan 2, Microsoft 365 E5, Microsoft Agent 365, or Microsoft 365 E7 license.
- Your devices are [onboarded to Defender for Endpoint](onboard-configure), and Microsoft Defender Antivirus is running in active mode with real-time protection enabled.
- Your devices are running a supported version of Windows, and Microsoft Defender Antivirus has the latest platform, engine, and security intelligence updates.
- Your devices have one or more [supported local AI agents](ai-agent-runtime-protection-overview#supported-agents) installed for the runtime protection approach you plan to enable.
- To deploy the settings with Microsoft Intune, your account has an Intune role with permission to create, update, and assign device configurations, such as [Policy and Profile Manager](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#policy-and-profile-manager).
- To deploy the settings from the Microsoft Defender portal, your account has permission to manage endpoint security policies. For more information, see [Prerequisites for managing endpoint security policies](endpoint-security-policies-configure#prerequisites).
- To review alerts, your account has a supported Microsoft Entra role, such as Security Reader, Security Operator, or Security Administrator, or a Microsoft Defender custom role with permission to read security data. For more information, see [Required permissions to investigate alerts](/en-us/defender-xdr/investigate-alerts#required-permissions-to-investigate-alerts).

## Recommended deployment approach

Microsoft recommends the following phased rollout:

1. **Test**: Enable runtime protection in audit mode on a small set of devices where supported agents are actively used.
2. **Review**: Monitor alerts in the Microsoft Defender portal for one to two weeks. [Classify inaccurate alerts as false positives](/en-us/defender-xdr/investigate-alerts#manage-alert-status-and-classification). If a detection involves a file incorrectly identified as malicious, [submit the file to Microsoft for analysis](defender-endpoint-false-positives-negatives#part-4-submit-a-file-for-analysis).
3. **Deploy**: Deploy throughout your organization in audit mode to more device groups by using Microsoft Intune or the Microsoft Defender portal.
4. **Enforce**: After validating that alerts are accurate and actionable, switch to block mode on device groups where you want active enforcement.

## Enable runtime protection

To enable runtime protection on a single device:

1. Open an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**).
2. Verify that `AntivirusSignatureVersion` is `1.451.224.0` or later:

    ```powershell
    Get-MpComputerStatus | Select-Object AntivirusSignatureVersion
    ```
3. Choose which runtime protection method to enable.

    You can enable agent-native event inspection, network inspection, or both. Both methods support the same modes: `Disabled`, `Audit`, and `Block`.

    - Use `AiAgentProtection` to protect agents that expose vendor-supported agent event interfaces.
    - Use `AiAgentNetworkInspection` to extend protection to agents that don't expose vendor-supported agent event interfaces.
4. Enable the method or methods you need:

    - To enable agent-native event inspection, replace `<mode>` with `Audit` or `Block`, and then run the following command:

        ```powershell
        Set-MpPreference -AiAgentProtection <mode>
        ```
    - To enable network inspection, replace `<mode>` with `Audit` or `Block`, and then run the following command:

        ```powershell
        Set-MpPreference -AiAgentNetworkInspection <mode>
        ```

    To turn off either runtime protection method, set its mode to `Disabled`.

    For details about each mode, see [What happens when you enable runtime protection](ai-agent-runtime-protection-overview#what-happens-when-you-enable-runtime-protection). For more information about the runtime protection methods, see [Network inspection](ai-agent-runtime-protection-overview#network-inspection) and [Agent-native event inspection](ai-agent-runtime-protection-overview#agent-native-event-inspection).
5. Verify the current settings:

    ```powershell
    Get-MpPreference | Select-Object AiAgentProtection, AiAgentNetworkInspection
    ```

    For both settings, the numerical values are `0` (`Disabled`), `1` (`Block`), and `2` (`Audit`).
6. Close the PowerShell window and any terminal windows used to run agents. Then open a new terminal window before starting the agent.

Tip

After you enable runtime protection on a test device, run the [AI agent runtime protection demonstration](defender-endpoint-demonstration-ai-agent-runtime-protection) to confirm that Defender detects a benign prompt injection test string.

## Configure prompt evidence collection

`PromptEvidenceCollection` enables or disables the collection of prompt evidence when AI agent runtime protection is configured. For feature defaults and privacy guidance, see [Prompt evidence collection](ai-agent-runtime-protection-overview#prompt-evidence-collection).

Prompt evidence collection requires the October 2026 Microsoft Defender Antivirus platform and engine updates or later: platform version family `4.18.26100.x` and engine version family `1.1.26100.x`. Keep both components up to date. To check the installed versions, run:

```powershell
Get-MpComputerStatus | Select-Object AMProductVersion, AMEngineVersion
```

In an elevated PowerShell session, use the following commands:

- To enable prompt evidence collection:

    ```powershell
    Set-MpPreference -PromptEvidenceCollection $true
    ```
- To disable prompt evidence collection:

    ```powershell
    Set-MpPreference -PromptEvidenceCollection $false
    ```
- To remove the locally configured preference:

    ```powershell
    Remove-MpPreference -PromptEvidenceCollection
    ```

Removing the local preference doesn't remove a setting configured by managed policy. A policy configured through Intune or another management channel takes precedence over a local PowerShell preference.

To review all three device settings, run:

```powershell
Get-MpPreference | Select-Object AiAgentProtection, AiAgentNetworkInspection, PromptEvidenceCollection
```

For parameter details, see [Set-MpPreference](/en-us/powershell/module/defender/set-mppreference), [Get-MpPreference](/en-us/powershell/module/defender/get-mppreference), and [Remove-MpPreference](/en-us/powershell/module/defender/remove-mppreference).

## Deploy settings throughout your organization with Microsoft Intune

Use a Microsoft Intune endpoint security Antivirus policy to deploy agent-native event inspection, network inspection, and prompt evidence collection to enrolled Windows devices. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Windows**.
- **Profile**: Select **Microsoft Defender AI agent runtime protection**.

On the **Configuration settings** page, configure the settings you need:

| Setting | Purpose | Configuration |
| --- | --- | --- |
| **Ai Agent Protection** (`AiAgentProtection`) | Inspect agent activity through supported agent-native event interfaces. | Choose the audit or block mode you need. The default is disabled. |
| **Ai Agent Network Inspection** (`AiAgentNetworkInspection`) | Inspect supported agent-to-LLM network traffic. | Choose audit or block mode independently of agent-native event inspection. The default is disabled. |
| **Prompt Evidence Collection** (`PromptEvidenceCollection`) | Collect prompt evidence when AI agent runtime protection is configured. | Enable or disable collection. |

For each inspection method, **Audit** detects and reports prompt injection while allowing the action to continue, and **Block** blocks detected threats at supported inspection points. Leave a method disabled if you don't need it. You can enable either inspection method or both.

Microsoft recommends that you initially assign the policy in audit mode to a limited device group. Review detections, and then change the inspection settings to block mode when you're ready to enforce protection. Choose whether to enable prompt evidence collection separately. Complete the policy wizard, assign the policy to the device groups you want to protect, and then create the policy.

After the policy applies, verify the settings on an enrolled device:

1. In the Microsoft Defender portal, open the device page.
2. On the **Configuration management** tab, select **Effective settings**.
3. Find the agent protection, network inspection, and prompt evidence collection settings you configured, and confirm their effective values and configuration sources. For more information, see [Effective settings on the device entity page](/en-us/defender-xdr/entity-page-device#effective-settings).

Close any terminal windows used to run agents, and then open a new terminal window before starting the agent. Run the [AI agent runtime protection demonstration](defender-endpoint-demonstration-ai-agent-runtime-protection) to confirm that Defender detects a benign prompt injection test string.

## Deploy settings throughout your organization with the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), use the **Microsoft Defender AI agent runtime protection** template to deploy agent-native event inspection, network inspection, and prompt evidence collection. The policy can apply to Intune-enrolled devices and devices managed through Defender for Endpoint security settings management.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy, use these specific settings:

- **Policy type**: On the **Windows policies** tab of the **Endpoint security policies** page in the Microsoft Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, select ![](media/defender-portal-icon-create.png)**Create new policy**.
- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender AI agent runtime protection**.

On the **Configuration settings** page, configure the settings you need:

- **Ai Agent Protection** (`AiAgentProtection`) for agent-native event inspection.
- **Ai Agent Network Inspection** (`AiAgentNetworkInspection`) for supported agent-to-LLM network traffic.
- **Prompt Evidence Collection** (`PromptEvidenceCollection`) to enable or disable collection of prompt evidence when AI agent runtime protection is configured.

Configure each inspection method independently. **Audit** detects and reports prompt injection while allowing the action to continue, and **Block** blocks detected threats at supported inspection points. Leave a method disabled if you don't need it.

Microsoft recommends that you initially assign the policy in audit mode to a limited device group. Review detections, and then change the inspection settings to block mode when you're ready to enforce protection. Choose whether to enable prompt evidence collection separately. Complete the policy wizard, assign the policy to the device groups you want to protect, and then create the policy.

Important

For devices managed through Defender for Endpoint security settings management that aren't enrolled in Intune, assign the policy to Microsoft Entra device groups. User targeting isn't supported for these devices.

After the policy applies, verify the settings on a device:

1. In the Microsoft Defender portal, open the device page.
2. On the **Configuration management** tab, select **Effective settings**.
3. Find the agent protection, network inspection, and prompt evidence collection settings you configured, and confirm their effective values and configuration sources. For more information, see [Effective settings on the device entity page](/en-us/defender-xdr/entity-page-device#effective-settings).

Close any terminal windows used to run agents, and then open a new terminal window before starting the agent. Run the [AI agent runtime protection demonstration](defender-endpoint-demonstration-ai-agent-runtime-protection) to confirm that Defender detects a benign prompt injection test string.

## Review and investigate detections

Important

During preview, a prompt injection alert might incorrectly report a block when runtime protection is configured in Audit mode. In Block mode, Claude Code might continue processing a tool response despite a reported post-tool-response block. See [Known issues (Preview)](ai-agent-runtime-protection-overview#known-issues-preview) for details.

After you enable runtime protection, review alerts to validate detection accuracy and tune your configuration before broadening enforcement. This step is critical during the audit phase because it helps you understand what agents are encountering and whether detections represent real threats.

When runtime protection detects prompt injection, Defender raises a **Suspicious AI prompt injection** alert and takes action based on the configured mode. The alert appears on the device timeline, and related alerts are correlated into incidents for security operations center (SOC) investigation. In block mode, the alert severity is **Critical**, **High**, **Medium**, or **Low** based on assessed risk. In audit mode, the alert is **Informational**, so your team can review what would have been blocked without triaging it as an active threat.

[![Screenshot of a Suspicious AI prompt injection alert in Microsoft Defender, including the process tree and related detection details.](media/configure-ai-agent-runtime-protection/runtime-protection-suspicious-prompt-injection-alert.png)](media/configure-ai-agent-runtime-protection/runtime-protection-suspicious-prompt-injection-alert.png#lightbox)

For more information about mode behavior, see [What happens when you enable runtime protection](ai-agent-runtime-protection-overview#what-happens-when-you-enable-runtime-protection).

### End-user experience

When Defender blocks an agent action, it follows the notification rules configured for the device. Users can receive the following notifications:

1. **In the agent terminal**: The agent displays a block message showing what was blocked, why, and confirmation that the action didn't execute.
2. **Windows toast notification**: If Windows Security notifications are enabled, a system notification appears regardless of whether the agent terminal is in focus.

The following screenshot shows an example of a blocked prompt injection in the agent terminal and the corresponding Windows toast notification:

[![Screenshot of a Defender block message in the agent terminal and a Windows toast notification for a blocked prompt injection attack.](media/configure-ai-agent-runtime-protection/ai-runtime-agent-block-and-toast.png)](media/configure-ai-agent-runtime-protection/ai-runtime-agent-block-and-toast.png#lightbox)

Users can also review detections under **Windows Security** &gt; **Virus & threat protection** &gt; **Current threats** and the **Protection history**, where they can see the threat name, severity, affected agent, and remediation status.

### Security operations experience

For security operations teams, runtime protection events appear in the Microsoft Defender portal. Select an alert to view the detection type, severity, affected agent, process tree details, and recommended actions.

Your security team uses the same investigation workflows as other endpoint detections: timeline review, alert and entity correlation, and response actions.

For more information, see [Investigate alerts in Microsoft Defender](/en-us/defender-xdr/investigate-alerts) and [Investigate incidents in Microsoft Defender](/en-us/defender-xdr/investigate-incidents).