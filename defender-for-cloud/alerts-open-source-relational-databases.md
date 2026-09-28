---
layout: Conceptual
title: Alerts for open-source relational databases - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-open-source-relational-databases
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
description: This article lists the security alerts for open-source relational databases visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 89cd9d64-7ea3-516c-8900-482c0528b4ba
document_version_independent_id: c0039d46-df67-1022-49ef-085e4a6e3ae1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-open-source-relational-databases.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-open-source-relational-databases
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-open-source-relational-databases.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e97707c7-9dfc-e779-4f14-b64cba14df13
---

# Alerts for open-source relational databases - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for open-source relational databases from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Open-source relational databases alerts

[Further details and notes](defender-for-databases-introduction)

### **Suspected brute force attack using a valid user**

(SQL.PostgreSQL\_BruteForce SQL.MySQL\_BruteForce)

**Description**: A potential brute force attack has been detected on your resource. The attacker is using the valid user (username), which has permissions to log in.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Suspected successful brute force attack**

(SQL.PostgreSQL\_BruteForce SQL.MySQL\_BruteForce)

**Description**: A successful login occurred after an apparent brute force attack on your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: High

### **Suspected brute force attack**

(SQL.PostgreSQL\_BruteForce SQL.MySQL\_BruteForce)

**Description**: A potential brute force attack has been detected on your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

### **Attempted logon by a potentially harmful application**

(SQL.PostgreSQL\_HarmfulApplication SQL.MySQL\_HarmfulApplication)

**Description**: A potentially harmful application attempted to access your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: High/Medium

### **Login from a principal user not seen in 60 days**

(SQL.PostgreSQL\_PrincipalAnomaly SQL.MySQL\_PrincipalAnomaly)

**Description**: A principal user not seen in the last 60 days has logged into your database. If this database is new or this is expected behavior caused by recent changes in the users accessing the database, Defender for Cloud will identify significant changes to the access patterns and attempt to prevent future false positives.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Login from a domain not seen in 60 days**

(SQL.PostgreSQL\_DomainAnomaly SQL.MySQL\_DomainAnomaly)

**Description**: A user has logged in to your resource from a domain no other users have connected from in the last 60 days. If this resource is new or this is expected behavior caused by recent changes in the users accessing the resource, Defender for Cloud will identify significant changes to the access patterns and attempt to prevent future false positives.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Log on from an unusual Azure Data Center**

(SQL.PostgreSQL\_DataCenterAnomaly SQL.MySQL\_DataCenterAnomaly)

**Description**: Someone logged on to your resource from an unusual Azure Data Center.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Probing

**Severity**: Informational

### **Logon from an unusual cloud provider**

(SQL.PostgreSQL\_CloudProviderAnomaly SQL.MySQL\_CloudProviderAnomaly)

**Description**: Someone logged on to your resource from a cloud provider not seen in the last 60 days. It's quick and easy for threat actors to obtain disposable compute power for use in their campaigns. If this is expected behavior caused by the recent adoption of a new cloud provider, Defender for Cloud will learn over time and attempt to prevent future false positives.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Medium

### **Log on from an unusual location**

(SQL.PostgreSQL\_GeoAnomaly SQL.MySQL\_GeoAnomaly)

**Description**: Someone logged on to your resource from an unusual Azure Data Center.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Login from a suspicious IP**

(SQL.PostgreSQL\_SuspiciousIpAnomaly SQL.MySQL\_SuspiciousIpAnomaly)

**Description**: Your resource has been accessed successfully from an IP address that Microsoft Threat Intelligence has associated with suspicious activity.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: PreAttack

**Severity**: Medium

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.