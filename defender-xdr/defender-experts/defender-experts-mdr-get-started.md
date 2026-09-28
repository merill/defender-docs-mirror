---
layout: Conceptual
title: Get started with Microsoft Defender Experts MDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-get-started
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Defender Experts MDR let you determine the individuals or groups within your organization that need to be notified if there's a critical incident
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-get-started
ms.topic: get-started
ms.custom:
- cx-ti
- cx-dex
- sfi-ga-nochange
ms.date: 2026-02-27T00:00:00.0000000Z
locale: en-us
document_id: d997f7b4-5ce8-1f96-7f93-3e8ecf490ce8
document_version_independent_id: d997f7b4-5ce8-1f96-7f93-3e8ecf490ce8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-get-started.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 5bcbd07d-5134-4454-e9b0-88a0db842444
---

# Get started with Microsoft Defender Experts MDR - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts MDR](defender-experts-mdr-overview)

For onboarding instructions, watch this short video:

When the Defender Experts team is ready to onboard your organization, you receive a welcome email to continue the setup and get started.

Select the link in the welcome email to directly launch the Defender Experts settings setup in the Microsoft Defender portal. You can also open this setup by going to **Settings** &gt; **Defender Experts** and selecting **Get started**.

[![Screenshot of the Get started page in Defender for Experts XDR settings step-by-step guide.](media/get-started-xdr/security-team-boost.png)](media/get-started-xdr/security-team-boost.png#lightbox)

## Grant permissions to our experts

By default, Defender Experts MDR requires **Service provider access** that lets our experts sign into your tenant and deliver services based on assigned security roles. [Learn more about cross-tenant access](/en-us/azure/active-directory/external-identities/cross-tenant-access-overview)

You also need to grant our experts one or both of the following permissions:

- **Investigate incidents and guide my responses** (default) – This option lets our experts proactively monitor and investigate incidents and guide you through any necessary response actions. (Access level: Security Reader)
- **Respond directly to active threats** (recommended) – This option lets our experts contain and remediate active threats immediately while investigating, thus reducing the threat's impact, and improving your overall response efficiency. (Access level: Security Operator)

[![Screenshot of manage exclusions option while setting up Defender Experts MDR.](media/get-started-xdr/managed-exclusions.png)](media/get-started-xdr/managed-exclusions.png#lightbox)

Important

If you skip providing additional permissions, our experts won't be able to take certain response actions to secure your organization.

Even though our experts are granted these relatively powerful permissions, they'll only have individual access to specific areas for a limited period. [Learn more about how Defender Experts MDR permissions work](defender-experts-mdr-permissions).

**To grant our experts permissions:**

1. In the same Defender Experts settings setup, under **Permissions**, choose one or more access levels you want to grant our experts.
2. If you want to exclude device and user groups in your organization from remediation actions, select **Manage exclusions**.
3. Select **Next** to add contact persons or groups.

To edit or update permissions after the initial setup, go to **Settings** &gt; **Defender Experts** &gt; **Permissions**.

## Exclude devices and users from remediation

Defender Experts MDR lets you exclude devices and users from remediation actions taken by our experts and instead get remediation guidance for those entities. These exclusions are based on identified [device groups](/en-us/defender-endpoint/machine-groups) in Microsoft Defender for Endpoint and identified [user groups](/en-us/entra/fundamentals/concept-learn-about-groups) in Microsoft Entra ID.

**To exclude device groups:**

1. In the same Defender Experts settings setup, under **Exclusions**, go to the **Device groups** tab.
2. Select **+ Add device groups**, then search for and choose one or more device groups that you want to exclude.

    Note

    This page only lists existing device groups. If you want to create a new device group, you need to go to the Defender for Endpoint settings in your Microsoft Defender portal. Then, refresh this page to search for and choose the newly created group. [Learn more about creating device groups](/en-us/defender-endpoint/machine-groups)
3. Select **Add device groups**.
4. Back on the **Device groups** tab, review the list of excluded device groups. If you want to remove a device group from the exclusion list, choose it then select **Remove device group**.
5. Select **Next** to confirm your exclusion list and proceed to adding contact persons or groups. Otherwise, select **Skip**, and all your added exclusions are discarded.

[![Screenshot of option to exclude device groups.](media/get-started-xdr/exclude-device-groups.png)](media/get-started-xdr/exclude-device-groups.png#lightbox)

**To exclude user groups:**

1. In the same Defender Experts settings setup, under **Exclusions**, go to the **User groups** tab.
2. Select **+ Add user groups**, then search for and choose one or more user groups that you want to exclude.

    Note

    This page only lists existing user groups. If you want to create a new user group, [learn more about creating user groups](/en-us/entra/fundamentals/groups-view-azure-portal)
3. Select **Add user groups**.
4. Back on the **User groups** tab, review the list of excluded user groups. If you want to remove a user group from the exclusion list, choose it then select **Remove user group**.
5. Select **Next** to confirm your exclusion list and proceed to adding contact persons or groups. Otherwise, select **Skip**, and all your added exclusions are discarded.

[![Screenshot to exclude user groups in Defender Experts MDR.](media/get-started-xdr/exclude-user-groups.png)](media/get-started-xdr/exclude-user-groups.png#lightbox)

Note

You can only exclude users by adding them to a Microsoft Entra ID security group. On-premises Microsoft Entra ID users can't be excluded at this time.

To edit or update exclusions after the initial setup, go to **Settings** &gt; **Defender Experts** &gt; **Exclusions**, then go to the **Device groups** or **User groups** tab.

## Tell us who to contact for important matters

The Defender Experts service lets you determine the individuals or groups within your organization that need to be notified if there are critical incidents, service updates, occasional queries, and other recommendations:

- **Incident notification contacts** – These contacts are persons or teams that we can notify for managed response actions or any communication that requires immediate response. Given the urgent nature of the communications, we recommended that these contacts are always available.
- **Service review contacts** – These contacts are persons or teams that will be engaged with for service updates and, if your service includes a Security Delivery Expert, service briefings.

When you add these contacts, the individuals or groups receive an email notifying them that they were added as a contact for incident notification or service review purposes.

[![Screenshot of Incident contacts page in Defender for Experts XDR settings step-by-step guide.](media/get-started-xdr/who-to-contact-for-important-matters.png)](media/get-started-xdr/who-to-contact-for-important-matters.png#lightbox)

**To add notification contacts:**

1. In the same Defender Experts settings setup, under **Contacts**, search for and add your **Contact person or team** in the text field provided.
2. Add a **Phone number** (optional) that Defender Experts can call for matters that require immediate attention.
3. Under the **Contact for** dropdown box, choose **Incident notification** or **Service review**.
4. Select **Add**.
5. Select **Next** to confirm your contacts list and proceed to creating a Teams channel where you can also receive incident notifications.

To edit or update your notification contacts after the initial setup, go to **Settings** &gt; **Defender Experts** &gt; **Notification contacts**.

[![Screenshot of notification contacts.](media/get-started-xdr/who-to-contact-for-imp-matters-2.png)](media/get-started-xdr/who-to-contact-for-imp-matters-2.png#lightbox)

## Receive managed response notifications and updates in Microsoft Teams

Apart from email and [in-portal chat](defender-experts-mdr-communication#in-portal-chat), you can also use Microsoft Teams to receive updates about managed responses and communicate with experts in real time. When you turn on this setting, you create a new team named **Defender Experts team**. Managed response notifications related to ongoing incidents are sent as new posts in the **Managed response** channel. [Learn more about using Teams chat](defender-experts-mdr-communication#teams-chat).

Important

Defender Experts have access to all messages posted on any channel in the created **Defender Experts team**. To prevent Defender Experts from accessing messages in this team, go to **Apps** in Teams, and then navigate to **Manage your apps** &gt; **Defender Experts** &gt; **Remove**. You can't reverse this removal action.

**To turn on Teams notifications and chat:**

1. In the same Defender Experts settings setup, under **Teams**, select the **Communicate on Teams** checkbox. This action creates a private team **Defender Experts team** with a **Managed Response** channel in it. The page then updates to show a **Open Teams channel** link.
2. Any notification contacts you added on the previous onboarding step are also added automatically as members of the Teams channel. To add additional SOC team members to the created channel, go to **Microsoft Teams** &gt; **Defender Experts team** &gt; **More options (...)** &gt; **Manage team** &gt; **Add member**.
3. Select **Next** to review your settings.
4. Select **Submit**. The step-by-step guide then completes the initial setup.
5. Select **View readiness assessment** to complete the necessary actions required to optimize your security posture.

Note

To set up the Defender Experts Teams application, you must have **Security administrator** or higher role assigned, and a Microsoft Teams license.

To turn on Teams notifications and chat after the initial setup, go to **Settings** &gt; **Defender Experts** &gt; **Teams**.

[![Screenshot of option to activate Teams for receiving managed response.](media/get-started-xdr/teams-managed-response.png)](media/get-started-xdr/teams-managed-response.png#lightbox)

## Prepare your environment for the Defender Experts service

Apart from onboarding service delivery, the expertise of Microsoft Defender Experts on the Microsoft Defender product suite enables them to help you run a **readiness assessment** and get the most out of your Microsoft security products.

The readiness assessment is based on the number of protected devices and identities in your environment, and Defender Experts' policy recommendations. To view the assessment, in your Microsoft Defender portal, go to **Settings** &gt; **Defender Experts** then select **Service status**.

[![Screenshot of readiness assessment environment.](media/get-started-xdr/readiness-assessment-xdr.png)](media/get-started-xdr/readiness-assessment-xdr.png#lightbox)

The readiness assessment has two parts:

- **Actions needed** – This section shows the number of actions or security settings that you need to complete, are in progress, or are completed. The table at the bottom part of the page lists these actions.

    The list outlines the required steps you need to take before initiating the service. Prioritize the actions that have the **Complete now** status to get the Defender Experts service started sooner.

    Note

    It can take up to 24 hours to get the latest status of your security settings.
- **Protected assets** – This section shows the current number of protected devices and identities versus the ones that you still need to protect to get the Defender Experts service started.

    The figures are based on your Defender for Endpoint and Defender for Identity licenses. To achieve these target number of protected assets, [onboard more devices](/en-us/defender-endpoint/onboarding) to Defender for Endpoint or [install more Defender for Identity sensors](/en-us/defender-for-identity/install-sensor).

Important

The Defender Experts service reviews your readiness assessment periodically, especially if there are any changes to your environment, such as the addition of new devices and identities. Regularly monitor and run the readiness assessment beyond the initial onboarding to ensure that your environment has a strong security posture to reduce risk.

After you complete all the required tasks and meet the onboarding targets in your readiness assessment, the monitoring phase of your Defender Experts service starts. For a few days, our experts start monitoring your environment closely to identify latent threats, sources of risk, and normal activity. As we get better understanding of your critical assets, we can streamline the service and fine-tune our responses.

Once our experts begin to perform comprehensive response work on your behalf, you'll start receiving [notifications about incidents](defender-experts-mdr-managed-response#incident-updates) that require remediation steps and targeted recommendations on critical incidents. You can also [chat with our experts](defender-experts-mdr-communication) or your Security Delivery Experts (SDXs) regarding important queries and regular business and security posture reviews. Additionally you can also [view real-time reports](defender-experts-mdr-reports) on the number of incidents we've investigated and resolved on your behalf.

### Next step

- [Managed detection and response](defender-experts-mdr-managed-response)
- [Get real-time visibility with Defender Experts reports](defender-experts-mdr-reports)
- [Communicating with experts in the Microsoft Defender Experts service](defender-experts-mdr-communication)

### See also

- [General information on Defender Experts service](defender-experts-mdr-faq)
- [How Microsoft Defender Experts permissions work](defender-experts-mdr-permissions)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).