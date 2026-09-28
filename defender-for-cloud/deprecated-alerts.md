---
layout: Conceptual
title: Reference table for deprecated security alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/deprecated-alerts
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: This article lists deprecated security alerts in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5477b4de-08c4-bece-3dfa-e5faf51e81d5
document_version_independent_id: b01fb659-a541-824f-f73c-c7fe1def4562
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/deprecated-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/deprecated-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/deprecated-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 607d88ef-6fdf-d855-6e85-8d967ef1f047
---

# Reference table for deprecated security alerts - Microsoft Defender for Cloud | Microsoft Learn

This article lists deprecated security alerts in Microsoft Defender for Cloud.

## Deprecated Defender for Containers alerts

The following lists include the Defender for Containers security alerts which were deprecated.

### **Manipulation of host firewall detected**

(K8S.NODE\_FirewallDisabled)

**Description**: Analysis of processes running within a container or directly on a Kubernetes node, has detected a possible manipulation of the on-host firewall. Attackers will often disable this to exfiltrate data.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: DefenseEvasion, Exfiltration

**Severity**: Medium

### **Suspicious use of DNS over HTTPS**

(K8S.NODE\_SuspiciousDNSOverHttps)

**Description**: Analysis of processes running within a container or directly on a Kubernetes node, has detected the use of a DNS call over HTTPS in an uncommon fashion. This technique is used by attackers to hide calls out to suspect or malicious sites.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: DefenseEvasion, Exfiltration

**Severity**: Medium

### **A possible connection to malicious location has been detected**

(K8S.NODE\_ThreatIntelCommandLineSuspectDomain)

**Description**: Analysis of processes running within a container or directly on a Kubernetes node, has detected a connection to a location that has been reported to be malicious or unusual. This is an indicator that a compromise might have occurred.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: InitialAccess

**Severity**: Medium

### **Digital currency mining activity**

(K8S.NODE\_CurrencyMining)

**Description**: Analysis of DNS transactions detected digital currency mining activity. Such activity, while possibly legitimate user behavior, is frequently performed by attackers following compromise of resources. Typical related attacker activity is likely to include the download and execution of common mining tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

## Deprecated Defender for Servers Linux alerts

### VM\_AbnormalDaemonTermination

**Alert Display Name**: Abnormal Termination

**Severity**: Low

### VM\_BinaryGeneratedFromCommandLine

**Alert Display Name**: Suspicious binary detected

**Severity**: Medium

### VM\_CommandlineSuspectDomain Suspicious

**Alert Display Name**: domain name reference

**Severity**: Low

### VM\_CommonBot

**Alert Display Name**: Behavior similar to common Linux bots detected

**Severity**: Medium

### VM\_CompCommonBots

**Alert Display Name**: Commands similar to common Linux bots detected

**Severity**: Medium

### VM\_CompSuspiciousScript

**Alert Display Name**: Shell Script Detected

**Severity**: Medium

### VM\_CompTestRule

**Alert Display Name**: Composite Analytic Test Alert

**Severity**: Low

### VM\_CronJobAccess

**Alert Display Name**: Manipulation of scheduled tasks detected

**Severity**: Informational

### VM\_CryptoCoinMinerArtifacts

**Alert Display Name**: Process associated with digital currency mining detected

**Severity**: Medium

### VM\_CryptoCoinMinerDownload

**Alert Display Name**: Possible Cryptocoinminer download detected

**Severity**: Medium

### VM\_CryptoCoinMinerExecution

**Alert Display Name**: Potential crypto coin miner started

**Severity**: Medium

### VM\_DataEgressArtifacts

**Alert Display Name**: Possible data exfiltration detected

**Severity**: Medium

### VM\_DigitalCurrencyMining

**Alert Display Name**: Digital currency mining related behavior detected

**Severity**: High

### VM\_DownloadAndRunCombo

**Alert Display Name**: Suspicious Download Then Run Activity

**Severity**: Medium

### VM\_EICAR

