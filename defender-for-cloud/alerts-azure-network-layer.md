---
layout: Conceptual
title: Alerts for Azure network layer - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-network-layer
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
description: This article lists the security alerts for Azure network layer visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a854926e-a48c-de6b-35d6-9ac7c5b1bd19
document_version_independent_id: b5516c64-ad7c-f918-523c-d80114432d43
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-network-layer.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-network-layer
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-network-layer.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f98c9a19-e481-4f15-8047-76b641e6ed57
- https://authoring-docs-microsoft.poolparty.biz/devrel/d4cf20b3-3e54-4ed9-8b09-370a52eee81b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f5685781-a4fd-40f1-8126-59abde4643bf
- https://authoring-docs-microsoft.poolparty.biz/devrel/9ecc2643-be13-4271-a1f4-87114737d63a
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a52d8a0c-b032-ddd5-8344-5ef98cbe6bc4
---

# Alerts for Azure network layer - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure network layer from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Azure network layer alerts

[Further details and notes](other-threat-protections#network-layer)

### **Network communication with a malicious machine detected**

(Network\_CommunicationWithC2)

**Description**: Network traffic analysis indicates that your machine (IP %{Victim IP}) has communicated with what is possibly a Command and Control center. When the compromised resource is a load balancer or an application gateway, the suspected activity might indicate that one or more of the resources in the backend pool (of the load balancer or application gateway) has communicated with what is possibly a Command and Control center.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Command and Control

**Severity**: Medium

### **Possible compromised machine detected**

(Network\_ResourceIpIndicatedAsMalicious)

**Description**: Threat intelligence indicates that your machine (at IP %{Machine IP}) might have been compromised by a malware of type Conficker. Conficker was a computer worm that targets the Microsoft Windows operating system and was first detected in November 2008. Conficker infected millions of computers including government, business and home computers in over 200 countries/regions, making it the largest known computer worm infection since the 2003 Welchia worm.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Command and Control

**Severity**: Medium

### **Possible incoming %{Service Name} brute force attempts detected**

(Generic\_Incoming\_BF\_OneToOne)

**Description**: Network traffic analysis detected incoming %{Service Name} communication to %{Victim IP}, associated with your resource %{Compromised Host} from %{Attacker IP}. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows suspicious activity between %{Start Time} and %{End Time} on port %{Victim Port}. This activity is consistent with brute force attempts against %{Service Name} servers.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Informational

### **Possible incoming SQL brute force attempts detected**

(SQL\_Incoming\_BF\_OneToOne)

**Description**: Network traffic analysis detected incoming SQL communication to %{Victim IP}, associated with your resource %{Compromised Host}, from %{Attacker IP}. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows suspicious activity between %{Start Time} and %{End Time} on port %{Port Number} (%{SQL Service Type}). This activity is consistent with brute force attempts against SQL servers.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Possible outgoing denial-of-service attack detected**

(DDOS)

**Description**: Network traffic analysis detected anomalous outgoing activity originating from %{Compromised Host}, a resource in your deployment. This activity might indicate that your resource was compromised and is now engaged in denial-of-service attacks against external endpoints. When the compromised resource is a load balancer or an application gateway, the suspected activity might indicate that one or more of the resources in the backend pool (of the load balancer or application gateway) was compromised. Based on the volume of connections, we believe that the following IPs are possibly the targets of the DOS attack: %{Possible Victims}. Note that it is possible that the communication to some of these IPs is legitimate.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Medium

### **Suspicious incoming RDP network activity from multiple sources**

(RDP\_Incoming\_BF\_ManyToOne)

**Description**: Network traffic analysis detected anomalous incoming Remote Desktop Protocol (RDP) communication to %{Victim IP}, associated with your resource %{Compromised Host}, from multiple sources. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Attacking IPs} unique IPs connecting to your resource, which is considered abnormal for this environment. This activity might indicate an attempt to brute force your RDP end point from multiple hosts (Botnet).

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Suspicious incoming RDP network activity**

(RDP\_Incoming\_BF\_OneToOne)

**Description**: Network traffic analysis detected anomalous incoming Remote Desktop Protocol (RDP) communication to %{Victim IP}, associated with your resource %{Compromised Host}, from %{Attacker IP}. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Connections} incoming connections to your resource, which is considered abnormal for this environment. This activity might indicate an attempt to brute force your RDP end point

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Suspicious incoming SSH network activity from multiple sources**

(SSH\_Incoming\_BF\_ManyToOne)

