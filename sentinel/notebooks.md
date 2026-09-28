---
layout: Conceptual
title: Jupyter notebooks with Microsoft Sentinel hunting capabilities | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/notebooks
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
description: Learn about Jupyter notebooks in Microsoft Sentinel for security hunting.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: concept-article
ms.custom: devx-track-python
ms.date: 2024-03-07T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: 778dfe03-28a2-29bf-31e3-e40ba4c4f21b
document_version_independent_id: 108e9b4a-74c8-8de9-9c7a-8609da938df5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/notebooks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/notebooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/notebooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 75ec7504-b4fb-daea-222e-1df2b695b9fb
---

# Jupyter notebooks with Microsoft Sentinel hunting capabilities | Microsoft Learn

Jupyter notebooks combine full programmability with a huge collection of libraries for machine learning, visualization, and data analysis. These attributes make Jupyter a compelling tool for security investigation and hunting.

The foundation of Microsoft Sentinel is the data store; it combines high-performance querying, dynamic schema, and scales to massive data volumes. The Azure portal and all Microsoft Sentinel tools use a common API to access this data store. The same API is also available for external tools such as [Jupyter](https://jupyter.org/) notebooks and Python.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## When to use Jupyter notebooks

While many common tasks can be carried out in the portal, Jupyter extends the scope of what you can do with this data.

For example, use notebooks to:

- **Perform analytics** that aren't provided out-of-the-box in Microsoft Sentinel, such as some Python machine learning features
- **Create data visualizations** that aren't provided out-of-the-box in Microsoft Sentinel, such as custom timelines and process trees
- **Integrate data sources** outside of Microsoft Sentinel, such as an on-premises data set.

We integrated the Jupyter experience into the Azure portal, making it easy for you to create and run notebooks to analyze your data. The *Kqlmagic* library provides the glue that lets you take Kusto Query Language (KQL) queries from Microsoft Sentinel and run them directly inside a notebook.

Several notebooks, developed by some of Microsoft's security analysts, are packaged with Microsoft Sentinel:

- Some of these notebooks are built for a specific scenario and can be used as-is.
- Others are intended as samples to illustrate techniques and features that you can copy or adapt for use in your own notebooks.

Import other notebooks from the [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel-Notebooks/).

## How Jupyter notebooks work

Notebooks have two components:

- **The browser-based interface**, where you enter and run queries and code, and where the results of the execution are displayed.
- **A *kernel*** that is responsible for parsing and executing the code itself.

The Microsoft Sentinel notebook's kernel runs on an Azure virtual machine (VM). The VM instance can support running many notebooks at once. If your notebooks include complex machine learning models, several licensing options exist to use more powerful virtual machines.

## Understand Python packages

The Microsoft Sentinel notebooks use many popular Python libraries such as *pandas*, *matplotlib*, *bokeh*, and others. There are a great many other Python packages for you to choose from, covering areas such as:

- Visualizations and graphics
- Data processing and analysis
- Statistics and numerical computing
- Machine learning and deep learning

To avoid having to type or paste complex and repetitive code into notebook cells, most Python notebooks rely on third-party libraries called *packages*. To use a package in a notebook, you need to both install and import the package. Azure Machine Learning Compute has most common packages pre-installed. Make sure that you import the package, or the relevant part of the package, such as a module, file, function, or class.

Microsoft Sentinel notebooks use a Python package called [MSTICPy](https://github.com/Microsoft/msticpy/), which is a collection of cybersecurity tools for data retrieval, analysis, enrichment, and visualization.

MSTICPy tools are designed specifically to help with creating notebooks for hunting and investigation and we're actively working on new features and improvements. For more information, see:

- [MSTIC Jupyter and Python Security Tools documentation](https://msticpy.readthedocs.io/)
- [Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebook-get-started)
- [Advanced configurations for Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebooks-msticpy-advanced)

## Find notebooks

In Microsoft Sentinel, select **Notebooks** to see notebooks that Microsoft Sentinel provides. Learn more about using notebooks in threat hunting and investigation by exploring notebook templates like **Credential Scan on Azure Log Analytics** and **Guided Investigation - Process Alerts**.

For more notebooks built by Microsoft or contributed from the community, go to [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel-Notebooks/). Use notebooks shared in the Microsoft Sentinel GitHub repository as useful tools, illustrations, and code samples that you can use when developing your own notebooks.

- The [`Sample-Notebooks`](https://github.com/Azure/Azure-Sentinel-Notebooks/tree/master/tutorials-and-examples/example-notebooks) directory includes sample notebooks that are saved with data that you can use to show intended output.
- The [`HowTos`](https://github.com/Azure/Azure-Sentinel-Notebooks/tree/master/tutorials-and-examples/how-tos) directory includes notebooks that describe concepts such as setting your default Python version, creating Microsoft Sentinel bookmarks from a notebook, and more.

## Manage access to Microsoft Sentinel notebooks

To use Jupyter notebooks in Microsoft Sentinel, you must first have the right permissions, depending on your user role.

While you can run Microsoft Sentinel notebooks in JupyterLab or Jupyter classic, in Microsoft Sentinel, notebooks are run on an [Azure Machine Learning](/en-us/azure/machine-learning/overview-what-is-azure-machine-learning) platform. To run notebooks in Microsoft Sentinel, you must have appropriate access to both Microsoft Sentinel workspace and an [Azure Machine Learning workspace](/en-us/azure/machine-learning/concept-workspace).

| Permission | Description |
| --- | --- |
| **Microsoft Sentinel permissions** | Like other Microsoft Sentinel resources, to access notebooks on Microsoft Sentinel Notebooks blade, a Microsoft Sentinel Reader, Microsoft Sentinel Responder, or Microsoft Sentinel Contributor role is required. For more information, see [Permissions in Microsoft Sentinel](roles). |
| **Azure Machine Learning permissions** | An Azure Machine Learning workspace is an Azure resource. Like other Azure resources, when a new Azure Machine Learning workspace is created, it comes with default roles. You can add users to the workspace and assign them to one of these built-in roles. For more information, see [Azure Machine Learning default roles](/en-us/azure/machine-learning/how-to-assign-roles) and [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles). **Important**: Role access can be scoped to multiple levels in Azure. For example, someone with owner access to a workspace may not have owner access to the resource group that contains the workspace. For more information, see [How Azure RBAC works](/en-us/azure/role-based-access-control/overview). If you're an owner of an Azure ML workspace, you can add and remove roles for the workspace and assign roles to users. For more information, see: - [Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal) - [PowerShell](/en-us/azure/role-based-access-control/role-assignments-powershell) - [Azure CLI](/en-us/azure/role-based-access-control/role-assignments-cli) - [REST API](/en-us/azure/role-based-access-control/role-assignments-rest) - [Azure Resource Manager templates](/en-us/azure/role-based-access-control/role-assignments-template) - [Azure Machine Learning CLI](/en-us/azure/machine-learning/how-to-assign-roles#manage-workspace-access)If the built-in roles are insufficient, you can also create custom roles. Custom roles might have read, write, delete, and compute resource permissions in that workspace. You can make the role available at a specific workspace level, a specific resource group level, or a specific subscription level. For more information, see [Create custom role](/en-us/azure/machine-learning/how-to-assign-roles#create-custom-role). |

## Submit feedback for a notebook

Submit feedback, requests for features, bug reports, or improvements to existing notebooks. Go to the [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel) to create an issue, or fork and upload a contribution.