**Alert Display Name**: Microsoft Defender for Cloud test alert (not a threat)

**Severity**: High

### VM\_ExecuteHiddenFile

**Alert Display Name**: Execution of hidden file

**Severity**: Informational

### VM\_ExploitAttempt

**Alert Display Name**: Possible command line exploitation attempt

**Severity**: Medium

### VM\_ExposedDocker

**Alert Display Name**: Exposed Docker daemon on TCP socket

**Severity**: Medium

### VM\_FairwareMalware

**Alert Display Name**: Behavior similar to Fairware ransomware detected

**Severity**: Medium

### VM\_FirewallDisabled

**Alert Display Name**: Manipulation of host firewall detected

**Severity**: Medium

### VM\_HadoopYarnExploit

**Alert Display Name**: Possible exploitation of Hadoop Yarn

**Severity**: Medium

### VM\_HistoryFileCleared

**Alert Display Name**: A history file has been cleared

**Severity**: Medium

### VM\_KnownLinuxAttackTool

**Alert Display Name**: Possible attack tool detected

**Severity**: Medium

### VM\_KnownLinuxCredentialAccessTool

**Alert Display Name**: Possible credential access tool detected

**Severity**: Medium

### VM\_KnownLinuxDDoSToolkit

**Alert Display Name**: Indicators associated with DDOS toolkit detected

**Severity**: Medium

### VM\_KnownLinuxScreenshotTool

**Alert Display Name**: Screenshot taken on host

**Severity**: Low

### VM\_LinuxBackdoorArtifact

**Alert Display Name**: Possible backdoor detected

**Severity**: Medium

### VM\_LinuxReconnaissance

**Alert Display Name**: Local host reconnaissance detected

**Severity**: Medium

### VM\_MismatchedScriptFeatures

**Alert Display Name**: Script extension mismatch detected

**Severity**: Medium

### VM\_MitreCalderaTools

**Alert Display Name**: MITRE Caldera agent detected

**Severity**: Medium

### VM\_NewSingleUserModeStartupScript

**Alert Display Name**: Detected Persistence Attempt

**Severity**: Medium

### VM\_NewSudoerAccount

**Alert Display Name**: Account added to sudo group

**Severity**: Low

### VM\_OverridingCommonFiles

**Alert Display Name**: Potential overriding of common files

**Severity**: Medium

### VM\_PrivilegedContainerArtifacts

**Alert Display Name**: Container running in privileged mode

**Severity**: Low

### VM\_PrivilegedExecutionInContainer

**Alert Display Name**: Command within a container running with high privileges

**Severity**: Low

### VM\_ReadingHistoryFile

**Alert Display Name**: Unusual access to bash history file

**Severity**: Informational

### VM\_ReverseShell

**Alert Display Name**: Potential reverse shell detected

**Severity**: Medium

### VM\_SshKeyAccess

**Alert Display Name**: Process seen accessing the SSH authorized keys file in an unusual way

**Severity**: Low

### VM\_SshKeyAddition

**Alert Display Name**: New SSH key added

**Severity**: Low

### VM\_SuspectCompilation

**Alert Display Name**: Suspicious compilation detected

**Severity**: Medium

### VM\_SuspectConnection

**Alert Display Name**: An uncommon connection attempt detected

**Severity**: Medium

### VM\_SuspectDownload

**Alert Display Name**: Detected file download from a known malicious source

**Severity**: Medium

### VM\_SuspectDownloadArtifacts

**Alert Display Name**: Detected suspicious file download

**Severity**: Low

### VM\_SuspectExecutablePath

**Alert Display Name**: Executable found running from a suspicious location

**Severity**: Medium

### VM\_SuspectHtaccessFileAccess

**Alert Display Name**: Access of htaccess file detected

**Severity**: Medium

### VM\_SuspectInitialShellCommand

**Alert Display Name**: Suspicious first command in shell

**Severity**: Low

### VM\_SuspectMixedCaseText

**Alert Display Name**: Detected anomalous mix of uppercase and lowercase characters in command line

