---
layout: Conceptual
title: Login pages in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/attack-simulation-training-login-pages
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Admins can learn how to create and manage login pages for simulated phishing attacks in Microsoft Defender for Office 365 Plan 2.
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 436cdd41-dee2-aa66-f800-fa0402e75bec
document_version_independent_id: 436cdd41-dee2-aa66-f800-fa0402e75bec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/attack-simulation-training-login-pages.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-simulation-training-login-pages
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/attack-simulation-training-login-pages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: dd8bf929-40ea-7aa1-909b-0e9a5c2ce4f9
---

# Login pages in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn

In Attack simulation training in Microsoft 365 E5 or Microsoft Defender for Office 365 Plan 2, login pages are shown to users in simulations that use **Credential Harvest** and **Link in Attachment**[social engineering techniques](attack-simulation-training-simulations#select-a-social-engineering-technique).

For getting started information about Attack simulation training, see [Get started using Attack simulation training](attack-simulation-training-get-started).

To see the available login pages, open the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; and then select **Login pages**. To go directly to the **Content library** tab where you can select **Login pages**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.

**Login pages** in the **Content library** tab has two tabs:

- **Global login pages** tab: Contains the built-in, unmodifiable login pages. There are four built-in login pages localized into 12+ languages:

    - **GitHub login page**
    - **LinkedIn login page**
    - **Microsoft login page**
    - **Non-branded login page**
- **Tenant login pages** tab: Contains the custom login pages that you created.

The following information is shown for each login page. You can sort the login pages by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Name**
- **⋮** (**Actions** control): Take action on the login page. The available actions depend on the **Status** value of the login page as described in Create login pages, Modify login pages, Copy login pages, and Remove login pages.
- **Language**
- **Source**: For built-in login pages, the value is **Global**. For custom login pages, the value is **Tenant**.
- **Status**: **Ready** or **Draft**.
- **Created by**: For built-in login pages, the value is **Microsoft**. For custom login pages, the value is the UPN of the user who created the login page.
- **Last modified**

To find a login page in the list, type part of the login page name in the ![](media/defender-portal-icon-search.png)**Search** box and then press the ENTER key.

Select ![](media/defender-portal-icon-filter.png)**Filter** to filter the login pages by **Language** or **Status**.

When you select a login page from the list by clicking anywhere in the row other than the check box next to the name, a details flyout appears with the following information:

- ![](media/defender-portal-icon-edit.png)**Edit** is available only in custom login pages on the **Tenant login pages** tab.
- ![](media/defender-portal-icon-set-as-default.png)**Mark as default** to make this login page the default selection in **Credential Harvest** or **Link in Attachment**[payloads](attack-simulation-training-payloads) or [payload automations](attack-simulation-training-payload-automations). If the login page is already the default, ![](media/defender-portal-icon-set-as-default.png)**Mark as default** isn't available.
- **Preview** tab: View the login page as users see it. **Page 1** and **Page 2** links are available at the bottom of the page for two-page login pages.
- **Details**tab: View details about the login page:
    - **Description**
    - **Status**: **Ready** or **Draft**.
    - **Login page source**: For built-in login pages, the value is **Global**. For custom login pages, the value is **Tenant**.
    - **Modified by**
    - **Language**
    - **Last modified**

Tip

To see details about other login pages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

## Create login pages

To create a custom login page, follow these steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; and then select **Login pages**. To go directly to the **Content library** tab where you can select **Login pages**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.
2. On the **Tenant login pages** tab, select ![](media/defender-portal-icon-create.png)**Create new** to start the new login page wizard.

    Note

    At any point after you name the login page during the new login page wizard, you can select **Save and close** to save your progress and continue later. The incomplete login page has the **Status** value **Draft**. You can pick up where you left off by selecting the login page from the list and then clicking the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.

    You can also create login pages during the creation of simulations or simulation automations. For more information, see [Create a simulation: Select a payload and login page](attack-simulation-training-simulations#select-a-payload-and-login-page) and [Create a simulation automation: Select payloads and login pages](attack-simulation-training-simulation-automations#select-payloads-and-login-pages).
3. On the **Define details for login page** page, configure the following settings:

    - **Name**: Enter a unique name.
    - **Description**: Enter an optional description.

    When you're finished on the **Define details for login page** page, select **Next**.
4. On the **Configure login page** page, configure the following settings:

    - **Select a language**: The available values are: **Chinese (Simplified)**, **Chinese (Traditional)**, **English**, **French**, **German**, **Italian**, **Japanese**, **Korean**, **Portuguese**, **Russian**, **Spanish**, **Dutch**, and **Other**.
    - **Make this the default login page**: If you select this option, the login page is the default selection in **Credential Harvest** or **Link in Attachment**[payloads](attack-simulation-training-payloads) or [payload automations](attack-simulation-training-payload-automations).
    - **Create a two-page login**: If you don't select this option, the login page is one page. If you select this option, **Page 1** and **Page 2** tabs appear for you to configure separately.
    - Login page content area: Two tabs are available:

        - **Text** tab: A rich text editor is available to create the login page. To see the typical font and formatting settings, toggle **Formatting controls** to ![](media/scc-toggle-on.png)**On**.

            The following controls are also available on the **Text** tab:

            - **Dynamic tag**: Select from the following tags:

                | Tag name | Tag value |
                | --- | --- |
                | **Insert User name** | `${userName}` |
                | **Insert First name** | `${firstName}` |
                | **Insert Last name** | `${lastName}` |
                | **Insert UPN** | `${upn}` |
                | **Insert Email** | `${emailAddress}` |
                | **Insert Department** | `${department}` |
                | **Insert Manager** | `${manager}` |
                | **Insert Mobile phone** | `${mobilePhone}` |
                | **Insert City** | `${city}` |
                | **Insert Date** | `${date|MM/dd/yyyy|offset}` |
            - **Use from default**: Select an available template to start with. You can modify the text and layout in the editing area. To reset the login page back to the default text and layout of the template, select **Reset to default**.
            - **Add compromise button**: Available on one-page logins or on **Page 2** of two-page logins. Select this link to add the compromise button to the login page. The default text on the button is **Submit**, but you can change it.
            - **Add Next button**: Available only on **Page 1** of two-page logins. Select this link to add the 'Next' button to the login page. The default text on the button is **Next**, but you can change it.

            Tip

            To add images, copy (CTRL+C) and paste (CTRL+V) the image into the editor on the **Text** tab. The editor automatically converts the image to Base64 as part of the HTML code.
        - **Code** tab: You can view and modify the HTML code directly.

            Tip

            To avoid sending passwords in plain text from custom login pages, avoid using the variable **name** in HTML code. Instead, use **type**, **id**, or **class**. For example:

            ```html
            <input id="input-field-loginPage" type="password" placeholder="Password">
            ```

    You can preview the results by clicking the **Preview login page** button at the top of the page.

    When you're finished on the **Configure login page** page, select **Next**.
5. On the **Review login page** page, you can review the details of your login page.

    You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review login page** page, select **Submit**.
6. On the **New login page &lt;Name&gt; created** page, you can use the links to create a new login page, launch a simulation, or view all login pages.

    When you're finished on the **New login page &lt;Name&gt; created** page, select **Done**.
7. Back on the **Tenant login pages** tab in **Login pages**, the login page that you created is now listed.

## Modify login pages

You can't modify built-in login pages on the **Global login pages** tab. You can only modify custom login pages on the **Tenant login pages** tab.

To modify an existing custom login page on the **Tenant login pages** tab, do one of the following steps:

- Select the login page from the list by clicking the check box next to the name. Select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the login page, and then select ![](media/defender-portal-icon-edit.png)**Edit**.
- Select the login page from the list by clicking anywhere in the row other than the check box next to the name. In the details flyout that opens, select ![](media/defender-portal-icon-edit.png)**Edit**.

The login page wizard opens with the settings and values of the selected login page. To modify the login page, follow the same wizard steps described in Create login pages.

## Copy login pages

To copy an existing login page on the **Tenant login pages** or **Global login pages** tabs, do one of the following steps:

- Select the login page from the list by clicking the check box next to the name, and then select the ![](media/defender-portal-icon-edit.png)**Create a copy** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the login page, and then select ![](media/defender-portal-icon-edit.png)**Create a copy**.

The login page wizard opens with the settings and values of the selected login page. To copy the login page, follow the same wizard steps described in Create login pages.

Note

When you copy a built-in login page on the **Global login pages** tab, be sure to change the **Name** value. This step ensures the copy is saved as a custom login page on the **Tenant login pages** tab.

The **Use from default** control on the **Configure login page** page in the login page wizard allows you to copy the contents of a built-in login page.

When you're creating or editing a login page, the **Use from default** control on the **Text** tab of the **Configure login page** step in the login page wizard also allows you to copy the contents of a built-in login page.

## Remove login pages

You can't remove built-in login pages from the **Global login pages** tab. You can only remove custom login pages from the **Tenant login pages** tab.

To remove an existing custom login page from the **Tenant login pages** tab, do one of the following steps:

- Select the login page from the list by clicking the check box next to the name, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the login page, and then select ![](media/defender-portal-icon-delete.png)**Delete**.

## Make a login page the default

The default login page is the default selection that's used in **Credential Harvest** or **Link in Attachment**[payloads](attack-simulation-training-payloads) or [payload automations](attack-simulation-training-payload-automations).

To make a login page the default on the **Tenant login pages** or **Global login pages** tabs, do one of the following steps:

- Select **⋮** (**Actions**) next to the **Name** value of the login page, and then select ![](media/defender-portal-icon-set-as-default.png)**Mark as default**.
- Select the login page from the list by clicking anywhere in the row other than the check box next to the name. In the details flyout that opens, select ![](media/defender-portal-icon-set-as-default.png)**Mark as default**.
- Select **Make this the default login page** on the **Configure login page** page in the wizard when you create a login page or modify a login page.

Note

The options for setting a default login page that are described in this section aren't available if the login page is already the default.

The default login page is also marked in the list, although you might need to widen the **Name** column to see it:

[![The default login page marked in the list of login pages in Attack simulation training.](media/attack-sim-training-login-pages-default.png)](media/attack-sim-training-login-pages-default.png#lightbox)