---
layout: Conceptual
title: Define an access restriction policy for Standard-plan playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/automation/define-playbook-access-restrictions
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
description: This article shows how to define an access restriction policy for Microsoft Sentinel Standard-plan playbooks, so that they can support private endpoints.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e6d90633-4411-b269-6829-0ab5a315e7a8
document_version_independent_id: 340d589e-9d6a-3343-37b7-d31fd0edea2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/automation/define-playbook-access-restrictions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/automation/define-playbook-access-restrictions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/automation/define-playbook-access-restrictions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
platformId: 697da6bb-f033-f173-9956-ced01b41ce16
---

# Define an access restriction policy for Standard-plan playbooks | Microsoft Learn

This article describes how to define an [access restriction policy](/en-us/azure/app-service/overview-access-restrictions) for Microsoft Sentinel Standard-plan playbooks, so that they can support private endpoints.

Define an access restriction policy to ensure that only Microsoft Sentinel has access to the Standard logic app containing your playbook workflows.

For more information, see:

- [Secure traffic between Standard logic apps and Azure virtual networks using private endpoints](/en-us/azure/logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint)
- [Supported logic app types](logic-apps-playbooks#supported-logic-app-types)

Important

The new version of access restriction policies is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](../overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

## Define an access restriction policy

Perform the following steps to define an access restriction policy for a Standard-plan playbook.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), select the **Configuration** &gt; **Automation** page. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation**.
2. On the **Automation** page, select the **Active playbooks** tab.
3. Filter the list for Standard-plan apps. Select the **Plan** filter and clear the **Consumption** checkbox, and then select **OK**. For example:

    ![Screenshot showing how to filter the list of apps for the standard plan type.](../media/define-playbook-access-restrictions/filter-list-for-standard.png)
4. Select a playbook to which you want to restrict access. For example:

    [![Screenshot showing how to select playbook from the list of playbooks.](../media/define-playbook-access-restrictions/select-playbook.png)](../media/define-playbook-access-restrictions/select-playbook.png#lightbox)
5. Select the logic app link on the playbook screen. For example:

    [![Screenshot showing how to select logic app from the playbook screen.](../media/define-playbook-access-restrictions/select-logic-app.png)](../media/define-playbook-access-restrictions/select-logic-app.png#lightbox)
6. From the navigation menu of your logic app, under **Settings**, select **Networking**. For example:

    [![Screenshot showing how to select networking settings from the logic app menu.](../media/define-playbook-access-restrictions/select-networking.png)](../media/define-playbook-access-restrictions/select-networking.png#lightbox)
7. In the **Inbound traffic configuration** area, select **Public network access**.
8. In the **Access Restrictions** page, select the **Enabled from select virtual networks and IP addresses** checkbox.

    ![Screenshot showing how to select access restriction policy for configuration.](../media/define-playbook-access-restrictions/select-access-restriction.png)
9. Under **Site access and rules**, select **+ Add**. The **Add rule** panel opens on the side. For example:

    ![Screenshot showing how to add a filter rule to your access restriction policy.](../media/define-playbook-access-restrictions/add-filter-rule.png)
10. In the **Add rule** pane, enter the following details.

    The name and optional description should reflect that this rule allows only Microsoft Sentinel to access the logic app. Leave the fields not mentioned below as they are.

    | Field | Enter or select |
    | --- | --- |
    | **Name** | Enter `SentinelAccess` or another name of your choosing. |
    | **Action** | Allow |
    | **Priority** | Enter `1` |
    | **Description** | Optional. Add a description of your choosing. |
    | **Type** | Select **Service Tag**. |
    | **Service Tag***(will appear only after youselect **Service Tag** above.)* | Search for and select **AzureSentinel**. |
11. Select **Add rule**.

## Review a sample access restriction policy

After following the procedure in this article, your policy should look as follows:

![Screenshot showing rules as they should appear in your access restriction policy.](../media/define-playbook-access-restrictions/resulting-rule.png)