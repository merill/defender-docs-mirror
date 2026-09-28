---
layout: Conceptual
title: Add Defender for Cloud data to Power BI - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/add-data-power-bi
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
description: Learn how to connect Power BI to Microsoft Defender for Cloud to gain enhanced value from the data collected by Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
locale: en-us
document_id: 68c14d64-b724-e334-d6c3-49110e538bbe
document_version_independent_id: c1bc14c6-489b-628d-84b7-78f409200b3a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/add-data-power-bi.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/add-data-power-bi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/add-data-power-bi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3197845-b4ce-44c6-a237-cd4be160e76c
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3928677-9b71-43a6-875f-004dc4f98b65
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/aea905fb-0a9d-4d46-b30f-e9cbaf772d1b
- https://authoring-docs-microsoft.poolparty.biz/devrel/6bbc70ca-58b2-4c69-8249-28ec92c08029
platformId: 2210f67e-07ac-4cf7-30ed-bf7c18123f06
---

# Add Defender for Cloud data to Power BI - Microsoft Defender for Cloud | Microsoft Learn

You can connect Microsoft Defender for Cloud data to Microsoft Power BI. Use this setup to track security metrics and spot threats. This article shows how to link Defender for Cloud to Power BI and create clear visuals from your security data. Before you begin, review the prerequisites to ensure you have the required setup and permissions.

## Prerequisites

Before you connect Defender for Cloud data to Power BI, make sure you complete the following prerequisites:

