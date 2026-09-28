---
layout: Conceptual
title: Deploy GitHub Advanced Security Integration with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/github-advanced-security-deploy
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
description: Use this step-by-step guide to integrate GitHub Advanced Security with Microsoft Defender for Cloud for code-to-runtime security.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ff53c406-f753-a103-cfa7-93b24a5f3ae8
document_version_independent_id: 0cd60343-b6fe-12f7-1c11-33d6929fd4a1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/github-advanced-security-deploy.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/github-advanced-security-deploy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/github-advanced-security-deploy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d4d610ea-c1f9-9394-df59-77b9b394e89e
---

# Deploy GitHub Advanced Security Integration with Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This guide provides setup steps and other actions to help you integrate GitHub Advanced Security (GHAS) and Microsoft Defender for Cloud, then validate the integration end to end. The integration helps maximize Microsoft's cloud-native application security by correlating runtime risks and context with the originating code for faster AI-powered remediation.

By following this guide, you:

- Set up your GitHub repository for Defender for Cloud coverage.
- Create a runtime risk factor.
- Test real use cases in Defender for Cloud.
- Link code to runtime resources.
- Start a security campaign on GitHub. This campaign uses runtime context to prioritize GHAS security alerts.
- Create GitHub issues from Defender for Cloud to start remediation.
- Close the loop between engineering and security teams.

## Prerequisites

| Aspect | Details |
| --- | --- |
| Environmental requirements | - GitHub account with a connector created in Defender for Cloud- GitHub Advanced Security (GHAS) license on connected repositories- Defender Cloud Security Posture Management (DCSPM) plan enabled on the subscription- Microsoft Security Copilot (optional for AI-powered automated remediation) |
| Roles and permissions | - Security Admin permissions- Security Admin on the Azure subscription to view findings in Defender for Cloud- GitHub organization owner for connecting repositories and configuring security campaigns |
| Cloud environments | - Available in commercial clouds only (not in Azure Government, Azure operated by 21Vianet, or other sovereign clouds) |

## Prepare your environment

Complete the following steps to configure your GitHub repository and Defender for Cloud settings before you validate the integration.

### Step 1: Set up the GitHub repository and run the workflow

