---
layout: Conceptual
title: Alerts for SQL Database and Azure Synapse Analytics - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-sql-database-and-azure-synapse-analytics
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
description: This article lists the security alerts for SQL Database and Azure Synapse Analytics visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2026-06-23T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8ed47ace-a3d7-67f0-b7a0-9d9b4f35bcbb
document_version_independent_id: 36f03be8-8563-37e5-f5bc-da6b4b01ffb2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-sql-database-and-azure-synapse-analytics.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-sql-database-and-azure-synapse-analytics
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-sql-database-and-azure-synapse-analytics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab7faaf-d791-4a26-96a2-3b11738538e7
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/302e28b0-1f09-4811-9a9b-2a72e0770581
platformId: 1dbddb2e-23d2-3ccf-013f-7ddaf2c24251
---

# Alerts for SQL Database and Azure Synapse Analytics - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for SQL Database and Azure Synapse Analytics. Microsoft Defender for Cloud and any enabled Microsoft Defender plans generate these alerts. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## SQL Database and Azure Synapse Analytics alerts

[Further details and notes](defender-for-sql-introduction)

### **A possible vulnerability to SQL Injection**

(SQL.DB\_VulnerabilityToSqlInjection SQL.VM\_VulnerabilityToSqlInjection SQL.MI\_VulnerabilityToSqlInjection SQL.DW\_VulnerabilityToSqlInjection Synapse.SQLPool\_VulnerabilityToSqlInjection)

**Description**: An application generates a faulty SQL statement in the database. This indicates a possible vulnerability to SQL injection attacks. There are two possible reasons for a faulty statement. A defect in application code might construct the faulty SQL statement. Or, application code or stored procedures don't sanitize user input when constructing the faulty SQL statement, which can be exploited for SQL injection.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: Medium

### **Logon activity from a potentially harmful application**

(SQL.DB\_HarmfulApplication SQL.VM\_HarmfulApplication SQL.MI\_HarmfulApplication SQL.DW\_HarmfulApplication Synapse.SQLPool\_HarmfulApplication)

**Description**: A potentially harmful application attempted to access your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: High

### **Log on from an unusual Azure Data Center**

(SQL.DB\_DataCenterAnomaly SQL.VM\_DataCenterAnomaly SQL.DW\_DataCenterAnomaly SQL.MI\_DataCenterAnomaly Synapse.SQLPool\_DataCenterAnomaly)

**Description**: There has been a change in the access pattern to an SQL Server, where someone has signed in to the server from an unusual Azure Data Center. In some cases, the alert detects a legitimate action (a new application or Azure service). In other cases, the alert detects a malicious action (attacker operating from breached resource in Azure).

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Probing

**Severity**: Informational

### **Log on from an unusual location**

(SQL.DB\_GeoAnomaly SQL.VM\_GeoAnomaly SQL.DW\_GeoAnomaly SQL.MI\_GeoAnomaly Synapse.SQLPool\_GeoAnomaly)

**Description**: There has been a change in the access pattern to SQL Server, where someone has signed in to the server from an unusual geographical location. In some cases, the alert detects a legitimate action (a new application or developer maintenance). In other cases, the alert detects a malicious action (a former employee or external attacker).

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Login from a principal user not seen in 60 days**

(SQL.DB\_PrincipalAnomaly SQL.VM\_PrincipalAnomaly SQL.DW\_PrincipalAnomaly SQL.MI\_PrincipalAnomaly Synapse.SQLPool\_PrincipalAnomaly)

**Description**: A principal user not seen in the last 60 days has logged into your database. If this database is new or this is expected behavior caused by recent changes in the users accessing the database, Defender for Cloud will identify significant changes to the access patterns and attempt to prevent future false positives.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Login from a domain not seen in 60 days**

(SQL.DB\_DomainAnomaly SQL.VM\_DomainAnomaly SQL.DW\_DomainAnomaly SQL.MI\_DomainAnomaly Synapse.SQLPool\_DomainAnomaly)

