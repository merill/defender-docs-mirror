---
layout: Conceptual
title: Create and manage OAuth app policies with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-app-policies-create
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: anandd512
manager: bagol
ms.author: andeshpande
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
ms.date: 2026-09-28T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: shragar
description: Learn how to create app governance policies for OAuth apps in Microsoft 365, Google Workspace, and Salesforce to detect risk and take action.
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d1ff15d1-1aeb-9cc2-dbc7-87a8b6d2e866
document_version_independent_id: d1ff15d1-1aeb-9cc2-dbc7-87a8b6d2e866
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-app-policies-create.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-app-policies-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-app-policies-create.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 120258a6-fd12-b417-f49b-d5ea324f9aad
---

# Create and manage OAuth app policies with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

App governance uses machine learning algorithms to detect anomalous app behavior and generate alerts. You can also create policies that enable you to:

- Specify conditions by which app governance alerts you to app behavior for automatic or manual remediation.
- Enforce the app compliance policies for your organization.

This article shows you how to create and configure OAuth app policies in app governance for apps connected to Microsoft 365, Google Workspace, and Salesforce, including using templates, creating custom policies, and working with anomaly detection policies.

## Create OAuth app policies for Microsoft Entra ID

For apps connected to Microsoft Entra ID, create app policies from provided templates that can be customized, or create your own custom app policy.

1. To create a new app policy for Microsoft 365 apps, go to **Microsoft Defender XDR** &gt; **App governance** &gt; **Policies** &gt; **Microsoft 365**.

    For example:

    ![Screenshot of the Microsoft 365 tab.](media/app-governance-app-policies-create/microsoft-365-policies.png)
