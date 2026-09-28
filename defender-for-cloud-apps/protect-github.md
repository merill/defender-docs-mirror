---
layout: Conceptual
title: Protect your GitHub Enterprise environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-github
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Connect GitHub Enterprise Cloud to Microsoft Defender for Cloud Apps by using the API connector to monitor user activity and detect anomalous behavior that could expose sensitive repositories and collaboration data.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f6355912-64ea-ed11-f3ba-85d4cdd0e233
document_version_independent_id: f6355912-64ea-ed11-f3ba-85d4cdd0e233
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-github.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-github
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-github.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 69c90d54-2778-3768-33fd-15b4be4ddf6e
---

# Protect your GitHub Enterprise environment - Microsoft Defender for Cloud Apps | Microsoft Learn

GitHub Enterprise Cloud is a service that helps organizations store and manage their code, as well as track and control changes to their code. Along with the benefits of building and scaling code repositories in the cloud, your organization's most critical assets might be exposed to threats. Exposed assets include repositories with potentially sensitive information, collaboration and partnership details, and more. Preventing exposure of this data requires continuous monitoring to prevent any malicious actors or security-unaware insiders from exfiltrating sensitive information.

Connecting GitHub Enterprise Cloud to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection for anomalous behavior.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats

The main threats to GitHub Enterprise Cloud environments include:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your GitHub Enterprise environment with the following best practices:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for GitHub Enterprise Cloud

To see security posture recommendations for GitHub in Microsoft Secure Score, create an API connector via the **Connectors** tab, with *Owner* and *Enterprise* permissions. In Secure Score, select **Recommended actions** and filter by **Product** = **GitHub**.

For example, recommendations for GitHub include:

- *Enable multifactor authentication (MFA)*
- *Enable single sign-on (SSO)*
- *Disable 'Allow members to change repository visibilities for this organization'*
- *Disable 'members with admin permissions for repositories can delete or transfer repositories'*

If a connector already exists and you don't see GitHub recommendations yet, refresh the connection by disconnecting the API connector, and then reconnecting it with the *Owner* and *Enterprise* permissions.

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Protect GitHub in real time

Review Defender for Cloud Apps best practices for [securing and collaborating with guests](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls).

## Connect GitHub Enterprise Cloud to Microsoft Defender for Cloud Apps

Use the following steps to connect Microsoft Defender for Cloud Apps to your existing GitHub Enterprise Cloud organization using the App Connector APIs. This connection gives you visibility into and control over your organization's GitHub Enterprise Cloud use. For more information about how Defender for Cloud Apps protects GitHub Enterprise Cloud, see [Protect GitHub Enterprise](protect-github).

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

### Prerequisites

Before you connect GitHub Enterprise Cloud to Defender for Cloud Apps, make sure the following prerequisites are met:

- Your organization must have a **GitHub Enterprise Cloud** license.
- The GitHub account used for connecting to Defender for Cloud Apps must have Owner permissions for your organization.
- For SSPM capabilities, the provided account must be the owner of the enterprise account.
- To verify owners of your organization, browse to your organization's page, select **People**, and then filter by *Owner*.

### Verify your GitHub domains

Verifying your domains is optional. We recommend that you do verify your domains so that Defender for Cloud Apps can match the domain emails of your GitHub organization's members to their corresponding Azure Active Directory user.

Domain verification is optional and separate from the GitHub Enterprise Cloud app configuration process. Skip this procedure if your domains are already verified.

1. Upgrade your organization to the [Corporate Terms of Service](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/upgrading-to-the-corporate-terms-of-service).
2. Verify [your organization's domains](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/verifying-your-organizations-domain).

    Note

    Make sure to verify each of the managed domains listed in your Defender for Cloud Apps settings. Managed domains are listed in the Microsoft Defender Portal under **Settings** &gt; **Cloud Apps** &gt; **System** &gt; **Organizational details** &gt; **Managed domains**.

### Configure GitHub Enterprise Cloud

1. Copy your organization's sign-in name. You'll need the organization's sign-in name later.

    Note

    The page will have a URL like `https://github.com/<your-organization>`. For example, if your organization's page is `https://github.com/sample-organization`, the organization's sign-in name is *sample-organization*.
2. Create an OAuth App for Defender for Cloud Apps to connect your GitHub organization.
3. Fill out the **Register a new OAuth app** details and then select **Register application**.

    - In the **Application name** box, enter a name for the app.
    - In the **Homepage URL** box, enter the URL for the app's homepage.
    - In the **Authorization callback URL** box, enter the following value: `https://portal.cloudappsecurity.com/api/oauth/connect`.

    Note

    - For US Government GCC customers, enter the following value: `https://portal.cloudappsecuritygov.com/api/oauth/connect`
    - For US Government GCC High customers, enter the following value: `https://portal.cloudappsecurity.us/api/oauth/connect`
    - Apps owned by an organization have access to the organization's apps. For more information, see [About OAuth App access restrictions](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/about-oauth-app-access-restrictions).
4. Select the OAuth App you created, and copy the **Client ID** and **Client Secret**.

### Configure Defender for Cloud Apps

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **GitHub**.
3. In the **Instance name** window, give the connector a descriptive name, and then select **Next**.
4. In the **Enter details** window, fill out the **Client ID** and **Client Secret** from the OAuth app and the **Organization Login Name** you copied when configuring GitHub Enterprise Cloud.

    ![Connect GitHub.](media/connect-github-connect-app.png)

    The **Enterprise slug**, also known as the enterprise name, is needed for supporting SSPM capabilities. To find the **Enterprise slug**:

    1. Select the **GitHub Profile picture** -&gt; **your enterprises**.
    2. Select **your enterprise account** and choose the account you want to connect to Microsoft Defender for Cloud Apps.
    3. Confirm that the URL contains the enterprise slug. For instance, `https://github.com/enterprises/testEnterprise`
    4. Enter only the enterprise slug, not the entire URL. In this example, *testEnterprise* is the enterprise slug.
5. Select **Connect GitHub**.

    If necessary, enter your GitHub administrator credentials to allow Defender for Cloud Apps access to your team's GitHub Enterprise Cloud instance.
6. Request organization access and authorize the app to give Defender for Cloud Apps access to your GitHub organization. Defender for Cloud Apps requires the following OAuth scopes:

    - **admin:org** - required for synchronizing your organization's audit log
    - **read:user** and **user:email** - required for synchronizing your organization's members
    - **repo:status** - required for synchronizing repository-related events in the audit log
    - **read:enterprise** - required for SSPM capabilities. The provided user must be the owner of the enterprise account.

    For more information about OAuth scopes, see [Understanding scopes for OAuth Apps](https://docs.github.com/developers/apps/building-oauth-apps/scopes-for-oauth-apps).

    Back in the Defender for Cloud Apps console, you should receive a message that GitHub was successfully connected.
7. Work with your GitHub organization owner to grant organization access to the OAuth app created under the GitHub **Third-party access** settings. For more information, see [Enabling OAuth app access restrictions for your organization](https://docs.github.com/en/organizations/managing-oauth-access-to-your-organizations-data/enabling-oauth-app-access-restrictions-for-your-organization).

    The organization owner will find the request from the OAuth app only after connecting GitHub to Defender for Cloud Apps.
8. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

After connecting GitHub Enterprise Cloud, you'll receive events for 7 days prior to connection.