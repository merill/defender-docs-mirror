---
layout: Conceptual
title: Enable Attack Disruption Actions on AWS with Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/aws-disruption
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Configure your AWS environment so Microsoft Sentinel can take automated attack disruption actions on SAML-assumed roles or IAM accounts when alerts are triggered.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: eyalhaik
ms.date: 2026-07-01T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b222617a-23b8-2309-da42-558a5d6ff318
document_version_independent_id: b12552c0-610f-e399-16cb-940dc1171ccb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/aws-disruption.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/aws-disruption
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/aws-disruption.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 185d3341-91d5-4e04-8da1-7966ea8fcac2
---

# Enable Attack Disruption Actions on AWS with Microsoft Sentinel | Microsoft Learn

This article describes how to configure your AWS environment so that Microsoft Sentinel can take automated actions on a user that assumes a SAML role, or on an AWS IAM account when an alert is triggered. [Automatic attack disruption in Microsoft Defender XDR](/en-us/defender-xdr/automatic-attack-disruption) uses high-confidence signals to contain compromised assets and limit the damage from attacks, including actions on identities in AWS. Before you begin, make sure the required AWS and Microsoft Sentinel prerequisites are in place.

## Prerequisites

Before you begin, you need the following prerequisites in place:

- You have an active AWS account with administrative privileges.
- Your Microsoft Sentinel analytic workspace is connected to the unified security operations portal.
- The AWS Connector for Microsoft Sentinel is deployed and enabled.
- AWS CloudTrail logs are being ingested into Microsoft Sentinel; see [Connect Microsoft Sentinel to Amazon Web Services to ingest AWS service log data](connect-aws).
- Appropriate IAM roles and permissions are configured in AWS to allow Microsoft Sentinel to perform actions on IAM accounts.
- The Amazon Web Services solution is installed from Content Hub in Microsoft Sentinel so that the **Amazon Web Services S3** connector appears in the data connectors gallery.

## Step 1: Prepare AWS for integration

Complete the following tasks to prepare your AWS environment for Microsoft Sentinel integration.

### 1.1 Create a dedicated IAM role for Microsoft Sentinel

[Create a new IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create.html) in the AWS Management Console.

1. Select **AWS service** as the trusted entity and choose **EC2** as a temporary placeholder. You replace this trust relationship with the correct Microsoft Sentinel principal in Configure trust relationship.
2. Attach the following IAM policy to the role. This policy grants Microsoft Sentinel the permissions needed to manage IAM user and role policies for attack disruption actions. Replace &lt;YOUR\_ACCOUNT\_ID&gt; as needed:

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "iam:GetUserPolicy",
            "iam:DeleteRolePolicy",
            "iam:PutUserPolicy",
            "iam:AttachUserPolicy",
            "iam:ListUserPolicies",
            "iam:PutRolePolicy",
            "iam:GetUser",
            "iam:DetachUserPolicy",
            "iam:GetRolePolicy",
            "iam:DeleteUserPolicy", 
         ],
         "Resource": "*"
        }
      ]
    }
    ```

### 1.2 Configure trust relationship

Create a [custom trust policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-custom.html#roles-creatingrole-custom-trust-policy-console) for the IAM role.

Use the following trust policy, specifying the Microsoft Sentinel integration principal (replace `<YOUR_AZURE_SUBSCRIPTION_ID>` with your actual Azure subscription ID):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com",
        "AWS": "arn:aws:iam::<YOUR_AZURE_SUBSCRIPTION_ID>:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## Step 2: Enable CloudTrail

Enable CloudTrail logging in all AWS regions so that Microsoft Sentinel can receive the required activity data.

1. In the AWS console, go to **CloudTrail**.
2. Ensure that a CloudTrail is enabled and logging is active for all regions.

## Step 3: Deploy and enable the AWS connector in Microsoft Sentinel

Deploy and enable the AWS S3 data connector in Microsoft Sentinel so that it can receive log data from your AWS environment. Before you begin, make sure the Amazon Web Services solution is installed from Content Hub in Microsoft Sentinel so that the **Amazon Web Services S3** connector appears in the data connectors gallery.

1. In the Azure portal, go to **Microsoft Sentinel &gt; Data connectors**.
2. Select **Amazon Web Services S3** from the data connectors gallery.
3. Follow the instructions in [Connect Microsoft Sentinel to Amazon Web Services to ingest AWS service log data](connect-aws) to set up your AWS environment and connect it to Microsoft Sentinel.
4. Provide the IAM role ARN and the Amazon SQS queue URL that receives S3 log notifications from your AWS environment. These values are created when you set up the connector by following [Connect Microsoft Sentinel to Amazon Web Services to ingest AWS service log data](connect-aws).

## Step 4: Validate integration

Use the following checks to confirm that the AWS connector integration is working correctly.

1. In Microsoft Sentinel, confirm that the connector status is **Connected**.
2. Verify log ingestion and connector health using the SentinelHealth diagnostic table, which reports connector and ingestion health status in your Log Analytics workspace. Also check the AWS SQS queue status to confirm that log notifications are being processed.
3. In AWS, check that CloudTrail and GuardDuty events are being sent to Microsoft Sentinel.

## Step 5: Test the integration

Perform the following test to verify that automated attack disruption response actions work as expected.

1. Trigger a test alert in AWS (for example, simulated credential compromise).
2. Confirm that Microsoft Sentinel can take the configured actions on the affected IAM account.
3. Review audit logs in AWS and Microsoft Sentinel to verify successful execution.

## Step 6: Monitor and maintain

Use the following practices to monitor and maintain the integration over time.

- Regularly review IAM role permissions and audit logs in AWS.
- Update Microsoft Sentinel analytic rules and automation playbooks as needed to reflect changes in your AWS environment.
- Monitor alerts and response actions in the Microsoft Sentinel portal.

The following scripts automate the AWS IAM role and OIDC provider setup for integrating Microsoft Sentinel with AWS to enable attack disruption:

# [Bash Script](#tab/bash)
The following Bash script automates the AWS OIDC provider configuration and IAM role creation for Microsoft Sentinel integration. Before you run it, ensure that the AWS CLI is installed and authenticated with an account that has IAM administrative permissions. Save the code snippet as a bash file and execute it.

```bash
#!/bin/bash
# AWS Sentinel OIDC Setup Script
# Configures IAM roles and policies for Microsoft Sentinel integration

