---
layout: Conceptual
title: Get started using Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/attack-simulation-training-get-started
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 
ms.collection:
- m365-security
- tier2
ms.custom:
- seo-marvel-apr2020
- sfi-ga-nochange
- msecd-doc-authoring-1016
description: Learn the basics of Attack simulation training in Microsoft Defender for Office 365, including supported attack scenarios, licensing requirements, and how simulations help identify vulnerable users.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 040318d5-e67c-8744-98c4-d154d63de827
document_version_independent_id: 040318d5-e67c-8744-98c4-d154d63de827
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/attack-simulation-training-get-started.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-simulation-training-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/attack-simulation-training-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: a1dc427b-40ca-c987-64c2-e0ef4713c484
---

# Get started using Attack simulation training - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft Defender for Office 365 Plan 2 (add-on licenses or included in subscriptions like Microsoft 365 E5), you can use Attack simulation training in the Microsoft Defender portal to run realistic attack scenarios in your organization. The simulated attacks in Attack simulation training can help you identify and find vulnerable users before a real attack impacts your bottom line.

This article explains the basics of Attack simulation training.

Watch this short video to learn more about Attack simulation training.

## What do you need to know before you begin?

Before you begin, review the following licensing, environment, and access requirements.

- Attack simulation training requires a Microsoft 365 E5 or [Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) license. For more information about licensing requirements, see [Licensing terms](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description#licensing-terms).
- Attack simulation training supports on-premises mailboxes, but with reduced reporting functionality. For more information, see [Reporting issues with on-premises mailboxes](attack-simulation-training-faq#reporting-issues-with-on-premises-mailboxes).
- To open the Microsoft Defender portal, go to https://security.microsoft.com. Attack simulation training is available at **Email and collaboration** &gt; **Attack simulation training**. To go directly to Attack simulation training, use https://security.microsoft.com/attacksimulator.
- For more information about the availability of Attack simulation training across different Microsoft 365 subscriptions, see [Microsoft Defender for Office 365 service description](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): You need membership in one of the following roles:

        - **Global Administrator**¹
        - **Security Administrator**
        - **Attack Simulation Administrator**²: Create and manage all aspects of attack simulation campaigns.
        - **Attack Payload Author**³: Create attack payloads that an admin can initiate later.
        - **Security Operator and Security Reader**⁴: View all aspects of attack simulation campaigns.

        Important

        ¹ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

        ² Adding users to this role group in [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions) is currently unsupported.

        ³ Members of Attack Payload Author have the following limitations in attack simulation training:

        - They can't create or edit simulations, training campaigns, simulation automations, or payload automations.
        - They can't change global settings.
        - They can't change content (for example, notifications), but they can change payloads.
        - They can't view tenant simulation reports, aggregate reports, simulation automation records, or payload automation records.

        ⁴ Members of Security Operator and Security Reader have the following limitations in attack simulation training:

        - They can't create or edit simulations, training campaigns, simulation automations, or payload automations.
        - They can't change global settings.
        - They can't change content (for example, tenant payloads or notifications).
        - They can access data through read APIs with user scope, but they can't use write APIs.

        Currently, [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) isn't supported.
- There are no corresponding PowerShell cmdlets for Attack simulation training.
- Attack simulation and training related data is stored with other customer data for Microsoft 365 services. For more information, see [Microsoft 365 data locations](/en-us/microsoft-365/enterprise/o365-data-locations). Attack simulation training is available in the following regions: APC, EUR, and NAM. Countries within these regions where Attack simulation training is available include ARE, AUS, AUT, BRA, CAN, CHE, CHL, DEU, DNK, ESP, FRA, GBR, IDN, IND, ISR, ITA, JPN, KOR, LAM, MEX, MYS, NOR, NZL, POL, QAT, SGP, SWE, TWN, and ZAF.

    Note

    NOR, ZAF, ARE, and DEU are the latest additions. All features except reported email telemetry are available in these regions. We're working to enable the features and we'll notify customers when reported email telemetry becomes available.
- Attack simulation training is available in Microsoft 365 GCC, GCC High, and DoD environments. Certain advanced features aren't available in GCC High and DoD (for example, payload automation, recommended payloads, and predicted compromised rate). If your organization has Microsoft 365 G5, Office 365 G5 or Microsoft Defender for Office 365 (Plan 2) for Government, you can use Attack simulation training as described in this article.

Note

Attack simulation training offers a subset of capabilities to E3 customers as a trial. The trial offering contains the ability to use a Credential Harvest payload and the ability to select 'ISA Phishing' or 'Mass Market Phishing' training experiences. No other capabilities are part of the E3 trial offering.

## Simulations

A simulation in Attack simulation training is the overall campaign that delivers realistic but harmless phishing messages to users. The basic elements of a simulation are:

- Who gets the simulated phishing message and on what schedule.
- Training that users get based on their action or lack of action (for both correct and incorrect actions) on the simulated phishing message.
- The *payload* used in the simulated phishing message (a link or an attachment), and the composition of the phishing message (for example, package delivered, problem with your account, or you won a prize).
- The *social engineering technique*. The payload and social engineering technique are closely related.

In Attack simulation training, multiple types of social engineering techniques are available. Except for **How-to Guide**, these techniques were curated from the [MITRE ATT&CK® framework](https://attack.mitre.org/techniques/enterprise/). Different payloads are available for different social engineering techniques in Attack simulation training.

The following social engineering techniques are available:

- **Credential Harvest**: An attacker sends the recipient a message that contains a link^\*^. When the recipient clicks on the link, they go to a website that typically shows a dialog box that asks the user for their username and password. Typically, the destination page is themed to represent a well-known website in order to build trust in the user.
- **Malware Attachment**: An attacker sends the recipient a message that contains an attachment. When the recipient opens the attachment, arbitrary code (for example, a macro) runs on the user's device to help the attacker install more code or further entrench themselves.
- **Link in Attachment**: This technique is a hybrid of a credential harvest. An attacker sends the recipient a message that contains a link inside of an attachment. When the recipient opens the attachment and clicks on the link, they go to a website that typically shows a dialog box that asks the user for their username and password. Typically, the destination page is themed to represent a well-known website in order to build trust in the user.
- **Link to Malware**^\*^: An attacker sends the recipient a message that contains a link to an attachment on a well-known file sharing site (for example, SharePoint or Dropbox). When the recipient clicks on the link, the attachment opens, and arbitrary code (for example, a macro) runs on the user's device to help the attacker install other code or further entrench themselves.
- **Drive-by-url**^\*^: An attacker sends the recipient a message that contains a link. When the recipient clicks on the link, they go to a website that tries to run background code. This background code attempts to gather information about the recipient or deploy arbitrary code on their device. Typically, the destination website is a well-known website that was compromised or a clone of a well-known website. Familiarity with the website helps convince the user that the link is safe to click. This technique is also known as a *watering hole attack*.
- **OAuth Consent Grant**^\*^: An attacker creates a malicious Azure Application that seeks to gain access to data. The application sends an email request that contains a link. When the recipient clicks on the link, the consent grant mechanism of the application asks for access to the data (for example, the user's Inbox).
- **How-to Guide**: A teaching guide that contains instructions for users (for example, how to report phishing messages).

^\*^ The link can be a URL or a QR code.

The URLs that are used by Attack simulation training are listed in the following table:

| - | - | - |
| --- | --- | --- |
| `https://www.attemplate.com` | `https://www.exportants.it` | `https://www.resetts.it` |
| `https://www.bankmenia.com` | `https://www.exportants.org` | `https://www.resetts.org` |
| `https://www.bankmenia.de` | `https://www.financerta.com` | `https://www.salarytoolint.com` |
| `https://www.bankmenia.es` | `https://www.financerta.de` | `https://www.salarytoolint.net` |
| `https://www.bankmenia.fr` | `https://www.financerta.es` | `https://www.securembly.com` |
| `https://www.bankmenia.it` | `https://www.financerta.fr` | `https://www.securembly.de` |
| `https://www.bankmenia.org` | `https://www.financerta.it` | `https://www.securembly.es` |
| `https://www.banknown.de` | `https://www.financerta.org` | `https://www.securembly.fr` |
| `https://www.banknown.es` | `https://www.financerts.com` | `https://www.securembly.it` |
| `https://www.banknown.fr` | `https://www.financerts.de` | `https://www.securembly.org` |
| `https://www.banknown.it` | `https://www.financerts.es` | `https://www.securetta.de` |
| `https://www.banknown.org` | `https://www.financerts.fr` | `https://www.securetta.es` |
| `https://www.browsersch.com` | `https://www.financerts.it` | `https://www.securetta.fr` |
| `https://www.browsersch.de` | `https://www.financerts.org` | `https://www.securetta.it` |
| `https://www.browsersch.es` | `https://www.hardwarecheck.net` | `https://www.shareholds.com` |
| `https://www.browsersch.fr` | `https://www.hrsupportint.com` | `https://www.sharepointen.com` |
| `https://www.browsersch.it` | `https://www.mcsharepoint.com` | `https://www.sharepointin.com` |
| `https://www.browsersch.org` | `https://www.mesharepoint.com` | `https://www.sharepointle.com` |
| `https://www.docdeliveryapp.com` | `https://www.officence.com` | `https://www.sharesbyte.com` |
| `https://www.docdeliveryapp.net` | `https://www.officenced.com` | `https://www.sharession.com` |
| `https://www.docstoreinternal.com` | `https://www.officences.com` | `https://www.sharestion.com` |
| `https://www.docstoreinternal.net` | `https://www.officentry.com` | `https://www.supportin.de` |
| `https://www.doctorican.de` | `https://www.officested.com` | `https://www.supportin.es` |
| `https://www.doctorican.es` | `https://www.passwordle.de` | `https://www.supportin.fr` |
| `https://www.doctorican.fr` | `https://www.passwordle.fr` | `https://www.supportin.it` |
| `https://www.doctorican.it` | `https://www.passwordle.it` | `https://www.supportres.de` |
| `https://www.doctorican.org` | `https://www.passwordle.org` | `https://www.supportres.es` |
| `https://www.doctrical.com` | `https://www.payrolltooling.com` | `https://www.supportres.fr` |
| `https://www.doctrical.de` | `https://www.payrolltooling.net` | `https://www.supportres.it` |
| `https://www.doctrical.es` | `https://www.prizeably.com` | `https://www.supportres.org` |
| `https://www.doctrical.fr` | `https://www.prizeably.de` | `https://www.techidal.com` |
| `https://www.doctrical.it` | `https://www.prizeably.es` | `https://www.techidal.de` |
| `https://www.doctrical.org` | `https://www.prizeably.fr` | `https://www.techidal.fr` |
| `https://www.doctricant.com` | `https://www.prizeably.it` | `https://www.techidal.it` |
| `https://www.doctrings.com` | `https://www.prizeably.org` | `https://www.techniel.de` |
| `https://www.doctrings.de` | `https://www.prizegiveaway.net` | `https://www.techniel.es` |
| `https://www.doctrings.es` | `https://www.prizegives.com` | `https://www.techniel.fr` |
| `https://www.doctrings.fr` | `https://www.prizemons.com` | `https://www.techniel.it` |
| `https://www.doctrings.it` | `https://www.prizesforall.com` | `https://www.templateau.com` |
| `https://www.doctrings.org` | `https://www.prizewel.com` | `https://www.templatent.com` |
| `https://www.exportants.com` | `https://www.prizewings.com` | `https://www.templatern.com` |
| `https://www.exportants.de` | `https://www.resetts.de` | `https://www.windocyte.com` |
| `https://www.exportants.es` | `https://www.resetts.es` |  |
| `https://www.exportants.fr` | `https://www.resetts.fr` |  |

Note

Check the availability of the simulated phishing URL in your supported web browsers before you use the URL in a phishing campaign. For more information, see [Phishing simulation URLs blocked by Google Safe Browsing](attack-simulation-training-faq#phishing-simulation-urls-blocked-by-google-safe-browsing).

### Create simulations

For instructions on how to create and launch Attack simulation training simulations, see [Simulate a phishing attack](attack-simulation-training-simulations).

The *landing page* in the simulation is where users go when they open the payload. When you create a simulation, you select the landing page to use. You can select from built-in landing pages, custom landing pages that you already created, or you can create a new landing page to use during the creation of the simulation. To create landing pages, see [Landing pages in Attack simulation training](attack-simulation-training-landing-pages).

*End user notifications* in the simulation send periodic reminders to users (for example, training assignment and reminder notifications). You can select from built-in notifications, custom notifications that you already created, or you can create new notifications to use during the creation of the simulation. To create notifications, see [End-user notifications for Attack simulation training](attack-simulation-training-end-user-notifications).

Tip

- *Simulation automations* provide the following improvements over traditional simulations:

    - Simulation automations can include multiple social engineering techniques and related payloads (simulations contain only one).
    - Simulation automations support automated scheduling options (more than just the start date and end date in simulations).

    For more information, see [Simulation automations for Attack simulation training](attack-simulation-training-simulation-automations).
- To see which departments are more vulnerable to phishing simulations, create identical simulations or simulation automations scoped by department, and then use the Attack simulation training reports and insights to compare the results.

### Create and manage payloads

Although Attack simulation training contains many built-in payloads for the available social engineering techniques, you can create custom payloads to better suit your business needs, including [copying and customizing an existing payload](attack-simulation-training-payloads#copy-payloads). You can create payloads at any time before you create the simulation or during the creation of the simulation. To create payloads, see [Create a custom payload for Attack simulation training](attack-simulation-training-payloads#create-payloads).

In simulations that use **Credential Harvest** or **Link in Attachment** social engineering techniques, *login pages* are part of the payload that you select. The login page is the web page where users enter their credentials. Each applicable payload uses a default login page, but you can change the login page that's used. You can select from built-in login pages, custom login pages that you already created, or you can create a new login page to use during the creation of the simulation or the payload. To create login pages, see [Login pages in Attack simulation training](attack-simulation-training-login-pages).

The best training experience for simulated phishing messages is to make them as close as possible to real phishing attacks that your organization might experience. What if you could capture and use harmless versions of real-world phishing messages that were detected in Microsoft 365 and use them in simulated phishing campaigns? You can, with *payload automations* (also known as *payload harvesting*). To create payload automations, see [Payload automations for Attack simulation training](attack-simulation-training-payload-automations).

Attack simulation training also supports using QR codes in payloads. You can choose from the list of built-in QR code payloads, or you can create custom QR code payloads. For more information, see [QR code payloads in Attack simulation training](attack-simulation-training-payloads#qr-code-payloads).

### View simulation reports and insights

After you create and launch your phishing simulation, you need to see how it's going. For example:

- Did everyone receive it?
- Who did what to the simulated phishing message and the payload within it (delete, report, open the payload, enter credentials, etc.).
- Who completed the assigned training.

The available reports and insights for Attack simulation training are described in [Reports for Attack simulation training](attack-simulation-training-insights).

### Understand the predicted compromise rate

You often need to tailor a simulated phishing campaign for specific audiences. If the phishing message is too close to perfect, almost everyone is fooled by it. If it's too suspicious, no is fooled by it. And, the phishing messages that some users consider difficult to identify are considered easy to identify by other users. So how do you strike a balance?

The *predicted compromise rate (PCR)* indicates the potential effectiveness when the payload is used in a simulation. PCR uses intelligent historical data across Microsoft 365 to predict the percentage of people who will be compromised by the payload. For example:

- Payload content.
- Aggregated and anonymized compromise rates from other simulations.
- Payload metadata.

PCR allows you to compare the predicted vs. actual click through rates for your phishing simulations. You can also use PCR and actual click-through-rate data to see how your organization performs compared to predicted outcomes.

PCR information for a payload is available wherever you view and select payloads, and in the following reports and insights:

- [Behavior impact on compromise rate card](attack-simulation-training-insights#behavior-impact-on-compromise-rate-card)
- [Training efficacy tab for the Attack simulation report](attack-simulation-training-insights#training-efficacy-tab-for-the-attack-simulation-report)

Tip

Attack Simulator uses Safe Links in Defender for Office 365 to securely track click data for the URL in the payload message sent to targeted recipients of a phishing campaign, even if the **Track user clicks** setting in Safe Links policies is turned off.

## Assign training without running simulations

Traditional phishing simulations present users with suspicious messages and the following goals:

- Get users to report the message as suspicious.
- Provide training after users click on or launch the simulated malicious payload and give up their credentials.

But, sometimes you don't want to wait for users to take correct or incorrect actions before you give them training. Attack simulation training provides the following features to skip the wait and go straight to training:

- **Training campaigns**: A Training campaign is a training-only assignment for the targeted users. You can directly assign training without putting users through the test of a simulation. Training campaigns make it easy to conduct learning sessions like monthly cybersecurity awareness training. For more information, see [Training campaigns in Attack simulation training](attack-simulation-training-training-campaigns).

    Tip

    [Training modules](attack-simulation-training-training-modules) are used in Training campaigns, but you can also use Training modules when you [assign training](attack-simulation-training-simulations#assign-training) in regular simulations.
- **How-to Guides in simulations**: Simulations based on the **How-to Guide** social engineering technique don't attempt to test users. A How-to guide is a lightweight learning experience that users can view directly in their Inbox. For example, the following built-in **How-to Guide** payloads are available, and you can create your own (including [copying and customizing an existing payload](attack-simulation-training-payloads#copy-payloads)):

    - **Teaching guide: How to report phishing messages**
    - **Teaching Guide: How to recognize and report QR phishing messages**

Tip

Attack simulation training provides the following built-in training options for QR code-based attacks:

- Training modules:
    - **Malicious digital QR codes**
    - **Malicious printed QR codes**
- How-to Guides in simulations: **Teaching Guide: How to recognize and report QR phishing messages**