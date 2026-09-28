---
layout: Conceptual
title: Configure case templates in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-case-templates
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to configure custom fields, custom statuses, and SLA policies for supported case types in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 9800f63b-cde3-4d02-37fb-badeeae72858
document_version_independent_id: 9800f63b-cde3-4d02-37fb-badeeae72858
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-case-templates.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-case-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-case-templates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 47135183-9806-513b-b3b6-af2de3f8cb83
---

# Configure case templates in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Use case templates to configure case management settings for supported case types in the Microsoft Defender portal. Case templates help admins standardize custom fields, custom statuses, and SLA policies for their organization's SecOps workflows.

For an overview of Case Management, see [Case management in the Microsoft Defender portal](siem-defender-case-management).

## Configure custom fields

Use custom fields to capture organization-specific information on cases. Custom fields help analysts track the information your security operations center requires for triage, investigation, remediation, handoff, or reporting.

### Create a custom field

To create a custom field:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **Custom fields**.
6. Select **Create**.

    ![Screenshot showing the Create custom field pane with field name, type, required option, and default value settings.](media/manage-case-templates/create-custom-field.png)
7. In **Field name**, enter a name for the custom field.
8. In **Field description**, enter a description.
9. In **Field type**, select the field type.
10. Configure the field options.

    Note

    Available options can vary depending on the field type.
11. To require analysts to fill in the field, select **Field required**.
12. If needed, set a default value.
13. Select **Save**.

### Edit a custom field

To edit a custom field:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **Custom fields**.
6. Select the custom field you want to edit.
7. Select **Edit**.
8. Update the field settings.
9. Select **Save**.

### Disable a custom field

To disable a custom field:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **Custom fields**.
6. Select the custom field you want to disable.
7. Select **Disable**.

### Delete a custom field

To delete a custom field:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **Custom fields**.
6. Select the custom field you want to delete.
7. Select **Delete**.
8. Select **Confirm**.

## Configure custom statuses

Use custom statuses to add organization-specific statuses to the case lifecycle. Custom statuses are grouped under the **New**, **Open**, and **Closed** lifecycle categories.

Default statuses can't be deleted.

### Create a custom status

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incident**
    - **Generic**
5. Select **Custom statuses**.

    [![Screenshot showing custom case statuses grouped under the New, Open, and Closed lifecycle categories.](media/manage-case-templates/case-management-custom-statuses.png)](media/manage-case-templates/case-management-custom-statuses.png#lightbox)
6. Under the lifecycle category where you want to add the status, select **Add**.
7. Enter a name for the custom status.
8. Select the check mark to add the status.
9. Select **Save**.

### Edit a custom status

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Manage case templates**.
4. Select **Incident**.
5. Select **Custom statuses**.
6. Find the custom status you want to change.
7. Select **Edit**.
8. Update the status name.
9. Select the check mark.
10. Select **Save**.

### Reorder a custom status

You can change the order of custom statuses within their lifecycle category.

1. On the **Custom statuses** page, find the custom status you want to move.
2. Select **More options** (...).
3. Select **Move up** or **Move down**.
4. Select **Save**.

### Delete a custom status

1. On the **Custom statuses** page, find the custom status you want to delete.
2. Select **More options** (...).
3. Select **Delete**.
4. Select **Save**.

## Configure SLA policies

Use SLA policies to define and track response-time expectations for cases. SLA policies help teams monitor whether cases are handled within required timeframes and identify cases that are at risk or breached.

For more information about how SLA policies work, see [SLA policies for cases in the Microsoft Defender portal](case-sla-policies).

### Create an SLA policy

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **SLA management**.
6. Select **Create**.

    [![Screenshot showing the Policy name step in the Create SLA policy wizard.](media/manage-case-templates/sla-policy-name.png)](media/manage-case-templates/sla-policy-name.png#lightbox)
7. On the **Policy name** step, enter a policy name and description.
8. Select **Next**.
9. On the **Start & end criteria** step, define when the SLA timer starts and stops.

    [![Screenshot showing the Start and end criteria step in the Create SLA policy wizard.](media/manage-case-templates/sla-start-end-criteria.png)](media/manage-case-templates/sla-start-end-criteria.png#lightbox)
10. Select **Next**.
11. On the **Pause criteria** step, define when the SLA timer pauses.
12. Select **Next**.
13. On the **Timers** step, define the SLA time limits.

    [![Screenshot showing the Timers step for setting exceeded and at-risk SLA time limits.](media/manage-case-templates/sla-timers.png)](media/manage-case-templates/sla-timers.png#lightbox)
14. Set the time limit for when the SLA is exceeded.
15. If needed, set when the SLA is considered at risk.
16. Select **Next**.
17. On the **Recalculate** step, choose how the SLA timer responds when a case property used in timer conditions changes.

    - **Don't recalculate**: The timer continues running with the original time limit.
    - **Recalculate and carry on**: The timer switches to the new time limit and keeps the elapsed time.
    - **Recalculate and reset**: The timer switches to the new time limit and restarts from zero.
18. Select **Next**.
19. Review the policy settings.
20. Under **Applies to**, confirm the case type or case types that the SLA policy evaluates.
21. To start evaluating new cases immediately after creation, set the policy to **Active**.
22. Select **Create**.

### Edit an SLA policy

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **SLA management**.
6. Select the SLA policy you want to edit.
7. Select **Edit**.
8. Update the policy settings.
9. Select **Save**.

### Delete an SLA policy

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Case management settings**.
4. Select the case type you want to configure:

    - **Incidents**
    - **Generic**
5. Select **SLA management**.
6. Select the SLA policy you want to delete.
7. Select **Delete**.
8. Select **Confirm**.