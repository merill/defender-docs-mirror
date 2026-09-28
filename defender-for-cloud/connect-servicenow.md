---
layout: Conceptual
title: Connect ServiceNow's ITSM module to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/connect-servicenow
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
description: Learn how to connect ServiceNow with Microsoft Defender for Cloud to protect Azure, hybrid, and multicloud machines.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 0f0e4d38-bdf6-99d8-a370-d2f6fbd3a27c
document_version_independent_id: 46981caa-b81c-278a-add6-ef3ae4d6c4a6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/connect-servicenow.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/connect-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/connect-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 9ee6a01a-27ac-1307-229e-f5f15f51524b
---

# Connect ServiceNow's ITSM module to Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates with ServiceNow IT Service Management (ITSM). This integration lets you connect your Defender for Cloud account to ServiceNow. You can use ServiceNow workflows to manage recommendations and prioritize remediation work. You can also create and view ServiceNow tickets for recommendations directly from Defender for Cloud.

## Prerequisites

- Have an application registry configured in ServiceNow. For setup steps, see [How to create a ServiceNow API key and secret](https://www.opslogix.com/knowledgebase/servicenow/kb-create-a-servicenow-api-key-and-secret-for-the-scom-servicenow-incident-connector).
- Enable Defender Cloud Security Posture Management (CSPM) on your Azure subscription. For setup steps, see [Enable Defender CSPM](tutorial-enable-cspm-plan).
- To create the integration, you must have one of these roles: Security Admin, Contributor, or Owner.
- To create ServiceNow tickets for recommendations on Amazon Web Services (AWS) or Google Cloud Platform (GCP) resources, configure the ServiceNow integration at the connector level. An integration that is scoped only to an Azure subscription doesn't apply to non-Azure resources.

## Connect a ServiceNow account to Defender for Cloud

To connect a ServiceNow account to a Defender for Cloud account:

1. Sign in to the Azure portal at [portal.azure.com](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select **Integrations**.

    ![Screenshot of environment settings page that shows where to select the ServiceNow option.](media/connect-servicenow/integrations.png)
4. Select **Add integration** &gt; **ServiceNow**.

    [![Screenshot that shows where the add integration button is and the ServiceNow option.](media/connect-servicenow/add-servicenow.png)](media/connect-servicenow/add-servicenow.png#lightbox)
5. Enter a name and select the scope.
6. Enter the instance URL, User name, Password, Client ID, and client secret from the application registry that you created in the ServiceNow portal.
7. Select **Next**.
8. Select Incident data, Problems data, and Changes table from the drop-down menus.

    ![Screenshot that shows the custom option selected and the accompanying fields you can enter information into.](media/connect-servicenow/customize-fields.png)
9. Select **Save**.

After you save the integration, a success notice appears.