set -e  # Exit on error

# Color codes for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
CYAN='\033[0;36m'
NC='\033[0m' # No Color

ms_federated_endpoint="sts.windows.net/33e01921-4d64-4f8c-a055-5bdaffd5e33d"
actions_audience="api://b7c1e142-0933-4310-ba00-8b28878bfece"
role_name="OIDC_Actions_Sentinel"
policy_name="SentinelActionsPolicy"

# Verify AWS credentials are configured
echo -e "${CYAN}Verifying AWS credentials...${NC}"
if ! account_id=$(aws sts get-caller-identity --query Account --output text 2>&1); then
    echo -e "\n${RED}ERROR: AWS credentials not configured or invalid${NC}"
    echo -e "${RED}Details: $account_id${NC}"
    echo -e "\n${YELLOW}Please authenticate using one of these methods:${NC}"
    echo -e "${YELLOW}  1. Run 'aws configure' to set up credentials${NC}"
    echo -e "${YELLOW}  2. Set AWS environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY)${NC}"
    echo -e "${YELLOW}  3. Use 'aws sso login --profile <profile-name>' for SSO${NC}"
    exit 1
fi
echo -e "${GREEN}✓ AWS authenticated (Account: $account_id)${NC}"
trust_policy_document=$(cat << EOM
{
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "arn:aws:iam::$account_id:oidc-provider/$ms_federated_endpoint/"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "$ms_federated_endpoint/:aud": "$actions_audience",
                    "sts:RoleSessionName": "MicrosoftSentinel_$account_id"
                }
            }
        }
    ]
}
EOM
)
permissions_policy_document=$(cat << EOM
{
  "Statement": [
    {
      "Sid": "SentinelActionsPermissions",
      "Effect": "Allow",
      "Action": [
        "iam:GetUserPolicy",
        "iam:DeleteRolePolicy",
        "iam:PutUserPolicy",
        "iam:AttachUserPolicy",
        "iam:ListUserPolicies",
        "iam:PutRolePolicy",
        "iam:GetUser",
        "iam:DetachUserPolicy",
        "iam:GetRolePolicy",
        "iam:DeleteUserPolicy",
        "s3:PutBucketPublicAccessBlock"
      ],
      "Resource": "*"
    }
  ]
}
EOM
)

aws iam add-client-id-to-open-id-connect-provider --open-id-connect-provider-arn arn:aws:iam::$account_id:oidc-provider/$ms_federated_endpoint/ --client-id $actions_audience
aws iam create-role --role-name $role_name --assume-role-policy-document "$trust_policy_document" || aws iam update-assume-role-policy --role-name $role_name --policy-document "$trust_policy_document"
aws iam put-role-policy --role-name $role_name --policy-name $policy_name --policy-document "$permissions_policy_document"

```

# [PowerShell Script](#tab/powershell)
The following PowerShell script is the Windows equivalent of the Bash setup script. It automates the same AWS OIDC provider configuration and IAM role creation for Microsoft Sentinel integration. Ensure that the AWS CLI is installed and authenticated before you run it.

```powershell
# AWS Sentinel OIDC Setup Script
# Configures IAM roles and policies for Microsoft Sentinel integration

$ErrorActionPreference = 'Stop'

$ms_federated_endpoint = "sts.windows.net/33e01921-4d64-4f8c-a055-5bdaffd5e33d"
$actions_audience = "api://b7c1e142-0933-4310-ba00-8b28878bfece"
$role_name = "OIDC_Actions_Sentinel"
$policy_name = "SentinelActionsPolicy"

