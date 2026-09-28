---
layout: Conceptual
title: Responding to ransomware attacks - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/playbook-responding-ransomware-m365-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: This article provides a generalized playbook for responding to ransomware attacks.
search.appverid: MET150
ms.author: pauloliveria
author: poliveria
ms.reviewer: noriordan
audience: ITPro
ms.topic: concept-article
ms.date: 2022-05-30T00:00:00.0000000Z
ms.service: defender-xdr
ms.localizationpriority: medium
ms.collection:
- msftsolution-secops
- tier1
ms.custom: cx-rw
f1.keywords: NOCSH
locale: en-us
document_id: f18a1397-a1f1-424a-28b0-cc93272377dd
document_version_independent_id: f18a1397-a1f1-424a-28b0-cc93272377dd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/playbook-responding-ransomware-m365-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: playbook-responding-ransomware-m365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/playbook-responding-ransomware-m365-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 849dff35-6bbd-fc94-ff26-30cbb0bfc125
---

# Responding to ransomware attacks - Microsoft Defender XDR | Microsoft Learn

Note

Want to experience Microsoft Defender XDR? Learn more about how you can [evaluate and pilot Microsoft Defender XDR](/en-us/defender-xdr/eval-overview?ocid=cx-docs-MTPtriallab).

When you suspect you were or are currently under a ransomware attack, establish secure communications with your incident response team immediately. They can perform the following response phases to disrupt the attack and mitigate the damage:

- Investigation and containment
- Eradication and recovery

This article provides a generalized playbook for responding to ransomware attacks. Consider adapting the described steps and tasks in this article to your own security operations playbook. NOTE: For information about preventing ransomware attacks, see [Quickly deploy ransomware preventions](/en-us/security/ransomware/protect-against-ransomware).

## Containment

Containment and investigation should occur as simultaneously as possible; however, you should focus on quickly achieving containment, so you have more time to investigate. These steps help you determine the scope of the attack and to isolate it to only affected entities, such as user accounts and devices.

### Step 1: Assess the scope of the incident

Run through this list of questions and tasks to discover the extent of the attack. Microsoft Defender can provide a consolidated view of all impacted or at-risk assets to aid in your incident response assessment. See [Incident response with Microsoft Defender](incidents-overview). You can use the alerts and the evidence list in the incident to determine:

- Which user accounts might be compromised?
    - Which accounts were used to deliver the payload?
- Which [onboarded](/en-us/defender-endpoint/investigate-machines) and [discovered](/en-us/defender-endpoint/device-discovery)devices are affected and how?
    - Originating devices
    - Impacted devices
    - Suspicious devices