**Severity**: Medium

### VM\_SuspectNetworkConnection

**Alert Display Name**: Suspicious network connection

**Severity**: Informational

### VM\_SuspectNohup

**Alert Display Name**: Detected suspicious use of the nohup command

**Severity**: Medium

### VM\_SuspectPasswordChange

**Alert Display Name**: Possible password change using crypt-method detected

**Severity**: Medium

### VM\_SuspectPasswordFileAccess

**Alert Display Name**: Suspicious password access

**Severity**: Informational

### VM\_SuspectPhp

**Alert Display Name**: Suspicious PHP execution detected

**Severity**: Medium

### VM\_SuspectPortForwarding

**Alert Display Name**: Potential port forwarding to external IP address

**Severity**: Medium

### VM\_SuspectProcessAccountPrivilegeCombo

**Alert Display Name**: Process running in a service account became root unexpectedly

**Severity**: Medium

### VM\_SuspectProcessTermination

**Alert Display Name**: Security-related process termination detected

**Severity**: Low

### VM\_SuspectUserAddition

**Alert Display Name**: Detected suspicious use of the useradd command

**Severity**: Medium

### VM\_SuspiciousCommandLineExecution

**Alert Display Name**: Suspicious command execution

**Severity**: High

### VM\_SuspiciousDNSOverHttps

**Alert Display Name**: Suspicious use of DNS over HTTPS

**Severity**: Medium

### VM\_SystemLogRemoval

**Alert Display Name**: Possible Log Tampering Activity Detected

**Severity**: Medium

### VM\_ThreatIntelCommandLineSuspectDomain

**Alert Display Name**: A possible connection to malicious location has been detected

**Severity**: Medium

### VM\_ThreatIntelSuspectLogon

**Alert Display Name**: A logon from a malicious IP has been detected

**Severity**: High

### VM\_TimerServiceDisabled

**Alert Display Name**: Attempt to stop apt-daily-upgrade.timer service detected

**Severity**: Informational

### VM\_TimestampTampering

**Alert Display Name**: Suspicious file timestamp modification

**Severity**: Low

### VM\_Webshell

**Alert Display Name**: Possible malicious web shell detected

**Severity**: Medium

## Deprecated Defender for Servers Windows alerts

### SCUBA\_MULTIPLEACCOUNTCREATE

**Alert Display Name**: Suspicious creation of accounts on multiple hosts

**Severity**: Medium

### SCUBA\_PSINSIGHT\_CONTEXT

**Alert Display Name**: Suspicious use of PowerShell detected

**Severity**: Informational

### SCUBA\_RULE\_AddGuestToAdministrators

**Alert Display Name**: Addition of Guest account to Local Administrators group

**Severity**: Medium

### SCUBA\_RULE\_Apache\_Tomcat\_executing\_suspicious\_commands

**Alert Display Name**: Apache\_Tomcat\_executing\_suspicious\_commands

**Severity**: Medium

### SCUBA\_RULE\_KnownBruteForcingTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_KnownCollectionTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_KnownDefenseEvasionTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_KnownExecutionTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_KnownPassTheHashTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_KnownSpammingTools

**Alert Display Name**: Suspicious process executed

**Severity**: Medium

### SCUBA\_RULE\_Lowering\_Security\_Settings

**Alert Display Name**: Detected the disabling of critical services

**Severity**: Medium

### SCUBA\_RULE\_OtherKnownHackerTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### SCUBA\_RULE\_RDP\_session\_hijacking\_via\_tscon

**Alert Display Name**: Suspect integrity level indicative of RDP hijacking

**Severity**: Medium

### SCUBA\_RULE\_RDP\_session\_hijacking\_via\_tscon\_service

**Alert Display Name**: Suspect service installation

**Severity**: Medium

### SCUBA\_RULE\_Suppress\_pesky\_unauthorized\_use\_prohibited\_notices

**Alert Display Name**: Detected suppression of legal notice displayed to users at logon

**Severity**: Low

### SCUBA\_RULE\_WDigest\_Enabling

