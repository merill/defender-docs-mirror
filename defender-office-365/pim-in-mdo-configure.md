---
layout: Conceptual
title: Configure Azure PIM for Microsoft Defender for Office 365 admin access - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/pim-in-mdo-configure
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.localizationpriority: high
ms.assetid: 56fee1c7-dc37-470e-9b09-33fff6d94617
ms.collection:
- m365-security
- tier1
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-image-nochange
description: Learn to integrate Azure PIM in order to grant just-in-time, time limited access to users to do elevated privilege tasks in Microsoft Defender for Office 365, lowering risk to your data.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: 7ecfa8ea-6aae-530c-d4b7-9e37dae0f0ec
document_version_independent_id: 7ecfa8ea-6aae-530c-d4b7-9e37dae0f0ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/pim-in-mdo-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: pim-in-mdo-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/pim-in-mdo-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 9f8e8209-c7f5-44b3-fe82-5839fa6f9dc2
---

# Configure Azure PIM for Microsoft Defender for Office 365 admin access - Microsoft Defender for Office 365 | Microsoft Learn

Privileged Identity Management (PIM) is an Azure feature that gives users access to data for a limited period of time (sometimes called a *time-boxed* period of time). Access is given 'just-in-time' to take the required action, and then access is removed. PIM limits user access to sensitive data, which reduces risk as compared to traditional admin accounts with permanent access to data and other settings. So, how can we use this feature (PIM) with Microsoft Defender for Office 365?

Tip

PIM access is scoped to the role and identity level to allow the completion of multiple tasks. In contrast, Privileged Access Management (PAM) is scoped at the task level.

## Steps to use PIM to grant just-in-time access to Defender for Office 365 related tasks

By setting up PIM to work with Microsoft Defender for Office 365, admins create a process for a user to *request and justify* the elevated privileges that they need.

This article uses the scenario for a user named Alex on the security team. We can elevate Alex's permissions for the following scenarios:

- Permissions for normal day-to-day operations (for example, [Threat Hunting](threat-explorer-threat-hunting)).
- A temporary higher-level of privilege for less frequent, sensitive operations (for example, [remediating malicious delivered email](remediate-malicious-email-delivered-office-365)).

Tip

Although this article includes specific steps for Alex on the security team, you can do the same steps for other permissions. For example, when an information worker requires day-to-day access in eDiscovery to perform searches and case work, but occasionally needs the elevated permissions to export data from the organization.

***Step 1***. In the Azure PIM console for your subscription, add the user (Alex) to the Azure Security Reader role and configure the security settings related to activation.

