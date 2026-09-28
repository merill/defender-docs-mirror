---
layout: Conceptual
title: Exploring and interacting with lake data using Jupyter Notebooks - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/notebooks-overview
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: This article gives an overview of Jupyter notebooks in Visual Studio Code for the Microsoft Sentinel data lake.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: overview
ms.date: 2026-06-25T00:00:00.0000000Z
locale: en-us
document_id: 175fa2d3-dacc-92ef-815e-0c5888066277
document_version_independent_id: f7ed1d93-4811-5a86-dede-ee99a890aa0c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/notebooks-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/notebooks-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/notebooks-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
platformId: e8d36c4b-b350-96f5-f151-c1010e86d33c
---

# Exploring and interacting with lake data using Jupyter Notebooks - Microsoft Security | Microsoft Learn

Jupyter notebooks are an integral part of the Microsoft Sentinel data lake ecosystem, offering powerful tools for data analysis and visualization. The notebooks are provided by the Microsoft Sentinel Visual Studio Code extension that allows you to interact with the data lake using Python for Spark (PySpark). Notebooks enable you to perform complex data transformations, run machine learning models, and create visualizations directly within the notebook environment.

The Microsoft Sentinel Visual Studio Code extension with Jupyter notebooks provides a powerful environment for exploring and analyzing lake data with the following benefits:

- **Interactive data exploration**: Jupyter notebooks provide an interactive environment for exploring and analyzing data. You can run code snippets, visualize results, and document your findings all in one place.
- **Integration with Python libraries**: The Microsoft Sentinel extension includes a wide range of Python libraries, enabling you to use existing tools and frameworks for data analysis, machine learning, and visualization.
- **Powerful data analysis**: With the integration of Apache Spark compute sessions, you can use the power of distributed computing to analyze large datasets efficiently. This allows you to perform complex transformations and aggregations on your security data.
- **Low-and-slow attacks**: Analyze large scale, complex, interconnected data related to security events, alerts, and incidents, enabling detection of sophisticated threats and patterns, such as lateral movement or low-and-slow attacks that can evade traditional rule-based systems.
- **AI and ML integration**: Integrate with AI and machine learning to enhance anomaly detection, threat prediction, and behavioral analysis, empowering security teams to build agents to automate their investigations.
- **Scalability**: Notebooks provide the scalability to process vast amounts of data cost efficiently and enable deep batch processing for uncovering trends, patterns, and anomalies.
- **Visualization capabilities**: Jupyter notebooks support various visualization libraries, enabling you to create charts, graphs, and other visual representations of your data, helping you gain insights and communicate findings effectively.
- **Collaboration and sharing**: Jupyter notebooks can be easily shared with colleagues, allowing for collaboration on data analysis projects. You can export notebooks in various formats, including HTML and PDF, for easy sharing and presentation.
- **Documentation and reproducibility**: Jupyter notebooks allow you to document your code, analysis, and findings in a single file, making it easier to reproduce results and share your work with others.

## Lake exploration scenarios for notebooks

The following scenarios illustrate how Jupyter notebooks in the Microsoft Sentinel Lake can be used to enhance security operations:

| Scenario | Description |
| --- | --- |
| **User behavior from failed sign ins** | Establish a baseline of normal user behavior by analyzing patterns of failed sign in attempts. Investigate operations attempted before and after the failed logins to detect potential compromise or brute-force activity. |
| **Sensitive data paths** | Identify users and devices that have access to sensitive data assets. Combine access logs with organizational context to assess risk exposure, map access paths, and prioritize areas for security review. |
| **Anomaly threat analysis** | Analyze threats by identifying deviations from established baselines, such as logins from unusual locations, devices, or times. Overlay user behavior with asset data to identify high-risk activity, including potential insider threats. |
| **Risk-scoring prioritization** | Apply custom risk scoring models to security events in the data lake. Enrich events with contextual signals such as asset criticality and user role to quantify risk, assess blast radius, and prioritize incidents for investigation. |
| **Exploratory analysis and visualization** | Perform exploratory data analysis across multiple log sources to reconstruct attack timelines, determine root causes, and build custom visualizations that help communicate findings to stakeholders. |

## Writing to the lake and analytics tier

You can write data to the lake tier and analytics tier using notebooks. The Microsoft Sentinel extension for Visual Studio Code provides a PySpark Python library that abstracts the complexity of writing to the lake and analytics tiers. You can use the `MicrosoftSentinelProvider` class's `save_as_table()` function to write data to custom tables or append data to existing tables in the lake tier or analytics tier. For more information, see [Microsoft Sentinel Provider class reference](sentinel-provider-class-reference).

## Jobs and scheduling

You can schedule jobs to run at specific times or intervals using the Microsoft Sentinel extension for Visual Studio Code. Jobs allow you to automate data processing tasks to summarize, transform, or analyze data in the Microsoft Sentinel data lake. Use jobs to process data and write results to custom tables in the lake tier or analytics tier. For more information, see [Create and manage Jupyter notebook jobs](notebook-jobs).

Notebook jobs can also use parameters defined in the notebook. Parameters let you reuse the same notebook job with different input values, such as running the same analysis for different users, entities, time ranges, or other investigation inputs. You can save parameter values with the job configuration and provide different values when you run the job manually. For more information, see [Create and manage parameterized notebook jobs](notebook-jobs#create-and-manage-parameterized-notebook-jobs).