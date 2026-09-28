---
layout: Conceptual
title: Landing pages in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/attack-simulation-training-landing-pages
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
description: Admins can learn how to create and manage landing pages for simulated phishing attacks in Microsoft Defender for Office 365 Plan 2.
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a78f8d20-ca83-c7b2-a050-e7aa8e70e330
document_version_independent_id: a78f8d20-ca83-c7b2-a050-e7aa8e70e330
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/attack-simulation-training-landing-pages.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-simulation-training-landing-pages
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/attack-simulation-training-landing-pages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: c783dbba-38e2-be57-d97c-39fb4aea1acc
---

# Landing pages in Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn

In Attack simulation training in Microsoft 365 E5 or Microsoft Defender for Office 365 Plan 2, landing pages are the web pages that users are taken to if they open the payload in the simulation.

For getting started information about Attack simulation training, see [Get started using Attack simulation training](attack-simulation-training-get-started).

To see the available landing pages, open the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; and then select **Phish landing pages**. To go directly to the **Content library** tab where you can select **Phish landing pages**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.

**Phish landing pages** in the **Content library** tab has two tabs:

- **Global landing pages** tab: Contains built-in, unmodifiable landing page templates named **Microsoft Landing Page Template 1** to **Microsoft Landing Page Template 5**. These built-in landing pages are localized into more than 12 languages.
- **Tenant landing pages** tab: Contains custom landing pages that you created.

The following information is shown for each landing page. You can sort the landing pages by clicking on an available column header. Select ![](media/defender-portal-icon-customize.png)**Customize columns** to change the columns that are shown. By default, all available columns are selected.

- **Name**
- **⋮** (**Actions** control): Take action on the landing page. The available actions depend on the **Status** value of the landing page as described in Modify landing pages and Remove landing pages.
- **Language**: One or more of the following values: **German**, **English**, **Spanish**, **French**, **Italian**, **Japanese**, **Korean**, **Dutch**, **Portuguese**, **Russian**, **Chinese (Simplified)**, and **Chinese (Traditional, Taiwan)**.
- **Default language**
- **Status**: **Ready** or **Draft**.
- **Linked simulations**
- **Created by**: For built-in landing pages, the value is **Microsoft**. For custom landing pages, the value is the user principal name (UPN) of the user who created the landing page.
- **Created time**
- **Modified by**

Tip

To see all columns, you likely need to do one or more of the following steps:

- Horizontally scroll in your web browser.
- Narrow the width of appropriate columns.
- Remove columns from the view.
- Zoom out in your web browser.

The **⋮** (**Actions** control) is associated with the **Notifications** column. If you remove that column from view, the **⋮** control goes away.

To find a landing page in the list, type part of the landing page name in the ![](media/defender-portal-icon-search.png)**Search** box and then press the ENTER key.

Select ![](media/defender-portal-icon-filter.png)**Filter** to filter the landing pages by **Language** or **Status**.

When you select a landing page from the list by clicking anywhere in the row other than the check box next to the name, a details flyout appears with the following information:

- **Preview** tab: View the landing page as users see it. Use the **Select language** dropdown list to see the landing page in different languages.
- **Details**tab: View details about the landing page:
    - **Description**
    - **Status**: **Ready** or **Draft**.
    - **Landing page source**: For built-in landing pages, the value is **Global**. For custom landing pages, the value is **Tenant**.
    - **Modified by**
    - **Language**
    - **Last modified**
    - **Created by**
    - **Created time**
    - **Linked simulations**
    - **Default language**

In custom landing pages only, an **Edit landing page** link is available at the bottom of both tabs.

Tip

To see details about other landing pages without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

## Create landing pages