1. Sign in to the [Microsoft Entra Admin Center](https://aad.portal.azure.com/) and select **Microsoft Entra ID** &gt; **Roles and administrators**.
2. Select **Security Reader** in the list of roles and then **Settings** &gt; **Edit**
3. Set the '**Activation maximum duration (hours)**' to a normal working day and 'On activation' to require **Azure MFA**.
4. Because this is Alex's normal privilege level for day-to-day operations, Uncheck **Require justification on activation** &gt; **Update**.
5. Select **Add Assignments** &gt; **No member selected** &gt; select or type the name to search for the correct member.
6. Select the **Select** button to choose the member you need to add for PIM privileges &gt; select **Next** &gt; make no changes on the Add Assignment page (both assignment type *Eligible* and duration *Permanently Eligible* are defaults) and **Assign**.

The name of the user (Alex in this scenario) appears under Eligible assignments on the next page. The user's appearance under Eligible assignments means they can activate the role in PIM using the activation settings you configured for the Security Reader role.

Note

For a quick review of Privileged Identity Management see [Privileged Identity Management overview](https://www.youtube.com/watch?v=VQMAg0sa_lE).

[![The Role setting details - Security Reader page](media/pim-mdo-role-setting-details-for-security-reader-show-8-hr-duration.png)](media/pim-mdo-role-setting-details-for-security-reader-show-8-hr-duration.png#lightbox)

***Step 2***. Create the required second (elevated) permission group for other tasks and assign eligibility.

Using [Privileged Access groups](/en-us/entra/id-governance/privileged-identity-management/concept-pim-for-groups) we can now create our own custom groups and combine permissions or increase granularity where required to meet your organizational practices and needs.

### Create a role or role group with the required permissions

Use one of the following methods:

- [Create an Email & collaboration role group in the Microsoft Defender portal](mdo-portal-permissions#create-email--collaboration-role-groups-in-the-microsoft-defender-portal):

Or

- Create a custom role in Microsoft Defender unified role based access control (RBAC). For information and instructions, see [Start using Microsoft Defender unified RBAC model](/en-us/defender-xdr/manage-rbac#start-using-microsoft-defender-unified-rbac-model). For Defender for Office 365-specific role templates and configuration steps, see [How to configure Unified RBAC for Defender for Office 365](step-by-step-guides/configure-unified-rbac-defender-office-365).

For either method:

- Use a descriptive name (for example, 'Contoso Search and Purge PIM').
- Don't add members. Add the required permissions, save, and then go to the next step.

### Create the security group in Microsoft Entra ID for elevated permissions

Create a Microsoft Entra security group to hold the elevated permissions and enable PIM for the group.

1. Browse back to the [Microsoft Entra Admin Center](https://aad.portal.azure.com/) and navigate to **Microsoft Entra ID** &gt; **Groups** &gt; **New Group**.
2. Name your Microsoft Entra group to reflect its purpose, **no owners or members are required** right now.
3. Turn **Microsoft Entra roles can be assigned to the group** to **Yes**.
4. Don't add any roles, members, or owners, create the group.
5. Go back into the group you created, and select **Privileged Identity Management** &gt; **Enable PIM**.
6. Within the group, select **Eligible assignments** &gt; **Add assignments** &gt; Add the user who needs Search & Purge as a role of **Member**.
7. Configure the **Settings** within the group's Privileged Access pane. Choose to **Edit** the settings for the role of **Member**.
8. Change the activation time to suit your organization. This example requires *Microsoft Entra multifactor authentication*, *justification*, and *ticket information* before selecting **Update**.

### Nest the newly created security group into the role group

Note

Nesting the security group into the role group is required only if you used an Email & collaboration role group in Create a role or role group with the required permissions. Defender unified RBAC supports direct permissions assignments to Microsoft Entra groups, and you can add members to the group for PIM.

1. [Connect to Security & Compliance PowerShell](/en-us/powershell/exchange/connect-to-scc-powershell) and run the following command to add the Azure security group as a member of the role group, which grants the group's members the permissions assigned to that role group:

    ```powershell
    Add-RoleGroupMember "<Role Group Name>" -Member "<Azure Security Group>"`
    ```

## Test your configuration of PIM with Defender for Office 365

Use the following steps to verify that the PIM configuration grants the expected day-to-day and elevated access.

1. Sign in with the test user (Alex), who should have no administrative access within the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender) at this point.
2. In the Microsoft Entra Admin Center, open **Privileged Identity Management** and activate the day-to-day Security Reader role.
3. If you try to purge an email using Threat Explorer, you get an error stating you need more permissions.
4. Activate the elevated Search and Purge PIM group in Privileged Identity Management. After a short delay, you should be able to purge emails without issue.

    [![The Actions pane under the Email tab](media/pim-mdo-add-the-search-and-purge-role-assignment-to-this-pim-role.png)](media/pim-mdo-add-the-search-and-purge-role-assignment-to-this-pim-role.png#lightbox)

Permanent assignment of administrative roles and permissions doesn't align with the Zero Trust security initiative. Instead, you can use PIM to grant just-in-time access to the required tools.

*Our thanks to Customer Engineer Ben Harris for access to the blog post and resources used for this content.*