# Verify AWS credentials are configured
Write-Host "Verifying AWS credentials..." -ForegroundColor Cyan
try {
    $account_id = aws sts get-caller-identity --query Account --output text 2>&1
    if ($LASTEXITCODE -ne 0) { 
        throw "AWS credentials not configured or invalid. Output: $account_id" 
    }
    Write-Host "✓ AWS authenticated (Account: $account_id)" -ForegroundColor Green
} catch {
    Write-Host "`nERROR: AWS credentials not configured or invalid" -ForegroundColor Red
    Write-Host "Details: $($_.Exception.Message)" -ForegroundColor Red
    Write-Host "`nPlease authenticate using one of these methods:" -ForegroundColor Yellow
    Write-Host "  1. Run 'aws configure' to set up credentials" -ForegroundColor Yellow
    Write-Host "  2. Set AWS environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY)" -ForegroundColor Yellow
    Write-Host "  3. Use 'aws sso login --profile <profile-name>' for SSO" -ForegroundColor Yellow
    exit 1
}

# Define trust policy document
$trust_policy_document = @"
{
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "arn:aws:iam::$account_id:oidc-provider/$ms_federated_endpoint/"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "$ms_federated_endpoint/:aud": "$actions_audience",
                    "sts:RoleSessionName": "MicrosoftSentinel_$account_id"
                }
            }
        }
    ]
}
"@

# Define permissions policy document
$permissions_policy_document = @"
{
  "Statement": [
    {
      "Sid": "SentinelActionsPermissions",
      "Effect": "Allow",
      "Action": [
        "iam:GetUserPolicy",
        "iam:DeleteRolePolicy",
        "iam:PutUserPolicy",
        "iam:AttachUserPolicy",
        "iam:ListUserPolicies",
        "iam:PutRolePolicy",
        "iam:GetUser",
        "iam:DetachUserPolicy",
        "iam:GetRolePolicy",
        "iam:DeleteUserPolicy",
        "s3:PutBucketPublicAccessBlock"
      ],
      "Resource": "*"
    }
  ]
}
"@

# Add client ID to OpenID Connect provider
Write-Host "`nAdding client ID to OIDC provider..." -ForegroundColor Cyan
try {
    $output = aws iam add-client-id-to-open-id-connect-provider `
        --open-id-connect-provider-arn "arn:aws:iam::$account_id:oidc-provider/$ms_federated_endpoint/" `
        --client-id $actions_audience 2>&1
    if ($LASTEXITCODE -ne 0) { throw $output }
    Write-Host "✓ Client ID added successfully" -ForegroundColor Green
} catch {
    Write-Host "ERROR: Failed to add client ID to OIDC provider" -ForegroundColor Red
    Write-Host "Details: $($_.Exception.Message)" -ForegroundColor Red
    exit 1
}

# Create or update IAM role
Write-Host "`nCreating/updating IAM role..." -ForegroundColor Cyan
try {
    $output = aws iam create-role `
        --role-name $role_name `
        --assume-role-policy-document $trust_policy_document 2>&1
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✓ Role created successfully" -ForegroundColor Green
    } else {
        throw $output
    }
} catch {
    if ($_.Exception.Message -like "*EntityAlreadyExists*") {
        Write-Host "Role already exists, updating assume role policy..." -ForegroundColor Yellow
        try {
            $output = aws iam update-assume-role-policy `
                --role-name $role_name `
                --policy-document $trust_policy_document 2>&1
            if ($LASTEXITCODE -ne 0) { throw $output }
            Write-Host "✓ Assume role policy updated" -ForegroundColor Green
        } catch {
            Write-Host "ERROR: Failed to update assume role policy" -ForegroundColor Red
            Write-Host "Details: $($_.Exception.Message)" -ForegroundColor Red
            exit 1
        }
    } else {
        Write-Host "ERROR: Failed to create IAM role" -ForegroundColor Red
        Write-Host "Details: $($_.Exception.Message)" -ForegroundColor Red
        exit 1
    }
}

# Attach inline policy to role
Write-Host "`nAttaching policy to role..." -ForegroundColor Cyan
try {
    $output = aws iam put-role-policy `
        --role-name $role_name `
        --policy-name $policy_name `
        --policy-document $permissions_policy_document 2>&1
    if ($LASTEXITCODE -ne 0) { throw $output }
    Write-Host "✓ Policy attached successfully" -ForegroundColor Green
} catch {
    Write-Host "ERROR: Failed to attach policy to role" -ForegroundColor Red
    Write-Host "Details: $($_.Exception.Message)" -ForegroundColor Red
    exit 1
}

Write-Host "`n========================================" -ForegroundColor Green
Write-Host "Setup completed successfully!" -ForegroundColor Green
Write-Host "========================================" -ForegroundColor Green
Write-Host "Role ARN: arn:aws:iam::$account_id:role/$role_name" -ForegroundColor Cyan
```

---