**Description**: A user has logged in to your resource from a domain no other users have connected from in the last 60 days. If this resource is new or this is expected behavior caused by recent changes in the users accessing the resource, Defender for Cloud will identify significant changes to the access patterns and attempt to prevent future false positives.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exploitation

**Severity**: Informational

### **Login from a suspicious IP**

(SQL.DB\_SuspiciousIpAnomaly SQL.VM\_SuspiciousIpAnomaly SQL.DW\_SuspiciousIpAnomaly SQL.MI\_SuspiciousIpAnomaly Synapse.SQLPool\_SuspiciousIpAnomaly)

**Description**: Your resource has been accessed successfully from an IP address that Microsoft Threat Intelligence has associated with suspicious activity.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: Medium

### **Potential SQL injection**

(SQL.DB\_PotentialSqlInjection SQL.VM\_PotentialSqlInjection SQL.MI\_PotentialSqlInjection SQL.DW\_PotentialSqlInjection Synapse.SQLPool\_PotentialSqlInjection)

**Description**: An active exploit has occurred against an identified application vulnerable to SQL injection. This means an attacker is trying to inject malicious SQL statements by using the vulnerable application code or stored procedures.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: High

### **Suspected brute force attack using a valid user**

(SQL.DB\_BruteForce SQL.VM\_BruteForce SQL.DW\_BruteForce SQL.MI\_BruteForce Synapse.SQLPool\_BruteForce)

**Description**: A potential brute force attack has been detected on your resource. The attacker is using the valid user (username), which has permissions to sign-in.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: High

### **Suspected brute force attack**

(SQL.DB\_BruteForce SQL.VM\_BruteForce SQL.DW\_BruteForce SQL.MI\_BruteForce Synapse.SQLPool\_BruteForce)

**Description**: A potential brute force attack has been detected on your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: High

### **Suspected successful brute force attack**

(SQL.DB\_BruteForce SQL.VM\_BruteForce SQL.DW\_BruteForce SQL.MI\_BruteForce Synapse.SQLPool\_BruteForce)

**Description**: A successful sign-in occurred after an apparent brute force attack on your resource.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Pre-Attack

**Severity**: High

### **SQL Server potentially spawned a Windows command shell and accessed an abnormal external source**

(SQL.DB\_ShellExternalSourceAnomaly SQL.VM\_ShellExternalSourceAnomaly SQL.DW\_ShellExternalSourceAnomaly SQL.MI\_ShellExternalSourceAnomaly Synapse.SQLPool\_ShellExternalSourceAnomaly)

**Description**: A suspicious SQL statement potentially spawned a Windows command shell with an external source that hasn't been seen before. Executing a shell that accesses an external source is a method used by attackers to download malicious payload and then execute it on the machine and compromise it. This enables an attacker to perform malicious tasks under remote direction. Alternatively, accessing an external source can be used to exfiltrate data to an external destination.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High/Medium

### **Unusual payload with obfuscated parts has been initiated by SQL Server**

(SQL.VM\_PotentialSqlInjection)

**Description**: Someone has initiated a new payload utilizing the layer in SQL Server that communicates with the operating system while concealing the command in the SQL query. Attackers commonly hide impactful commands, which are popularly monitored like xp\_cmdshell, sp\_add\_job and others. Obfuscation techniques abuse legitimate commands like string concatenation, casting, base changing, and others, to avoid regex detection and hurt the readability of the logs.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High/Medium

### **An abnormally large number of rows were extracted from your SQL Server - Preview**

(SQL.VM\_DataExfiltration)

**Description**: An unusually large number of rows has been extracted from your database in a single query. The activity might be related to legitimate operations, such as nonstandard backups or maintenance tasks. Alternatively, it could indicate a potential attempt to exfiltrate data from your SQL Server instances.

*Applies only to Defender for SQL on machines with extension version 2.0.3448.357 and later.*

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Exfiltration

**Severity**: Medium

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.