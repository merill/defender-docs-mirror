---
layout: Conceptual
title: Create ASIM parsers using AI agent skills in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-create-parsers-ai-agent
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
ms.reviewer: ofshezaf
description: Use GitHub Copilot or the Microsoft Sentinel VS Code extension skills to create, validate, deploy, and package ASIM parsers in Microsoft Sentinel so you can normalize security data faster.
ms.author: derricklee
author: derricklee
ms.topic: how-to
ms.date: 2026-09-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: 78942dff-0dd5-e789-6de2-0713a337108f
document_version_independent_id: 6f99f5d6-f72b-9dfe-c7c9-cf8a80be32e6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-create-parsers-ai-agent.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-create-parsers-ai-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-create-parsers-ai-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: b5bf99ba-c46d-7452-6e7c-ccd15ef48b9a
---

# Create ASIM parsers using AI agent skills in Microsoft Sentinel | Microsoft Learn

Use [Agent skills](/en-us/agent-framework/agents/skills) to create, validate, deploy, and package Advanced Security Information Model (ASIM) parsers. These skills are available in GitHub Copilot CLI and in the [Microsoft Sentinel VS Code extension](https://marketplace.visualstudio.com/items?itemName=ms-security.ms-sentinel). They automate the parser workflow from source data collection and Kusto Query Language (KQL) parser generation to validation, Log Analytics deployment, and pull request packaging. By the end of this guide, you'll have a working ASIM parser in your workspace, ready for production use.

## Prerequisites

Before you begin, make sure you have the following items in place:

- An active Microsoft Sentinel workspace
- One of the following:

    - [GitHub Copilot](https://github.com/features/copilot/cli/)
    - [Microsoft Sentinel VS Code extension](https://marketplace.visualstudio.com/items?itemName=ms-security.ms-sentinel)
- [PowerShell 7](/en-us/powershell/scripting/install/install-powershell-on-windows)
- [Azure CLI](/en-us/cli/azure/install-azure-cli)

    - You should have query access to your Sentinel Log Analytics workspace.
- A local clone of the [Azure-Sentinel](https://github.com/Azure/Azure-Sentinel) repository. [Fork the repository](https://github.com/Azure/Azure-Sentinel/fork) so that you can submit pull requests with your parsers for Microsoft review.

### Quick start with GitHub Copilot CLI

To run the ASIM parser creation workflow in Copilot CLI, follow these steps:

1. Open a terminal in PowerShell 7.
2. Navigate to the root directory of the Azure-Sentinel repository. `cd \Azure-Sentinel`
3. Run `copilot`. This command starts Copilot CLI. Running `copilot` in the Azure-Sentinel repository preloads existing skills in the repository.

    If the ASIM parser skills don't appear when you run `/skills list`, load the skills manually with `/skills add .github/skills/`.
4. Select Claude Sonnet 4.6+ or Claude Opus 4.6+ for best results by running `/model` .
5. Prompt Copilot in the session to create an ASIM parser with the following prompt: `Create an ASIM parser for me.`

### Quick start with the Microsoft Sentinel VS Code extension

The extension includes the same ASIM parser skills and orchestrates the workflow identically to the CLI experience.

To run the ASIM parser creation workflow using the Microsoft Sentinel VS Code extension, follow these steps:

1. Install the [Microsoft Sentinel extension](https://marketplace.visualstudio.com/items?itemName=ms-security.ms-sentinel) from the VS Code Marketplace.
2. Open your preferred workspace/repository in VS Code.
3. Open the Copilot chat panel and select Claude Sonnet 4.6+ or Claude Opus 4.6+ for best results. Prompt: `Create an ASIM parser for me.`

[![Screenshot of the agent experience on Visual Studio Code.](media/normalization-create-parsers-ai-agent/vscode-extension-experience.png)](media/normalization-create-parsers-ai-agent/vscode-extension-experience.png#lightbox)

## ASIM Parser Creation Orchestration

The `asim-parser-creator-orchestrator` skill orchestrates the ASIM parser creation workflow, which calls specialized skills at each step. The following sections describe each stage of the process.

### Requirements gathering

The `asim-parser-user-prompter` skill gathers the information needed to create a parser. Provide the following information:

- **Source documentation link** - A link to the documentation for the data source you want to normalize.
- **Source table name** - The name of the table in Microsoft Sentinel where the data is stored.
- **Log Analytics workspace ID** - The GUID of the workspace where the table exists. The skill validates the workspace and table by querying it.
- **Target ASIM schema** - Your table can contain a large range of logs. If necessary, you need to confirm which ASIM schema you want your data to normalize to. The skill evaluates what ASIM schema the data maps to based on the documentation and table name, using the available schemas listed in [ASIM schemas](/en-us/azure/sentinel/normalization-about-schemas).

    [![Screenshot of the agent prompt for choosing ASIM schema in GitHub Copilot.](media/normalization-create-parsers-ai-agent/choose-schema.png)](media/normalization-create-parsers-ai-agent/choose-schema.png#lightbox)

### Azure CLI authentication

The orchestrator verifies you're authenticated with Azure CLI by running `az account show`. If the check fails, you're prompted to run `az login` before continuing. This step prevents authentication failures during later querying and deployment stages.

### Parser creation

The `asim-parser-create-parser` skill generates the initial parameter-less ASIM parser. During this step, Copilot performs the following actions:

1. **Samples your data** - Queries the source table to get the schema (`getschema`) and up to 2,000 sample rows to understand the data structure.
2. **Builds the parser** - Creates a KQL function that transforms source data into the target ASIM schema, mapping source columns to ASIM fields using high-performance parsing operators (`split`, `parse-kv`, `parse`).
3. **Saves the parser** - Outputs a file named `ASim<Schema><Vendor><Product>.kql` and verifies it runs without syntax errors.

Important

The parser creation skills normalize each source record independently and preserve record cardinality. Query-local static mappings created with `datatable` and applied with `lookup` are allowed when each lookup key is unique. The skills don't use same-table or cross-table event enrichment, one-to-many fan-out, `mv-*` operators, or event-record aggregation and reaggregation operators such as `summarize`. If a field requires one of these prohibited patterns, correct the connector or source event shape, or leave a nonmandatory field unmapped. For detailed guidance, see [Develop ASIM parsers](/en-us/azure/sentinel/normalization-develop-parsers#keep-parser-operations-record-local).

### Validation

The `asim-parser-validator` skill runs two validations against the parser:

- **Schema validation (`ASimSchemaTester`)** - Checks that the parser output columns match the ASIM schema, including correct column names, data types, and aliases.
- **Data validation (`ASimDataTester`)** - Checks that column values are correctly mapped and formatted, including enumerations, data type formatting (for example, IP addresses), and value normalization.

Both validations run directly against your Log Analytics workspace using the `log-analytics-workspace-queryer` skill.

### Refinement loop

The orchestrator iterates through a fix-and-revalidate cycle until the parser passes both validations. Each cycle performs the following steps:

1. Fixes errors identified by the validator in the parser `.kql` file.
2. Re-runs both schema and data validation.
3. Checks the results.

This cycle continues until no errors remain. If errors persist after five refinement cycles, the remaining errors are presented for manual review.

### Parameterized parser creation

The `asim-parser-create-parameter-parser` skill creates a second version of the parser that accepts filter parameters (for example, time range, hostname, IP address). These parameters improve query efficiency by allowing the parser to filter data early. The output is a file named `vim<Schema><Vendor><Product>.kql`.

After creation, the parameterized parser goes through the same validation and refinement loop described in the Validation and Refinement loop sections.

### Parameterized filter validation

The `asim-parser-filter-validator` skill verifies that the parameterized parser's filtering parameters behave correctly. It runs a PowerShell-based test suite against your Log Analytics workspace that checks each parameter declared in the parser's KQL function signature.

### Deployment or packaging

After both parsers are validated, you choose what to do next:

- **Option A: Deploy to Log Analytics workspace** - The `asim-parser-la-deployer` skill creates an ARM template with the escaped KQL queries and deploys both parsers to your workspace using `az deployment group create`. After deployment, the skill verifies the parsers work by running test queries.
- **Option B: Package as a GitHub PR** - The `asim-parser-github-pr-packager` skill packages the parsers into a pull request for the Azure-Sentinel repository. The steps include creating YAML parser definitions, changelogs, sample data files, updating unifying parsers, generating ARM templates, and committing the changes on a new branch.

You can choose one or both options.

[![Screenshot of the agent prompt for choosing what to do with the ASIM parsers in GitHub Copilot.](media/normalization-create-parsers-ai-agent/parser-final-decision.png)](media/normalization-create-parsers-ai-agent/parser-final-decision.png#lightbox)

### Summary report

After the workflow completes, a summary report is presented that includes:

- Source column to ASIM field mappings.
- The target ASIM schema name and version.
- Event vendor and product names.
- File paths of the generated parser files.
- Any validation warnings that were reviewed and accepted.
- Deployment or PR creation status.

## Submit your parsers as a pull request

We highly recommend submitting your parsers as a pull request to the [Azure-Sentinel](https://github.com/Azure/Azure-Sentinel) repository. By contributing your parsers to the open-source repository, Microsoft developers can review them for correctness and best practices, maintain them as part of the official ASIM parser library, and ensure ongoing compatibility with schema updates and platform changes. Community-contributed parsers also benefit other Microsoft Sentinel users who work with the same data sources.

## References

- For more information about the skills, you can refer to the skills folder in the [Azure-Sentinel](https://github.com/Azure/Azure-Sentinel/tree/master/.github/skills) repository.
- The [ASIM parser agent README](https://github.com/Azure/Azure-Sentinel/blob/master/ASIM/tools/ASIMParserCreation-Agentic/README.md) in the repository also provides troubleshooting guidance.
- [Develop ASIM parsers](/en-us/azure/sentinel/normalization-develop-parsers) provides detailed guidance on manually developing and testing ASIM parsers.

## Getting Help

- For ISV partners building integrations, contact: azuresentinelpartner@microsoft.com
- For technical questions, use [Microsoft Q&A](/en-us/answers/topics/azure-sentinel.html) with the tag 'azure-sentinel'