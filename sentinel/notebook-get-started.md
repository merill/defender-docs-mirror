---
layout: Conceptual
title: Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/notebook-get-started
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
description: Walk through the Getting Started Guide For Microsoft Sentinel ML Notebooks to learn the basics of Microsoft Sentinel notebooks with MSTICPy and queries.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: a6fe1ed9-7c86-fa0a-97f4-2a508493dd80
document_version_independent_id: 90c06374-4ebe-217a-6110-f411c85d1ee5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/notebook-get-started.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/notebook-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/notebook-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: bc6aee1a-8e73-1f82-211b-52e15ec1ae6c
---

# Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel | Microsoft Learn

This article describes how to run the **Getting Started Guide For Microsoft Sentinel ML Notebooks** notebook, which sets up basic configurations for running Jupyter notebooks in Microsoft Sentinel and provides examples for running simple queries. Before you begin, make sure you complete the prerequisites, including permissions, Python setup, and external data provider accounts.

The **Getting Started Guide for Microsoft Sentinel ML Notebooks** notebook uses [MSTICPy](https://msticpy.readthedocs.io/en/latest/), a powerful Python library designed to enhance security investigations and threat hunting within Microsoft Sentinel notebooks. MSTICPy provides built-in tools for data enrichment, visualization, anomaly detection, and automated queries, helping analysts streamline their workflow without extensive custom coding.

For more information, see [Use notebooks to power investigations](hunting#use-notebooks-to-power-investigations) and [Use Jupyter notebooks to hunt for security threats](notebooks).

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you begin, make sure you have the required permissions and resources.

| Prerequisite | Description |
| --- | --- |
| **Permissions** | To use notebooks in Microsoft Sentinel, make sure that you have the required permissions. For more information, see [Manage access to Microsoft Sentinel notebooks](notebooks#manage-access-to-microsoft-sentinel-notebooks). |
| **Python** | To perform the steps in this article, you need Python 3.6 or later. In Azure Machine Learning, you can use either a Python 3.8 kernel (recommended) or a Python 3.6 kernel. If you use the notebook described in this article in another Jupyter environment, you can use any kernel that supports Python 3.6 or later. To use MSTICPy notebooks outside of Microsoft Sentinel and Azure Machine Learning (ML), you also need to configure your Python environment. Install Python 3.6 or later with the Anaconda distribution, which includes many of the required packages. |
| [**MaxMind GeoLite2**](https://www.maxmind.com) | This notebook uses the MaxMind GeoLite2 geolocation lookup service for IP addresses. To use the MaxMind GeoLite2 service, you need a license key. You can sign up for a free account and key at the [Maxmind signup page](https://www.maxmind.com/en/geolite2/signup). |
| [**VirusTotal**](https://www.virustotal.com) | This notebook uses VirusTotal (VT) as a threat intelligence source. To use VirusTotal threat intelligence lookup, you need a VirusTotal account and API key. If you're using a VT enterprise key, store it an Azure Key Vault instead of the **msticpyconfig.yaml** file. For more information, see [Specify secrets as Key Vault secrets](https://msticpy.readthedocs.io/en/latest/getting_started/msticpyconfig.html#specifying-secrets-as-key-vault-secrets) in the MSTICPY documentation. If you don’t want to set up an Azure Key Vault right now, sign up for and use a free account until you can set up Key Vault storage. |

## Install and run the Getting Started Guide notebook

The following steps describe how to launch the Getting Started Guide notebook with Microsoft Sentinel.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Threat management** &gt; **Notebooks**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Threat management**, select **Notebooks**.
2. From the **Templates** tab, select **A Getting Started Guide For Microsoft Sentinel ML Notebooks** .
3. Select **Create from template**.
4. Edit the name and select the Azure Machine Learning workspace as appropriate.
5. Select **Save** to save the notebook to your Azure Machine Learning workspace.
6. Select **Launch notebook** to run the notebook. The notebook contains a series of cells:

    - *Markdown* cells contain text and graphics with instructions for using the notebook
    - *Code* cells contain executable code that performs the notebook functions
7. At the top of the page, select your **Compute**.
8. Continue by reading markdown cells and running code cells in order, using the instructions in the notebook. Skipping cells or running them out of order might cause errors later in the notebook.

    Depending on the function being performed, the code in the cell might run quickly, or it might take some time to complete. When the cell is running, the play button changes to a loading spinner, and the status is displayed at the bottom of the cell, together with the elapsed time.

    The first time you run a code cell, it may several a few minutes to start the session, depending on your compute settings. A **Ready** indication is shown when the notebook is ready to run code cells. For example:

    ![Screenshot of a machine learning environment ready to run code cells.](media/notebook-get-started/compute-ready.png)

The **Getting Started Guide For Microsoft Sentinel ML Notebooks** notebook includes sections for the following activities:

| Name | Description |
| --- | --- |
| **Introduction** | Describe notebook basics and provides sample code you can run to see how notebooks work. |
| **Initializing the notebook and MSTICPy** | Helps you get your environment ready to run the rest of the notebook. When initializing the notebook, configuration warnings about missing settings are expected because you didn't configure anything yet. |
| **Querying Data from Microsoft Sentinel** | Helps you verify, configure, and test Microsoft Sentinel settings. Use the code in this section to authenticate to Microsoft Sentinel and run a sample query to test the connection. |
| **Configure and test external data providers (VirusTotal and Maxmind GeoLite2)** | Helps you configure settings for VirusTotal, as a sample threat intelligence service, and MaxMind GeoLite2, as a sample geo-location lookup service. Use the code in this section to run sample queries against these data providers to test the provider connections. |

The code in the **Getting Started Guide For Microsoft Sentinel ML Notebooks** launches a tabbed configuration tool called **MpConfigEdit**, which you use to configure your notebook environment. As you make changes in the **MpConfigEdit** tool, make sure to save your changes before proceeding to the next tab. Settings for the notebook are stored in the **msticpyconfig.yaml** file, which is automatically populated with initial details for your workspace.

Make sure to read through the markdown cells carefully so that you understand the notebook configuration process completely, including each of the settings and the **msticpyconfig.yaml** file. Next steps, extra resources, and frequently asked questions from the [Azure Sentinel Notebooks wiki](https://github.com/Azure/Azure-Sentinel-Notebooks/wiki/) are linked from the end of the notebook.

## Customize your queries (optional)

The **Getting Started Guide For Microsoft Sentinel ML Notebooks** notebook provides sample queries for you to use when learning about notebooks. Customize the built-in queries by adding more query logic, or run complete queries using the `exec_query` function. For example, most built-in queries support the `add_query_items` parameter, which you can use to append filters or other operations to the queries.

1. Run the following code cell to add a data frame that summarizes the number of alerts by alert name:

    ```python
    from datetime import datetime, timedelta
    
    qry_prov.SecurityAlert.list_alerts(
       start=datetime.utcnow() - timedelta(28),
        end=datetime.utcnow(),
        add_query_items="| summarize NumAlerts=count() by AlertName"
    )
    ```
2. Pass a full Kusto Query Language (KQL) query string to the query provider. The query runs against the connected workspace, and the data returns as a panda DataFrame. Run:

    ```python
    # Define your query
    test_query = """
    OfficeActivity
    | where TimeGenerated > ago(1d)
    | take 10
    """
    
    # Pass the query to your QueryProvider
    office_events_df = qry_prov.exec_query(test_query)
    display(office_events_df.head())
    
    ```

For more information, see:

- The [MSTICPy query reference](https://msticpy.readthedocs.io/en/latest/data_acquisition/DataQueries.html)
- [Running MSTICPy pre-defined queries](https://msticpy.readthedocs.io/en/latest/data_acquisition/DataProviders.html#running-an-pre-defined-query)

## Apply guidance to other notebooks

The steps in this article describe how to run the **Getting Started Guide for Microsoft Sentinel ML Notebooks** notebook in your Azure Machine Learning workspace via Microsoft Sentinel. You can also use this article as guidance for launching and configuring notebooks in other environments, including locally.

Several Microsoft Sentinel notebooks don't use [MSTICPy](https://msticpy.readthedocs.io/en/latest/) (the Python library for security investigations in Microsoft Sentinel notebooks), such as the **Credential Scanner** notebooks, or the PowerShell and C# examples. Notebooks that don't use MSTICpy don't need the MSTICPy configuration described in Install and run the Getting Started Guide notebook.

Try out other Microsoft Sentinel notebooks, such as:

- **Configuring your Notebook Environment**
- **A Tour of Cybersec notebook features**
- **Machine Learning in Notebooks Examples**
- The **Entity Explorer** series, including variations for accounts, domains and URLs, IP addresses, and Linux or Windows hosts.

For more information, see:

- [Jupyter notebooks with Microsoft Sentinel hunting capabilities](notebooks)
- [Advanced configurations for Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebooks-msticpy-advanced)
- [Create your first Microsoft Sentinel notebook](https://techcommunity.microsoft.com/t5/microsoft-sentinel-blog/creating-your-first-microsoft-sentinel-notebook/ba-p/2977745) (Blog series)
- [Linux Host Explorer Notebook walkthrough](https://techcommunity.microsoft.com/t5/azure-sentinel/explorer-notebook-series-the-linux-host-explorer/ba-p/1138273) (Blog)