To create a landing page in Attack simulation training, use the following steps:

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Attack simulation training** &gt; **Content library** tab &gt; and then select **Phish landing pages**. To go directly to the **Content library** tab where you can select **Phish landing pages**, use https://security.microsoft.com/attacksimulator?viewid=contentlibrary.
2. On the **Tenant landing pages** tab, select ![](media/defender-portal-icon-create.png)**Create new** to start the new landing page wizard.

    Note

    At any point after you name the landing page during the new landing page wizard, you can select **Save and close** to save your progress and continue later. The incomplete landing page has the **Status** value **Draft**. You can pick up where you left off by selecting the landing page from the list and then selecting the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.

    You can also create landing pages during the creation of simulations and simulation automations. For more information, see [Create a simulation: Select a landing page](attack-simulation-training-simulations#select-a-landing-page) and [Create a simulation automation: Select a landing page](attack-simulation-training-simulation-automations#select-a-landing-page).
3. On the **Define details for phish landing page** page, configure the following settings:

    - **Name**: Enter a unique, descriptive name for the landing page.
    - **Description**: Enter an optional description.

    When you're finished on the **Define details for phish landing page** page, select **Next**.
4. On the **Configure landing page** page, select **Define content in preferred language**. In the **Add content in default language** flyout that opens, configure the following settings:

    - **Select the language for the landing page**: Select one of the available languages: **Chinese (Simplified)**, **Chinese (Traditional, Taiwan)**, **Dutch**, **English**, **Spanish**, **French**, **German**, **Italian**, **Japanese**, **Korean**, **Portuguese**, **Russian**, **Swedish**, **Norwegian Bokmål**, **Polish**, **Finnish**, **Turkish**, **Hungarian**, **Hebrew**, **Thai**, **Arabic**, **Vietnamese**, **Slovak**, **Greek**, **Indonesian**, **Romanian**, **Slovenian**, **Croatian**, **Catalan**, or **Other**.
    - **Mark this as default language**: For the first landing page you create, this setting is selected and unchangeable.
    - Landing page content: Two tabs are available:
        - **Text** tab: A rich text editor is available to create the landing page. To see the typical font and formatting settings, toggle **Formatting controls** to ![](media/scc-toggle-on.png)**On**.

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
                | **Insert sender name** | `${FromName}` |
                | **Insert sender email** | `${FromEmail}` |
                | **Insert Payload subject** | `${EmailSubject}` |
                | **Insert Payload content** | `${EmailContent}` |
                | **Insert Date** | `${date|MM/dd/yyyy|offset}` |
            - **Import from library**: Select an available template to start with. You can modify the text and layout in the editing area. To reset the landing page back to the default text and layout of the template, select **Reset to default**.

            Tip

            To add images, copy (CTRL+C) and paste (CTRL+V) the image into the editor on the **Text** tab. The editor automatically converts the image to Base64 as part of the HTML code.
        - **Code** tab: You can view and modify the HTML code directly.

    You can preview the results by selecting **Preview phish landing page** at the top of the page.

    When you're finished on the **Add content in default language** flyout, select **Save**.

    Back on the **Configure landing page** page, the landing page you created is now listed. In the **Action** column, you can select ![](media/defender-portal-icon-edit.png)**Edit** or ![](media/defender-portal-icon-eye.png)**Preview** to edit or view the landing page.

    Select ![](media/defender-portal-icon-create.png)**Add translation** to create additional translations of the landing page in other languages.

    Other than the flyout title changing to **Add translation**, the same options are available as the **Add content in default language** flyout in the first landing page you created. Now the **Mark this as default language** check box is available to select. Only one translation of landing page can be the default language.

    When two or more translations of the landing page are listed on the **Configure landing page** page, the ![](media/defender-portal-icon-delete.png)**Delete** icon is available in the **Actions** column to delete any landing page translations that aren't designated as the default language.

    When you're finished on the **Configure landing page** page, select **Next**.
5. On the **Review landing page** page, you can review your selections. Select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review landing page** page, select **Submit**, and then select **Done** on the confirmation page.
6. Back on the **Tenant landing pages** tab of the **Select phish landing page**, select the landing page you created by selecting the check box next to the **Name**, and then select **Next**.

## Modify landing pages

You can't modify built-in landing pages on the **Global landing pages** tab. You can only modify custom landing pages on the **Tenant landing pages** tab.

To modify an existing custom landing page on the **Tenant landing pages** tab, do one of the following steps:

- Select the landing page from the list by selecting the check box next to the name. Select the ![](media/defender-portal-icon-edit.png)**Edit** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the landing page, and then select ![](media/defender-portal-icon-edit.png)**Edit**.
- Select the landing page from the list by clicking anywhere in the row other than the check box. In the details flyout that opens, select **Edit landing page** at the bottom of the flyout.

The landing page wizard opens with the settings and values of the selected landing page. The wizard uses the same steps as creating a landing page: define details, configure content and translations, review, and submit. For details, see Create landing pages.

## Copy landing pages

To copy an existing landing page on the **Tenant landing pages** or **Global landing pages** tabs, do one of the following steps:

- Select the landing page from the list by selecting the check box, and then select the ![](media/defender-portal-icon-edit.png)**Create a copy** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the landing page, and then select ![](media/defender-portal-icon-edit.png)**Create a copy**.

When you copy a custom landing page on the **Tenant landing pages** tab, a copy of the landing page named "&lt;OriginalName&gt; - Copy" is added to the list.

When you copy a built-in landing page on the **Global landing pages** tab, a **Create copy** dialog appears. The dialog confirms that a copy of the landing page has been created, and is available on the **Tenant landing pages** tab. If you select **Go to Tenant landing page**, you're taken to the **Tenant landing pages** tab, where the copied built-in landing page appears with the name "&lt;OriginalName&gt; - Copy." If you select **Stay here** in the dialog, you return to the **Global landing pages** tab.

After the copy is created, you can modify it as described in Modify landing pages.

Tip

When you're creating or editing a landing page, the **Use from default** control on the **Text** tab of the **Add content in default language** step in the landing page wizard also allows you to copy the contents of a built-in landing page.

## Remove landing pages

You can't remove built-in landing pages from the **Global landing pages** tab. You can only remove custom landing pages on the **Tenant landing pages** tab.

To remove an existing custom landing page from the **Tenant landing pages** tab, do one of the following steps:

Warning

When you delete a landing page, all translations of the landing page are also deleted.

- Select the landing page from the list by selecting the check box next to the name, and then select the ![](media/defender-portal-icon-delete.png)**Delete** action that appears.
- Select **⋮** (**Actions**) next to the **Name** value of the landing page, and then select ![](media/defender-portal-icon-delete.png)**Delete**.

In the confirmation dialog that opens, select **Delete**.