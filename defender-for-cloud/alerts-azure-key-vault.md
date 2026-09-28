---
layout: Conceptual
title: Alerts for Azure Key Vault - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-key-vault
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
description: This article lists the security alerts for Azure Key Vault visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d2e8aaa9-f74d-1a98-cfe1-4e8ceaeb9e10
document_version_independent_id: c23159fb-9be0-4afa-7cd6-e44cbacaf1ad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-key-vault.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-key-vault
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-key-vault.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: a6112b2f-bff8-8127-87fd-b86a242346ef
---

# Alerts for Azure Key Vault - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure Key Vault from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Azure Key Vault alerts

[Further details and notes](defender-for-key-vault-introduction)

### **Access from a suspicious IP address to a key vault**

(KV\_SuspiciousIPAccess)

**Description**: A key vault has been successfully accessed by an IP that has been identified by Microsoft Threat Intelligence as a suspicious IP address. This might indicate that your infrastructure has been compromised. We recommend further investigation. Learn more about [Microsoft's threat intelligence capabilities](https://www.microsoft.com/security/business/siem-and-xdr/microsoft-defender-threat-intelligence/).

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Access from a TOR exit node to a key vault**

(KV\_TORAccess)

**Description**: A key vault has been accessed from a known TOR exit node. This could be an indication that a threat actor has accessed the key vault and is using the TOR network to hide their source location. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **High volume of operations in a key vault**

(KV\_OperationVolumeAnomaly)

**Description**: An anomalous number of key vault operations were performed by a user, service principal, and/or a specific key vault. This anomalous activity pattern might be legitimate, but it could be an indication that a threat actor has gained access to the key vault and the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Suspicious policy change and secret query in a key vault**

(KV\_PutGetAnomaly)

**Description**: A user or service principal has performed an anomalous Vault Put policy change operation followed by one or more Secret Get operations. This pattern is not normally performed by the specified user or service principal. This might be legitimate activity, but it could be an indication that a threat actor has updated the key vault policy to access previously inaccessible secrets. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Suspicious secret listing and query in a key vault**

(KV\_ListGetAnomaly)

**Description**: A user or service principal has performed an anomalous Secret List operation followed by one or more Secret Get operations. This pattern is not normally performed by the specified user or service principal and is typically associated with secret dumping. This might be legitimate activity, but it could be an indication that a threat actor has gained access to the key vault and is trying to discover secrets that can be used to move laterally through your network and/or gain access to sensitive resources. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Unusual access denied - User accessing high volume of key vaults denied**

(KV\_AccountVolumeAccessDeniedAnomaly)

**Description**: A user or service principal has attempted access to anomalously high volume of key vaults in the last 24 hours. This anomalous access pattern might be legitimate activity. Though this attempt was unsuccessful, it could be an indication of a possible attempt to gain access of key vault and the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Discovery

**Severity**: Low

### **Unusual access denied - Unusual user accessing key vault denied**

(KV\_UserAccessDeniedAnomaly)

**Description**: A key vault access was attempted by a user that does not normally access it, this anomalous access pattern might be legitimate activity. Though this attempt was unsuccessful, it could be an indication of a possible attempt to gain access of key vault and the secrets contained within it.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access, Discovery

**Severity**: Low

### **Unusual application accessed a key vault**

(KV\_AppAnomaly)

**Description**: A key vault has been accessed by a service principal that doesn't normally access it. This anomalous access pattern might be legitimate activity, but it could be an indication that a threat actor has gained access to the key vault in an attempt to access the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Unusual operation pattern in a key vault**

(KV\_OperationPatternAnomaly)

**Description**: An anomalous pattern of key vault operations was performed by a user, service principal, and/or a specific key vault. This anomalous activity pattern might be legitimate, but it could be an indication that a threat actor has gained access to the key vault and the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Unusual user accessed a key vault**

(KV\_UserAnomaly)

**Description**: A key vault has been accessed by a user that does not normally access it. This anomalous access pattern might be legitimate activity, but it could be an indication that a threat actor has gained access to the key vault in an attempt to access the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Unusual user-application pair accessed a key vault**

(KV\_UserAppAnomaly)

**Description**: A key vault has been accessed by a user-service principal pair that doesn't normally access it. This anomalous access pattern might be legitimate activity, but it could be an indication that a threat actor has gained access to the key vault in an attempt to access the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **User accessed high volume of key vaults**

(KV\_AccountVolumeAnomaly)

**Description**: A user or service principal has accessed an anomalously high volume of key vaults. This anomalous access pattern might be legitimate activity, but it could be an indication that a threat actor has gained access to multiple key vaults in an attempt to access the secrets contained within them. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

### **Denied access from a suspicious IP to a key vault**

(KV\_SuspiciousIPAccessDenied)

**Description**: An unsuccessful key vault access has been attempted by an IP that has been identified by Microsoft Threat Intelligence as a suspicious IP address. Though this attempt was unsuccessful, it indicates that your infrastructure might have been compromised. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Low

### **Unusual access to the key vault from a suspicious IP (Non-Microsoft or external)**

(KV\_UnusualAccessSuspiciousIP)

**Description**: A user or service principal has attempted anomalous access to key vaults from a non-Microsoft IP in the last 24 hours. This anomalous access pattern might be legitimate activity. It could be an indication of a possible attempt to gain access of the key vault and the secrets contained within it. We recommend further investigations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Medium

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.