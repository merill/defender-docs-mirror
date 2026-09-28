---
layout: Conceptual
title: What's new in Microsoft Secure Score - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-secure-score-whats-new
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Describes changes to Microsoft Secure Score in the Microsoft Defender portal.
ms.localizationpriority: medium
f1.keywords:
- NOCSH
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
audience: ITPro
ms.collection:
- m365-security
- tier2
ms.topic: whats-new
search.appverid:
- MOE150
- MET150
ms.date: 2024-02-19T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 49f52c69-c804-3d26-4ed3-2bc742d52691
document_version_independent_id: 49f52c69-c804-3d26-4ed3-2bc742d52691
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-secure-score-whats-new.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-secure-score-whats-new
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-secure-score-whats-new.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 99887cbe-4e7d-9ab1-9ca2-8ebc11052c2d
---

# What's new in Microsoft Secure Score - Microsoft Defender XDR | Microsoft Learn

To make Microsoft Secure Score a better representative of your security posture, we continue to add new features and improvement actions.

The more improvement actions you take, the higher your Secure Score is. For more information, see [Microsoft Secure Score](microsoft-secure-score).

Microsoft Secure Score can be found at https://security.microsoft.com/securescore in the [Microsoft Defender portal](microsoft-365-defender-portal).

## February 2024

The following recommendation is added as a Microsoft Secure Score improvement action:

**Microsoft Defender for Identity:**

- Edit insecure ADCS certificate enrollment IIS endpoints (ESC11)

## January 2024

The following recommendations were added as Microsoft Secure Score improvement actions:

**Microsoft Entra (AAD):**

- Ensure "Phishing-resistant MFA strength" is required for Administrators.
- Ensure custom banned passwords lists are used.
- Ensure "Windows Azure Service Management API" is limited to administrative roles.

**Admin Center:**

- Ensure "User owned apps and services" is restricted.

**Microsoft Forms:**

- Ensure internal phishing protection for Forms is enabled.

**Microsoft Share Point:**

- Ensure that SharePoint guests can't share items they don't own.

### Defender for Cloud Apps support for multiple instances of an app

Microsoft Defender for Cloud Apps now supports Secure Score recommendations across multiple instances of the same app. For example, if you have multiple instances of AWS, you can configure and filter for Secure Score recommendations for each instance individually.

For more information, see [Turn on and manage SaaS security posture management (SSPM)](/en-us/defender-cloud-apps/security-saas).

## December 2023

The following recommendations were added as Microsoft Secure Score improvement actions:

**Microsoft Entra (AAD):**

- Ensure "Microsoft Azure Management" is limited to administrative roles.

**Microsoft Sway:**

- Ensure that Sways can't be shared with people outside of your organization.

**Microsoft Exchange Online:**

- Ensure users installing Outlook add-ins isn't allowed.

**Zendesk:**

- Enable and adopt two-factor authentication (2FA).
- Send a notification on password change for admins, agents, and end users.
- Enable IP restrictions.
- Block customers to bypass IP restrictions.
- Use the Zendesk Support mobile app (admins and agents).
- Enable Zendesk authentication.
- Enable session timeout for users.
- Block account assumption.
- Block admins to set passwords.
- Enable automatic redaction.

**Net Document:**

- Adopt Single sign on (SSO) in netDocument.

**Meta Workplace:**

- Adopt Single sign on (SSO) in Workplace by Meta.

**Dropbox:**

- Enable web session timeout for web users.

**Atlassian:**

- Enable multi-factor authentication (MFA).
- Enable Single Sign On (SSO).
- Enable strong Password Policies.
- Enable session timeout for web users.
- Enable Password expiration policies.
- Atlassian mobile app security - Users that are affected by policies.
- Atlassian mobile app security - App data protection.
- Atlassian mobile app security - App access requirement.

**Microsoft Defender for Identity: New Active Directory Certificate Services (ADCS) related recommendations:**

- **Certificate templates recommended actions**:
    - [Prevent users to request a certificate valid for arbitrary users based on the certificate template (ESC1)](/en-us/defender-for-identity/security-assessment-prevent-users-request-certificate)
    - [Edit overly permissive Certificate Template with privileged EKU (Any purpose EKU or No EKU) (ESC2)](/en-us/defender-for-identity/security-assessment-edit-overly-permissive-template)
    - [Misconfigured enrollment agent certificate template (ESC3)](/en-us/defender-for-identity/security-assessment-edit-misconfigured-enrollment-agent)
    - [Edit misconfigured certificate templates ACL (ESC4)](/en-us/defender-for-identity/security-assessment-edit-misconfigured-acl)
    - [Edit misconfigured certificate templates owner](/en-us/defender-for-identity/security-assessment-edit-misconfigured-owner)
