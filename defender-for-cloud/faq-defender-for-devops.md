---
layout: FAQ
title: Common questions -  DevOps Security - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/faq-defender-for-devops
summary: >
  <p>Get answers to common questions about Microsoft DevOps Security.</p>
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Get answers to frequently asked questions about Microsoft DevOps Security.
ms.topic: faq
ms.date: 2025-05-18T00:00:00.0000000Z
locale: en-us
document_id: 97409b0d-8205-45da-4349-4494a17d5393
document_version_independent_id: b8cb28f7-12fd-09ee-63ee-653e975180c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/faq-defender-for-devops.yml
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: faq
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/faq-defender-for-devops
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/faq-defender-for-devops.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bd2b3fa-c186-4b92-a3c8-09f22a249d37
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/7eba7926-b7b2-4a7a-bf89-e6ac53b3e7f6
platformId: 820af462-7a10-ba8a-f7b3-dcbb3fd616de
---

# Common questions -  DevOps Security - Microsoft Defender for Cloud | Microsoft Learn

Get answers to common questions about Microsoft DevOps Security.

## Why am I getting an error while trying to connect?

When you select the *Authorize* button, the account that you're logged in with is used. That account can have the same email but might have a different tenant. Make sure you have the right account/tenant combination selected in the popup consent screen and Visual Studio.