2. Select the **Create New Policy** option, and then do one of the following steps:

    - To create a new app policy from a template, choose the relevant template category followed by the template in that category.
    - To create a custom policy, select the **Custom** category.

    For example:

    [![Screenshot showing the 'Choose a policy template' interface.](media/app-governance/app-governance-create-policy.png)](media/app-governance/app-governance-create-policy.png#lightbox)

## App policy templates

To create a new app policy based on an app policy template, on the **Choose App policy template page**, select a category of app template, select the name of the template, and then select **Next**.

App policy templates are grouped into these categories: Usage, Permissions, Risk management, and Certification.

### Usage-based app policy templates

The following table lists the app governance templates supported to generate alerts for app usage.

| Template name | Description |
| --- | --- |
| **Unused app** | Find apps that have not authenticated recently. This policy checks the following conditions: <br>- Last used: More than 90 days (customizable) |
| **New app with high data usage** | Find newly registered apps that have uploaded or downloaded large amounts of data using Microsoft Graph and EWS APIs. This policy checks the following conditions: <br>- Registration age: Seven days or less (customizable)<br>- Data usage: Greater than 1 GB in one day (customizable) |
| **Increase in users** | Find apps with a sizable increase in the number of users. This policy checks the following conditions: <br>- Time range: Last 90 days<br>- Increase in consenting users: At least 50% (customizable) |

### Permission-based app policy templates

The following table lists the app governance templates supported to generate alerts for app permissions.

| Template name | Description |
| --- | --- |
| **Overprivileged app** | Find apps that have unused Microsoft Graph API permissions. These apps have been granted permissions that could be unnecessary for regular use. |
| **New highly privileged app** | Find newly registered apps that have been granted write access and other powerful permissions to Microsoft Graph and other common Microsoft first-party APIs. This policy checks the following conditions: <br>- Registration age: Seven days or less (customizable) |
| **New app with non-Graph API permissions** | Find newly registered apps that have permissions to non-Graph APIs. These apps can expose you to risks if the APIs they access receive limited support and updates.  This policy checks the following conditions: <br>- Registration age: Seven days or less (customizable)<br>- Non-Graph API permissions: Yes |

### Risk management based app policy templates

The following table lists the app governance templates supported to generate alerts based on app risk.

| Template name | Description |
| --- | --- |
| **New high risk app** | Find newly registered apps that have a high risk. This policy checks the following conditions: <br>- Registration age: Seven days or less (customizable)<br>- Risk score: Greater than 70 (customizable) |

### Certification-based app policy templates

The following table lists the app governance templates supported to generate alerts for Microsoft 365 certification.

| Template name | Description |
| --- | --- |
| **New uncertified app** | Find newly registered apps that don't have publisher attestation or Microsoft 365 certification. This policy checks the following conditions: <br>- Registration age: Seven days or less (customizable)<br>- Certification: No certification (customizable) |

## Create custom OAuth app policies

Use a custom app policy when you need to do something not already done by one of the built-in templates.

1. To create a new custom app policy, first select **Create new policy** on the **Policies** page. On the **Choose App policy template page**, select the **Custom** category, the **Custom policy** template, and then select **Next**.
2. On the **Name and description** page, configure the following settings:

    - Policy Name
    - Policy Description
    - Select the policy severity, which sets the severity of alerts generated by this policy.
        - High
        - Medium
        - Low
3. On the **Choose Policy settings and conditions** page, for **Choose which apps this policy is applicable for**, select:

    - All Apps
    - Choose specific apps
    - All apps except
4. If you choose specific apps, or all apps except for this policy, select **Add apps** and select the desired apps from the list. In the **Choose apps** pane, you can select multiple apps to which this policy applies, and then select **Add**. Select **Next** when you're satisfied with the list.
5. Select **Edit conditions** &gt; **Add condition** and choose a condition from the list. Set the desired threshold for your selected condition. Repeat to add more conditions.
6. Select **Save** to save the rule, and when you're finished adding rules, select **Next**.

    Note

    Some policy conditions are only applicable to apps that access Graph API permissions. When evaluating apps that access only non-Graph APIs, app governance skips these policy conditions and proceeds to check only other policy conditions.
7. Here are the available conditions for a custom app policy:

    | Condition | Condition values accepted | Description | More information |
    | --- | --- | --- | --- |
    | **Registration age** | Within last X days | Apps that were registered to Microsoft Entra ID within a specified period from the current date |  |
    | **Risk score** | Greater than X | Apps with a risk score greater than the specified value |  |
    | **Certification** | No certification, Publisher attested, Microsoft 365 Certified | Apps that are Microsoft 365 Certified, have a publisher attestation report, or neither | [Microsoft 365 Certification framework overview](/en-us/microsoft-365-app-certification/docs/certification) |
    | **Publisher verified** | Yes or No | Apps that have verified publishers | [Publisher Verification](/en-us/entra/identity-platform/publisher-verification-overview) |
    | **Application permissions** (Graph only) | Select one or more API permissions from list | Apps with specific Graph API permissions that have been granted directly | [Microsoft Graph permissions reference](/en-us/graph/permissions-reference) |
    | **Delegated permissions** (Graph only) | Select one or more API permissions from list | Apps with specific Graph API permissions given by a user | [Microsoft Graph permissions reference](/en-us/graph/permissions-reference) |
    | **Highly privileged** | Yes or No | Apps with powerful permissions to Microsoft Graph and other common Microsoft first-party APIs, or with high-privilege Microsoft Entra roles | An internal designation based on the same logic used by Defender for Cloud Apps. |
    | **Overprivileged** (Graph only) | Yes or No | Apps with unused Graph API permissions | Apps with more granted permissions than are being used by those apps. |
    | **Non-Graph API permissions** | Yes or No | Apps with permissions to non-Graph APIs. These apps can expose you to risks if the APIs they access receive limited support and updates. |  |
    | **Data usage** | Greater than X GB of data downloaded and uploaded per day | Apps that have read and written more than a specified amount of data using Microsoft Graph and EWS APIs |  |
    | **Data usage trend** | X % increase in data usage compared to previous day | Apps whose data reads and writes using Microsoft Graph and EWS APIs have increased by a specified percentage compared to the previous day |  |
    | **API access** (Graph only) | Greater than X API calls per day | Apps that have made over a specified number of Graph API calls in a day |  |
    | **API access trend** (Graph only) | X % increase in API calls compared to previous day | Apps whose number of Graph API calls have increased by a specified percentage compared to the previous day |  |
    | **Number of consenting users** | (Greater than or Less than) X consented users | Apps that have been given consent by a greater or fewer number of users than specified |  |
    | **Increase in consenting users** | X % increase in users in the last 90 days | Apps whose number of consenting users have increased by over a specified percentage in the last 90 days |  |
    | **Priority account consent given** | Yes or No | Apps that have been given consent by priority users | A user with a [priority account](/en-us/microsoft-365/admin/setup/priority-accounts). |
    | **Names of consenting users** | Select users from list | Apps that have been given consent by specific users |  |
    | **Roles of consenting users** | Select roles from list | Apps that have been given consent by users with specific roles | Multiple selections allowed.  Any Microsoft Entra role with assigned member should be made available in this list. |
    | **Sensitivity labels accessed** | Select one or more sensitivity labels from the list | Apps that accessed data with specific sensitivity labels in the last 30 days. |  |
    | **Services accessed** (Graph only) | Exchange and/or OneDrive and/or SharePoint and/or Teams | Apps that have accessed OneDrive, SharePoint, or Exchange Online using Microsoft Graph and EWS APIs | Multiple selections allowed. |
    | **Error rate** (Graph only) | Error rate is greater than X% in the last seven days | Apps whose Graph API error rates in the last seven days are greater than a specified percentage |  |
    | **Last used** | Within last X days | Apps that have not authenticated within a specified period from the current date |  |
    | **App origin** | External or Internal | Apps that originated within the tenant or registered in an external tenant |  |

    All of the specified conditions must be met for this app policy to generate an alert.
8. When you're done specifying the conditions, select **Save**, and then select **Next**.
9. On the **Define Policy Actions** page, select **Disable app** if you want app governance to disable the app when an alert based on this policy is generated, and then select **Next**. Use caution when applying actions because a policy may affect users and legitimate app use.
10. On the **Define Policy Status** page, select one of these options:

    - **Active**: Policies are evaluated and configured actions will occur.
    - **Inactive**: Policies aren't evaluated and configured actions won't occur.
11. Carefully review all parameters of your custom policy. Select **Submit** when you're satisfied. You can also go back and change settings by selecting **Edit** beneath any of the settings.

## Monitor your new app policy

After you create an app policy, monitor it on the **Policies** page to confirm that it generates the expected number of active and total alerts.

[![Screenshot of the app governance policies summary page in Microsoft Defender XDR, with a highlighted policy.](media/app-governance/mapg-cc-policies-policy.png)](media/app-governance/mapg-cc-policies-policy.png#lightbox)

If the number of alerts is unexpectedly low, review and update the app policy settings.

## Create a new policy for OAuth apps connected to Salesforce and Google Workspace

Policies for OAuth apps trigger alerts only on policies that are authorized by users in the tenant.

**To create a new app policy for Salesforce, Google and other apps**:

1. In Microsoft Defender XDR, go to **Cloud Apps** &gt; **App governance** &gt; **Policies** &gt; **Other apps**. For example:

    ![Screenshot of the Other apps policy creation page in App Governance](media/app-governance-app-policies-create/other-apps-policy-creation.jpg)
2. Filter the apps according to your needs. For example, you might want to view all apps that request **Permission** to **Modify calendars in your mailbox**.

    Tip

    Use the **Community use** filter to get information on whether allowing permission to a selected app is common, uncommon, or rare. The **Community use** filter can be helpful if you have an app that's rare and requests permission that has a high severity level or requests permission from many users.
3. You might want to set the policy based on the group memberships of the users who authorized the apps. For example, an admin can decide to set a policy that revokes uncommon apps if they ask for high permissions, only if the user who authorized the permissions is a member of the Administrators group.

    For example:

    ![Screenshot of the new OAuth app policy configuration page with group-based permission settings](media/app-permissions-policy.png)

### Anomaly detection policies for OAuth apps connected to Salesforce and Google Workspace

In addition to Oauth app policies that you can create, Microsoft Defender for Cloud Apps provides out-of-the-box anomaly detection policies that profile metadata of OAuth apps to identify ones that are potentially malicious. Defender for Cloud Apps is the Microsoft security service that helps protect your organization's cloud app environment, including OAuth apps connected to Salesforce and Google Workspace.

The out-of-the-box anomaly detection policies are only relevant for Salesforce and Google Workspace applications.

Note

Anomaly detection policies are only available for OAuth apps that are authorized in your Microsoft Entra ID. The severity of OAuth app anomaly detection policies can't be modified.

The following table describes the out-of-the-box anomaly detection policies provided by Defender for Cloud Apps:

| Policy | Description |
| --- | --- |
| **Misleading OAuth app name** | Scans OAuth apps connected to your environment and triggers an alert when an app with a misleading name is detected. Misleading names, such as foreign letters that resemble Latin letters, could indicate an attempt to disguise a malicious app as a known and trusted app. |
| **Misleading publisher name for an OAuth app** | Scans OAuth apps connected to your environment and triggers an alert when an app with a misleading publisher name is detected. Misleading publisher names, such as foreign letters that resemble Latin letters, could indicate an attempt to disguise a malicious app as an app coming from a known and trusted publisher. |
| **Malicious OAuth app consent** | Scans OAuth apps connected to your environment and triggers an alert when a potentially malicious app is authorized. Malicious OAuth apps might be used as part of a phishing campaign in an attempt to compromise users. This detection uses Microsoft security research and threat intelligence expertise to identify malicious apps. |
| **Suspicious OAuth app file download activities** | For more information, see [Anomaly detection policies](/en-us/defender-cloud-apps/anomaly-detection-policy). |

## Manage app policies

Use app governance to manage OAuth policies for Microsoft 365, Google Workspace, and Salesforce.

You might need to manage your app policies as follows to keep up-to-date with your organization's apps, respond to new app-based attacks, and for ongoing changes to your app compliance needs:

- Create new policies targeted at new apps
- Change the status of an existing policy (active or disable)
- Change the conditions of an existing policy
- Change the actions of an existing policy for auto-remediation of alerts

### Edit an app policy configuration

To change the configuration of a user-defined app policy:

1. Select the policy in the policy list, and then select **Edit** on the app policy pane.
2. In the **Edit policy** page, you can make the following changes:

    - **Description**: Change the description to make it easier to understand the policy's purpose.
    - **Severity**: Change the severity for your app policy to low, medium, or high.
    - **Policy settings**: Change the set of apps to which the policy applies. You can also choose to use the existing conditions or modify the conditions.
    - **Actions**: Change the autoremediation action for alerts generated by the policy.
    - **Status**: Change the policy status.

[![Screenshot of the Edit policy pane for a user-defined app policy in App Governance.](media/app-governance-app-policies-manage/edit-user-defined-policy.png)](media/app-governance-app-policies-manage/edit-user-defined-policy.png#lightbox)

### Delete an app policy

To delete an app policy, you can:

- Select the policy in the policy list, and then select **Delete** on the app policy pane.

An alternative to deleting an app policy is to change the app policy status to disabled. Once disabled, the policy doesn't generate alerts. For example, rather than deleting an app policy for an app with a specific set of conditions that are useful for a future policy, rename the app policy to indicate its usefulness and set its status to disabled.

### Edit an existing user-defined policy

Follow these steps to edit an existing user-defined policy:

1. On the **App governance** page, select the **Policies** tab and select the policy you want to edit. A panel opens on the right side with the details of the existing policy.
2. Select **Edit**.

    While you can't change the name of the policy once created, you can change the description and policy severity as needed. When you're done, select **Next**.
3. Choose whether you want to continue with the existing policy settings or customize them. Select **No, I'll customize the policy** to make changes, and then select **Next**.
4. Choose whether this policy applies to all apps, specific apps, or all apps except the apps you select.
5. Select **Choose apps** to select which apps to apply the policy to, and then select **Next**.
6. Choose whether to modify the existing conditions of the policy.

    - If you choose to modify the conditions, select **Edit or modify existing conditions for the policy** and choose which policy conditions to apply.
    - Otherwise, select **Use existing conditions of the policy**.
7. When you're done, select **Next**.
8. Choose whether to disable the app if it triggers the policy conditions and then select **Next**.
9. Set the policy status to **Active**, or **Disabled**, as needed, and then select **Next**.
10. Review your setting choices for the policy and if everything is the way you want it, select **Submit**.