- Identify any network communication that is associated with the incident.
- Which applications are affected?
- What payloads were spread?
- How is the attacker communicating with the compromised devices? (Network protection must be [enabled](/en-us/defender-endpoint/enable-network-protection)):
    - Go to the [indicators page](/en-us/defender-endpoint/indicator-ip-domain#create-indicators-for-ips-and-urlsdomains) to add a block for the IP and URL (if you have that information).
- What was the payload delivery medium?

### Step 2: Preserve existing systems

Run through this list of tasks and questions to protect existing systems from attack:

- If you have online backups, consider disconnecting the backup system from the network until you're confident that the attack is contained, see [Backup and restore plan to protect against ransomware](/en-us/azure/security/fundamentals/backup-plan-to-protect-against-ransomware).
- If you're experiencing or expect an imminent and active ransomware deployment:
    - [Suspend privileged and local accounts](investigate-users) that you suspect are part of the attack. You can do this from the **Users** tab in the properties of the incident in the Microsoft Defender portal.
    - Stop all [remote logon sessions](/en-us/defender-for-identity/playbook-domain-dominance).
    - Reset the compromised user account passwords and require the users of compromised user accounts to sign in again.
    - Do the same for user accounts that might be compromised.
    - If shared local accounts are compromised, have your IT admin help you to enforce a password change across all exposed devices. Example Kusto query:

```kusto
DeviceLogonEvents | where DeviceName  contains (AccountDomain) | take 10
```

- For the devices that aren't yet isolated and aren't part of the critical infrastructure:
    - Isolate compromised devices from the network but don't shut them off.
    - If you identify the originating or spreader devices, isolate those first.
- Preserve compromised systems for analysis.

### Step 3: Prevent the spread

Use this list to keep the attack from spreading to additional entities.

- If shared local accounts are being used in the attack, consider [Blocking Remote Use of Local Accounts](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/blocking-remote-use-of-local-accounts/ba-p/701042).
    - Kusto query for all network logons that are local admins:

```kusto
DeviceLogonEvents
| where IsLocalAdmin == true and AccountDomain == DeviceName
| extend IsLocalLogon = tobool(todynamic(AdditionalFields).IsLocalLogon)
| where IsLocalLogon==false
```

- Kusto query for non-RDP logons (more realistic for most networks):

```kusto
DeviceLogonEvents
| where IsLocalAdmin == true and AccountDomain == DeviceName and LogonType != 'RemoteInteractive'
| extend IsLocalLogon = tobool(todynamic(AdditionalFields).IsLocalLogon)
| where IsLocalLogon==false
```

- Quarantine and add indicators for files that are infected.
- Ensure that your antivirus solution is configurable in its optimal protection state. For Microsoft Defender Antivirus, this includes:
    - [Real time protection](/en-us/defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus) is enabled.
    - [Tamper protection](/en-us/defender-endpoint/tamper-protection-overview) is enabled. In the Microsoft Defender portal, select **Settings &gt; Endpoints &gt; Advanced features &gt; Tamper protection**.
    - [Attack surface reduction rules](/en-us/defender-endpoint/enable-attack-surface-reduction) are enabled.
    - [Cloud protection](/en-us/defender-endpoint/cloud-protection-configure) is enabled.
- Disable Exchange ActiveSync and OneDrive sync.
    - To disable Exchange ActiveSync for a mailbox, see [How to disable Exchange ActiveSync for users in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-exchange-activesync).
    - To disable other types of access to a mailbox, see:
        - [Enable or disable MAPI for a mailbox](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-mapi).
        - [Enable or Disable POP3 or IMAP4 access for a user](/en-us/exchange/clients-and-mobile-in-exchange-online/pop3-and-imap4/enable-or-disable-pop3-or-imap4-access).
    - Pausing OneDrive sync helps protect your cloud data from being updated by potentially infected devices. For more information, see [How to Pause and Resume sync in OneDrive](https://support.microsoft.com/office/how-to-pause-and-resume-sync-in-onedrive-2152bfa4-a2a5-4d3a-ace8-92912fb4421e).
- Apply relevant patches and configuration changes on affected systems.
- Block ransomware communications using internal and external controls.
- Purge cached content

## Investigation

Use this section to investigate the attack and plan your response.

### Assess your current situation

- What initially made you aware of the ransomware attack?
    - If IT staff identified the initial threat—such as noticing backups being deleted, antivirus alerts, endpoint detection and response (EDR) alerts, or suspicious system changes—it's often possible to take quick decisive measures to thwart the attack, typically by the containment actions described in this article.
- What date and time did you first learn of the incident?
    - What system and security updates weren't installed on devices on that date? This is important to understand what vulnerabilities might have been leveraged so they can be addressed on other devices.
    - What user accounts were used on that date?
    - What new user accounts were created since that date?
    - What programs were added to automatically start around the time that the incident occurred?
- Is there any indication that the attacker is currently accessing systems?
    - Are there any suspected compromised systems that are experiencing unusual activity?
    - Are there any suspected compromised accounts that appear to be actively used by the adversary?
    - Is there any evidence of active command-and-control (C2) servers in EDR, firewall, VPN, web proxy, and other logs?

### Identify the ransomware process

- Using [advanced hunting](advanced-hunting-overview), search for the identified process in the process creation events on other devices.

### Look for exposed credentials in the infected devices

- For user accounts whose credentials were potentially compromised, reset the account passwords, and require the users to sign in again.
- The following IOAs might indicate lateral movement:

Click to expand

- SuspiciousExploratoryCommands
- MLFileBasedAlert
- IfeoDebuggerPersistence
- SuspiciousRemoteFileDropAndExecution
- ExploratoryWindowsCommands
- IoaStickyKeys
- Mimikatz Defender Amplifier
- Network scanning tool used by PARINACOTA
- DefenderServerAlertMSSQLServer
- SuspiciousLowReputationFileDrop
- SuspiciousServiceExecution
- AdminUserAddition
- MimikatzArtifactsDetector
- Scuba-WdigestEnabledToAccessCredentials
- DefenderMalware
- MLSuspCmdBehavior
- MLSuspiciousRemoteInvocation
- SuspiciousRemoteComponentInvocation
- SuspiciousWmiProcessCreation
- MLCmdBasedWithRemoting
- Process Accesses Lsass
- Suspicious Rundll32 Process Execution
- BitsAdmin
- DefenderCobaltStrikeDetection
- DefenderHacktool
- IoaSuspPSCommandline
- Metasploit
- MLSuspToolBehavior
- RegistryQueryForPasswords
- SuspiciousWdavExclusion
- ASEPRegKey
- CobaltStrikeExecutionDetection
- DefenderBackdoor
- DefenderBehaviorSuspiciousActivity
- DefenderMalwareExecuted
- DefenderServerAlertDomainController
- DupTokenPrivilegeEscalationDetector
- FakeWindowsBinary
- IoaMaliciousCmdlets
- LivingOffTheLandBinary
- MicrosoftSignedBinaryAbuse
- MicrosoftSignedBinaryScriptletAbuse
- MLFileBasedWithRemoting
- MLSuspSvchostBehavior
- ReadSensitiveMemory
- RemoteCodeInjection-IREnabled
- Scuba-EchoSeenOverPipeOnLocalhost
- Scuba-SuspiciousWebScriptFileDrop
- Suspicious DLL registration by odbcconf
- Suspicious DPAPI Activity
- Suspicious Exchange Process Execution
- Suspicious scheduled task launch
- SuspiciousLdapQueryDetector
- SuspiciousScheduledTaskRegistration
- Untrusted application opens a RDP connection

### Identify the line of business (LOB) apps that are unavailable due to the incident

- Does the app require an identity?
    - How is authentication performed?
    - How are credentials such as certificates or secrets stored and managed?
- Are evaluated backups of the application, its configuration, and its data available?
- Determine your compromise recovery process.

## Eradication and recovery

Use these steps to eradicate the threat and recover damaged resources.

### Step 1: Verify your backups

If you have offline backups, you can probably restore the data that has been encrypted after you've removed the ransomware payload (malware) from your environment and after you've verified that there's no unauthorized access in your Microsoft 365 tenant.

### Step 2: Add indicators

Add any known attacker communication channels as indicators, blocked in firewalls, in your proxy servers, and on endpoints.

### Step 3: Reset compromised users

Reset the passwords of any known compromised user accounts and require a new sign-in.

- Consider resetting the passwords for any privileged account with broad administrative authority, such as the members of the Domain Admins group.
- If a user account might have been created by an attacker, disable the account. Don't delete the account unless there are no plans to perform security forensics for the incident.

### Step 4: Isolate attacker control points

Isolate any known attacker control points inside the enterprise from the Internet.

### Step 5: Remove malware

Remove the malware from the affected devices.

- Run a full, current antivirus scan on all suspected computers and devices to detect and remove the payload that is associated with the ransomware.
- Don't forget to scan devices that synchronize data or the targets of mapped network drives.

### Step 6: Recover files on a cleaned device

Recover files on a cleaned device.

- You can use [File History](https://support.microsoft.com/help/17128) in Windows 11, Windows 10, Windows 8.1, and System Protection in Windows 7 to attempt to recover your local files and folders.

### Step 7: Recover files in OneDrive for Business

Recover files in OneDrive for Business.

- Files Restore in OneDrive for Business allows you to restore an entire OneDrive to a previous point in time within the last 30 days. For more information, see [Restore your OneDrive](https://support.microsoft.com/office/restore-your-onedrive-fa231298-759d-41cf-bcd0-25ac53eb8a15).

### Step 8: Recover deleted email

Recover deleted email.

- In the rare case that the ransomware deleted all the email in a mailbox, you can recover the deleted items. See [Recover deleted messages in a user's mailbox in Exchange Online](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages).

### Step 9: Re-enable Exchange ActiveSync and OneDrive sync

- After you've cleaned your computers and devices and recovered the data, you can re-enable Exchange ActiveSync and OneDrive sync that you previously disabled in step 3 of containment.

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).