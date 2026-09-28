---
layout: Conceptual
title: Alerts for Resource Manager - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-resource-manager
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
description: This article lists the security alerts for Resource Manager visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2025-06-09T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fe4e7eaa-2f77-1a3e-dd52-66cb427caa8e
document_version_independent_id: 38711941-7cec-ecdc-9a0e-2d11de297ef8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-resource-manager.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-resource-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-resource-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e38b9880-83d3-9ab8-ae4b-3ccdec7de7c6
---

# Alerts for Resource Manager - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Resource Manager from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Resource Manager alerts

Note

Alerts with a **delegated access** indication are triggered due to activity of third-party service providers. learn more about [service providers activity indications](defender-for-resource-manager-usage).

[Further details and notes](defender-for-resource-manager-introduction)

### **Azure Resource Manager operation from suspicious IP address**

(ARM\_OperationFromSuspiciousIP)

**Description**: Microsoft Defender for Resource Manager detected an operation from an IP address that has been marked as suspicious in threat intelligence feeds.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Azure Resource Manager operation from suspicious proxy IP address**

(ARM\_OperationFromSuspiciousProxyIP)

**Description**: Microsoft Defender for Resource Manager detected a resource management operation from an IP address that is associated with proxy services, such as TOR. While this behavior can be legitimate, it's often seen in malicious activities, when threat actors try to hide their source IP.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Defense Evasion

**Severity**: Medium

### **MicroBurst exploitation toolkit used to enumerate resources in your subscriptions**

(ARM\_MicroBurst.AzDomainInfo)

**Description**: A PowerShell script was run in your subscription and performed suspicious pattern of executing an information gathering operations to discover resources, permissions, and network structures. Threat actors use automated scripts, like MicroBurst, to gather information for malicious activities. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: Low

### **MicroBurst exploitation toolkit used to enumerate resources in your subscriptions**

(ARM\_MicroBurst.AzureDomainInfo)

**Description**: A PowerShell script was run in your subscription and performed suspicious pattern of executing an information gathering operations to discover resources, permissions, and network structures. Threat actors use automated scripts, like MicroBurst, to gather information for malicious activities. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: Low

### **MicroBurst exploitation toolkit used to execute code on your virtual machine**

(ARM\_MicroBurst.AzVMBulkCMD)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of executing code on a VM or a list of VMs. Threat actors use automated scripts, like MicroBurst, to run a script on a VM for malicious activities. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High

### **MicroBurst exploitation toolkit used to execute code on your virtual machine**

(RM\_MicroBurst.AzureRmVMBulkCMD)

**Description**: MicroBurst's exploitation toolkit was used to execute code on your virtual machines. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **MicroBurst exploitation toolkit used to extract keys from your Azure key vaults**

(ARM\_MicroBurst.AzKeyVaultKeysREST)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of extracting keys from an Azure Key Vault(s). Threat actors use automated scripts, like MicroBurst, to list keys and use them to access sensitive data or perform lateral movement. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **MicroBurst exploitation toolkit used to extract keys to your storage accounts**

(ARM\_MicroBurst.AZStorageKeysREST)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of extracting keys to Storage Account(s). Threat actors use automated scripts, like MicroBurst, to list keys and use them to access sensitive data in your Storage Account(s). This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: Low

### **MicroBurst exploitation toolkit used to extract secrets from your Azure key vaults**

(ARM\_MicroBurst.AzKeyVaultSecretsREST)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of extracting secrets from an Azure Key Vault(s). Threat actors use automated scripts, like MicroBurst, to list secrets and use them to access sensitive data or perform lateral movement. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **PowerZure exploitation toolkit used to elevate access from Microsoft Entra ID to Azure**

(ARM\_PowerZure.AzureElevatedPrivileges)

**Description**: PowerZure exploitation toolkit was used to elevate access from AzureAD to Azure. This was detected by analyzing Azure Resource Manager operations in your tenant.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **PowerZure exploitation toolkit used to enumerate resources**

(ARM\_PowerZure.GetAzureTargets)

**Description**: PowerZure exploitation toolkit was used to enumerate resources on behalf of a legitimate user account in your organization. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: High

### **PowerZure exploitation toolkit used to enumerate storage containers, shares, and tables**

(ARM\_PowerZure.ShowStorageContent)

**Description**: PowerZure exploitation toolkit was used to enumerate storage shares, tables, and containers. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **PowerZure exploitation toolkit used to execute a Runbook in your subscription**

(ARM\_PowerZure.StartRunbook)

**Description**: PowerZure exploitation toolkit was used to execute a Runbook. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **PowerZure exploitation toolkit used to extract Runbooks content**

(ARM\_PowerZure.AzureRunbookContent)

**Description**: PowerZure exploitation toolkit was used to extract Runbook content. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: High