**Alert Display Name**: Detected enabling of the WDigest UseLogonCredential registry key

**Severity**: Medium

### VM.Windows\_ApplockerBypass

**Alert Display Name**: Potential attempt to bypass AppLocker detected

**Severity**: High

### VM.Windows\_BariumKnownSuspiciousProcessExecution

**Alert Display Name**: Detected suspicious file creation

**Severity**: High

### VM.Windows\_Base64EncodedExecutableInCommandLineParams

**Alert Display Name**: Detected encoded executable in command line data

**Severity**: High

### VM.Windows\_CalcsCommandLineUse

**Alert Display Name**: Detected suspicious use of Cacls to lower the security state of the system

**Severity**: Medium

### VM.Windows\_CommandLineStartingAllExe

**Alert Display Name**: Detected suspicious command line used to start all executables in a directory

**Severity**: Medium

### VM.Windows\_DisablingAndDeletingIISLogFiles

**Alert Display Name**: Detected actions indicative of disabling and deleting IIS log files

**Severity**: Medium

### VM.Windows\_DownloadUsingCertutil

**Alert Display Name**: Suspicious download using Certutil detected

**Severity**: Medium

### VM.Windows\_EchoOverPipeOnLocalhost

**Alert Display Name**: Detected suspicious named pipe communications

**Severity**: High

### VM.Windows\_EchoToConstructPowerShellScript

**Alert Display Name**: Dynamic PowerShell script construction

**Severity**: Medium

### VM.Windows\_ExecutableDecodedUsingCertutil

**Alert Display Name**: Detected decoding of an executable using built-in certutil.exe tool

**Severity**: Medium

### VM.Windows\_FileDeletionIsSospisiousLocation

**Alert Display Name**: Suspicious file deletion detected

**Severity**: Medium

### VM.Windows\_KerberosGoldenTicketAttack

**Alert Display Name**: Suspected Kerberos Golden Ticket attack parameters observed

**Severity**: Medium

### VM.Windows\_KeygenToolKnownProcessName

**Alert Display Name**: Detected possible execution of keygen executable Suspicious process executed

**Severity**: Medium

### VM.Windows\_KnownCredentialAccessTools

**Alert Display Name**: Suspicious process executed

**Severity**: High

### VM.Windows\_KnownSuspiciousPowerShellScript

**Alert Display Name**: Suspicious use of PowerShell detected

**Severity**: High

### VM.Windows\_KnownSuspiciousSoftwareInstallation

**Alert Display Name**: High risk software detected

**Severity**: Medium

### VM.Windows\_MsHtaAndPowerShellCombination

**Alert Display Name**: Detected suspicious combination of HTA and PowerShell

**Severity**: Medium

### VM.Windows\_MultipleAccountsQuery

**Alert Display Name**: Multiple Domain Accounts Queried

**Severity**: Medium

### VM.Windows\_NewAccountCreation

**Alert Display Name**: Account creation detected

**Severity**: Informational

### VM.Windows\_ObfuscatedCommandLine

**Alert Display Name**: Detected obfuscated command line.

**Severity**: High

### VM.Windows\_PcaluaUseToLaunchExecutable

**Alert Display Name**: Detected suspicious use of Pcalua.exe to launch executable code

**Severity**: Medium

### VM.Windows\_PetyaRansomware

**Alert Display Name**: Detected Petya ransomware indicators

**Severity**: High

### VM.Windows\_PowerShellPowerSploitScriptExecution

**Alert Display Name**: Suspicious PowerShell cmdlets executed

**Severity**: Medium

### VM.Windows\_RansomwareIndication

**Alert Display Name**: Ransomware indicators detected

**Severity**: High

### VM.Windows\_SqlDumperUsedSuspiciously

**Alert Display Name**: Possible credential dumping detected [seen multiple times]

**Severity**: Medium

### VM.Windows\_StopCriticalServices

**Alert Display Name**: Detected the disabling of critical services

**Severity**: Medium