You can [check which account is signed in](https://app.vssps.visualstudio.com/profile/view).

## Why can't I find my Azure DevOps repository?

The Defender for Cloud DevOps security onboarding only supports the repository type `TfsGit`. The repository type `TFSVC` isn't supported today.

Ensure that you have [onboarded your repositories](quickstart-onboard-devops?branch=main) to Microsoft Defender for Cloud. If you still can't see your repository, ensure that you're signed in with the correct Azure DevOps organization user account. Your Azure subscription and Azure DevOps Organization need to be in the same tenant. If the user for the connector is wrong, you need to delete the previously created connector, sign in with the correct user account and re-create the connector.

## Why don't I see the generated SARIF file in the path I chose to drop it?

If you don't see SARIF file in the expected path, you might have chosen a different drop path than the `CodeAnalysisLogs/msdo.sarif` one. Currently you should drop your SARIF files to `CodeAnalysisLogs/msdo.sarif`.

## Why don't I see the results for my Azure DevOps Projects in Microsoft Defender for Cloud?

When you use classic pipeline configuration, make sure you don't change artifact name. This can result not seeing the results for your project. You can learn more about how to [Review your findings](defender-for-devops-introduction).

## I successfully onboarded a DevOps connector, where can I find my related recommendations?

We recommend navigating to the DevOps Security pane to see an overview of your DevOps security posture. You can sort and filter by the DevOps resource you care about to see the recommendation details.

You can also use the [DevOps Workbook](custom-dashboards-azure-workbooks#use-the-devops-security-workbook) and customize it for your needs.

## What information does the DevOps security product store about me and my enterprise, and where is the data stored and processed?

DevOps security features connect to your source code management system, for example, Azure DevOps, GitHub, and/or GitLab to provide a central console for your DevOps resources and security posture. DevOps security features processes and stores the following information:

- Metadata on your connected source code management systems and associated repositories. This data includes user, organizational, and authentication information.
- Scan results for recommendations and details.

DevOps security features are a part of [Microsoft Defender for Cloud](defender-for-cloud-introduction). Refer to the following [data residency guidance](https://azure.microsoft.com/explore/global-infrastructure/data-residency/#select-geography) and [EU Data Boundary details](/en-us/privacy/eudb/eu-data-boundary-permanent-transfers-from-services#security-services) as it relates to the Microsoft Defender for Cloud service.

DevOps security doesn't process or store your code, build, and audit logs today but might in the future as it expands its capabilities.

Learn more about [Microsoft Privacy Statement](https://www.microsoft.com/privacy/privacystatement).

## For my Azure DevOps connector, why are write permissions required for work items, build, code, service hooks, and advanced security?

These permissions are required for certain DevOps security features, such as pull request annotations, to work.

## Is the recommendation exemptions capability available and tracked for application security vulnerability management?

Exemptions aren't available for DevOps security recommendations within Microsoft Defender for Cloud at the moment.

## Why am I not able to see GitHub Advanced Security for Azure DevOps (GHAzDO) results in Defender for Cloud?

Confirm your connectors is properly authorized.

Ensure you're using the same Subscription ID for GHAzDO and Defender for Cloud. If you're still unable to see the results, the issue might be caused by your ADO connector lacking the necessary scope. DevOps security introduced new scopes to Azure DevOps connectors in June. If you created the connector before June and haven't updated it, you won't be able to see GHAzDO results due to missing scope on the connector. You would need to create a new ADO connector, which will automatically include the new scopes.

Ensure the user permissions for the Microsoft Defender for DevOps have `Advanced Security: view alerts` and `Read` set to `Allow`. These permissions might have changed if the "Inheritance" toggle was switched off. If the necessary permissions are set to `Not set` or `Deny`, they'll need to be manually updated to `Allow` otherwise the GHAzDO findings won't show up in Defender for Cloud recommendations.

[![Screenshot that shows advanced security permissions.](media/faq-defender-for-devops/devops-user-permissions-set.png)](media/faq-defender-for-devops/devops-user-permissions-set.png#lightbox)

## Is continuous, automatic scanning available?

Currently, scanning occurs at build time.

## Why am I not able to configure Pull Request Annotations?

Make sure you have write (owner/contributor) access to the subscription. If you don't have this type of access today, you can get it through [activating a Microsoft Entra role in PIM](/en-us/azure/active-directory/privileged-identity-management/pim-how-to-activate-role).

## What programming languages are supported by DevOps security features?

The following languages are supported by DevOps security features:

- Python
- JavaScript
- TypeScript

For a list of languages supported by GitHub Advanced Security, see [here](https://codeql.github.com/docs/codeql-overview/supported-languages-and-frameworks/).

## Can I migrate the connector to a different region?

For example, can I migrate the connector from the Central US region to the West Europe region?

We don't support automatic migration for the DevOps security connectors from one region to another at this time.

If you want to move the location of a DevOps connector to different region, the recommendation is to delete the existing connector and then to recreate the connector in the new region.

## Do API calls made by Defender for Cloud count against my consumption limit?

Yes, API calls made by Defender for Cloud count against the [Azure DevOps Global consumption limit](/en-us/azure/devops/integrate/concepts/rate-limits). Defender for Cloud makes calls on-behalf of the user who onboards the connector.

## Why is my organization list empty in the UI?

If your organization list is empty in the UI after you onboarded an Azure DevOps connector, you need to ensure that the organization in Azure DevOps is connected to the Azure tenant that has the user who authenticated the connector.

For information on how to correct this issue, check out the [DevOps trouble shooting guide](troubleshooting-guide#troubleshoot-connector-problems-for-the-azure-devops-organization).

## I have a large Azure DevOps organization with many repositories. Can I still onboard?

Yes, there's no limit to how many Azure DevOps repositories you can onboard for DevOps security capabilities.

However, there are two main implications when onboarding large organizations – speed and throttling. The speed of discovery for your DevOps repositories is determined by the number of projects for each connector (approximately 100 projects per hour). Throttling can happen because Azure DevOps API calls have a [global rate limit](/en-us/azure/devops/integrate/concepts/rate-limits) and we limit the calls for project discovery to use a small portion of overall quota limits.

Consider using an alternative Azure DevOps identity (that is, an Organization Administrator account used as a service account) to avoid individual accounts from being throttled when onboarding large organizations. Below are some scenarios of when to use an alternate identity to onboard a DevOps security connector:

- Large number of Azure DevOps Organizations and Projects (~500 Projects or more).
- Large number of concurrent builds that peak during work hours.
- Authorized user is a [Power Platform](/en-us/power-platform/) user making extra Azure DevOps API calls, using up the global rate limit quotas.

Once you have onboarded the Azure DevOps repositories using this account and [configured and ran the Microsoft Security DevOps Azure DevOps extension](configure-azure-devops-extension) in your CI/CD pipeline, then the scanning results will appear near instantaneously in Microsoft Defender for Cloud.