---
layout: Conceptual
title: Policy Engine Automation | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/policy-engine
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/133/azure
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
ms.service: defender-easm
description: Automate inventory curation by leveraging the policy engine to proactively implement certain actions based on predetermined parameters.
author: danielledennis
ms.author: dandennis
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9fafc87c-cb15-fd74-bddd-b7d4aa20e7c9
document_version_independent_id: 4ceb5a50-fbc0-4ff3-7cfc-d4c16593b513
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/policy-engine.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/policy-engine
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/policy-engine.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 91396aa0-f70c-4c97-8909-6dc58c9d6940
---

# Policy Engine Automation | Microsoft Learn

The policy engine enables Defender External Attack Surface Management (Defender EASM) users to automate certain actions based on predetermined parameters. You can elect to label assets or change their states based on highly flexible query parameters to automate the curation of your attack surface. Once defined, policies run automatically to ensure that your inventory is categorized according to your specific needs on a recurrent basis. With the policy engine, you can apply business context to your inventory in bulk with minimal manual effort with the following actions:

- Add or remove labels
- Set an external ID
- Set an asset state
- Remove from inventory

## Access and understand policies

To quickly access policy information, navigate to the dedicated Policies page in your Defender EASM resource. The Policies page is located under the **Manage** section of the left-hand navigation pane.

[![Screenshot of Defender EASM navigation with Policies selected under Manage.](media/policies-1.png)](media/policies-1.png#lightbox)

The Policies page displays a list of all active policies in your Defender EASM resource. The policy list view provides immediate access to key information about each policy, including:

- **Policy:** The designated name for the policy.
- **Description:** The designated description for the policy, providing more context about the configuration and intended business value.
- **Query:** The underlying quer(ies) that power each policy. Policy actions are applied specifically to assets that match these configured filter parameters.
- **Action:** A description of the action that takes place when assets match the designated filter parameters. Actions include: add or remove labels, set state, set external ID, and remove from inventory.
- **Created by:** The email alias of the Defender EASM user who created the policy.
- **Created on:** The date that the policy was first created.
- **Affected assets:** A count of all assets that were updated in accordance with the policy. Clicking the numerical count routes you to the inventory list view, filtered to display only the assets that match the underlying quer(ies) that power the policy.

[![Screenshot of the Policies page showing policy list columns including name, description, query, action, created by, created on, and affected assets.](media/policies-2.png)](media/policies-2.png#lightbox)

## Create a policy

To create a policy in your Defender EASM resource, perform the following steps:

1. Navigate to the Policies page by selecting **Policies** from the **Manage** section of the left-hand navigation pane within your Defender EASM resource.
2. Select **+ Add Policy**. Selecting this button opens a right-hand pane to configure the policy.

[![Screenshot of Policies page with Add Policies button highlighted and policy configuration panel open.](media/policies-3.png)](media/policies-3.png#lightbox)

1. Complete the listed fields to create your policy. First provide a name and description that explain the business context for the policy. You can't edit the name of the policy once it's created. While all other fields can be adjusted later, you will need to create a new policy if you wish to change the name.
2. Then select the query that triggers the policy; any assets that match the query parameters are automatically updated with the designated action. For instance, you may want to label all expiring entities (e.g. domains, SSL certificates) with a "needs renewal" label. You can create a saved query that searches for metadata that expires within 30 days or is already expired. You can then designate that the system applies a "needs renewal" label to all applicable assets. You can either select to power the policy with a previously saved filter, or you can create a new query. All saved queries are visible within the dropdown, or select Create new saved query to configure new filter parameters. If you would like to view the assets that match your query before setting up a policy, it is recommended that you first create a saved query from the Inventory page.
3. Once all fields are configured, select Add to create your policy.

Newly created policies can take up to one week to apply changes to your inventory. Once the changes are implemented, you see them reflected in the Change history tab. You can also see the impacted assets when using the **Policy name** filter on your inventory, and the **Policies** page lists an accurate count of impacted assets. Preexisting policies update any newly applicable assets within five to seven days of the last run.

## Edit or delete policies

You can edit policies individually or delete one or more policies simultaneously.

### Edit policies

To edit a policy, click on the policy name from the list view. This opens a right-hand pane that enables you to edit the policy configuration. Users can't edit the name of their policy, but all other fields are adjustable. Once you make your intended changes, select Update to save the policy.

### Delete policies

You can delete policies individually or in bulk. From the main Policies page, select the polic(ies) that you’d like to delete by selecting the checkbox next to the policy name. Select **Remove policy** and confirm the removal. Deleting a policy won't revert any previously implemented actions, but it stops the automated actions from taking place in the future. If you need to make one-time changes to the assets impacted by the policy, you can leverage the same saved query underlying the policy from the Inventory page to revert the changes.