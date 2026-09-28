---
layout: Conceptual
title: Scenarios detected by the Microsoft Sentinel Fusion engine | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/fusion-scenario-reference
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn about the scenarios detected by Fusion, listed here grouped by threat classification.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2021-11-09T00:00:00.0000000Z
locale: en-us
document_id: 6884a621-6813-0c4f-074a-877a5062de1b
document_version_independent_id: 787dd740-2c08-a030-12d3-0cb001e9e061
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/fusion-scenario-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/fusion-scenario-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/fusion-scenario-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: a8f5a41f-6987-48ce-6aa1-2dbfe6b3eae4
---

# Scenarios detected by the Microsoft Sentinel Fusion engine | Microsoft Learn

This document lists the types of scenario-based multistage attacks, grouped by threat classification, that Microsoft Sentinel detects using the Fusion correlation engine.

Since [Fusion](fusion) correlates multiple signals from various products to detect advanced multistage attacks, successful Fusion detections are presented as **Fusion incidents** on the Microsoft Sentinel **Incidents** page and not as **alerts**, and are stored in the *Incidents* table in **Logs** and not in the *SecurityAlerts* table.

In order to enable these Fusion-powered attack detection scenarios, any data sources listed must be ingested to your Log Analytics workspace. For scenarios with scheduled analytics rules, follow the instructions in [Configure scheduled analytics rules for Fusion detections](configure-fusion-rules#configure-scheduled-analytics-rules-for-fusion-detections).

Note

Some of these scenarios are in **PREVIEW**. They will be so indicated.

## Compute resource abuse

### Multiple VM creation activities following suspicious Microsoft Entra sign-in

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Resource Hijacking (T1496)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of VMs were created in a single session following a suspicious sign-in to a Microsoft Entra account. This type of alert indicates, with a high degree of confidence, that the account noted in the Fusion incident description has been compromised and used to create new VMs for unauthorized purposes, such as running crypto mining operations. The permutations of suspicious Microsoft Entra sign-in alerts with the multiple VM creation activities alert are:

- **Impossible travel to an atypical location leading to multiple VM creation activities**
- **Sign-in event from an unfamiliar location leading to multiple VM creation activities**
- **Sign-in event from an infected device leading to multiple VM creation activities**
- **Sign-in event from an anonymous IP address leading to multiple VM creation activities**
- **Sign-in event from user with leaked credentials leading to multiple VM creation activities**

## Credential access

(New threat classification)

### Multiple passwords reset by user following suspicious sign-in

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Credential Access

**MITRE ATT&CK techniques:** Valid Account (T1078), Brute Force (T1110)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a user reset multiple passwords following a suspicious sign-in to a Microsoft Entra account. This evidence suggests that the account noted in the Fusion incident description has been compromised and was used to perform multiple password resets in order to gain access to multiple systems and resources. Account manipulation (including password reset) may aid adversaries in maintaining access to credentials and certain permission levels within an environment. The permutations of suspicious Microsoft Entra sign-in alerts with multiple passwords reset alerts are:

- **Impossible travel to an atypical location leading to multiple passwords reset**
- **Sign-in event from an unfamiliar location leading to multiple passwords reset**
- **Sign-in event from an infected device leading to multiple passwords reset**
- **Sign-in event from an anonymous IP leading to multiple passwords reset**
- **Sign-in event from user with leaked credentials leading to multiple passwords reset**

### Suspicious sign-in coinciding with successful sign-in to Palo Alto VPN by IP with multiple failed Microsoft Entra sign-ins

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Credential Access

**MITRE ATT&CK techniques:** Valid Account (T1078), Brute Force (T1110)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a suspicious sign-in to a Microsoft Entra account coincided with a successful sign-in through a Palo Alto VPN from an IP address from which multiple failed Microsoft Entra sign-ins occurred in a similar time frame. Though not evidence of a multistage attack, the correlation of these two lower-fidelity alerts results in a high-fidelity incident suggesting malicious initial access to the organization's network. Alternatively, this could be an indication of an attacker trying to use brute force techniques to gain access to a Microsoft Entra account. The permutations of suspicious Microsoft Entra sign-in alerts with "IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN" alerts are:

- **Impossible travel to an atypical location coinciding with IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN**
- **Sign-in event from an unfamiliar location coinciding with IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN**
- **Sign-in event from an infected device coinciding with IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN**
- **Sign-in event from an anonymous IP coinciding with IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN**
- **Sign-in event from user with leaked credentials coinciding with IP with multiple failed Microsoft Entra logins successfully logs in to Palo Alto VPN**

## Credential harvesting

(New threat classification)

### Malicious credential theft tool execution following suspicious sign-in

**MITRE ATT&CK tactics:** Initial Access, Credential Access

**MITRE ATT&CK techniques:** Valid Account (T1078), OS Credential Dumping (T1003)

**Data connector sources:** Microsoft Entra ID Protection, Microsoft Defender for Endpoint

**Description:** Fusion incidents of this type indicate that a known credential theft tool was executed following a suspicious Microsoft Entra sign-in. This evidence suggests with high confidence that the user account noted in the alert description has been compromised and may have successfully used a tool like **Mimikatz** to harvest credentials such as keys, plaintext passwords and/or password hashes from the system. The harvested credentials may allow an attacker to access sensitive data, escalate privileges, and/or move laterally across the network. The permutations of suspicious Microsoft Entra sign-in alerts with the malicious credential theft tool alert are:

- **Impossible travel to atypical locations leading to malicious credential theft tool execution**
- **Sign-in event from an unfamiliar location leading to malicious credential theft tool execution**
- **Sign-in event from an infected device leading to malicious credential theft tool execution**
- **Sign-in event from an anonymous IP address leading to malicious credential theft tool execution**
- **Sign-in event from user with leaked credentials leading to malicious credential theft tool execution**

### Suspected credential theft activity following suspicious sign-in

**MITRE ATT&CK tactics:** Initial Access, Credential Access

**MITRE ATT&CK techniques:** Valid Account (T1078), Credentials from Password Stores (T1555), OS Credential Dumping (T1003)

**Data connector sources:** Microsoft Entra ID Protection, Microsoft Defender for Endpoint

**Description:** Fusion incidents of this type indicate that activity associated with patterns of credential theft occurred following a suspicious Microsoft Entra sign-in. This evidence suggests with high confidence that the user account noted in the alert description has been compromised and used to steal credentials such as keys, plain-text passwords, password hashes, and so on. The stolen credentials may allow an attacker to access sensitive data, escalate privileges, and/or move laterally across the network. The permutations of suspicious Microsoft Entra sign-in alerts with the credential theft activity alert are:

- **Impossible travel to atypical locations leading to suspected credential theft activity**
- **Sign-in event from an unfamiliar location leading to suspected credential theft activity**
- **Sign-in event from an infected device leading to suspected credential theft activity**
- **Sign-in event from an anonymous IP address leading to suspected credential theft activity**
- **Sign-in event from user with leaked credentials leading to suspected credential theft activity**

## Crypto-mining

(New threat classification)

### Crypto-mining activity following suspicious sign-in

**MITRE ATT&CK tactics:** Initial Access, Credential Access

**MITRE ATT&CK techniques:** Valid Account (T1078), Resource Hijacking (T1496)

**Data connector sources:** Microsoft Entra ID Protection, Microsoft Defender for Cloud

**Description:** Fusion incidents of this type indicate crypto-mining activity associated with a suspicious sign-in to a Microsoft Entra account. This evidence suggests with high confidence that the user account noted in the alert description has been compromised and was used to hijack resources in your environment to mine crypto-currency. This can starve your resources of computing power and/or result in significantly higher-than-expected cloud usage bills. The permutations of suspicious Microsoft Entra sign-in alerts with the crypto-mining activity alert are:

- **Impossible travel to atypical locations leading to crypto-mining activity**
- **Sign-in event from an unfamiliar location leading to crypto-mining activity**
- **Sign-in event from an infected device leading to crypto-mining activity**
- **Sign-in event from an anonymous IP address leading to crypto-mining activity**
- **Sign-in event from user with leaked credentials leading to crypto-mining activity**

## Data destruction

### Mass file deletion following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Data Destruction (T1485)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of unique files were deleted following a suspicious sign-in to a Microsoft Entra account. This evidence suggests that the account noted in the Fusion incident description may have been compromised and was used to destroy data for malicious purposes. The permutations of suspicious Microsoft Entra sign-in alerts with the mass file deletion alert are:

- **Impossible travel to an atypical location leading to mass file deletion**
- **Sign-in event from an unfamiliar location leading to mass file deletion**
- **Sign-in event from an infected device leading to mass file deletion**
- **Sign-in event from an anonymous IP address leading to mass file deletion**
- **Sign-in event from user with leaked credentials leading to mass file deletion**

### Mass file deletion following successful Microsoft Entra sign-in from IP blocked by a Cisco firewall appliance

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Data Destruction (T1485)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that an anomalous number of unique files were deleted following a successful Microsoft Entra sign-in despite the user's IP address being blocked by a Cisco firewall appliance. This evidence suggests that the account noted in the Fusion incident description has been compromised and was used to destroy data for malicious purposes. Because the IP was blocked by the firewall, that same IP logging on successfully to Microsoft Entra ID is potentially suspect and could indicate credential compromise for the user account.

### Mass file deletion following successful sign-in to Palo Alto VPN by IP with multiple failed Microsoft Entra sign-ins

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Credential Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Brute Force (T1110), Data Destruction (T1485)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that an anomalous number of unique files were deleted by a user who successfully signed in through a Palo Alto VPN from an IP address from which multiple failed Microsoft Entra sign-ins occurred in a similar time frame. This evidence suggests that the user account noted in the Fusion incident may have been compromised using brute force techniques, and was used to destroy data for malicious purposes.

### Suspicious email deletion activity following suspicious Microsoft Entra sign-in

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Data Destruction (T1485)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of emails were deleted in a single session following a suspicious sign-in to a Microsoft Entra account. This evidence suggests that the account noted in the Fusion incident description may have been compromised and was used to destroy data for malicious purposes, such as harming the organization or hiding spam-related email activity. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious email deletion activity alert are:

- **Impossible travel to an atypical location leading to suspicious email deletion activity**
- **Sign-in event from an unfamiliar location leading to suspicious email deletion activity**
- **Sign-in event from an infected device leading to suspicious email deletion activity**
- **Sign-in event from an anonymous IP address leading to suspicious email deletion activity**
- **Sign-in event from user with leaked credentials leading to suspicious email deletion activity**

## Data exfiltration

### Mail forwarding activities following new admin-account activity not seen recently

This scenario belongs to two threat classifications in this list: **data exfiltration** and **malicious administrative activity**. For the sake of clarity, it appears in both sections.

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Collection, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Email Collection (T1114), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that either a new Exchange administrator account has been created, or an existing Exchange admin account took some administrative action for the first time, in the last two weeks, and that the account then did some mail-forwarding actions, which are unusual for an administrator account. This evidence suggests that the user account noted in the Fusion incident description has been compromised or manipulated, and that it was used to exfiltrate data from your organization's network.

### Mass file download following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of files were downloaded by a user following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the account noted in the Fusion incident description has been compromised and was used to exfiltrate data from your organization’s network. The permutations of suspicious Microsoft Entra sign-in alerts with the mass file download alert are:

- **Impossible travel to an atypical location leading to mass file download**
- **Sign-in event from an unfamiliar location leading to mass file download**
- **Sign-in event from an infected device leading to mass file download**
- **Sign-in event from an anonymous IP leading to mass file download**
- **Sign-in event from user with leaked credentials leading to mass file download**

### Mass file download following successful Microsoft Entra sign-in from IP blocked by a Cisco firewall appliance

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that an anomalous number of files were downloaded by a user following a successful Microsoft Entra sign-in despite the user's IP address being blocked by a Cisco firewall appliance. This could possibly be an attempt by an attacker to exfiltrate data from the organization's network after compromising a user account. Because the IP was blocked by the firewall, that same IP logging on successfully to Microsoft Entra ID is potentially suspect and could indicate credential compromise for the user account.

### Mass file download coinciding with SharePoint file operation from previously unseen IP

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Exfiltration

**MITRE ATT&CK techniques:** Exfiltration Over Web Service (T1567), Data Transfer Size Limits (T1030)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that an anomalous number of files were downloaded by a user connected from a previously unseen IP address. Though not evidence of a multistage attack, the correlation of these two lower-fidelity alerts results in a high-fidelity incident suggesting an attempt by an attacker to exfiltrate data from the organization's network from a possibly compromised user account. In stable environments, such connections by previously unseen IPs may be unauthorized, especially if associated with spikes in volume that could be associated with large-scale document exfiltration.

### Mass file sharing following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a number of files above a particular threshold were shared to others following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the account noted in the Fusion incident description has been compromised and used to exfiltrate data from your organization's network by sharing files such as documents, spreadsheets, etc., with unauthorized users for malicious purposes. The permutations of suspicious Microsoft Entra sign-in alerts with the mass file sharing alert are:

- **Impossible travel to an atypical location leading to mass file sharing**
- **Sign-in event from an unfamiliar location leading to mass file sharing**
- **Sign-in event from an infected device leading to mass file sharing**
- **Sign-in event from an anonymous IP address leading to mass file sharing**
- **Sign-in event from user with leaked credentials leading to mass file sharing**

### Multiple Power BI report sharing activities following suspicious Microsoft Entra sign-in

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of Power BI reports were shared in a single session following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the account noted in the Fusion incident description has been compromised and was used to exfiltrate data from your organization's network by sharing Power BI reports with unauthorized users for malicious purposes. The permutations of suspicious Microsoft Entra sign-in alerts with the multiple Power BI report sharing activities are:

- **Impossible travel to an atypical location leading to multiple Power BI report sharing activities**
- **Sign-in event from an unfamiliar location leading to multiple Power BI report sharing activities**
- **Sign-in event from an infected device leading to multiple Power BI report sharing activities**
- **Sign-in event from an anonymous IP address leading to multiple Power BI report sharing activities**
- **Sign-in event from user with leaked credentials leading to multiple Power BI report sharing activities**

### Office 365 mailbox exfiltration following a suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Exfiltration, Collection

**MITRE ATT&CK techniques:** Valid Account (T1078), E-mail collection (T1114), Automated Exfiltration (T1020)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a suspicious inbox forwarding rule was set on a user's inbox following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the user's account (noted in the Fusion incident description) has been compromised, and that it was used to exfiltrate data from your organization's network by enabling a mailbox forwarding rule without the true user's knowledge. The permutations of suspicious Microsoft Entra sign-in alerts with the Office 365 mailbox exfiltration alert are:

- **Impossible travel to an atypical location leading to Office 365 mailbox exfiltration**
- **Sign-in event from an unfamiliar location leading to Office 365 mailbox exfiltration**
- **Sign-in event from an infected device leading to Office 365 mailbox exfiltration**
- **Sign-in event from an anonymous IP address leading to Office 365 mailbox exfiltration**
- **Sign-in event from user with leaked credentials leading to Office 365 mailbox exfiltration**

### SharePoint file operation from previously unseen IP following malware detection

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Exfiltration, Defense Evasion

**MITRE ATT&CK techniques:** Data Transfer Size Limits (T1030)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that an attacker attempted to exfiltrate large amounts of data by downloading or sharing through SharePoint through the use of malware. In stable environments, such connections by previously unseen IPs may be unauthorized, especially if associated with spikes in volume that could be associated with large-scale document exfiltration.

### Suspicious inbox manipulation rules set following suspicious Microsoft Entra sign-in

This scenario belongs to two threat classifications in this list: **data exfiltration** and **lateral movement**. For the sake of clarity, it appears in both sections.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Lateral Movement, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Internal Spear Phishing (T1534), Automated Exfiltration (T1020)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that anomalous inbox rules were set on a user's inbox following a suspicious sign-in to a Microsoft Entra account. This evidence provides a high-confidence indication that the account noted in the Fusion incident description has been compromised and was used to manipulate the user’s email inbox rules for malicious purposes, possibly to exfiltrate data from the organization's network. Alternatively, the attacker could be trying to generate phishing emails from within the organization (bypassing phishing detection mechanisms targeted at email from external sources) for the purpose of moving laterally by gaining access to additional user and/or privileged accounts. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious inbox manipulation rules alert are:

- **Impossible travel to an atypical location leading to suspicious inbox manipulation rule**
- **Sign-in event from an unfamiliar location leading to suspicious inbox manipulation rule**
- **Sign-in event from an infected device leading to suspicious inbox manipulation rule**
- **Sign-in event from an anonymous IP address leading to suspicious inbox manipulation rule**
- **Sign-in event from user with leaked credentials leading to suspicious inbox manipulation rule**

### Suspicious Power BI report sharing following suspicious Microsoft Entra sign-in

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a suspicious Power BI report sharing activity occurred following a suspicious sign-in to a Microsoft Entra account. The sharing activity was identified as suspicious because the Power BI report contained sensitive information identified using Natural language processing, and because it was shared with an external email address, published to the web, or delivered as a snapshot to an externally subscribed email address. This alert indicates with high confidence that the account noted in the Fusion incident description has been compromised and was used to exfiltrate sensitive data from your organization by sharing Power BI reports with unauthorized users for malicious purposes. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious Power BI report sharing are:

- **Impossible travel to an atypical location leading to suspicious Power BI report sharing**
- **Sign-in event from an unfamiliar location leading to suspicious Power BI report sharing**
- **Sign-in event from an infected device leading to suspicious Power BI report sharing**
- **Sign-in event from an anonymous IP address leading to suspicious Power BI report sharing**
- **Sign-in event from user with leaked credentials leading to suspicious Power BI report sharing**

## Denial of service

### Multiple VM deletion activities following suspicious Microsoft Entra sign-in

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Endpoint Denial of Service (T1499)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of VMs were deleted in a single session following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the account noted in the Fusion incident description has been compromised and was used to attempt to disrupt or destroy the organization's cloud environment. The permutations of suspicious Microsoft Entra sign-in alerts with the multiple VM deletion activities alert are:

- **Impossible travel to an atypical location leading to multiple VM deletion activities**
- **Sign-in event from an unfamiliar location leading to multiple VM deletion activities**
- **Sign-in event from an infected device leading to multiple VM deletion activities**
- **Sign-in event from an anonymous IP address leading to multiple VM deletion activities**
- **Sign-in event from user with leaked credentials leading to multiple VM deletion activities**

## Lateral movement

### Office 365 impersonation following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Lateral Movement

**MITRE ATT&CK techniques:** Valid Account (T1078), Internal Spear Phishing (T1534)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of impersonation actions occurred following a suspicious sign-in from a Microsoft Entra account. In some software, there are options to allow users to impersonate other users. For example, email services allow users to authorize other users to send email on their behalf. This alert indicates with higher confidence that the account noted in the Fusion incident description has been compromised and was used to conduct impersonation activities for malicious purposes, such as sending phishing emails for malware distribution or lateral movement. The permutations of suspicious Microsoft Entra sign-in alerts with the Office 365 impersonation alert are:

- **Impossible travel to an atypical location leading to Office 365 impersonation**
- **Sign-in event from an unfamiliar location leading to Office 365 impersonation**
- **Sign-in event from an infected device leading to Office 365 impersonation**
- **Sign-in event from an anonymous IP address leading to Office 365 impersonation**
- **Sign-in event from user with leaked credentials leading to Office 365 impersonation**

### Suspicious inbox manipulation rules set following suspicious Microsoft Entra sign-in

This scenario belongs to two threat classifications in this list: **lateral movement** and **data exfiltration**. For the sake of clarity, it appears in both sections.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Lateral Movement, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Internal Spear Phishing (T1534), Automated Exfiltration (T1020)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that anomalous inbox rules were set on a user's inbox following a suspicious sign-in to a Microsoft Entra account. This evidence provides a high-confidence indication that the account noted in the Fusion incident description has been compromised and was used to manipulate the user’s email inbox rules for malicious purposes, possibly to exfiltrate data from the organization's network. Alternatively, the attacker could be trying to generate phishing emails from within the organization (bypassing phishing detection mechanisms targeted at email from external sources) for the purpose of moving laterally by gaining access to additional user and/or privileged accounts. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious inbox manipulation rules alert are:

- **Impossible travel to an atypical location leading to suspicious inbox manipulation rule**
- **Sign-in event from an unfamiliar location leading to suspicious inbox manipulation rule**
- **Sign-in event from an infected device leading to suspicious inbox manipulation rule**
- **Sign-in event from an anonymous IP address leading to suspicious inbox manipulation rule**
- **Sign-in event from user with leaked credentials leading to suspicious inbox manipulation rule**

## Malicious administrative activity

### Suspicious cloud app administrative activity following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Persistence, Defense Evasion, Lateral Movement, Collection, Exfiltration, and Impact

**MITRE ATT&CK techniques:** N/A

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an anomalous number of administrative activities were performed in a single session following a suspicious Microsoft Entra sign-in from the same account. This evidence suggests that the account noted in the Fusion incident description may have been compromised and was used to make any number of unauthorized administrative actions with malicious intent. This also indicates that an account with administrative privileges may have been compromised. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious cloud app administrative activity alert are:

- **Impossible travel to an atypical location leading to suspicious cloud app administrative activity**
- **Sign-in event from an unfamiliar location leading to suspicious cloud app administrative activity**
- **Sign-in event from an infected device leading to suspicious cloud app administrative activity**
- **Sign-in event from an anonymous IP address leading to suspicious cloud app administrative activity**
- **Sign-in event from user with leaked credentials leading to suspicious cloud app administrative activity**

### Mail forwarding activities following new admin-account activity not seen recently

This scenario belongs to two threat classifications in this list: **malicious administrative activity** and **data exfiltration**. For the sake of clarity, it appears in both sections.

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Collection, Exfiltration

**MITRE ATT&CK techniques:** Valid Account (T1078), Email Collection (T1114), Exfiltration Over Web Service (T1567)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate that either a new Exchange administrator account has been created, or an existing Exchange admin account took some administrative action for the first time, in the last two weeks, and that the account then did some mail-forwarding actions, which are unusual for an administrator account. This evidence suggests that the user account noted in the Fusion incident description has been compromised or manipulated, and that it was used to exfiltrate data from your organization's network.

## Malicious execution with legitimate process

### PowerShell made a suspicious network connection, followed by anomalous traffic flagged by Palo Alto Networks firewall.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Execution

**MITRE ATT&CK techniques:** Command and Scripting Interpreter (T1059)

**Data connector sources:** Microsoft Defender for Endpoint (formerly Microsoft Defender Advanced Threat Protection, or MDATP), Microsoft Sentinel (scheduled analytics rule)

**Description:** Fusion incidents of this type indicate that an outbound connection request was made via a PowerShell command, and following that, anomalous inbound activity was detected by the Palo Alto Networks Firewall. This evidence suggests that an attacker has likely gained access to your network and is trying to perform malicious actions. Connection attempts by PowerShell that follow this pattern could be an indication of malware command and control activity, requests for the download of additional malware, or an attacker establishing remote interactive access. As with all “living off the land” attacks, this activity could be a legitimate use of PowerShell. However, the PowerShell command execution followed by suspicious inbound Firewall activity increases the confidence that PowerShell is being used in a malicious manner and should be investigated further. In Palo Alto logs, Microsoft Sentinel focuses on [threat logs](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/view-and-manage-logs/log-types-and-severity-levels/threat-logs), and traffic is considered suspicious when threats are allowed (suspicious data, files, floods, packets, scans, spyware, URLs, viruses, vulnerabilities, wildfire-viruses, wildfires). Also reference the Palo Alto Threat Log corresponding to the [Threat/Content Type](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/use-syslog-for-monitoring/syslog-field-descriptions/threat-log-fields.html) listed in the Fusion incident description for additional alert details.

### Suspicious remote WMI execution followed by anomalous traffic flagged by Palo Alto Networks firewall

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Execution, Discovery

**MITRE ATT&CK techniques:** Windows Management Instrumentation (T1047)

**Data connector sources:** Microsoft Defender for Endpoint (formerly MDATP), Microsoft Sentinel (scheduled analytics rule)

**Description:** Fusion incidents of this type indicate that Windows Management Interface (WMI) commands were remotely executed on a system, and following that, suspicious inbound activity was detected by the Palo Alto Networks Firewall. This evidence suggests that an attacker may have gained access to your network and is attempting to move laterally, escalate privileges, and/or execute malicious payloads. As with all “living off the land” attacks, this activity could be a legitimate use of WMI. However, the remote WMI command execution followed by suspicious inbound Firewall activity increases the confidence that WMI is being used in a malicious manner and should be investigated further. In Palo Alto logs, Microsoft Sentinel focuses on [threat logs](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/view-and-manage-logs/log-types-and-severity-levels/threat-logs), and traffic is considered suspicious when threats are allowed (suspicious data, files, floods, packets, scans, spyware, URLs, viruses, vulnerabilities, wildfire-viruses, wildfires). Also reference the Palo Alto Threat Log corresponding to the [Threat/Content Type](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/use-syslog-for-monitoring/syslog-field-descriptions/threat-log-fields.html) listed in the Fusion incident description for additional alert details.

### Suspicious PowerShell command line following suspicious sign-in

**MITRE ATT&CK tactics:** Initial Access, Execution

**MITRE ATT&CK techniques:** Valid Account (T1078), Command and Scripting Interpreter (T1059)

**Data connector sources:** Microsoft Entra ID Protection, Microsoft Defender for Endpoint (formerly MDATP)

**Description:** Fusion incidents of this type indicate that a user executed potentially malicious PowerShell commands following a suspicious sign-in to a Microsoft Entra account. This evidence suggests with high confidence that the account noted in the alert description has been compromised and further malicious actions were taken. Attackers often use PowerShell to execute malicious payloads in memory without leaving artifacts on the disk, in order to avoid detection by disk-based security mechanisms such as virus scanners. The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious PowerShell command alert are:

- **Impossible travel to atypical locations leading to suspicious PowerShell command line**
- **Sign-in event from an unfamiliar location leading to suspicious PowerShell command line**
- **Sign-in event from an infected device leading to suspicious PowerShell command line**
- **Sign-in event from an anonymous IP address leading to suspicious PowerShell command line**
- **Sign-in event from user with leaked credentials leading to suspicious PowerShell command line**

## Malware C2 or download

### Beacon pattern detected by Fortinet following multiple failed user sign-ins to a service

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Command and Control

**MITRE ATT&CK techniques:** Valid Account (T1078), Non-Standard Port (T1571), T1065 (retired)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Defender for Cloud Apps

**Description:** Fusion incidents of this type indicate communication patterns, from an internal IP address to an external one, that are consistent with beaconing, following multiple failed user sign-ins to a service from a related internal entity. The combination of these two events could be an indication of malware infection or of a compromised host doing data exfiltration.

### Beacon pattern detected by Fortinet following suspicious Microsoft Entra sign-in

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Command and Control

**MITRE ATT&CK techniques:** Valid Account (T1078), Non-Standard Port (T1571), T1065 (retired)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate communication patterns, from an internal IP address to an external one, that are consistent with beaconing, following a user sign-in of a suspicious nature to Microsoft Entra ID. The combination of these two events could be an indication of malware infection or of a compromised host doing data exfiltration. The permutations of beacon pattern detected by Fortinet alerts with suspicious Microsoft Entra sign-in alerts are:

- **Impossible travel to an atypical location leading to beacon pattern detected by Fortinet**
- **Sign-in event from an unfamiliar location leading to beacon pattern detected by Fortinet**
- **Sign-in event from an infected device leading to beacon pattern detected by Fortinet**
- **Sign-in event from an anonymous IP address leading to beacon pattern detected by Fortinet**
- **Sign-in event from user with leaked credentials leading to beacon pattern detected by Fortinet**

### Network request to TOR anonymization service followed by anomalous traffic flagged by Palo Alto Networks firewall.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Command and Control

**MITRE ATT&CK techniques:** Encrypted Channel (T1573), Proxy (T1090)

**Data connector sources:** Microsoft Defender for Endpoint (formerly MDATP), Microsoft Sentinel (scheduled analytics rule)

**Description:** Fusion incidents of this type indicate that an outbound connection request was made to the TOR anonymization service, and following that, anomalous inbound activity was detected by the Palo Alto Networks Firewall. This evidence suggests that an attacker has likely gained access to your network and is trying to conceal their actions and intent. Connections to the TOR network following this pattern could be an indication of malware command and control activity, requests for the download of additional malware, or an attacker establishing remote interactive access. In Palo Alto logs, Microsoft Sentinel focuses on [threat logs](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/view-and-manage-logs/log-types-and-severity-levels/threat-logs), and traffic is considered suspicious when threats are allowed (suspicious data, files, floods, packets, scans, spyware, URLs, viruses, vulnerabilities, wildfire-viruses, wildfires). Also reference the Palo Alto Threat Log corresponding to the [Threat/Content Type](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/use-syslog-for-monitoring/syslog-field-descriptions/threat-log-fields.html) listed in the Fusion incident description for additional alert details.

### Outbound connection to IP with a history of unauthorized access attempts followed by anomalous traffic flagged by Palo Alto Networks firewall

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Command and Control

**MITRE ATT&CK techniques:** Not applicable

**Data connector sources:** Microsoft Defender for Endpoint (formerly MDATP), Microsoft Sentinel (scheduled analytics rule)

**Description:** Fusion incidents of this type indicate that an outbound connection to an IP address with a history of unauthorized access attempts was established, and following that, anomalous activity was detected by the Palo Alto Networks Firewall. This evidence suggests that an attacker has likely gained access to your network. Connection attempts following this pattern could be an indication of malware command and control activity, requests for the download of additional malware, or an attacker establishing remote interactive access. In Palo Alto logs, Microsoft Sentinel focuses on [threat logs](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/view-and-manage-logs/log-types-and-severity-levels/threat-logs), and traffic is considered suspicious when threats are allowed (suspicious data, files, floods, packets, scans, spyware, URLs, viruses, vulnerabilities, wildfire-viruses, wildfires). Also reference the Palo Alto Threat Log corresponding to the [Threat/Content Type](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/use-syslog-for-monitoring/syslog-field-descriptions/threat-log-fields.html) listed in the Fusion incident description for additional alert details.

## Persistence

(New threat classification)

### Rare application consent following suspicious sign-in

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Persistence, Initial Access

**MITRE ATT&CK techniques:** Create Account (T1136), Valid Account (T1078)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that an application was granted consent by a user who has never or rarely done so, following a related suspicious sign-in to a Microsoft Entra account. This evidence suggests that the account noted in the Fusion incident description may have been compromised and used to access or manipulate the application for malicious purposes. Consent to application, Add service principal and Add OAuth2PermissionGrant should typically be rare events. Attackers may use this type of configuration change to establish or maintain their foothold on systems. The permutations of suspicious Microsoft Entra sign-in alerts with the rare application consent alert are:

- **Impossible travel to an atypical location leading to rare application consent**
- **Sign-in event from an unfamiliar location leading to rare application consent**
- **Sign-in event from an infected device leading to rare application consent**
- **Sign-in event from an anonymous IP leading to rare application consent**
- **Sign-in event from user with leaked credentials leading to rare application consent**

## Ransomware

### Ransomware execution following suspicious Microsoft Entra sign-in

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Data Encrypted for Impact (T1486)

**Data connector sources:** Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that anomalous user behavior indicating a ransomware attack was detected following a suspicious sign-in to a Microsoft Entra account. This indication provides high confidence that the account noted in the Fusion incident description has been compromised and was used to encrypt data for the purposes of extorting the data owner or denying the data owner access to their data. The permutations of suspicious Microsoft Entra sign-in alerts with the ransomware execution alert are:

- **Impossible travel to an atypical location leading to ransomware in cloud app**
- **Sign-in event from an unfamiliar location leading to ransomware in cloud app**
- **Sign-in event from an infected device leading to ransomware in cloud app**
- **Sign-in event from an anonymous IP address leading to ransomware in cloud app**
- **Sign-in event from user with leaked credentials leading to ransomware in cloud app**

## Remote exploitation

### Suspected use of attack framework followed by anomalous traffic flagged by Palo Alto Networks firewall

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Execution, Lateral Movement, Privilege Escalation

**MITRE ATT&CK techniques:** Exploit Public-Facing Application (T1190), Exploitation for Client Execution (T1203), Exploitation of Remote Services(T1210), Exploitation for Privilege Escalation (T1068)

**Data connector sources:** Microsoft Defender for Endpoint (formerly MDATP), Microsoft Sentinel (scheduled analytics rule)

**Description:** Fusion incidents of this type indicate that non-standard uses of protocols, resembling the use of attack frameworks such as Metasploit, were detected, and following that, suspicious inbound activity was detected by the Palo Alto Networks Firewall. This may be an initial indication that an attacker has exploited a service to gain access to your network resources or that an attacker has already gained access and is trying to further exploit available systems/services to move laterally and/or escalate privileges. In Palo Alto logs, Microsoft Sentinel focuses on [threat logs](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/view-and-manage-logs/log-types-and-severity-levels/threat-logs), and traffic is considered suspicious when threats are allowed (suspicious data, files, floods, packets, scans, spyware, URLs, viruses, vulnerabilities, wildfire-viruses, wildfires). Also reference the Palo Alto Threat Log corresponding to the [Threat/Content Type](https://docs.paloaltonetworks.com/pan-os/8-1/pan-os-admin/monitoring/use-syslog-for-monitoring/syslog-field-descriptions/threat-log-fields.html) listed in the Fusion incident description for additional alert details.

## Resource hijacking

(New threat classification)

### Suspicious resource / resource group deployment by a previously unseen caller following suspicious Microsoft Entra sign-in

This scenario makes use of alerts produced by **scheduled analytics rules**.

This scenario is currently in **PREVIEW**.

**MITRE ATT&CK tactics:** Initial Access, Impact

**MITRE ATT&CK techniques:** Valid Account (T1078), Resource Hijacking (T1496)

**Data connector sources:** Microsoft Sentinel (scheduled analytics rule), Microsoft Entra ID Protection

**Description:** Fusion incidents of this type indicate that a user has deployed an Azure resource or resource group - a rare activity - following a suspicious sign-in, with properties not recently seen, to a Microsoft Entra account. This could possibly be an attempt by an attacker to deploy resources or resource groups for malicious purposes after compromising the user account noted in the Fusion incident description.

The permutations of suspicious Microsoft Entra sign-in alerts with the suspicious resource / resource group deployment by a previously unseen caller alert are:

- **Impossible travel to an atypical location leading to suspicious resource / resource group deployment by a previously unseen caller**
- **Sign-in event from an unfamiliar location leading to suspicious resource / resource group deployment by a previously unseen caller**
- **Sign-in event from an infected device leading to suspicious resource / resource group deployment by a previously unseen caller**
- **Sign-in event from an anonymous IP leading to suspicious resource / resource group deployment by a previously unseen caller**
- **Sign-in event from user with leaked credentials leading to suspicious resource / resource group deployment by a previously unseen caller**