- **Certificate authority recommended actions**:
    - [Edit vulnerable Certificate Authority setting](/en-us/defender-for-identity/security-assessment-edit-vulnerable-ca-setting)
    - [Edit misconfigured Certificate Authority ACL (ESC7)](/en-us/defender-for-identity/security-assessment-edit-misconfigured-ca-acl)
    - [Enforce encryption for RPC certificate enrollment interface (ESC8)](/en-us/defender-for-identity/security-assessment-enforce-encryption-rpc)

For more information, see [Microsoft Defender for Identity's security posture assessments](/en-us/defender-for-identity/security-assessment).

## October 2023:

The following recommendations were added as Microsoft Secure Score improvement actions:

**Microsoft Entra (AAD):**

- Ensure "Phishing-resistant MFA strength" is required for administrators.
- Ensure custom banned passwords lists are used.

**Microsoft Sway:**

- Ensure that Sways can't be shared with people outside of your organization.

**Atlassian:**

- Enable multifactor authentication (MFA).
- Enable Single Sign On (SSO).
- Enable strong Password Policies.
- Enable session time out for web users.
- Enable Password expiration policies.
- Atlassian mobile app security - Users who are affected by policies.
- Atlassian mobile app security - App data protection.
- Atlassian mobile app security - App access requirement.

## September 2023:

The following recommendations were added as Microsoft Secure Score improvement actions:

**Microsoft Information Protection:**

- Ensure Microsoft 365 audit log search is enabled.
- Ensure DLP policies are enabled for Microsoft Teams.

**Exchange Online:**

- Ensure that SPF records are published for all Exchange Domains.
- Ensure modern authentication for Exchange Online is enabled.
- Ensure MailTips are enabled for end users.
- Ensure mailbox auditing for all users is enabled.
- Ensure other storage providers are restricted in Outlook on the web.

**Microsoft Defender for Cloud Apps:**

- Ensure Microsoft Defender for Cloud Apps is enabled.

**Microsoft Defender for Office:**

- Ensure Exchange Online Spam Policies are set to notify administrators.
- Ensure all forms of mail forwarding are blocked and/or disabled.
- Ensure Safe Links for Office Applications is enabled.
- Ensure Safe Attachments policy is enabled.
- Ensure that an anti-phishing policy was created.

## August 2023

The following recommendations were added as Microsoft Secure Score improvement actions:

**Microsoft Information Protection:**

- Ensure Microsoft 365 audit log search is enabled.

**Microsoft Exchange Online:**

- Ensure modern authentication for Exchange Online is enabled.
- Ensure Exchange Online Spam Policies are set to notify administrators.
- Ensure all forms of mail forwarding are blocked and/or disabled.
- Ensure MailTips are enabled for end users.
- Ensure mailbox auditing for all users is enabled.
- Ensure other storage providers are restricted in Outlook on the web.

**Microsoft Entra ID:**

To see the following new Microsoft Entra controls in the Office 365 connector, you need to turn on Microsoft Defender for Cloud Apps in the App connectors settings page:

- Ensure password protection is enabled for on-premises Active Directory.
- Ensure "LinkedIn account connections" is disabled.

**SharePoint:**

- Ensure Safe Links for Office Applications is enabled.
- Ensure Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is enabled.
- Ensure that an anti-phishing policy was created.

To see the following new SharePoint controls in the Office 365 connector, you need to turn on Microsoft Defender for Cloud Apps in the App connectors settings page:

- Ensure SharePoint external sharing is managed through domain allowlists/blocklists.
- Block OneDrive for Business sync from unmanaged devices.

### Microsoft Secure Score integration with Microsoft Lighthouse 365

Microsoft 365 Lighthouse helps Managed Service Providers (MSPs) grow their business and deliver services to customers at scale from a single portal. Lighthouse allows customers to standardize configurations, manage risk, identify artificial intelligence (AI)-driven sales opportunities, and engage with customers to help them maximize their investment in Microsoft 365.

We've integrated Microsoft Secure Score into Microsoft 365 Lighthouse. This integration provides an aggregate view of the Secure Score across all managed tenants, and Secure Score details for each individual tenant. Access to Secure Score is available from a new card on the Lighthouse homepage or by selecting a tenant on the Lighthouse Tenants page.

Note

The integration with Microsoft Lighthouse 365 is available to Microsoft partners who use the Cloud Solution Provider (CSP) program to manage customer tenants.

### Microsoft Secure Score permissions integration with Microsoft Defender unified role-based access control (RBAC) is now in Public Preview

Previously, only Microsoft Entra global roles could access Microsoft Secure Score. Now, you can control access and grant granular permissions for the Microsoft Secure Score experience as part of the Microsoft Defender XDR Unified RBAC model.

You can add the new permission and choose the data sources the user has access to by selecting the **Security posture** permissions group when creating the role. For more information, see [Create custom roles with Microsoft Defender unified RBAC](create-custom-rbac-roles). Users see Secure Score data for the data sources they have permissions to.

A new data source **Secure Score – Additional data source** is also available. Users with permissions to this data source have access to additional data within the Secure score dashboard. For more information on additional data sources, see [Products included in Secure Score](microsoft-secure-score#products-included-in-secure-score).

## July 2023

The following Microsoft Defender for Identity recommendations were added as Microsoft Secure Score improvement actions:

- Remove the attribute "password never expires" from accounts in your domain.
- Remove access rights on suspicious accounts with the Admin SDHolder permission.
- Manage accounts with passwords more than 180 days old.
- Remove local admins on identity assets.
- Remove non-admin accounts with DCSync permissions.
- Start your Defender for Identity deployment, installing Sensors on Domain Controllers and other eligible servers.

The following Google workspace recommendations were added as a Microsoft Secure Score improvement action:

- Enable multifactor authentication (MFA)

In order to view this new control, Google workspace connector in Microsoft Defender for Cloud Apps must be configured via the App connectors settings page.

## May 2023

A new Microsoft Exchange Online recommendation is now available as Secure Score improvement action:

- Ensure mail transport rules don't allow specific domains.

New Microsoft SharePoint recommendations are now available as Secure Score improvement actions:

- Ensure modern authentication for SharePoint applications is required.
- Ensure that external users can't share files, folders, and sites they don't own.

## April 2023

New recommendations are now available in Microsoft Secure Score for customers with an active Microsoft Defender for Cloud Apps license:

- Ensure that only organizationally managed/approved public groups exist.
- Ensure Sign-in frequency is enabled and browser sessions aren't persistent for Administrative users.
- Ensure Administrative accounts are separate, unassigned, and cloud-only.
- Ensure third party integrated applications aren't allowed.
- Ensure the admin consent workflow is enabled.
- Ensure DLP policies are enabled for Microsoft Teams.
- Ensure that SPF records are published for all Exchange Domains.
- Ensure Microsoft Defender for Cloud Apps is Enabled.
- Ensure mobile device management policies are set to require advanced security configurations to protect from basic internet attacks.
- Ensure that mobile device password reuse is prohibited.
- Ensure that mobile devices are set to never expire passwords.
- Ensure that users can't connect from devices that are jail broken or rooted.
- Ensure mobile devices are set to wipe on multiple sign-in failures to prevent brute force compromise.
- Ensure that mobile devices require a minimum password length to prevent brute force attacks.
- Ensure devices lock after a period of inactivity to prevent unauthorized access.
- Ensure that mobile device encryption is enabled to prevent unauthorized access to mobile data.
- Ensure that mobile devices require complex passwords (Type = Alphanumeric).
- Ensure that mobile devices require complex passwords (Simple Passwords = Blocked).
- Ensure that devices connecting have AV and a local firewall enabled.
- Ensure mobile device management policies are required for email profiles.
- Ensure mobile devices require the use of a password.

Note

To view the new Defender for Cloud Apps recommendations, the Office 365 connector in Microsoft Defender for Cloud Apps must be toggled on via the App connectors settings page. For more information, see, [How to connect Office 365 to Defender for Cloud Apps](/en-us/defender-cloud-apps/connect-office-365#how-to-connect-office-365-to-defender-for-cloud-apps).

## September 2022

New Microsoft Defender for Office 365 recommendations for anti-phishing policies are now available as Secure Score improvement actions:

- Set the phishing email level threshold at 2 or higher.
- Enable impersonated user protection.
- Enable impersonated domain protection.
- Ensure that mailbox intelligence is enabled.
- Ensure that intelligence for impersonation protection is enabled.
- Quarantine messages that are detected from impersonated users.
- Quarantine messages that are detected from impersonated domains.
- Move messages that are detected as impersonated users by mailbox intelligence.
- Enable the "show first contact safety tip" option.
- Enable the user impersonation safety tip.
- Enable the domain impersonation safety tip.
- Enable the user impersonation unusual characters safety tip.

A New SharePoint Online recommendation is now available as a Secure Score improvement action:

- Sign out inactive users in SharePoint Online.

## August 2022

New Microsoft Purview Information Protection recommendations are now available as Secure Score improvement actions:

- **Labeling**
    - Extend Microsoft 365 sensitivity labeling to assets in Azure Purview data map.
    - Ensure Autolabeling data classification policies are set up and used.
    - Publish Microsoft 365 sensitivity label data classification policies.
    - Create Data Loss Prevention (DLP) policies.

New Microsoft Defender for Office 365 recommendations are now available as Secure Score improvement actions:

- **Anti-spam - Inbound policy**

    - Set the email bulk complaint level (BCL) threshold to 6 or lower.
    - Set action to take on spam detection.
    - Set action to take on high confidence spam detection.
    - Set action to take on phishing detection.
    - Set action to take on high confidence phishing detection.
    - Set action to take on bulk spam detection.
    - Retain spam in quarantine for 30 days.
    - Ensure spam safety tips are enabled.
    - Ensure that no sender domains are in the allowed domains list in anti-spam policies (replaces "Ensure that there are no sender domains allowed for Anti-spam policies" to extend functionality also for specific senders).
- **Anti-spam - Outbound policy**

    - Set maximum number of external recipients that a user can email per hour.
    - Set maximum number of internal recipients that a user can send to within an hour.
    - Set a daily message limit.
    - Block users who reached the message limit.
    - Set Automatic email forwarding rules to be system controlled.
- **Anti-spam - Connection filter**

    - Don't add allowed IP addresses in the connection filter policy.

## June 2022

- New Microsoft Defender for Endpoint and Microsoft Defender Vulnerability Management recommendations are now available as Secure Score improvement actions:

    - Disallow offline access to shares.
    - Remove share write permission set to **Everyone**.
    - Remove shares from the root folder.
    - Set folder access-based enumeration for shares.
    - Update Microsoft Defender for Endpoint core components.
- A new Microsoft Defender for Identity recommendation is available as a Secure Score improvement action:

    - Resolve unsecure domain configurations.
- A new [app governance](/en-us/defender-cloud-apps/app-governance-manage-app-governance) recommendation is now available as a Secure Score improvement action:

    - Regulate apps with consent from priority accounts.
- New Salesforce and ServiceNow recommendations are now available as Secure Score improvement actions for Microsoft Defender for Cloud Apps customers. For more information, see [SaaS Security Posture Management overview](https://aka.ms/saas_security_posture_management).

Note

Salesforce and ServiceNow controls are now available in public preview.

## April 2022

- Turn on user authentication for remote connections.

## December 2021

- Turn on Safe Attachments in block mode.
- Prevent sharing Exchange Online calendar details with external users.
- Turn on Safe Documents for Office clients.
- Turn on the common attachments filter setting for anti-malware policies.
- Ensure that there are no sender domains allowed for anti-spam policies.
- Create Safe Links policies for email messages.
- Create zero-hour auto purge policies for malware.
- Turn on Microsoft Defender for Office 365 in SharePoint, OneDrive, and Microsoft Teams.
- Create zero-hour auto purge policies for phishing messages.
- Create zero-hour auto purge policies for spam messages.
- Block abuse of exploited vulnerable signed drivers.
- Turn on scanning of removable drives during a full scan.

## We want to hear from you

If you have any issues, let us know by posting in the [Defender XDR community](https://techcommunity.microsoft.com/category/microsoft-defender-xdr/discussions/microsoftthreatprotection). We're monitoring the community to provide help.

## Related resources

- [Assess your security posture](microsoft-secure-score-improvement-actions)
- [Track your Microsoft Secure Score history and meet goals](microsoft-secure-score-history-metrics-trends)
- [What's coming](whats-new)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).