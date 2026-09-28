---
layout: Conceptual
title: Alerts for Azure VM extensions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-vm-extensions
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
description: This article lists the security alerts for Azure VM extensions visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: edc554f4-16ef-27f6-9a9b-67814dcb61ea
document_version_independent_id: 477732a8-f4f3-3279-26a5-cf51694b83fa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-vm-extensions.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-vm-extensions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-vm-extensions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 57648703-b7d0-61ef-2baa-cc6f46992501
---

# Alerts for Azure VM extensions - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure VM extensions from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Azure VM extensions alerts

These alerts focus on detecting suspicious activities of Azure virtual machine extensions and provides insights into attackers' attempts to compromise and perform malicious activities on your virtual machines.

Azure virtual machine extensions are small applications that run post-deployment on virtual machines and provide capabilities such as configuration, automation, monitoring, security, and more. While extensions are a powerful tool, they can be used by threat actors for various malicious intents, for example:

- Data collection and monitoring
- Code execution and configuration deployment with high privileges
- Resetting credentials and creating administrative users
- Encrypting disks

Learn more about [Defender for Cloud latest protections against the abuse of Azure VM extensions](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/microsoft-defender-for-cloud-latest-protection-against/ba-p/3970121).

### **Suspicious failure installing GPU extension in your subscription (Preview)**

(VM\_GPUExtensionSuspiciousFailure)

**Description**: Suspicious intent of installing a GPU extension on unsupported VMs. This extension should be installed on virtual machines equipped with a graphic processor, and in this case the virtual machines are not equipped with such. These failures can be seen when malicious adversaries execute multiple installations of such extension for crypto-mining purposes.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Medium

### **Suspicious installation of a GPU extension was detected on your virtual machine (Preview)**

(VM\_GPUDriverExtensionUnusualExecution)

**Description**: Suspicious installation of a GPU extension was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use the GPU driver extension to install GPU drivers on your virtual machine via the Azure Resource Manager to perform cryptojacking. This activity is deemed suspicious as the principal's behavior departs from its usual patterns.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Low

### **Run Command with a suspicious script was detected on your virtual machine (Preview)**

(VM\_RunCommandSuspiciousScript)

**Description**: A Run Command with a suspicious script was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use Run Command to execute malicious code with high privileges on your virtual machine via the Azure Resource Manager. The script is deemed suspicious as certain parts were identified as being potentially malicious.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High

### **Suspicious unauthorized Run Command usage was detected on your virtual machine (Preview)**

(VM\_RunCommandSuspiciousFailure)

**Description**: Suspicious unauthorized usage of Run Command has failed and was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might attempt to use Run Command to execute malicious code with high privileges on your virtual machines via the Azure Resource Manager. This activity is deemed suspicious as it hasn't been commonly seen before.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Suspicious Run Command usage was detected on your virtual machine (Preview)**

(VM\_RunCommandSuspiciousUsage)

**Description**: Suspicious usage of Run Command was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use Run Command to execute malicious code with high privileges on your virtual machines via the Azure Resource Manager. This activity is deemed suspicious as it hasn't been commonly seen before.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Low

### **Suspicious usage of multiple monitoring or data collection extensions was detected on your virtual machines (Preview)**

(VM\_SuspiciousMultiExtensionUsage)

**Description**: Suspicious usage of multiple monitoring or data collection extensions was detected on your virtual machines by analyzing the Azure Resource Manager operations in your subscription. Attackers might abuse such extensions for data collection, network traffic monitoring, and more, in your subscription. This usage is deemed suspicious as it hasn't been commonly seen before.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Reconnaissance

**Severity**: Medium

### **Suspicious installation of disk encryption extensions was detected on your virtual machines (Preview)**

(VM\_DiskEncryptionSuspiciousUsage)

**Description**: Suspicious installation of disk encryption extensions was detected on your virtual machines by analyzing the Azure Resource Manager operations in your subscription. Attackers might abuse the disk encryption extension to deploy full disk encryptions on your virtual machines via the Azure Resource Manager in an attempt to perform ransomware activity. This activity is deemed suspicious as it hasn't been commonly seen before and due to the high number of extension installations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Impact

**Severity**: Medium

### **Suspicious usage of VMAccess extension was detected on your virtual machines (Preview)**

(VM\_VMAccessSuspiciousUsage)

**Description**: Suspicious usage of VMAccess extension was detected on your virtual machines. Attackers might abuse the VMAccess extension to gain access and compromise your virtual machines with high privileges by resetting access or managing administrative users. This activity is deemed suspicious as the principal's behavior departs from its usual patterns, and due to the high number of the extension installations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Persistence

**Severity**: Medium

### **Desired State Configuration (DSC) extension with a suspicious script was detected on your virtual machine (Preview)**

(VM\_DSCExtensionSuspiciousScript)

**Description**: Desired State Configuration (DSC) extension with a suspicious script was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use the Desired State Configuration (DSC) extension to deploy malicious configurations, such as persistence mechanisms, malicious scripts, and more, with high privileges, on your virtual machines. The script is deemed suspicious as certain parts were identified as being potentially malicious.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High

### **Suspicious usage of a Desired State Configuration (DSC) extension was detected on your virtual machines (Preview)**

(VM\_DSCExtensionSuspiciousUsage)

**Description**: Suspicious usage of a Desired State Configuration (DSC) extension was detected on your virtual machines by analyzing the Azure Resource Manager operations in your subscription. Attackers might use the Desired State Configuration (DSC) extension to deploy malicious configurations, such as persistence mechanisms, malicious scripts, and more, with high privileges, on your virtual machines. This activity is deemed suspicious as the principal's behavior departs from its usual patterns, and due to the high number of the extension installations.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Low

### **Custom script extension with a suspicious script was detected on your virtual machine (Preview)**

(VM\_CustomScriptExtensionSuspiciousCmd)

**Description**: Custom script extension with a suspicious script was detected on your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use Custom script extension to execute malicious code with high privileges on your virtual machine via the Azure Resource Manager. The script is deemed suspicious as certain parts were identified as being potentially malicious.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: High

### **Suspicious failed execution of custom script extension in your virtual machine**

(VM\_CustomScriptExtensionSuspiciousFailure)

**Description**: Suspicious failure of a custom script extension was detected in your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Such failures might be associated with malicious scripts run by this extension.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Unusual deletion of custom script extension in your virtual machine**

(VM\_CustomScriptExtensionUnusualDeletion)

**Description**: Unusual deletion of a custom script extension was detected in your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use custom script extensions to execute malicious code on your virtual machines via the Azure Resource Manager.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Unusual execution of custom script extension in your virtual machine**

(VM\_CustomScriptExtensionUnusualExecution)

**Description**: Unusual execution of a custom script extension was detected in your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use custom script extensions to execute malicious code on your virtual machines via the Azure Resource Manager.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Custom script extension with suspicious entry-point in your virtual machine**

(VM\_CustomScriptExtensionSuspiciousEntryPoint)

**Description**: Custom script extension with a suspicious entry-point was detected in your virtual machine by analyzing the Azure Resource Manager operations in your subscription. The entry-point refers to a suspicious GitHub repository. Attackers might use custom script extensions to execute malicious code on your virtual machines via the Azure Resource Manager.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

### **Custom script extension with suspicious payload in your virtual machine**

(VM\_CustomScriptExtensionSuspiciousPayload)

**Description**: Custom script extension with a payload from a suspicious GitHub repository was detected in your virtual machine by analyzing the Azure Resource Manager operations in your subscription. Attackers might use custom script extensions to execute malicious code on your virtual machines via the Azure Resource Manager.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Execution

**Severity**: Medium

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.