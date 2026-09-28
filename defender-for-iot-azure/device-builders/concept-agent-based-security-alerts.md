---
layout: Conceptual
title: Micro agent security alerts - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/concept-agent-based-security-alerts
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: Learn about security alerts and recommended remediation using Defender for IoT device's features, and services.
ms.topic: concept-article
ms.date: 2023-01-01T00:00:00.0000000Z
locale: en-us
document_id: 61314db8-629f-63fb-944f-611e1842b478
document_version_independent_id: e8adcdec-25da-a361-923b-1898a588d739
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/concept-agent-based-security-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/concept-agent-based-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/concept-agent-based-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 46354ce8-c641-1a60-6a6e-507c863c033b
---

# Micro agent security alerts - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT continuously analyzes your IoT solution using advanced analytics and threat intelligence to alert you to malicious activity. In addition, you can create custom alerts based on your knowledge of expected device behavior. An alert acts as an indicator of potential compromise, and should be investigated and remediated.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

In this article, you'll find a list of built-in alerts, which can be triggered on your IoT devices.

## Security alerts

### High severity

| Name | Severity | Data Source | Description | Suggested remediation steps | Alert type |
| --- | --- | --- | --- | --- | --- |
| Binary Command Line | High | Defender-IoT-micro-agent | LA Linux binary being called/executed from the command line was detected. This process may be legitimate activity, or an indication that your device is compromised. | Review the command with the user that ran it and check if this is something legitimately expected to run on the device. If not, escalate the alert to your information security team. | IoT\_BinaryCommandLine |
| Disable firewall | High | Defender-IoT-micro-agent | Possible manipulation of on-host firewall detected. Malicious actors often disable the on-host firewall in an attempt to exfiltrate data. | Review with the user that ran the command to confirm if this was legitimate expected activity on the device. If not, escalate the alert to your information security team. | IoT\_DisableFirewall |
| Port forwarding detection | High | Defender-IoT-micro-agent | Initiation of port forwarding to an external IP address detected. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_PortForwarding |
| Possible attempt to disable Auditd logging detected | High | Defender-IoT-micro-agent | Linux Auditd system provides a way to track security-relevant information on the system. The system records as much information about the events that are happening on your system as possible. This information is crucial for mission-critical environments to determine who violated the security policy and the actions they performed. Disabling Auditd logging may prevent your ability to discover violations of security policies used on the system. | Check with the device owner if this was legitimate activity with business reasons. If not, this event may be hiding activity by malicious actors. Immediately escalated the incident to your information security team. | IoT\_DisableAuditdLogging |
| Reverse shells | High | Defender-IoT-micro-agent | Analysis of host data on a device detected a potential reverse shell. Reverse shells are often used to get a compromised machine to call back into a machine controlled by a malicious actor. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_ReverseShell |
| Successful local login | High | Defender-IoT-micro-agent | Successful local sign-in to the device detected. | Make sure the signed in user is an authorized party. | IoT\_SuccessfulLocalLogin |
| Web shell | High | Defender-IoT-micro-agent | Possible web shell detected. Malicious actors commonly upload a web shell to a compromised machine to gain persistence or for further exploitation. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_WebShell |
| Behavior similar to ransomware detected | High | Defender-IoT-micro-agent | Execution of files similar to known ransomware that may prevent users from accessing their system, or personal files, and may demand ransom payment to regain access. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_Ransomware |
| Crypto coin miner image | High | Defender-IoT-micro-agent | Execution of a process normally associated with digital currency mining detected. | Verify with the user that ran the command if this was legitimate activity on the device. If not, escalate the alert to the information security team. | IoT\_CryptoMiner |
| New USB Connection | High | Defender-IoT-micro-agent | A USB device connection was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_USBConnection |
| USB Disconnection | High | Defender-IoT-micro-agent | A USB device disconnection was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_UsbDisconnection |
| New Ethernet Connection | High | Defender-IoT-micro-agent | A new Ethernet connection was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_EthernetConnection |
| Ethernet Disconnection | High | Defender-IoT-micro-agent | A new Ethernet disconnection was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_EthernetDisconnection |
| New File Created | High | Defender-IoT-micro-agent | A new file was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_FileCreated |
| File Modified | High | Defender-IoT-micro-agent | File modification was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_FileModified |
| File Deleted | High | Defender-IoT-micro-agent | File deletion was detected. This may indicate malicious activity. | Confirm this is a legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_FileDeleted |

### Medium severity

