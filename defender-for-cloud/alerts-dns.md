---
layout: Conceptual
title: Alerts for DNS - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-dns
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
description: This article lists the security alerts for DNS visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a1b39adf-c159-6720-1a55-35ce1ef740b8
document_version_independent_id: 3feeac8a-d14b-229e-6745-74270e6fa1e1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-dns.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-dns
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-dns.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 480e0fd4-beef-1d6d-451a-1bf9e7a88c53
---

# Alerts for DNS - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for DNS from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Alerts for DNS

Important

- As of August 1, 2023, customers with an existing subscription to Defender for DNS can continue to use the service as a standalone plan.
- For new subscriptions, alerts about suspicious DNS activity are included as part of Defender for Servers Plan 2 (P2).
- There's no change to the protection scope: Defender for DNS continues to protect all Azure resources connected to Azure's default DNS resolvers. The change affects how DNS protection is billed and bundled, not what resources are covered.

### **Anomalous network protocol usage**

(AzureDNS\_ProtocolAnomaly)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected anomalous protocol usage. Such traffic, while possibly benign, might indicate abuse of this common protocol to bypass network traffic filtering. Typical related attacker activity includes copying remote administration tools to a compromised host and exfiltrating user data from it.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: -

### **Anonymity network activity**

(AzureDNS\_DarkWeb)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected anonymity network activity. Such activity, while possibly legitimate user behavior, is frequently employed by attackers to evade tracking and fingerprinting of network communications. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

### **Anonymity network activity using web proxy**

(AzureDNS\_DarkWebProxy)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected anonymity network activity. Such activity, while possibly legitimate user behavior, is frequently employed by attackers to evade tracking and fingerprinting of network communications. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

### **Attempted communication with suspicious sinkholed domain**

(AzureDNS\_SinkholedDomain)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected request for sinkholed domain. Such activity, while possibly legitimate user behavior, is frequently an indication of the download or execution of malicious software. Typical related attacker activity is likely to include the download and execution of further malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Medium

### **Communication with possible phishing domain**

(AzureDNS\_PhishingDomain)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected a request for a possible phishing domain. Such activity, while possibly benign, is frequently performed by attackers to harvest credentials to remote services. Typical related attacker activity is likely to include the exploitation of any credentials on the legitimate service.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Informational

### **Communication with suspicious algorithmically generated domain**

(AzureDNS\_DomainGenerationAlgorithm)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected possible usage of a domain generation algorithm. Such activity, while possibly benign, is frequently performed by attackers to evade network monitoring and filtering. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Informational

### **Communication with suspicious domain identified by threat intelligence**

(AzureDNS\_ThreatIntelSuspectDomain)

**Description**: Communication with suspicious domain was detected by analyzing DNS transactions from your resource and comparing against known malicious domains identified by threat intelligence feeds. Communication to malicious domains is frequently performed by attackers and could imply that your resource is compromised.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access

**Severity**: Medium

### **Communication with suspicious random domain name**

(AzureDNS\_RandomizedDomain)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected usage of a suspicious randomly generated domain name. Such activity, while possibly benign, is frequently performed by attackers to evade network monitoring and filtering. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Informational

### **Digital currency mining activity**

(AzureDNS\_CurrencyMining)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected digital currency mining activity. Such activity, while possibly legitimate user behavior, is frequently performed by attackers following compromise of resources. Typical related attacker activity is likely to include the download and execution of common mining tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

### **Network intrusion detection signature activation**

(AzureDNS\_SuspiciousDomain)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected a known malicious network signature. Such activity, while possibly legitimate user behavior, is frequently an indication of the download or execution of malicious software. Typical related attacker activity is likely to include the download and execution of further malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Medium

### **Possible data download via DNS tunnel**

(AzureDNS\_DataInfiltration)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected a possible DNS tunnel. Such activity, while possibly legitimate user behavior, is frequently performed by attackers to evade network monitoring and filtering. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

### **Possible data exfiltration via DNS tunnel**

(AzureDNS\_DataExfiltration)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected a possible DNS tunnel. Such activity, while possibly legitimate user behavior, is frequently performed by attackers to evade network monitoring and filtering. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

### **Possible data transfer via DNS tunnel**

(AzureDNS\_DataObfuscation)

**Description**: Analysis of DNS transactions from %{CompromisedEntity} detected a possible DNS tunnel. Such activity, while possibly legitimate user behavior, is frequently performed by attackers to evade network monitoring and filtering. Typical related attacker activity is likely to include the download and execution of malicious software or remote administration tools.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Low

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.