### VM.Windows\_SubvertingAccessibilityBinary

**Alert Display Name**: Sticky keys attack detected Suspicious account creation detected Medium

### VM.Windows\_SuspiciousAccountCreation

**Alert Display Name**: Suspicious Account Creation Detected

**Severity**: Medium

### VM.Windows\_SuspiciousFirewallRuleAdded

**Alert Display Name**: Detected suspicious new firewall rule

**Severity**: Medium

### VM.Windows\_SuspiciousFTPSSwitchUsage

**Alert Display Name**: Detected suspicious use of FTP -s switch

**Severity**: Medium

### VM.Windows\_SuspiciousSQLActivity

**Alert Display Name**: Suspicious SQL activity

**Severity**: Medium

### VM.Windows\_SVCHostFromInvalidPath

**Alert Display Name**: Suspicious process executed

**Severity**: High

### VM.Windows\_SystemEventLogCleared

**Alert Display Name**: The Windows Security log was cleared

**Severity**: Informational

### VM.Windows\_TelegramInstallation

**Alert Display Name**: Detected potentially suspicious use of Telegram tool

**Severity**: Medium

### VM.Windows\_UndercoverProcess

**Alert Display Name**: Suspiciously named process detected

**Severity**: High

### VM.Windows\_UserAccountControlBypass

**Alert Display Name**: Detected change to a registry key that can be abused to bypass UAC

**Severity**: Medium

### VM.Windows\_VBScriptEncoding

**Alert Display Name**: Detected suspicious execution of VBScript.Encode command

**Severity**: Medium

### VM.Windows\_WindowPositionRegisteryChange

**Alert Display Name**: Suspicious WindowPosition registry value detected

**Severity**: Low

### VM.Windows\_ZincPortOpenningUsingFirewallRule

**Alert Display Name**: Malicious firewall rule created by ZINC server implant

**Severity**: High

### VM\_DigitalCurrencyMining

**Alert Display Name**: Digital currency mining related behavior detected

**Severity**: High

### VM\_MaliciousSQLActivity

**Alert Display Name**: Malicious SQL activity

**Severity**: High

### VM\_ProcessWithDoubleExtensionExecution

**Alert Display Name**: Suspicious double extension file executed

**Severity**: High

### VM\_RegistryPersistencyKey

**Alert Display Name**: Windows registry persistence method detected

**Severity**: Low

### VM\_ShadowCopyDeletion

**Alert Display Name**: Suspicious Volume Shadow Copy Activity Executable found running from a suspicious location

**Severity**: High

### VM\_SuspectExecutablePath

**Alert Display Name**: Executable found running from a suspicious location Detected anomalous mix of uppercase and lowercase characters in command line

**Severity**: Informational

Medium

### VM\_SuspectPhp

**Alert Display Name**: Suspicious PHP execution detected

**Severity**: Medium

### VM\_SuspiciousCommandLineExecution

**Alert Display Name**: Suspicious command execution

**Severity**: High

### VM\_SuspiciousScreenSaverExecution

**Alert Display Name**: Suspicious Screensaver process executed

**Severity**: Medium

### VM\_SvcHostRunInRareServiceGroup

**Alert Display Name**: Rare SVCHOST service group executed

**Severity**: Informational

### VM\_SystemProcessInAbnormalContext

**Alert Display Name**: Suspicious system process executed

**Severity**: Medium

### VM\_ThreatIntelCommandLineSuspectDomain

**Alert Display Name**: A possible connection to malicious location has been detected

**Severity**: Medium

### VM\_ThreatIntelSuspectLogon

**Alert Display Name**: A logon from a malicious IP has been detected

**Severity**: High

### VM\_VbScriptHttpObjectAllocation

**Alert Display Name**: VBScript HTTP object allocation detected

**Severity**: High

### VM\_TaskkillBurst

**Alert Display Name**: Suspicious process termination burst

**Severity**: Low

### VM\_RunByPsExec

**Alert Display Name**: PsExec execution detected

**Severity**: Informational

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.