| Name | Severity | Data Source | Description | Suggested remediation steps | Alert type |
| --- | --- | --- | --- | --- | --- |
| Behavior similar to common Linux bots detected | Medium | Defender-IoT-micro-agent | Execution of a process normally associated with common Linux botnets detected. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_CommonBots |
| Behavior similar to Fairware ransomware detected | Medium | Defender-IoT-micro-agent | Execution of rm -rf commands applied to suspicious locations detected using analysis of host data. Because rm -rf recursively deletes files, it's normally only used on discrete folders. In this case, it's being used in a location that could remove a large amount of data. Fairware ransomware is known to execute rm -rf commands in this folder. | Review with the user that ran the command this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_FairwareMalware |
| Crypto coin miner container image detected | Medium | Defender-IoT-micro-agent | Container detecting running known digital currency mining images. | 1. If this behavior isn't intended, delete the relevant container image.  2. Make sure that the Docker daemon isn't accessible via an unsafe TCP socket.  3. Escalate the alert to the information security team. | IoT\_CryptoMinerContainer |
| Detected suspicious use of the nohup command | Medium | Defender-IoT-micro-agent | Suspicious use of the nohup command on host detected. Malicious actors commonly run the nohup command from a temporary directory, effectively allowing their executables to run in the background. Seeing this command run on files located in a temporary directory is not expected or usual behavior. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_SuspiciousNohup |
| Detected suspicious use of the useradd command | Medium | Defender-IoT-micro-agent | Suspicious use of the useradd command detected on the device. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_SuspiciousUseradd |
| Exposed Docker daemon by TCP socket | Medium | Defender-IoT-micro-agent | Machine logs indicate that your Docker daemon (dockerd) exposes a TCP socket. By default, Docker configuration, does not use encryption or authentication when a TCP socket is enabled. Default Docker configuration enables full access to the Docker daemon, by anyone with access to the relevant port. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_ExposedDocker |
| Failed local login | Medium | Defender-IoT-micro-agent | A failed local login attempt to the device was detected. | Make sure no unauthorized party has physical access to the device. | IoT\_FailedLocalLogin |
| Detected file download from a malicious source | Medium | Defender-IoT-micro-agent | Download of a file from a known malware source detected. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_PossibleMalware |
| htaccess file access detected | Medium | Defender-IoT-micro-agent | Analysis of host data detected possible manipulation of a htaccess file. Htaccess is a powerful configuration file that allows you to make multiple changes to a web server running Apache Web software, including basic redirect functionality, and more advanced functions, such as basic password protection. Malicious actors often modify htaccess files on compromised machines to gain persistence. | Confirm this is legitimate expected activity on the host. If not, escalate the alert to your information security team. | IoT\_AccessingHtaccessFile |
| Known attack tool | Medium | Defender-IoT-micro-agent | A tool often associated with malicious users attacking other machines in some way was detected. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_KnownAttackTools |
| Local host reconnaissance detected | Medium | Defender-IoT-micro-agent | Execution of a command normally associated with common Linux bot reconnaissance detected. | Review the suspicious command line to confirm that it was executed by a legitimate user. If not, escalate the alert to your information security team. | IoT\_LinuxReconnaissance |
| Mismatch between script interpreter and file extension | Medium | Defender-IoT-micro-agent | Mismatch between the script interpreter and the extension of the script file provided as input detected. This type of mismatch is commonly associated with attacker script executions. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_ScriptInterpreterMismatch |
| Possible backdoor detected | Medium | Defender-IoT-micro-agent | A suspicious file was downloaded and then run on a host in your subscription. This type of activity is commonly associated with the installation of a backdoor. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_LinuxBackdoor |
| Possible loss of data detected | Medium | Defender-IoT-micro-agent | Possible data egress condition detected using analysis of host data. Malicious actors often egress data from compromised machines. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_EgressData |
| Privileged container detected | Medium | Defender-IoT-micro-agent | Machine logs indicate that a privileged Docker container is running. A privileged container has full access to host resources. If compromised, a malicious actor can use the privileged container to gain access to the host machine. | If the container doesn't need to run in privileged mode, remove the privileges from the container. | IoT\_PrivilegedContainer |
| Removal of system logs files detected | Medium | Defender-IoT-micro-agent | Suspicious removal of log files on the host detected. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_RemovalOfSystemLogs |
| Space after filename | Medium | Defender-IoT-micro-agent | Execution of a process with a suspicious extension detected using analysis of host data. Suspicious extensions may trick users into thinking files are safe to be opened and can indicate the presence of malware on the system. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_ExecuteFileWithTrailingSpace |
| Tools commonly used for malicious credentials access detected | Medium | Defender-IoT-micro-agent | Detection usage of a tool commonly associated with malicious attempts to access credentials. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_CredentialAccessTools |
| Suspicious compilation detected | Medium | Defender-IoT-micro-agent | Suspicious compilation detected. Malicious actors often compile exploits on a compromised machine to escalate privileges. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_SuspiciousCompilation |
| Suspicious file download followed by file run activity | Medium | Defender-IoT-micro-agent | Analysis of host data detected a file that was downloaded and run in the same command. This technique is commonly used by malicious actors to get infected files onto victim machines. | Review with the user that ran the command if this was legitimate activity that you expect to see on the device. If not, escalate the alert to the information security team. | IoT\_DownloadFileThenRun |
| Suspicious IP address communication | Medium | Defender-IoT-micro-agent | Communication with a suspicious IP address detected. | Verify if the connection is legitimate. Consider blocking communication with the suspicious IP. | IoT\_TiConnection |
| Malicious Domain Name Request | Medium | Defender-IoT-micro-agent | Suspicious network activity was detected. This activity may be associated with an attack exploiting a method used by known malware. | Disconnect the source from the network. Perform incident response. | IoT\_MaliciousNameQueriesDetection |

### Low severity

| Name | Severity | Data Source | Description | Suggested remediation steps | Alert type |
| --- | --- | --- | --- | --- | --- |
| Bash history cleared | Low | Defender-IoT-micro-agent | Bash history log cleared. Malicious actors commonly erase bash history to hide their own commands from appearing in the logs. | Review with the user that ran the command that the activity in this alert to see if you recognize this as legitimate administrative activity. If not, escalate the alert to the information security team. | IoT\_ClearHistoryFile |