**Description**: Network traffic analysis detected anomalous incoming SSH communication to %{Victim IP}, associated with your resource %{Compromised Host}, from multiple sources. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Attacking IPs} unique IPs connecting to your resource, which is considered abnormal for this environment. This activity might indicate an attempt to brute force your SSH end point from multiple hosts (Botnet)

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Suspicious incoming SSH network activity**

(SSH\_Incoming\_BF\_OneToOne)

**Description**: Network traffic analysis detected anomalous incoming SSH communication to %{Victim IP}, associated with your resource %{Compromised Host}, from %{Attacker IP}. When the compromised resource is a load balancer or an application gateway, the suspected incoming traffic has been forwarded to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Connections} incoming connections to your resource, which is considered abnormal for this environment. This activity might indicate an attempt to brute force your SSH end point

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Suspicious outgoing %{Attacked Protocol} traffic detected**

(PortScanning)

**Description**: Network traffic analysis detected suspicious outgoing traffic from %{Compromised Host} to destination port %{Most Common Port}. When the compromised resource is a load balancer or an application gateway, the suspected outgoing traffic has been originated from to one or more of the resources in the backend pool (of the load balancer or application gateway). This behavior might indicate that your resource is taking part in %{Attacked Protocol} brute force attempts or port sweeping attacks.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Discovery

**Severity**: Medium

### **Suspicious outgoing RDP network activity to multiple destinations**

(RDP\_Outgoing\_BF\_OneToMany)

**Description**: Network traffic analysis detected anomalous outgoing Remote Desktop Protocol (RDP) communication to multiple destinations originating from %{Compromised Host} (%{Attacker IP}), a resource in your deployment. When the compromised resource is a load balancer or an application gateway, the suspected outgoing traffic has been originated from to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows your machine connecting to %{Number of Attacked IPs} unique IPs, which is considered abnormal for this environment. This activity might indicate that your resource was compromised and is now used to brute force external RDP end points. Note that this type of activity could possibly cause your IP to be flagged as malicious by external entities.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Discovery

**Severity**: High

### **Suspicious outgoing RDP network activity**

(RDP\_Outgoing\_BF\_OneToOne)

**Description**: Network traffic analysis detected anomalous outgoing Remote Desktop Protocol (RDP) communication to %{Victim IP} originating from %{Compromised Host} (%{Attacker IP}), a resource in your deployment. When the compromised resource is a load balancer or an application gateway, the suspected outgoing traffic has been originated from to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Connections} outgoing connections from your resource, which is considered abnormal for this environment. This activity might indicate that your machine was compromised and is now used to brute force external RDP end points. Note that this type of activity could possibly cause your IP to be flagged as malicious by external entities.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral Movement

**Severity**: High

### **Suspicious outgoing SSH network activity to multiple destinations**

(SSH\_Outgoing\_BF\_OneToMany)

**Description**: Network traffic analysis detected anomalous outgoing SSH communication to multiple destinations originating from %{Compromised Host} (%{Attacker IP}), a resource in your deployment. When the compromised resource is a load balancer or an application gateway, the suspected outgoing traffic has been originated from to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows your resource connecting to %{Number of Attacked IPs} unique IPs, which is considered abnormal for this environment. This activity might indicate that your resource was compromised and is now used to brute force external SSH end points. Note that this type of activity could possibly cause your IP to be flagged as malicious by external entities.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Discovery

**Severity**: Medium

### **Suspicious outgoing SSH network activity**

(SSH\_Outgoing\_BF\_OneToOne)

**Description**: Network traffic analysis detected anomalous outgoing SSH communication to %{Victim IP} originating from %{Compromised Host} (%{Attacker IP}), a resource in your deployment. When the compromised resource is a load balancer or an application gateway, the suspected outgoing traffic has been originated from to one or more of the resources in the backend pool (of the load balancer or application gateway). Specifically, sampled network data shows %{Number of Connections} outgoing connections from your resource, which is considered abnormal for this environment. This activity might indicate that your resource was compromised and is now used to brute force external SSH end points. Note that this type of activity could possibly cause your IP to be flagged as malicious by external entities.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral Movement

**Severity**: Medium

### **Traffic detected from IP addresses recommended for blocking**

(Network\_TrafficFromUnrecommendedIP)

**Description**: Microsoft Defender for Cloud detected inbound traffic from IP addresses that are recommended to be blocked. This typically occurs when this IP address doesn't communicate regularly with this resource. Alternatively, the IP address has been flagged as malicious by Defender for Cloud's threat intelligence sources.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Probing

**Severity**: Informational

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.