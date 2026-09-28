---
layout: Conceptual
title: Microsoft Security Copilot Security Alert Triage Agent in Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-alert-triage-agent
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the Security Alert Triage Agent, an autonomous agent in the Microsoft Defender ecosystem that helps security teams triage alerts at scale using AI-driven reasoning, prioritization, and enrichment.
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier1
- security-copilot
- magic-ai-copilot
ms.topic: how-to
search.appverid:
- MOE150
- MET150
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 15b2fcbe-fb0c-2014-f952-b915f6de2704
document_version_independent_id: 15b2fcbe-fb0c-2014-f952-b915f6de2704
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-alert-triage-agent.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-alert-triage-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-alert-triage-agent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: a400e458-a72d-92cf-2eb4-1eed0d71ff4c
---

# Microsoft Security Copilot Security Alert Triage Agent in Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn

Note

The Security Alert Triage Agent is the same agent as the [Phishing Triage Agent](phishing-triage-agent), which has demonstrated measurable improvements in triage accuracy and efficiency in controlled evaluations. The agent is extended to triage a broader set of alerts in Microsoft Defender, starting with a subset of identity and cloud alerts. These expanded capabilities are currently in preview. The set of supported alerts is expected to grow over time.

Security Operations Centers (SOCs) process large volumes of alerts across multiple workloads, each requiring different context, signals, and investigative depth. Differences in how these alerts are evaluated can lead to inconsistent triage decisions and slow the ability to distinguish real threats from false alarms. As a result, high-risk activity can be missed or delayed, while analysts spend disproportionate time filtering noise instead of acting on what matters most.

The Microsoft Security Copilot Security Alert Triage Agent is an autonomous agent embedded in Microsoft Defender that helps security teams triage alerts at scale. It applies AI-driven, dynamic reasoning across evidence to deliver clear verdicts for supported security workloads. By identifying which alerts represent real attacks and which are false positives, the agent enables analysts to focus on investigating real threats, with transparent, step-by-step reasoning to support every decision.

This article provides an overview of the Security Alert Triage Agent, how it works, and its alert triage capabilities. Before you set up the agent, make sure you meet the Security Alert Triage Agent prerequisites, including Security Copilot provisioning, unified RBAC activation, and workload-specific licensing. Watch this video to see a quick demo:

## How the Security Alert Triage Agent works

The Security Alert Triage Agent is a [Security Copilot agent](/en-us/copilot/security/agents-overview) in Microsoft Defender that classifies and triages alerts across supported workloads and alert types. The agent’s key capabilities include:

- **Autonomous triage:** Uses advanced AI tools to evaluate alerts and determine whether they represent malicious activity or false alarms without requiring step‑by‑step human input.
- **Transparent rationale:** Records classification verdicts and provides supporting reasoning in natural language and visual graphs, including the evidence used to reach each conclusion.
- **Learning based on feedback:** For supported alert types, the agent can incorporate analyst feedback when explicitly provided and approved to tune its verdict analysis. This capability is currently available for email and collaboration alerts only.

## Supported alert types for the Security Alert Triage Agent

The Security Alert Triage Agent currently supports the following subset of alert types in Microsoft Defender. The set of supported alerts is expected to grow over time.

| Alert type | Alert name |
| --- | --- |
| **Email and collaboration alerts, including phishing (Generally Available)** | Email reported by user as malware or phish |
| **Cloud alerts, including containers (Preview)** | View all cloud alerts<br><br>- Potential Backdoor Utilities or Proxy Binaries Detected (Preview)<br>- Potential backdoor installations from running processes (Preview)<br>- Possible executable detected in a command line, encoded in Base64 (Preview)<br>- Potential base64 encoded shell script execution (Preview)<br>- Unusual access to Bash profile file<br>- SSH server is running inside a container (Preview)<br>- Suspicious Cron operations in command line detected<br>- Process associated with digital currency mining detected<br>- Possible Cryptocoinminer download detected<br>- Kubernetes crypto-miner process kills detected (Preview)<br>- Possible access to a cryptocurrency mining pool detected (Preview)<br>- Digital currency mining related behavior detected<br>- Possible web service exploitation by using path traversal (Preview)<br>- Detected possible disabling of security tools (Preview)<br>- Blocked binary drift executing in the container (Preview)<br>- A drift binary detected executing in the container<br>- Suspicious file attribute changes using chattr detected (Preview)<br>- Docker build operation detected on a Kubernetes node (Preview)<br>- Access to cloud metadata service detected<br>- Possible Impairing of Command History Logging (Preview)<br>- Possible attack tool detected<br>- Possible credential access tool detected<br>- Access to kubelet kubeconfig file detected<br>- Attempt to create a new Linux namespace from a container detected<br>- Network Scanning Tool Detected (Preview)<br>- Account added to sudo group<br>- Usage of OAST domain detected (Preview)<br>- Kubernetes penetration testing tool detected (Preview)<br>- Possible exploitation of java based program has been detected (Preview)<br>- Command within a container running with high privileges<br>- Suspicious Proxyware or Traffic monetizers detected in command line<br>- Potential React2Shell command injection detected<br>- Unusual access to bash history file<br>- Potential reverse shell detected<br>- Possible Secret Reconnaissance Detected<br>- Detected possible tampering of security configurations (Preview)<br>- Detected suspicious termination of security process (Preview)<br>- Sensitive Files Access Detected<br>- Sha1-Hulud Campaign Detected: Possible command injection to exfiltrate credentials (Preview)<br>- Process seen accessing the SSH authorized keys file in an unusual way<br>- An uncommon connection attempt detected<br>- Detected file download from a known malicious source<br>- Suspicious PHP execution detected<br>- Potential port forwarding to external IP address<br>- Process Invocation By a DB Process Detected<br>- Suspicious Netcat activity detected on a Kubernetes node (Preview)<br>- Possible Log Tampering Activity Detected<br>- Suspicious file timestamp modification<br>- Possible malicious web shell detected<br>- Suspicious request to Kubernetes API<br>- Possible Web Shell Activity Detected<br>- Suspicious access to workload identity token or service account token detected<br>- Permissions to run a binary from a suspicious folder has been granted after download (Preview)<br>- A command line executed within a container contains a suspicious DNS<br>- A command line executed within a container contains a suspicious IP address<br>- Microsoft Defender for Cloud Kubernetes Malware execution detected (Preview)<br>- Microsoft Defender for Cloud Kubernetes Malware execution blocked (Preview) |
| **Identity alerts (Preview)** | View all identity alerts<br><br>- Password spray<br>- Possible BEC-related inbox rule<br>- Account compromised following a password-spray attack |