To test the integration, use your own repositories or an [example sandbox project](github-advanced-security-deploy-sandbox). The sandbox project provides a test GitHub repository with everything you need to build a vulnerable container image.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **DevOps security**.
3. Enter your code repo name in the search bar, for example, *zava-webshop*.
4. Validate that it belongs to the organization you're monitoring, for example, the **zava-corporation** organization.
5. Review if there are any findings for the repo.
6. Ensure **Advanced security status** is **On**. This setting indicates that GitHub Advanced Security is enabled on the monitored repository.
7. If your repository isn't found, see the [GitHub connector onboarding quickstart](quickstart-onboard-github) for troubleshooting and setup guidance.
8. Make sure that agentless scanning is turned on for your GitHub connector.

    [![Screenshot of Plan Configuration in Defender CSPM with Agentless code scanning toggled on and all scanner options enabled.](media/github-advanced-security-deploy/agentless-scan.png)](media/github-advanced-security-deploy/agentless-scan.png#lightbox)

### Step 2: Validate that your environment is ready

This environment validation confirms that your repository and cloud resources are set up correctly. It checks that Defender can show code-to-runtime recommendations and produce useful results. During the environment validation step, Defender verifies that:

- Microsoft Defender for Cloud continuously monitors source code repositories for security vulnerabilities.
- Build artifacts, such as container images, are scanned in container registries before deployment.
- Runtime workloads deployed to Kubernetes clusters are monitored for security risks.
- Defender for Cloud correlates and traces each artifact from code, through build and deployment, to runtime and back.

Note

It can take up to 24 hours after the previous steps are applied to see results. 

#### Validate full code-to-runtime visibility

Test that [GitHub agentless scanning](agentless-code-scanning) picks up the repository.

Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer** and perform the query. The validation queries test whether Defender can identify artifacts produced by your pipelines and workloads. If the queries return results, it indicates that scanning and correlation are working as expected.

[![Screenshot of Defender for Cloud's Cloud Security Explorer showing a query for GitHub repository pushes to container images.](media/github-advanced-security-deploy/validate-mdc-container-scan-results.jpg)](media/github-advanced-security-deploy/validate-mdc-container-scan-results.jpg#lightbox)

Note

If no results are returned, it might indicate that artifacts aren't yet generated, scanning isn't configured, or permissions are missing. See [User roles and permissions](permissions) for more information.

1. In Azure Container Registry, validate that Defender for Cloud scanned the container image and used it to create a container.
2. In your query, add the conditions for your specific deployment.

    [![Screenshot of Defender for Cloud's Cloud Security Explorer showing a query for GitHub repository pushes to container images with vulnerabilities.](media/github-advanced-security-deploy/github-repo-container-vulnerabilities.jpg)](media/github-advanced-security-deploy/github-repo-container-vulnerabilities.jpg#lightbox)
3. Validate that the container is running and that Defender for Cloud scanned the AKS cluster.

    [![Screenshot of Defender for Cloud's Cloud Security Explorer showing a query for GitHub pushes to container images with vulnerabilities.](media/github-advanced-security-deploy/github-repo-container-scan-aks.jpg)](media/github-advanced-security-deploy/github-repo-container-scan-aks.jpg#lightbox)
4. Validate that the risk factors are configured correctly on the Defender for Cloud side. Search for your container name on the Defender for Cloud inventory page. You should see it marked as critical.

Note

This step is required only if risk factors aren't already configured in your environment. If you already use risk factors, you can verify their configuration under **Settings** &gt; **Resource criticality**.

Successful validation ensures that next steps, such as recommendations, campaigns, and GitHub issue generation, produce meaningful results.

Note

After you classify your resource as critical, it can take up to 12 hours for Defender for Cloud to send the data to GitHub. For more information, see [Prioritizing Dependabot and code scanning alerts](https://docs.github.com/en/code-security/securing-your-organization/understanding-your-organizations-exposure-to-vulnerabilities/alerts-in-production-code).

### Step 3: Create a GitHub campaign

To create a scanning campaign, work at the GitHub organization level. This experience isn't available at the individual repository level.

1. In GitHub, go to the GitHub organization that you used for the setup testing.
2. Select **Security** &gt; **Campaigns** &gt; **Create campaign** &gt; **From code scanning filters**.

    The runtime-risk campaign helps prioritize GitHub Advanced Security (GHAS) findings that belong to code that is truly deployed and running.
3. Select **Runtime Risks** filters for the campaign.

    [![Screenshot of GitHub code scanning campaign creation with a filter bar, Filter button, and a tooltip about filtering by artifact metadata.](media/github-advanced-security-deploy/select-filters.png)](media/github-advanced-security-deploy/select-filters.png#lightbox)

    [![Screenshot of advanced filters dialog in GitHub campaign creation with Runtime Risk filter and selectable risk factors menu open.](media/github-advanced-security-deploy/advanced-filters.png)](media/github-advanced-security-deploy/advanced-filters.png#lightbox)
4. Select **Save** &gt; **Publish as campaign**. Enter the required information and then publish the campaign.
5. Track campaign advancement.

    [![Screenshot of GitHub campaign page showing overdue status, campaign progress bar, critical alerts list, and filter options.](media/github-advanced-security-deploy/test-campaign.png)](media/github-advanced-security-deploy/test-campaign.png#lightbox)

### Step 4: Act on recommendations

Use the running Containers VA recommendations code-to-runtime functionality and correlation of the identified CVEs to **Dependabot** security alerts to understand the status of security issues. You can then assign the recommendation for resolution to the relevant engineering team based on code-to-runtime mapping.

1. In the Defender for Cloud portal, go to the **Recommendations** tab.
2. Search for the name of the container that you created from your code repo.
3. Open one of the **Update software** recommendations. The recommendation name begins with **Update**.
4. Select **Associated CVEs**.

    Security alerts appear as part of the recommendation evaluation flow. These alerts provide indications about GitHub Advanced Security findings that are already known to engineering. Some CVE IDs have a View on GitHub link in the Related GitHub Alerts column.

    [![Screenshot of Defender for Cloud Findings tab showing CVE-2024-21409 alerts, fix status, CVSS scores, and GitHub alert details popup.](media/github-advanced-security-deploy/findings.png)](media/github-advanced-security-deploy/findings.png#lightbox)

Select the link to open the relevant GHAS security alert. To view the GHAS alert content in GitHub, you must have access permissions to the relevant GitHub repository. If you don't have access permissions, you can always copy the link for next usage or contact your GitHub administrator.

If the **Related GitHub Alerts** column shows a matched Dependabot alert, the vulnerability is already known to engineering. If the alert status is **Active**, no one fixed it yet, and the issue needs to be prioritized for a fix.

If no matched GitHub alert appears in the column, the CVE represents a runtime risk unknown to engineering that needs to be prioritized for a fix.

#### Create a GitHub issue

To close the loop between security and engineering teams, you can create a GitHub issue that prioritizes the security issues that the engineering team should focus on. This prioritization can include passing findings that GHAS didn't pick up but that Defender for Cloud detected for CVE IDs that aren't part of direct dependencies. These findings can include vulnerabilities in the base image, operating system, or software like NGINX.

The GitHub issue is automatically generated in the source code repository with all the CVE IDs found in the scope of the recommendation, including other runtime and container SDLC-related contexts that can help with the fix and testing.

From the recommendation view, you can explicitly generate a GitHub issue to track remediation work.

1. Go to **Remediation Insights** and view the code-to-runtime diagram. The diagram maps your running container to the container image in the code repository and to the code repository of origin in GitHub.

    [![Screenshot of Remediation Insights showing code-to-runtime diagram with risk levels and Take Action menu open on the Runtime box.](media/github-advanced-security-deploy/code-runtime-flow-diagram.png)](media/github-advanced-security-deploy/code-runtime-flow-diagram.png#lightbox)

    1. On the **Remediation Insights** tab, review the affected **Runtime** box.
    2. **Validate whether a GitHub issue already exists**. If a GitHub issue already exists, a GitHub icon is displayed on the box. Hover over the icon to view issue details.
    3. If no issue exists and you have the required permissions, you can generate a new GitHub issue. Select **Take action**.
    4. Select the **Generate GitHub issue** option from the popup.
    5. If the issue was created successfully, you see a popup notification with a link to the issue. The issue is created in the code repository of origin.

        [![Screenshot of GitHub issues list showing open issues for dependencies with labels like Defender for Cloud and security.](media/github-advanced-security-deploy/link-issue.png)](media/github-advanced-security-deploy/link-issue.png#lightbox)

    Note

    If the **Generate GitHub** issue option isn't available, you might lack GitHub or repository permissions. Contact your GitHub or repository administrator to request access.

    [![Screenshot showing a generated GitHub issue for an open dependency with Defender for Cloud and security labels.](media/github-advanced-security-deploy/github-issue.png)](media/github-advanced-security-deploy/github-issue.png#lightbox)

    1. Track ownership and status updates. Changes to issue status or assignment made in GitHub are reflected in Microsoft Defender for Cloud. This fact allows you to track ownership and remediation progress from the **Recommendations** view.

        [![Screenshot of Microsoft Defender for Cloud Recommendations page showing high-risk issues with GitHub issue details popup.](media/github-advanced-security-deploy/recommendations-pane.png)](media/github-advanced-security-deploy/recommendations-pane.png#lightbox)

## Make agentic fixes

If you have a GitHub Copilot license, you can resolve the issue with the help of the GitHub coding agent:

1. Assign a GitHub coding agent to the issue.
2. Review the generated fix.
3. If the fix seems reasonable, apply it.
4. Observe as Defender for Cloud updates the issue status to **Closed**.