---
layout: Conceptual
title: Use a Microsoft Sentinel playbook to stop potentially compromised users | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/tutorial-respond-threats-playbook
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: sshuster
description: Learn how to use Microsoft Sentinel playbooks and automation rules to automate a sample incident response and remediate security threats.
ms.topic: concept-article
ms.author: monaberdugo
author: mberdugo
ms.date: 2024-05-01T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: dc9ff6f0-4832-12a3-62c4-a84cd2c48a8d
document_version_independent_id: aa1683de-2d93-a36b-5ef2-06f7c8a3793f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/tutorial-respond-threats-playbook.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/tutorial-respond-threats-playbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/tutorial-respond-threats-playbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: b8e951f2-09aa-736f-41cc-59fb96b4aa7a
---

# Use a Microsoft Sentinel playbook to stop potentially compromised users | Microsoft Learn

This article describes a sample scenario of how you can use a playbook and automation rule to automate incident response and remediate security threats. Automation rules help you triage incidents in Microsoft Sentinel, and are also used to run playbooks in response to incidents or alerts. For more information, see [Automation in Microsoft Sentinel: Security orchestration, automation, and response (SOAR)](automation).

The sample scenario described in this article describes how to use an automation rule and playbook to stop a potentially compromised user when an incident is created.

Note

Because playbooks make use of Azure Logic Apps, additional charges may apply. Visit the [Azure Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps/) pricing page for more details.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

The following roles are required to use Azure Logic Apps to create and run playbooks in Microsoft Sentinel.

| Role | Description |
| --- | --- |
| **Owner** | Lets you grant access to playbooks in the resource group. |
| **Microsoft Sentinel Contributor** | Lets you attach a playbook to an analytics or automation rule. |
| **Microsoft Sentinel Responder** | Lets you access an incident in order to run a playbook manually, but doesn't allow you to run the playbook. |
| **Microsoft Sentinel Playbook Operator** | Lets you run a playbook manually. |
| **Microsoft Sentinel Automation Contributor** | Allows automation rules to run playbooks. This role isn't used for any other purpose. |

The following table describes required roles based on whether you select a Consumption or Standard logic app to create your playbook:

| Logic app | Azure roles | Description |
| --- | --- | --- |
| Consumption | **Logic App Contributor** | Edit and manage logic apps. Run playbooks. Doesn't allow you to grant access to playbooks. |
| Consumption | **Logic App Operator** | Read, enable, and disable logic apps. Doesn't allow you to edit or update logic apps. |
| Standard | **Logic Apps Standard Operator** | Enable, resubmit, and disable workflows in a logic app. |
| Standard | **Logic Apps Standard Developer** | Create and edit logic apps. |
| Standard | **Logic Apps Standard Contributor** | Manage all aspects of a logic app. |

The **Active playbooks** tab on the **Automation** page displays all active playbooks available across any selected subscriptions. By default, a playbook can be used only within the subscription to which it belongs, unless you specifically grant Microsoft Sentinel permissions to the playbook's resource group.

### Extra permissions required to run playbooks on incidents

Microsoft Sentinel uses a service account to run playbooks on incidents, to add security and enable the automation rules API to support CI/CD use cases. This service account is used for incident-triggered playbooks, or when you run a playbook manually on a specific incident.

In addition to your own roles and permissions, this Microsoft Sentinel service account must have its own set of permissions on the resource group where the playbook resides, in the form of the **Microsoft Sentinel Automation Contributor** role. Once Microsoft Sentinel has this role, it can run any playbook in the relevant resource group, manually or from an automation rule.

To grant Microsoft Sentinel with the required permissions, you must have an **Owner** or **User access administrator** role. To run the playbooks, you'll also need the **Logic App Contributor** role on the resource group that contains the playbooks you want to run.

## Stop potentially compromised users

SOC teams want to make sure that potentially compromised users can't move around their network and steal information. We recommend that you create an automated, multifaceted response to incidents generated by rules that detect compromised users to handle such scenarios.

**Configure your automation rule and playbook to use the following flow**:

1. An incident is created for a potentially compromised user and an automation rule is triggered to call your playbook.
2. The playbook opens a ticket in your IT ticketing system, such as ServiceNow.
3. The playbook also sends a message to your security operations channel in Microsoft Teams or Slack to make sure your security analysts are aware of the incident.
4. The playbook also sends all the information in the incident in an email message to your senior network admin and security admin. The email message includes **Block** and **Ignore** user option buttons.
5. The playbook waits until a response is received from the admins, then continues with its next steps.

    - If the admins choose **Block**, the playbook sends a command to Microsoft Entra ID to disable the user, and one to the firewall to block the IP address.
    - If the admins choose **Ignore**, the playbook closes the incident in Microsoft Sentinel, and the ticket in ServiceNow.

The following screenshot shows the actions and conditions you would add in creating this sample playbook:

[![Screenshot of a Logic App showing this playbook's actions and conditions.](../media/tutorial-respond-threats-playbook/logic-app.png)](../media/tutorial-respond-threats-playbook/logic-app.png#lightbox)