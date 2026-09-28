---
layout: Conceptual
title: Understand Just-in-time Virtual Machine Access - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/just-in-time-access-overview
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
description: Learn how just-in-time VM access in Microsoft Defender for Cloud reduces attack surface to lock down inbound management ports and allow access only when needed.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 1cc55d90-021d-45b6-f76c-f7521e431f3b
document_version_independent_id: b3794684-bc6e-79e5-d0cf-a8119ab83d94
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/just-in-time-access-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/just-in-time-access-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/just-in-time-access-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: cb437166-f1d1-cb8e-6705-10da8bc74491
---

# Understand Just-in-time Virtual Machine Access - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's Defender for Servers Plan 2 offers the just-in-time machine access feature. Just-in-time protects your resources from threat actors actively hunting for machines with open management ports, such as Remote Desktop Protocol (RDP) or Secure Shell (SSH). All machines are potential targets for attacks. Once compromised, a machine can serve as an entry point to further attack resources in the environment.

To reduce attack surfaces, minimize open ports, especially management ports. Legitimate users also need these ports, making it impractical to keep them closed.

Defender for Cloud's just-in-time machine access feature locks down inbound traffic to your virtual machines (VMs), which reduces exposure to attacks while ensuring easy access when needed.

## Just-in-time access and network resources

### Just-in-time access for Azure resources

In Azure, enable just-in-time access to block inbound traffic on specific ports.

- Defender for Cloud ensures *deny all inbound traffic* rules exist for your selected ports in the [network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview#security-rules) and [Azure Firewall rules](/en-us/azure/firewall/rule-processing).
- These rules restrict access to your Azure VMs' management ports and defend them from attack.
- If other rules already exist for the selected ports, those existing rules take priority over the new *deny all inbound traffic* rules.
- If no existing rules are on the selected ports, the new rules take top priority in the NSG and Azure Firewall.

### Just-in-time access for AWS resources

In Amazon Web Services (AWS), enable just-in-time access to revoke the relevant rules in the attached EC2 security groups for the selected ports. This approach blocks inbound traffic on those specific ports.

- When a user requests access to a VM, Defender for Servers checks that the user has [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/role-assignments-portal) permissions for that VM.
- If the user's access request is approved, Defender for Cloud configures the NSGs and Azure Firewall to allow inbound traffic to the selected ports from the relevant IP address (or range) for the specified amount of time.
- In AWS, Defender for Cloud creates a new EC2 security group that allows inbound traffic to the specified ports.
- After the approved access period expires, Defender for Cloud restores the NSGs to their previous states.
- Connections that are already established aren't interrupted.

Note

- Just-in-time access doesn't support VMs protected by Azure Firewalls controlled by [Azure Firewall Manager](/en-us/azure/firewall-manager/overview).
- The Azure Firewall must be configured with Rules (Classic) and can't use Firewall policies.

## Identify VMs for just-in-time access

The following diagram shows the logic that Defender for Servers applies when deciding how to categorize your supported VMs:

# [Azure](#tab/jit-azure)
The following diagram shows the decision flow for Azure VMs:

[![Just-in-time (JIT) virtual machine (VM) logic flow.](media/just-in-time-explained/jit-logic-flow.png)](media/just-in-time-explained/jit-logic-flow.png#lightbox)

# [AWS](#tab/jit-aws)
The following diagram shows the decision flow for AWS machines:

![A chart that explains the logic flow for the AWS just-in-time logic flow.](media/just-in-time-explained/aws-jit-logic-flow.png)

---

When Defender for Cloud finds a machine that can benefit from just-in-time access, it adds that machine to the recommendation's **Unhealthy resources** tab.

[![Screenshot that shows an unhealthy resource.](media/just-in-time-explained/unhealthy-resources.png)](media/just-in-time-explained/unhealthy-resources.png#lightbox)