### **PREVIEW - FSecure's Azurite toolkit detected**

(ARM\_Azurite)

**Description**: A known cloud-environment reconnaissance toolkit run has been detected in your environment. The tool [Azurite](https://github.com/mwrlabs/Azurite) can be used by an attacker (or penetration tester) to map your subscriptions' resources and identify insecure configurations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: High

### **Suspicious creation of compute resources detected**

(ARM\_SuspiciousComputeCreation)

**Description**: Microsoft Defender for Resource Manager identified a suspicious creation of compute resources in your subscription utilizing Virtual Machines/Azure Scale Set. The identified operations are designed to allow administrators to efficiently manage their environments by deploying new resources when needed. While this activity might be legitimate, a threat actor might utilize such operations to conduct crypto mining. The activity is deemed suspicious as the compute resources scale is higher than previously observed in the subscription. This can indicate that the principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Medium

### **Suspicious key vault recovery detected**

(Arm\_Suspicious\_Vault\_Recovering)

**Description**: Microsoft Defender for Resource Manager detected a suspicious recovery operation for a soft-deleted key vault resource. The user recovering the resource is different from the user that deleted it. This is highly suspicious because the user rarely invokes such an operation. In addition, the user logged on without multifactor authentication (MFA). This might indicate that the user is compromised and is attempting to discover secrets and keys to gain access to sensitive resources, or to perform lateral movement across your network.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral movement

**Severity**: Medium/high

### **PREVIEW - Suspicious management session using an inactive account detected**

(ARM\_UnusedAccountPersistence)

**Description**: Subscription activity logs analysis has detected suspicious behavior. A principal not in use for a long period of time is now performing actions that can secure persistence for an attacker.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Medium

### **PREVIEW - Suspicious invocation of a high-risk 'Credential Access' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.CredentialAccess)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to access credentials. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential access

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Data Collection' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.Collection)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to collect data. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to collect sensitive data on resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Defense Evasion' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.DefenseEvasion)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to evade defenses. The identified operations are designed to allow administrators to efficiently manage the security posture of their environments. While this activity might be legitimate, a threat actor might utilize such operations to avoid being detected while compromising resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Defense Evasion

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Execution' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.Execution)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation on a machine in your subscription, which might indicate an attempt to execute code. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Defense Execution

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Impact' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.Impact)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempted configuration change. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Initial Access' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.InitialAccess)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to access restricted resources. The identified operations are designed to allow administrators to efficiently access their environments. While this activity might be legitimate, a threat actor might utilize such operations to gain initial access to restricted resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial access

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Lateral Movement Access' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.LateralMovement)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to perform lateral movement. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to compromise more resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral movement

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'persistence' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.Persistence)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to establish persistence. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to establish persistence in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Informational

### **PREVIEW - Suspicious invocation of a high-risk 'Privilege Escalation' operation by a service principal detected**

(ARM\_AnomalousServiceOperation.PrivilegeEscalation)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to escalate privileges. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to escalate privileges while compromising resources in your environment. This can indicate that the service principal is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Privilege escalation

**Severity**: Informational

### **PREVIEW - Suspicious management session using an inactive account detected**

(ARM\_UnusedAccountPersistence)

**Description**: Subscription activity logs analysis has detected suspicious behavior. A principal not in use for a long period of time is now performing actions that can secure persistence for an attacker.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Medium

### **PREVIEW - Suspicious management session using PowerShell detected**

(ARM\_UnusedAppPowershellPersistence)

**Description**: Subscription activity logs analysis has detected suspicious behavior. A principal that doesn't regularly use PowerShell to manage the subscription environment is now using PowerShell, and performing actions that can secure persistence for an attacker.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Medium

### **PREVIEW â€“ Suspicious management session using Azure portal detected**

(ARM\_UnusedAppIbizaPersistence)

**Description**: Analysis of your subscription activity logs has detected a suspicious behavior. A principal that doesn't regularly use the Azure portal (Ibiza) to manage the subscription environment (hasn't used Azure portal to manage for the last 45 days, or a subscription that it is actively managing), is now using the Azure portal and performing actions that can secure persistence for an attacker.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Medium

### **Privileged custom role created for your subscription in a suspicious way**

(ARM\_PrivilegedRoleDefinitionCreation)

**Description**: Microsoft Defender for Resource Manager detected a suspicious creation of privileged custom role definition in your subscription. This operation might have been performed by a legitimate user in your organization. Alternatively, it might indicate that an account in your organization was breached, and that the threat actor is trying to create a privileged role to use in the future to evade detection.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Privilege Escalation, Defense Evasion

**Severity**: Informational

### **Suspicious Azure role assignment detected (Preview)**

(ARM\_AnomalousRBACRoleAssignment)