## Prerequisites

These prerequisites apply regardless of the alert types you want the agent to triage.

| Prerequisite | Details |
| --- | --- |
| **Security Copilot** | Provisioned capacity in **Security Compute Units (SCU)**. See [Get started with Security Copilot](/en-us/copilot/security/get-started-security-copilot) or check whether you're entitled to SCUs as part of the [Microsoft Security Copilot inclusion model](/en-us/copilot/security/security-copilot-inclusion). |
| **Security Copilot plugins** | The Security Alert Triage Agent automatically activates these plugins: Microsoft Defender XDR, Microsoft Threat Intelligence, and Security Alert Triage Agent. For more information, see [Plugins overview - Microsoft Security Copilot](/en-us/copilot/security/plugin-overview). |
| **Alert-tuning rules** | Disable tuning rules that resolve the alerts you want the agent to triage. The agent doesn't triage resolved alerts. For more information, see [Tune an alert](investigate-alerts#tune-an-alert). |
| **Unified RBAC** | Enable unified role-based access control and activate the relevant workloads for the alert types you want to triage. For more information, see Workload-specific prerequisites. |
| **Products and licenses** | You need specific products and licenses based on the alert types you want the agent to triage. For more information, see Workload-specific prerequisites. |

### Workload-specific prerequisites

The following prerequisites depend on the alert types you want the agent to triage.

# [Email and collaboration alerts](#tab/email-alerts)
The following prerequisites apply when you want the agent to triage email and collaboration alerts.

##### Product and license requirements

The following product and license are required for email and collaboration alerts:

- [Microsoft Defender for Office P2](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description)

##### Unified RBAC requirements