- [Download and install Power BI Desktop](https://www.microsoft.com/power-platform/products/power-bi/desktop).
- Ensure you have the correct [permissions to access Azure Resource Graph](/en-us/azure/governance/resource-graph/overview#permissions-in-azure-resource-graph).

## Connect Power BI to Azure Resource Graph

To connect Power BI to Azure Resource Graph:

1. On your desktop open Power BI Desktop.
2. Select **Blank report**.
3. Select **Get data** &gt; **more**.

    [![Screenshot of the Power BI Desktop main screen that shows where the get data button is located and the more option.](media/add-data-power-bi/get-data-more.png)](media/add-data-power-bi/get-data-more.png#lightbox)
4. Search for and select **Azure Resource Graph**.
5. Select **Connect**.

## Query Defender for Cloud data into Power BI

Use Azure Resource Graph queries in Power BI to retrieve Defender for Cloud data. To query Defender for Cloud data into Power BI:

### Run Defender for Cloud queries

Once Power BI Desktop is connected to Azure Resource Graph, you can use Azure Resource Graph to query various data sources from Defender for Cloud into Power BI.

The following sample queries are examples that return sample results. Azure Resource Graph supports many data queries, and you can customize them to meet your requirements.

1. Copy and paste one of the provided queries into the query editor in Power BI Desktop.

# [Recommendations by risk](#tab/Recommendations-by-risk)
This query retrieves security recommendations by risk from Defender for Cloud, allowing you to analyze assessments and identify areas that need attention.

    ```kusto
    securityresources 
            | where type =~ "microsoft.security/assessments"
            | extend assessmentType = iff(type == "microsoft.security/assessments", tostring(properties.metadata.assessmentType), dynamic(null))
            | where (type == "microsoft.security/assessments" and (assessmentType in~ ("BuiltIn", "CustomerManaged")))
            | extend assessmentTypeSkimmed = iff(type == "microsoft.security/assessments", case(
                        tostring(properties.metadata.assessmentType) == "BuiltIn", "BuiltIn",
                        tostring(properties.metadata.assessmentType) == "BuiltInPolicy", "BuiltIn",
                        tostring(properties.metadata.assessmentType) == "CustomPolicy", "Custom",
                        tostring(properties.metadata.assessmentType) == "CustomerManaged", "Custom",
                        tostring(properties.metadata.assessmentType) == "ManualCustomPolicy", "Custom",
                        tostring(properties.metadata.assessmentType) == "ManualBuiltInPolicy", "BuiltIn",
                        dynamic(null)
                    ), dynamic(null))
            | extend assessmentId = tolower(id)
            | extend assessmentKey = iff(type == "microsoft.security/assessments", name, dynamic(null))
            | extend source = iff(type == "microsoft.security/assessments", trim(' ', tolower(tostring(properties.resourceDetails.Source))), dynamic(null))
            | extend statusCode = iff(type == "microsoft.security/assessments", tostring(properties.status.code), dynamic(null))
            | extend resourceId = iff(type == "microsoft.security/assessments", trim(" ", tolower(tostring(case(source =~ "azure", properties.resourceDetails.Id,
                (type == "microsoft.security/assessments" and (source =~ "aws" and isnotempty(tostring(properties.resourceDetails.ConnectorId)))), properties.resourceDetails.Id,
                (type == "microsoft.security/assessments" and (source =~ "gcp" and isnotempty(tostring(properties.resourceDetails.ConnectorId)))), properties.resourceDetails.Id,
                source =~ "aws", properties.resourceDetails.AzureResourceId,
                source =~ "gcp", properties.resourceDetails.AzureResourceId,
                extract("^(?i)(.+)/providers/Microsoft.Security/assessments/.+$",1,id)
                )))), dynamic(null))
            | extend resourceName = iff(type == "microsoft.security/assessments", tostring(coalesce(properties.resourceDetails.ResourceName, properties.additionalData.CloudNativeResourceName, properties.additionalData.ResourceName, properties.additionalData.resourceName, split(resourceId, '/')[-1], extract(@"(.+)/(.+)", 2, resourceId))), dynamic(null))
            | extend resourceType = iff(type == "microsoft.security/assessments", tolower(properties.resourceDetails.ResourceType), dynamic(null))
            | extend riskLevelText = iff(type == "microsoft.security/assessments", tostring(properties.risk.level), dynamic(null))
            | extend riskLevel = iff(type == "microsoft.security/assessments", case(riskLevelText =~ "Critical", 4,
                      riskLevelText =~ "High", 3,
                      riskLevelText =~ "Medium", 2,
                      riskLevelText =~ "Low", 1,
                      0), dynamic(null))
            | extend riskFactors = iff(type == "microsoft.security/assessments", iff(isnull(properties.risk.riskFactors), dynamic([]), properties.risk.riskFactors), dynamic(null))
            | extend attackPaths = array_length(iff(type == "microsoft.security/assessments", iff(isnull(properties.risk.attackPathsReferences), dynamic([]), properties.risk.attackPathsReferences), dynamic(null)))           
            | extend displayName = iff(type == "microsoft.security/assessments", tostring(properties.displayName), dynamic(null))
            | extend statusCause = iff(type == "microsoft.security/assessments", tostring(properties.status.cause), dynamic(null))
            | extend isExempt = iff(type == "microsoft.security/assessments", iff(statusCause == "Exempt", tobool(1), tobool(0)), dynamic(null))
            | extend statusChangeDate = tostring(iff(type == "microsoft.security/assessments", todatetime(properties.status.statusChangeDate), dynamic(null)))
            | project assessmentId,
                        statusChangeDate,
                        isExempt,
                        riskLevel,
                        riskFactors,
                        attackPaths,
                        statusCode,
                        displayName,
                        resourceId,               
                        assessmentKey,
                        resourceType,
                        resourceName,
                        assessmentTypeSkimmed               
                | join kind=leftouter (
                    securityresources
                    | where type == 'microsoft.security/assessments/governanceassignments'
                    | extend assignedResourceId = tolower(iff(type == "microsoft.security/assessments/governanceassignments", tostring(properties.assignedResourceId), dynamic(null)))
                    | extend dueDate = iff(type == "microsoft.security/assessments/governanceassignments", todatetime(properties.remediationDueDate), dynamic(null))
                    | extend owner = iff(type == "microsoft.security/assessments/governanceassignments", iff(isempty(tostring(properties.owner)), "unspecified", tostring(properties.owner)), dynamic(null))
                    | extend governanceStatus = iff(type == "microsoft.security/assessments/governanceassignments", case(
                                isnull(todatetime(properties.remediationDueDate)), "NoDueDate",
                                todatetime(properties.remediationDueDate) >= bin(now(), 1d), "OnTime",
                                "Overdue"
                            ), dynamic(null))
                    | project assignedResourceId, dueDate, owner, governanceStatus
                ) on $left.assessmentId == $right.assignedResourceId
                | extend completionStatusNumber = case(governanceStatus == "Overdue", 5,
                                                           governanceStatus == "OnTime", 4,
                                                           statusCode == "Unhealthy", 3, 
                                                           isExempt, 7,
                                                           1)
                    | extend completionStatus = case(completionStatusNumber == 5, "Overdue",
                                                     completionStatusNumber == 4, "OnTime",
                                                     completionStatusNumber == 3, "Unassigned",
                                                     completionStatusNumber == 7, "Exempted",
                                                     "Completed")
                | where completionStatus in~ ("OnTime","Overdue","Unassigned")
                | project-away assignedResourceId, governanceStatus, isExempt
                           | order by riskLevel desc, attackPaths desc, displayName
    ```

# [Attack Paths](#tab/attack-paths)
Use this query to fetch attack path data, providing insights into potential attack vectors within your cloud environment.

    ```kusto
    securityresources
    | where type == "microsoft.security/attackpaths"
    | extend riskCategories = tostring(properties.riskCategories)
    | extend riskCategories = tostring(split(riskCategories, "[")[1])
    | extend riskCategories = tostring(split(riskCategories, "]")[0])
    | extend riskCategory = iff('{riskCategories}' == "All", riskCategories, '{riskCategories}')
    | where riskCategories has(riskCategory)
    | project apId = name, apTemplate = tostring(properties.displayName), riskCategories
    | summarize Path_Count = count() by Attack_Path = apTemplate, riskCategories
    | project Attack_Path, Path_Count, riskCategories
    ```

# [Secure Score](#tab/secure-score)
This query retrieves secure score data, helping you understand your overall security posture and prioritize remediation efforts.

    ```Kusto
    securityresources 
    | where type == "microsoft.security/securescores" 
    | where name == "ascScore"
    | extend environment = tostring(properties.environment)
    | extend scopeMaxScore = toint(properties.score.max)
    | extend scopeWeight = toint(properties.weight)
    | extend scopeScorePerc = round(todouble(properties.score.percentage), 0)
    ```

# [Governance](#tab/governance)
Use this query to get data on governance rules, enabling you to manage compliance and governance policies effectively.

    ```kusto
    securityresources         
    | where type == "microsoft.security/assessments"
    | where isnull(properties.resourceDetails.AwsResourceId) and isnull(properties.resourceDetails.GcpResourceId)
    | extend DisplayName = tostring(properties.displayName)
    | where isempty(DisplayName) == false
    | join kind=leftouter   (securityresources         
    | where type == "microsoft.security/assessments/governanceassignments"
    | extend  assignedResourceId = tostring(todynamic(properties).assignedResourceId)
    | extend remediationDueDate = todatetime(properties.remediationDueDate)
    | project id = assignedResourceId, governanceassignmentsProperties = todynamic(properties), remediationDueDate) on id
    | extend hasAssignment = isempty( governanceassignmentsProperties) == false and isnull( governanceassignmentsProperties) == false
    | extend assignmentStatus = iif(tostring(properties.status.code) == "Unhealthy",iif(hasAssignment == true, iif(bin(remediationDueDate, 1d) < bin(now(), 1d), "Overdue", "Ontime"), "Unassigned") , "Completed")
    | summarize count() by assignmentStatus
    ```

# [Compliance](#tab/compliance)
This query retrieves compliance data from Defender for Cloud, which is essential for maintaining and demonstrating adherence to various regulatory requirements.

    ```kusto
    securityresources
    | where type == "microsoft.security/regulatorycompliancestandards/regulatorycompliancecontrols/regulatorycomplianceassessments" | extend scope = properties.scope
    | where isempty(scope) or  scope in~("Subscription", "MultiCloudAggregation")
    | parse id with * "regulatoryComplianceStandards/" complianceStandardId "/regulatoryComplianceControls/" complianceControlId "/regulatoryComplianceAssessments" *
    | extend complianceStandardId = replace( "-", " ", complianceStandardId)
    | extend Status = properties.state
    ```

---
2. Select **Ok**.

    [![Screenshot that shows where to enter the Azure Resource Graph query and where the Ok button is located.](media/add-data-power-bi/select-ok.png)](media/add-data-power-bi/select-ok.png#lightbox)

    Note

    By default, Resource Graph limits any query to returning only 1,000 records. This control protects both you and the service from unintentional queries that would result in large data sets. If you want query results not to be truncated by the 1,000 records limit, set the value of the "Advanced Option - $resultTruncated (optional)" to FALSE.

    [![Screenshot that shows where the advanced options are located and how to set it to false.](media/add-data-power-bi/advanced-options-false.png)](media/add-data-power-bi/advanced-options-false.png#lightbox)
3. Select **Load**.