**Description**: Microsoft Defender for Resource Manager identified a suspicious Azure role assignment / performed using PIM (Privileged Identity Management) in your tenant, which might indicate that an account in your organization was compromised. The identified operations are designed to allow administrators to grant principals access to Azure resources. While this activity might be legitimate, a threat actor might utilize role assignment to escalate their permissions allowing them to advance their attack.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral Movement, Defense Evasion

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Credential Access' operation detected (Preview)**

(ARM\_AnomalousOperation.CredentialAccess)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to access credentials. The identified operations are designed to allow administrators to efficiently access their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Credential Access

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Data Collection' operation detected (Preview)**

(ARM\_AnomalousOperation.Collection)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to collect data. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to collect sensitive data on resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Collection

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Defense Evasion' operation detected (Preview)**

(ARM\_AnomalousOperation.DefenseEvasion)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to evade defenses. The identified operations are designed to allow administrators to efficiently manage the security posture of their environments. While this activity might be legitimate, a threat actor might utilize such operations to avoid being detected while compromising resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Defense Evasion

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Execution' operation detected (Preview)**

(ARM\_AnomalousOperation.Execution)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation on a machine in your subscription, which might indicate an attempt to execute code. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Impact' operation detected (Preview)**

(ARM\_AnomalousOperation.Impact)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempted configuration change. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to access restricted credentials and compromise resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Initial Access' operation detected (Preview)**

(ARM\_AnomalousOperation.InitialAccess)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to access restricted resources. The identified operations are designed to allow administrators to efficiently access their environments. While this activity might be legitimate, a threat actor might utilize such operations to gain initial access to restricted resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Initial Access

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Lateral Movement' operation detected (Preview)**

(ARM\_AnomalousOperation.LateralMovement)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to perform lateral movement. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to compromise more resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral Movement

**Severity**: Informational

### **Suspicious elevate access operation**

(ARM\_AnomalousElevateAccess)

**Description**: Microsoft Defender for Resource Manager identified a suspicious "Elevate Access" operation. The activity is deemed suspicious, as this principal rarely invokes such operations. While this activity might be legitimate, a threat actor might utilize an "Elevate Access" operation to perform privilege escalation for a compromised user.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Privilege Escalation

**Severity**: Medium

### **Suspicious invocation of a high-risk 'Persistence' operation detected (Preview)**

(ARM\_AnomalousOperation.Persistence)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to establish persistence. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to establish persistence in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Informational

### **Suspicious invocation of a high-risk 'Privilege Escalation' operation detected (Preview)**

(ARM\_AnomalousOperation.PrivilegeEscalation)

**Description**: Microsoft Defender for Resource Manager identified a suspicious invocation of a high-risk operation in your subscription, which might indicate an attempt to escalate privileges. The identified operations are designed to allow administrators to efficiently manage their environments. While this activity might be legitimate, a threat actor might utilize such operations to escalate privileges while compromising resources in your environment. This can indicate that the account is compromised and is being used with malicious intent.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Privilege Escalation

**Severity**: Informational

### **Usage of MicroBurst exploitation toolkit to run an arbitrary code or exfiltrate Azure Automation account credentials**

(ARM\_MicroBurst.RunCodeOnBehalf)

**Description**: A PowerShell script was run in your subscription and performed a suspicious pattern of executing an arbitrary code or exfiltrate Azure Automation account credentials. Threat actors use automated scripts, like MicroBurst, to run arbitrary code for malicious activities. This was detected by analyzing Azure Resource Manager operations in your subscription. This operation might indicate that an identity in your organization was breached, and that the threat actor is trying to compromise your environment for malicious intentions.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence, Credential Access

**Severity**: High

### **Usage of NetSPI techniques to maintain persistence in your Azure environment**

(ARM\_NetSPI.MaintainPersistence)

**Description**: Usage of NetSPI persistence technique to create a webhook backdoor and maintain persistence in your Azure environment. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **Usage of PowerZure exploitation toolkit to run an arbitrary code or exfiltrate Azure Automation account credentials**

(ARM\_PowerZure.RunCodeOnBehalf)

**Description**: PowerZure exploitation toolkit detected attempting to run code or exfiltrate Azure Automation account credentials. This was detected by analyzing Azure Resource Manager operations in your subscription.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: -

**Severity**: High

### **Suspicious classic role assignment detected (Preview)**

(ARM\_AnomalousClassicRoleAssignment)

**Description**: Microsoft Defender for Resource Manager identified a suspicious classic role assignment in your tenant, which might indicate that an account in your organization was compromised. The identified operations are designed to provide backward compatibility with classic roles that are no longer commonly used. While this activity might be legitimate, a threat actor might utilize such assignment to grant permissions to another user account under their control.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Lateral Movement, Defense Evasion

**Severity**: High

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.