Activate **Defender for Office 365** in Microsoft Defender XDR unified RBAC settings. For more information, see [Activate workloads in Microsoft Defender XDR settings](activate-defender-rbac#activate-in-microsoft-defender-xdr-settings).

[![Screenshot of the Activate unified role-based access control page showing the Defender for Office 365 toggle, which needs to be enabled for the Security Alert Triage Agent.](media/security-alert-triage-agent/activate-defender-for-office-365-workloads.png)](media/security-alert-triage-agent/activate-defender-for-office-365-workloads.png#lightbox)

##### Configure user reported settings

Enable **Monitor reported messages in Outlook** to define how users report potentially malicious messages in Microsoft Outlook and select any of the **Reported message destinations** options:

[![Screenshot of the User reported settings page showing the Outlook report button and reported message destinations configurations.](media/security-alert-triage-agent/configure-user-reported-settings.png)](media/security-alert-triage-agent/configure-user-reported-settings.png#lightbox)

For more information, see [Use the Microsoft Defender portal to configure user reported settings](/en-us/defender-office-365/submissions-user-reported-messages-custom-mailbox).

If you’re using a third-party email reporting tool, review [Options for third-party reporting tools](/en-us/defender-office-365/submissions-user-reported-messages-custom-mailbox) and view your vendor’s configuration options to integrate reported messages with Microsoft Defender.

##### Add alert policy

The Security Alert Triage Agent addresses email and collaboration incidents that include alerts with the type **Email reported by user as malware or phish**.

Ensure that you have the corresponding alert policy enabled. For more information, see [Alert policies in the Microsoft Defender portal](alert-policies).

Important

The Security Alert Triage Agent doesn't triage alerts resolved by [alert tuning](investigate-alerts#tune-an-alert). Make sure to disable the **Auto-Resolve – Email reported by user as malware or phish** built-in alert tuning rule and any custom tuning rules that resolve this alert.

# [Cloud alerts](#tab/cloud-alerts)
The following prerequisites apply when you enable cloud alert triage.

##### Product and license requirements

Cloud alert triage requires the following products and licenses:

- [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)
- [Microsoft Defender for Containers (part of Microsoft Defender for Cloud)](/en-us/azure/defender-for-cloud/defender-for-containers-deployment-overview)

##### Unified RBAC requirements

Unified RBAC for cloud alerts is enabled automatically. No additional activation is required.

No additional configuration is required beyond the general prerequisites.

# [Identity alerts](#tab/identity-alerts)
The following prerequisites apply when you enable identity alert triage.

##### Product and license requirements

Identity alert triage requires the following products and licenses:

- [Entra ID P2 license](/en-us/entra/fundamentals/licensing)
- [Microsoft Defender for Identity](/en-us/defender-for-identity/what-is)
- [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)

##### Unified RBAC requirements

Activate **Microsoft Defender for Identity** and **Microsoft Defender for Cloud Apps** in Microsoft Defender unified RBAC settings. For more information, see [Activate workloads in Microsoft Defender settings](activate-defender-rbac#activate-in-microsoft-defender-xdr-settings).

[![Screenshot of Microsoft Defender XDR Permissions and roles page showing unified RBAC activation with Identity and Cloud Apps settings.](media/security-alert-triage-agent/rbac-settings-defender-identity.png)](media/security-alert-triage-agent/rbac-settings-defender-identity.png#lightbox)

---

## Required user permissions

Users who interact with the Security Alert Triage Agent need these permissions:

| User action | Required permissions |
| --- | --- |
| **View agent results** | The same permissions as the agent (or higher), as described in Security Alert Triage Agent required permissions. |
| **View agent settings** | **Security Copilot (read)** and **Security data basics (read)** under the **Security operations** permissions group in the Defender portal.**OR** **Security Administrator** in **Microsoft Entra ID**. |
| **Manage agent settings** (set up, pause, remove the agent, and manage agent identity) | **Security Administrator** in **Microsoft Entra ID**. |
| **Teach agent through feedback** | The same permissions as the agent (or higher), as described in Security Alert Triage Agent required permissions. |
| **View feedback page** | **Security Copilot (read)**, **Security data basics (read)**, and **Email & collaboration metadata (read)** under the **Security operations** permissions group in the Defender portal.**OR** **Security Administrator** in **Microsoft Entra ID**. |
| **Reject feedback** | **Security Administrator** in **Microsoft Entra ID**. |

For more information about unified RBAC in the Defender portal, see [Microsoft Defender Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## Set up the Security Alert Triage Agent

Make sure you have the required user permissions and that all agent prerequisites are met before setting up the agent.

### Begin setup

Open the Security Alert Triage Agent setup wizard in one of two ways:

- From the **Incidents** queue in the Microsoft Defender portal, select **Set up agent**.

    [![Screenshot of the incident queue with the Security Alert Triage Agent setup option highlighted.](media/security-alert-triage-agent/phishing-triage-setup-incident.png)](media/security-alert-triage-agent/phishing-triage-setup-incident.png#lightbox)
- From the Security Store in the Microsoft Defender portal, as explained in [Deploy AI agents in Microsoft Defender](security-copilot-agents-defender#discover-and-deploy-agents-in-the-microsoft-defender-portal). The agent might appear as **Phishing Triage Agent** in the Security Store, but it’s the same agent.

Follow the steps in the setup wizard, as described in Select which alert types to triage and Assign the agent's identity and permissions.

### Select which alert types to triage

Select the alert types you want the agent to triage from the list of supported alert types. Permissions and data scopes depend on that selection.

[![Screenshot of agent supported alerts setup with toggles for email, cloud, and identity alerts, and Continue and Back buttons.](media/security-alert-triage-agent/security-alert-triage-alert-types.png)](media/security-alert-triage-agent/security-alert-triage-alert-types.png#lightbox)

### Assign the agent’s identity and permissions

The setup wizard walks you through assigning the agent an identity and the permissions required to do its work.

#### Assign an identity

The agent requires an identity to operate. The wizard prompts you to select one of two identity types.

[![Screenshot of the Select a new identity screen in the Security Alert Triage Agent setup wizard.](media/security-alert-triage-agent/setup-assign-identity.png)](media/security-alert-triage-agent/setup-assign-identity.png#lightbox)

Select:

- **Create a new agent identity (recommended)** - Automatically create a new Microsoft Entra Agent ID. Microsoft Entra creates Agent IDs specifically for AI agents. Using Agent IDs keeps access scoped, secure, and easier to manage. For more information, see [What are agent identities?](/en-us/entra/agent-id/identity-platform/what-is-agent-id).

    OR
- **Connect an existing user account** - Assign an existing user account as the agent identity. The agent inherits the user account's access and permissions. To use this identity option, you need to create the identity yourself and assign it the permissions the agent requires before setup. For information on creating a user account, see [Create a new user](/en-us/entra/fundamentals/how-to-create-delete-users#create-a-new-user).

    When you connect the agent to an account, we recommend setting a long account expiration date and closely monitoring its authentication status to ensure continuous operation of the agent. If authentication expires, the agent stops functioning until it’s renewed.

    The agent's specified user identity isn't compatible with PIM or TAP because they don't support long-term background operations.

    Tip

    Use a dedicated identity account with the minimum required permissions for the agent. When creating the account, assign a distinct display name like *Security Alert Triage Agent* to easily identify it in the Microsoft Defender portal.

    **Set conditional access policies for Security Copilot** to enable the agent to function based on the user account created for it. For more information, see [Troubleshoot Conditional Access policies for Microsoft Security Copilot](/en-us/entra/identity/conditional-access/troubleshoot-security-copilot-policies).

Note

You can change the agent identity after setup as described in Edit agent settings.

#### Assign permissions

In alignment with [the principle of least privileges](/en-us/entra/identity-platform/secure-least-privileged-access), we recommend assigning the agent identity only the permissions the Security Alert Triage Agent requires to perform its tasks.

- If you use an Agent ID, the dropdown only displays roles in your organization that have the permissions the agent needs. Select an existing role in your organization or automatically create a new role with the required permissions if you don't already have a suitable role set up.

    [![Screenshot of the Create a new agent identity screen in the Security Alert Triage Agent setup wizard.](media/security-alert-triage-agent/setup-assign-entra-agent-id.png)](media/security-alert-triage-agent/setup-assign-entra-agent-id.png#lightbox)
- If you use an existing user account, you need to assign the required permissions to that identity before assigning the agent identity during setup - you can't do this from the setup wizard.

    [![Screenshot of the Connect with an existing user account screen in the Security Alert Triage Agent setup wizard](media/security-alert-triage-agent/setup-assign-user.png)](media/security-alert-triage-agent/setup-assign-user.png#lightbox)

##### Security Alert Triage Agent required permissions

The Security Alert Triage Agent requires specific permissions to access the necessary data and perform its triage functions. The required permissions depend on the alert types and associated products you want the agent to work with.

This table summarizes the required permissions and data scopes for each alert type:

| Alert type | Permissions | Data scopes |
| --- | --- | --- |
| **Email and collaboration alerts, including phishing** | Security Copilot (read), Security data basics (read), Alerts (manage), Email & collaboration metadata (read), Email & collaboration content: Emails associated with alerts (read) | Microsoft Defender for Office 365 |
| **Cloud alerts, including containers** | Security Copilot (read), Security data basics (read), Alerts (manage) | Microsoft Defender for Cloud |
| **Identity alerts** | Security Copilot (read), Security data basics (read), Alerts (manage) | Microsoft Defender for Identity and Microsoft Defender for Cloud Apps |

These permissions are under the **Security operations** permissions group:

[![Screenshot of required permissions for Alert Triage](media/security-alert-triage-agent/agent-permissions.png)](media/security-alert-triage-agent/agent-permissions.png#lightbox)

To create a role manually:

1. Ensure that the relevant unified RBAC workloads are activated to allow the agent to effectively analyze alerts with comprehensive context. Follow the steps in Workload-specific prerequisites.
2. [Create a role](create-custom-rbac-roles#create-a-custom-role) with the required permissions or assign an existing role with these permissions to the agent.

    Make sure to grant the role access to all of the relevant data sources based on the supported alerts you want to associate with the Security Alert Triage Agent.

    [![Screenshot of required data sources for Security Alert Triage](/en-us/defender-xdr/media/security-alert-triage-agent/agent-permissions-sources.png)](/en-us/defender-xdr/media/security-alert-triage-agent/agent-permissions-sources.png#lightbox)
3. Assign the role to the agent identity.

Important

After assigning the agent its permissions, ensure the user group monitoring the agent has equal or higher permissions to oversee its activity and output. To do this, compare the permissions of the user group to the agent in the Permissions page in the Microsoft Defender portal.

## Use the Security Alert Triage Agent

The agent helps security teams manage the large volume of alerts organizations receive daily by automatically triaging supported alerts and updating their classification and status in Microsoft Defender incidents.

### Agent trigger and flow

After setup, the Security Alert Triage Agent automatically runs when a relevant alert is created. The agent then autonomously analyzes the alert using sophisticated AI tools and your organization's context to determine whether the associated threat is malicious or just a false alarm.

If the alert is determined to be a false alarm, the agent classifies it as a False Positive and resolves it accordingly. If the alert is deemed malicious, it's classified as a True Positive, and the status of the associated incident remains open and in progress for an analyst to investigate and take further action.

For every alert it processes, the agent provides a detailed explanation of its verdict in the corresponding incident.

### Collaborate with the agent

To maintain transparency, the agent routinely updates incident fields during the triage process. When triaging starts, the agent assigns the alert to itself and adds an **Agent** tag to the corresponding incident. Analysts can filter the incident queue to see only incidents tagged by the agent, which simplifies oversight and prioritization.

Tip

You can also filter the incident queue using the name of the identity you assigned to the Security Alert Triage Agent to see the incidents the agent is actively working on.

When an alert is identified as a true threat, the Security Alert Triage Agent marks it as a True Positive, allowing analysts to filter and prioritize incidents based on confirmed classifications.

[![Screenshot of the incident queue filtered by the Security Alert Triage Agent tag](media/security-alert-triage-agent/incident-queue-agent-only.png)](media/security-alert-triage-agent/incident-queue-agent-only.png#lightbox)

### Transparency and explainability in alert triage

For each alert it processes, the Security Alert Triage Agent provides a detailed explanation of its verdict and a graphical representation of its decision‑making workflow.

To review the agent’s findings, follow these steps:

1. Select an incident from the incident queue.
2. On the incident page, look for the Security Alert Triage Agent card in the Copilot or Tasks side panel under the Guided Response Triage section. The task is marked as completed and assigned to the agent. The card presents the agent’s verdict based on its classification, highlighting key pieces of incriminating evidence that informed the decision.

    [![Screenshot of the incident page with the Security Alert Triage Agent card highlighted](media/security-alert-triage-agent/incident-main.png)](media/security-alert-triage-agent/incident-main.png#lightbox)
3. You can select the **More actions** ellipsis to view more alert details, copy the agent’s classification details to the clipboard, or manage feedback.

    [![Screenshot highlighting the more actions options within the Security Alert Triage Agent card](media/security-alert-triage-agent/more-actions-card.png)](media/security-alert-triage-agent/more-actions-card.png#lightbox)
4. To view the steps the agent took prior to reaching its classification, select **View agent activity** in the Security Alert Triage Agent card. This shows the logic behind the agent’s final classification.

    [![Screenshot highlighting the View agent activity pane.](media/security-alert-triage-agent/view-agent-activity.png)](media/security-alert-triage-agent/view-agent-activity.png#lightbox)

## Teach the agent your organization's context through feedback

Important

The feedback option is currently only available for email and collaboration alerts.

For supported alert types, analysts can optionally provide feedback on agent classifications in plain, natural language, with no complex configurations required. Authorized users can review feedback, evaluate it, and explicitly apply it to influence how the agent classifies similar alerts in the future. This capability is currently available for email and collaboration alerts only.

To provide feedback and teach the agent, follow these steps:

1. In the incident page, look for the Security Alert Triage Agent card in the Copilot or Tasks side panel under the Guided Response Triage section.
2. Review the agent's classification and reasoning displayed in the card's title and content. If the decision doesn't align with your organization's classification criteria, select **Change classification**. Alternatively, you can update the classification by selecting the specific alert from the **Alerts** tab, then choosing **Manage alert**.

    [![Screenshot highlighting the Change classification option in the Security Alert Triage Agent card](media/security-alert-triage-agent/change-classification.png)](media/security-alert-triage-agent/change-classification.png#lightbox)
3. In the **Manage alert** pane, select the new classification from the **Classification** dropdown menu. Then, provide your reason for the change by filling out the **Why did you change this classification** field. This step records your input on the feedback management page for auditing purposes only. The agent won't use this feedback to improve its decision-making until you explicitly select **Use this feedback to teach the agent**. If you choose not to use this feedback for teaching the agent, you can select **Save**, which will only audit the feedback without inserting it into the agent's memory.

    [![Screenshot highlighting the classification and feedback fields in the Manage alert pane](media/security-alert-triage-agent/manage-alert-why.png)](media/security-alert-triage-agent/manage-alert-why.png#lightbox)
4. To apply your feedback, select **Use this feedback to teach the agent**. You can use the best practices for writing agent feedback to help you craft effective input, and then choose **Evaluate feedback** to allow you to preview how the agent translates your feedback into a lesson and assess whether the outcome aligns with your intent. Additionally, the feedback evaluation performs basic safety checks to ensure that the applied feedback is relevant for the agent to use and doesn't conflict with previous feedback.

    Note

    You can only provide feedback to the agent once per alert, and it can only be used to teach the agent how to classify email and collaboration alerts, specifically by selecting either True Positive (phishing) or False Positive (not malicious). Always review your feedback and verify the AI-generated response before saving the lesson.
5. If the result meets your expectations, you can choose to insert the lesson into the agent's memory to influence its future decisions. Select **Save** to save the lesson and store it as a lesson in the agent's memory if applicable. All feedback is recorded for audit purposes, and lessons added to the agent's memory can be reviewed later in the feedback management page.

The agent utilizes stored feedback to triage and classify similar alerts in the future. When a relevant alert that matches the feedback characteristics is received, the agent applies this feedback to determine its classification, incorporating it as supporting evidence in its decision-making process.

### Best practices for writing feedback

Lessons provide systematic guidelines that help the agent determine whether an alert is a genuine phishing threat or a false alarm. To ensure the agent effectively incorporates your feedback, follow these best practices when providing input to the Security Alert Triage Agent:

1. **Ensure feedback is relevant and contextual.** Feedback should pertain only to the email currently under review. It must also align with the updated classification you've assigned.
2. **Be descriptive and specific.** Clearly explain the characteristics of the email. Provide relevant details like the email subject, message body, sender, or recipients to help the agent understand the context. Specific feedback with multiple details enhances effectiveness.
3. **Ensure clarity and decisiveness.** Avoid vague or universal statements. Give feedback that's clear and actionable. Use decisive and clear identification terms.
4. **Be consistent with previous feedback.** Ensure that new feedback aligns with what was previously provided to avoid contradictions that could confuse the agent or reduce the accuracy of its decisions. You can review all previously submitted input on the agent feedback management page.
5. **Review the agent's interpretation of your feedback.** When you submit feedback, always verify that the feedback is accurately translated into a lesson. Confirm that the lesson reflects your intent and maintains consistency with your original input. Checking the validity of AI-generated responses to ensure they're applicable to the scenario.

Here are examples of how you can write your feedback to the agent.

| Area | Examples of well-written feedback | Examples of feedback that can lead to failure | Comparison |
| --- | --- | --- | --- |
| Feedback about a sender | Any email claiming to be from benefits providers must originate from "@benefits.company.com". | The sender in the 2nd alert in the incident is not legitimate. | Feedback must relate to the email in the current alert and its context. It will be tied to the chosen classification (even if not mentioned explicitly in the feedback) and used for similar future alerts. |
| Feedback about the sender and email body | Emails offering file sharing or document access should only come from our authorized provider Contoso.com. | Emails offering file sharing or document access should only come from our authorized providers. | Well-written feedback clearly states specific requirements (for example, sender domain), while vague references (for example "authorized providers") do not contain actionable information. |
| Feedback about email subject | Any email that its subject contains a request for billing transaction is not allowed in our organization and is considered as phishing. | If the subject has a positive natural sentiment, it's legitimate. | Feedback that is descriptive and specific can be effectively validated, while subjective feedback may lead to unintended outcomes. |
| Feedback about the email body | Emails requesting credential verification should include a reference to the specific account or service. Any generic 'verify your account' request without details should be treated as phishing. | This email should be treated as phishing. | Feedback that includes detailed information is more likely to be clearly understood, while feedback lacking detail may be interpreted in various ways and could lead to unpredictable outcomes. |
| Feedback about a recipient and email body | This email was sent to multiple employees, and the body instructs recipients to download an 'important attachment' without describing its contents—legitimate emails always specify attachment details. | Mass internal emails with attachments are phishing. | Feedback that highlights specific missing details commonly found in legitimate emails is more effective. Feedback that contains broad generalizations (mass emails) or vague terms (such as "internal") may lead to an excessive number of true positives. |
| Feedback about a recipient and a domain | New contractor onboarding emails should only be sent to email addresses starting with 'v-' to ensure they are directed to the correct recipients. | Contractor emails look different from usual, so they might be phishing. | Well-written feedback clearly defines the expected recipient format, while feedback that is indecisive ("might be") and lacks clear identification criteria ("looks different from usual" without specifying what is different), makes detection unreliable. |

### Resolve feedback failures

When the agent takes your feedback, it translates it into a lesson. If the agent doesn't succeed in interpreting the feedback, a relevant message shows what caused the failure. You can address these failures based on the message returned by the agent.

Here are examples of failures you might encounter when writing feedback to the agent, and how you can resolve them.

| Failure message | Recommended action |
| --- | --- |
| [![Screenshot the error message about irrelevant information in the feedback provided](media/security-alert-triage-agent/feedback-irrelevant.png)](media/security-alert-triage-agent/feedback-irrelevant.png#lightbox) Part of the feedback provided can't be addressed as the agent currently doesn't support this type of input and therefore couldn't be translated to a lesson at all. | Rewrite your feedback and ensure that it follows the best practices. Select **Evaluate feedback** to try again. |
| [![Screenshot the error message about unsupported features in the feedback provided](media/security-alert-triage-agent/feedback-unsupported.png)](media/security-alert-triage-agent/feedback-unsupported.png#lightbox) The feedback contains input that the agent can support but it's not relevant to the email at hand and therefore couldn't be translated into an actionable lesson to be saved in the memory. | Rewrite your feedback and ensure that it addresses descriptions of the email that it can support. Then select **Evaluate feedback** to try again. |
| [![Screenshot the error message about conflicting data in the feedback provided](media/security-alert-triage-agent/feedback-conflict.png)](media/security-alert-triage-agent/feedback-conflict.png#lightbox) The given feedback conflicts with previous feedback given to a similar email. | In the feedback management page search for the feedback ID to view the feedback that it conflicts with. Based on your review, you can:- Reject the previous feedback in the feedback management page. Thereafter, select **Evaluate** to try inserting your feedback again.- Rewrite your given feedback in a way that isn't conflicting and then select **Evaluate feedback** for the agent to reevaluate your new input. |

Note

You can choose not to resolve feedback failures. You can leave your feedback and select **Save** without checking the box for teaching the agent. The feedback won't be saved to the agent's memory and will only be documented on the feedback management page for your future tracking classification changes.

When applicable feedback is approved and stored, the agent can apply it when triaging similar alerts in the future, subject to the same permissions and controls.

## Monitor and manage the Security Alert Triage Agent

To view agent metrics and manage the agent, go to the Security Alert Triage Agent card in the incident queue or the Agents page:

- To open the **Security Alert Triage Agent** page directly, select **Security Copilot &gt; Agents**, look for the Security Alert Triage Agent under **Agents in use** and select **Go to agent**.

    This page consists of two tabs: **Overview** and **Performance**.

    - The **Overview** tab provides details about the agent’s current status, identity, role, and recent activity.

        [![Screenshot of the Overview tab on the Security Alert Triage Agent page.](media/security-alert-triage-agent/phishing-triage-agent-page-overview.png)](media/security-alert-triage-agent/phishing-triage-agent-page-overview.png#lightbox)

        Select an activity from the **Recent activity** list to view details about the agent's investigation and the agent full workflow.

        [![Screenshot of the activity details pane that opens from the Security Alert Triage Agent page.](media/security-alert-triage-agent/security-alert-triage-agent-activity-details.png)](media/security-alert-triage-agent/security-alert-triage-agent-activity-details.png#lightbox)

        Select **See full agent workflow** to view a graphical representation of the agent’s decision-making process for that specific activity.

        [![Screenshot of the full agent workflow page that opens from the Security Alert Triage Agent page.](media/security-alert-triage-agent/security-alert-triage-agent-workflow.png)](media/security-alert-triage-agent/security-alert-triage-agent-workflow.png#lightbox)
    - The **Performance** tab displays key metrics about the agent’s activity over time, including daily activity, mean time to triage (MTTT), and SCU consumption.

        [![Screenshot of the Performance tab on the Security Alert Triage Agent page.](media/security-alert-triage-agent/phishing-triage-agent-page.png)](media/security-alert-triage-agent/phishing-triage-agent-page.png#lightbox)

    Select the ellipsis (...) at the top right corner of the page to access management options for the agent, as described in the sections below.

    Select **Pause** or **Run** to temporarily stop or restart the agent’s activities.
- To open the Security Alert Triage Agent card in the incident queue, select **Investigation & response &gt; Incidents & alerts &gt; Incidents** .

    The Security Alert Triage Agent card above the incident queue shows some of the agent’s key metrics, including **Incidents addressed**, which are incidents containing alerts that the agent classified as true threats or false alarms.

    This data helps demonstrate the agent’s impact and can be used to inform broader strategic conversations, highlight return on investment, or support decisions around scaling automation across your organization.

    Metrics are calculated based on the agent’s activity, beginning either from its first recorded incident or from the last 30 days - whichever is more recent.

    [![Screenshot of the incident queue with the Security Alert Triage Agent card highlighted.](/en-us/defender/media/agents-in-defender/phishing-triage/incident-queue-with-agent.png)](/en-us/defender/media/agents-in-defender/phishing-triage/incident-queue-with-agent.png#lightbox)

    Select **Manage agent** on the card to open the **Security Alert Triage Agent** page, which has more performance metrics and management options.

### Edit agent settings

To edit the agent’s settings:

1. Select **Security Copilot &gt; Agents**.
2. Look for the Security Alert Triage Agent under **Agents in use**, and select **Go to agent**.
3. Select the **ellipsis (...) &gt; Edit agent** at the top right corner of the **Security Alert Triage Agent** page.

    The **Edit agent** page has three tabs:

    - **Identity and role** - Change the agent’s identity. Select **Select a new identity** and follow the steps described in Assign the agent’s identity and permissions.
    - **Feedback** - View and manage user-submitted feedback. For more information, see View and manage feedback to the agent.
    - **Supported alerts** - View which of the supported alert types the agent can triage. To activate or deactivate specific alert types for the agent:

        1. Select **Edit supported alerts** to open the **Agent supported alerts** page.

            [![Screenshot of the Edit supported alerts option on the Edit agent page.](media/security-alert-triage-agent/edit-agent-supported-alerts.png)](media/security-alert-triage-agent/edit-agent-supported-alerts.png#lightbox)
        2. Toggle individual alert types on or off and select **Update**.

            [![Screenshot of the Agent supported alerts page with toggles for each alert type.](media/security-alert-triage-agent/agent-supported-alerts-settings.png)](media/security-alert-triage-agent/agent-supported-alerts-settings.png#lightbox)
        3. Select **Update role permissions** to apply the updates.

            [![Screenshot of Agent supported alerts panel with toggles for email, cloud, and identity alerts, and Update button highlighted.](media/security-alert-triage-agent/update-role-permissions-security-agent.png)](media/security-alert-triage-agent/update-role-permissions-security-agent.png#lightbox)

### View and manage feedback to the agent

The Security Alert Triage Agent learns from user-submitted feedback and improves its performance over time. It stores applicable feedback in its memory as lessons. You can view and manage feedback for the Security Alert Triage Agent on the **Agent feedback** page.

This page provides a comprehensive list of all feedback submitted to the agent. You can review key details for each piece of feedback, including:

- The agent’s original classification and the user-applied change
- The original feedback provided by the user, when changing the classification
- The translated lesson generated by the agent (if applicable)
- Feedback status: in use, not in use, or conflict
- The user who provided the feedback
- Feedback submission date, feedback ID, alert ID, and the incident ID

[![Screenshot of the Feedback management page](media/security-alert-triage-agent/phishing-triage-feedback-management.png)](media/security-alert-triage-agent/phishing-triage-feedback-management.png#lightbox)

This table explains the feedback statuses:

| Status | Description |
| --- | --- |
| In use | The feedback was successfully converted into a lesson in the agent’s memory and is actively used to triage and classify similar incidents. |
| Conflict | The feedback provided conflicted with previously provided feedback in a similar incident. Learn how you can resolve feedback failures. |
| Not in use | The feedback was either not incorporated into the agent's memory or not marked by the user for teaching. Rejected lessons appear as "not in use" and are saved only for auditing, not for triaging and classifying incidents. For more details, select the details panel. |

Tip

Feedback can only be managed individually. Bulk management of multiple feedback entries isn't currently supported.

To view and manage user-submitted feedback:

1. Select **Security Copilot &gt; Agents**, look for the Security Alert Triage Agent under **Agents in use** and select **Go to agent**.
2. Select the **ellipsis (...) &gt; Edit agent** at the top right corner of the page. This opens the **Edit agent** page.
3. Select **Feedback** in the left pane to open the **Agent feedback** page.
4. Select an entry from the feedback list to open the **Review feedback** pane.
5. Check the details of the feedback provided, the agent’s lesson, the classification changes, and other important details.

    [![Screenshot of the Review feedback pane](/en-us/defender/media/agents-in-defender/phishing-triage/review-feedback-pane.png)](/en-us/defender/media/agents-in-defender/phishing-triage/review-feedback-pane.png#lightbox)
6. To reject specific feedback, select **Reject feedback**. The agent stops using the feedback in future triage decisions.

    Note

    To reject feedback provided, you need the **Security Administrator** role in Microsoft Entra ID.

### Remove the agent

When you remove the agent, triage and classification of new incidents stop, and all feedback is deleted. However, the history of previously triaged incidents is retained for your reference.

To remove the agent:

1. Select **Security Copilot &gt; Agents**, look for the Security Alert Triage Agent under **Agents in use** and select **Go to agent**.
2. Select the ellipsis (...) at the top right corner of the page, and then select **Remove**.

## Frequently asked questions

This section answers commonly asked questions about the Security Alert Triage Agent. For information about the agent's capabilities and requirements, see How the Security Alert Triage Agent works and Prerequisites.

### What is the Security Alert Triage Agent, how does it differ from the Phishing Triage Agent, and how do I onboard if I’m already using the agent to triage phishing alerts?

The **Security Alert Triage Agent** is an autonomous Microsoft Security Copilot agent in Microsoft Defender that helps security teams triage alerts at scale. It evaluates alerts using AI‑driven reasoning, arrives at a verdict, and records its conclusions directly in Microsoft Defender incidents to help analysts prioritize what requires action.

The Security Alert Triage Agent is the same agent as the [Phishing Triage Agent](phishing-triage-agent), extended to triage additional alert types beyond email and collaboration. The Security Alert Triage Agent is modular - you choose which alert types you want the agent to triage. The agent now extends to identity and cloud alerts, starting with containers, which are currently in preview. Email and collaboration alert triage capabilities are already generally available (GA). The set of supported alerts is expected to grow over time.

If you’re already using the Phishing Triage Agent, you don’t need to install a new agent. Your existing agent will continue to operate, and you can enable the additional alert types through configuration. To onboard to the expanded capabilities, review the Security Alert Triage Agent prerequisites for the additional alert types and edit the Security Alert Triage Agent settings to select the alert types you want to enable.

Your existing phishing triage configuration and feedback carry over automatically. For more information, see How the Security Alert Triage Agent works and Set up the Security Alert Triage Agent.

### When is the agent triggered?

This agent runs automatically when a new alert is detected. Built in tuning rules resolving supported alert types will be disabled during setup.

### Can the Security Alert Triage Agent be trusted?

Microsoft AI agents follow strict Responsible AI guidelines and undergo thorough reviews to ensure compliance with all AI standards and safeguards. The Security Alert Triage Agent is fully incorporated into these controls. During setup, you assign the agent an identity and configure it with the minimum permissions required for its operation, ensuring that it doesn't have unnecessary permissions. All agent activities are logged in detail, with the complete flow available for review by analysts and admins at any time. Feedback provided to the agent to help it adapt to the organization's environment is logged, reflected in the system, and accessible for review and modification by admins as needed.

### How does the agent differ from a standard SOAR solution?

While both SOAR solutions and the Security Alert Triage Agent automate aspects of security operations, they use different approaches.

SOAR solutions typically rely on predefined, rule-based workflows that require manual configuration and ongoing maintenance. In contrast, the Security Alert Triage Agent uses reasoning-based analysis to triage alerts and record classifications within Microsoft Defender, with human oversight and optional feedback where supported.

The agent operates within defined permissions and workflows in Microsoft Defender and does not replace existing investigation or response tools.

### What level of visibility and control do I have over the agent?

Microsoft provides tools for organizations to maintain visibility into and control over the Security Alert Triage Agent from deployment through ongoing operations. [The agents adhere to Microsoft's Responsible AI (RAI) standards](/en-us/copilot/security/rai-faqs-security-copilot-agents) for fairness, reliability, safety, privacy, security, inclusiveness, transparency, and accountability. Administrators configure the agent’s identity and access levels during installation, following least-privilege principles. Security and IT teams can authorize specific actions, monitor performance, and review outputs directly in Microsoft Defender. Capacity consumption and data access limits are also configurable by administrators.

The Security Alert Triage Agent operates within a zero-trust environment. The system enforces organizational policies on every agent action by evaluating the intent and scope of each operation. All decisions, reasoning, and actions taken by the agent are transparently documented as a decision tree within Defender and recorded in Microsoft Purview audit logs for traceability and compliance.

### I want to try the Security Alert Triage Agent - how do I set it up in Microsoft Defender?

To set up the agent, you must have access to **Security Copilot in Microsoft Defender** and meet the necessary prerequisites. If you haven’t onboarded to Security Copilot, see [Get started with Security Copilot](/en-us/copilot/security/get-started-security-copilot) or contact your Microsoft representative. After you've onboarded to Security Copilot, it can take a bit of time for the agent setup option to become available in the Microsoft Defender portal.

### I've tried the Security Alert Triage Agent - how can I estimate the SCU capacity needed for the agent in my organization?

It's important to ensure that your organization has sufficient SCUs for healthy agent operation. To evaluate SCU usage and plan capacity going forward, see the [Usage monitoring dashboard in the Security Copilot portal](https://securitycopilot.microsoft.com/usage-monitoring) and check whether you're entitled to SCUs as part of the [Microsoft Security Copilot inclusion model](/en-us/copilot/security/security-copilot-inclusion). The dashboard shows:

- **Cost per email processed**
- **Capacity consumption over time**

You can also export the dashboard data into Excel for more detailed analysis, and to filter on agent operations only.

After evaluating your SCU usage needs, update the SCU capacity for your organization. For more information about managing SCUs, see [Manage security compute unit usage in Security Copilot](/en-us/copilot/security/manage-usage).