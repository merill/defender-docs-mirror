---
layout: Conceptual
title: Advanced configurations for Jupyter notebooks and MSTICPy in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/notebooks-msticpy-advanced
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
description: Learn about advanced configurations available for Jupyter notebooks with MSTICPy when working in Microsoft Sentinel.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.custom: devx-track-python, msecd-doc-authoring-1016
ms.date: 2026-08-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 161fb7f8-b58a-5d20-62f4-df9ba39b4ab6
document_version_independent_id: 50a40f3d-945f-f4dd-edc7-2d310df8eec2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/notebooks-msticpy-advanced.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/notebooks-msticpy-advanced
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/notebooks-msticpy-advanced.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: c2ddb27a-9627-2b51-80b4-6d805c7a8830
---

# Advanced configurations for Jupyter notebooks and MSTICPy in Microsoft Sentinel | Microsoft Learn

This article describes how to configure authentication parameters for Azure and Microsoft Sentinel APIs, define autoloading query providers and MSTICPy components, manage Python kernel versions, and set environment variables for your **msticpyconfig.yaml** configuration file when working with Jupyter notebooks and MSTICPy in Microsoft Sentinel.

For more information, see [Use Jupyter notebooks to hunt for security threats](notebooks) and [Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebook-get-started).

## Prerequisites

This article covers advanced MSTICPy configuration tasks, including setting authentication parameters, defining autoloading query providers and components, switching Python kernels, and configuring environment variables for your **msticpyconfig.yaml** file. Before you begin, complete the steps in [Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebook-get-started).

## Specify authentication parameters for Azure and Microsoft Sentinel APIs

Configure authentication parameters for Microsoft Sentinel and other Azure API resources in your **msticpyconfig.yaml** file by using the following steps.

**To add Azure authentication and Microsoft Sentinel API settings in the MSTICPy settings editor**:

1. Proceed to the next cell, with the following code, and run it:

    ```python
    mpedit.set_tab("Data Providers")
    mpedit
    ```
2. In the **Data Providers** tab, select **AzureCLI** &gt; **Add**.
3. Select the authentication methods to use:

    - While you can use a different set of methods from the defaults, this usage isn't a typical configuration. For more information, see the [**Getting Started Guide For Azure Sentinel ML Notebooks** notebook](notebook-get-started).
    - Unless you want to use environment variable (**env**) authentication, leave the **clientId**, **tenantId**, and **clientSecret** fields empty.
    - While not recommended, MSTICPy also supports using client app IDs and secrets for your authentication. In such cases, define your **clientId**, **tenantId**, and **clientSecret** fields directly in the **Data Providers** tab.
4. Select **Save File** to save your changes.

## Define autoloading query providers

You can configure MSTICPy to automatically load specific query providers when you run the `nbinit.init_notebook` function.

When you frequently author new notebooks, autoloading query providers can save you time by ensuring that required providers are loaded before other components, such as pivot functions and notebooklets.

**To add autoloading query providers**:

1. Proceed to the next cell, with the following code, and run it:

    ```python
    mpedit.set_tab("Autoload QueryProvs")
    mpedit
    ```
2. In the **Autoload QueryProv** tab:

    - For Microsoft Sentinel providers, specify both the provider name and the workspace name you want to connect to.
    - For other query providers, specify the provider name only.

    Each provider also has the following optional values:

    - **Auto-connect:** This option is defined as **True** by default, and MSTICPy tries to authenticate to the provider immediately after loading. MSTICPy assumes that you configured credentials for the provider in your settings.
    - **Alias:** When MSTICPy loads a provider, it assigns the provider to a Python variable name. By default, the variable name is **qryworkspace\_name** for Microsoft Sentinel providers and **qryprovider\_name** for other providers.

        For example, if you load a query provider for the *ContosoSOC* workspace, this query provider is created in your notebook environment with the name `qry_ContosoSOC`. Add an alias if you want to use something shorter or easier to type and remember. The provider variable name is `qry_<alias>`, where `<alias>` is replaced by the alias name that you provided.

        Providers you load by this mechanism are also added to the MSTICPy `current_providers` attribute, which is used, for example, in the following code:

        ```python
        import msticpy
        msticpy.current_providers
        ```
3. Select **Save Settings** to save your changes.

## Define autoloaded MSTICPy components

You can define additional components that MSTICPy automatically loads when you run the `nbinit.init_notebook` function.

Supported components include, in the following order:

1. **TILookup:** The TI provider library you want to use
2. **GeoIP:** The GeoIP provider you want to use
3. **AzureData:** The module you use to query details about Azure resources
4. **AzureSentinelAPI:** The module you use to query the Microsoft Sentinel API
5. **Notebooklets:** Notebooklets from the [msticnb package](https://msticnb.readthedocs.io/en/latest/)
6. **Pivot:** Pivot functions

The components load in the order listed because the Pivot component needs query and other providers loaded to find the pivot functions that it attaches to entities. For more information, see [MSTICPy documentation](https://msticpy.readthedocs.io/en/latest/data_analysis/PivotFunctions.html). For more information, see the [**Getting Started Guide For Azure Sentinel ML Notebooks** notebook](notebook-get-started).

**To define auto-loaded MSTICPy components**:

1. Proceed to the next cell, with the following code, and run it:

    ```python
    mpedit.set_tab("Autoload Components")
    mpedit
    ```
2. In the **Autoload Components** tab, define any parameter values as needed. For example:

    - **GeoIpLookup**. Enter the name of the GeoIP provider you want to use, either *GeoLiteLookup* or *IPStack*.
    - **AzureData and AzureSentinelAPI components**. Define the following values:

        - **auth\_methods:** Override the default settings for AzureCLI, and connect using the selected methods.
        - **Auto-connect:** Set to false to load without connecting.

        For more information, see Specify authentication parameters for Azure and Microsoft Sentinel APIs.
    - **Notebooklets**. The **Notebooklets** component has a single parameter block: **AzureSentinel**.

        Specify your Microsoft Sentinel workspace using the following syntax: `workspace:\<workspace name>`. The workspace name must be one of the workspaces defined in the **Microsoft Sentinel** tab.

        If you want to add more parameters to send to the `notebooklets init` function, specify them as key:value pairs, separated by newlines. For example:

        ```python
        workspace:<workspace name>
        providers=["LocalData","geolitelookup"]
        ```

        For more information, see the [MSTICNB (MSTIC Notebooklets) documentation](https://msticnb.readthedocs.io/en/latest/msticnb.html#msticnb.data_providers.init).

    Some components, like **TILookup** and **Pivot,** don't require any parameters.
3. Select **Save Settings** to save your changes.

## Switch between Python 3.6 and 3.8 kernels

If you're switching between Python 3.65 and 3.8 kernels, you might find that MSTICPy and other packages don't get installed as expected.

This installation issue might happen when the `!pip install pkg` command installs correctly in the first environment, but then doesn't install correctly in the second. The failed installation in the second environment means that environment can't import or use the package.

We recommend that you don't use `!pip install...` to install packages in Azure Machine Learning notebooks. Instead, use one of the following options:

- **Use the %pip line magic within a notebook**. Run:

    ```python
    
    %pip install --upgrade msticpy
    ```
- **Install from a terminal**:

    1. Open a terminal in Azure Machine Learning notebooks and run the following commands:

        ```bash
        conda activate azureml_py38
        pip install --upgrade msticpy
        ```
    2. Close the terminal and restart the kernel.

## Set an environment variable for your msticpyconfig.yaml file

If you're running in Azure Machine Learning and have your **msticpyconfig.yaml** file in the root of your user folder, MSTICPy automatically finds these settings. However, if you're running the notebooks in another environment, set an environment variable that points to the location of your configuration file by using the following steps.

Defining the path to your **msticpyconfig.yaml** file in an environment variable allows you to store your file in a known location and make sure that you always load the same settings.

Use multiple configuration files, with multiple environment variables, if you want to use different settings for different notebooks.

1. Decide on a location for your **msticpyconfig.yaml** file, such as in **~/.msticpyconfig.yaml** or **%userprofile%/msticpyconfig.yaml**.

    **Azure ML users**: If you store your configuration file in your Azure Machine Learning user folder, the MSTICPy `init_notebook` function (run in the initialization cell) automatically finds and uses the file, and you don't need to set a **MSTICPYCONFIG** environment variable.

    However, if you also have secrets stored in the file, we recommend storing the configuration file on the compute local drive. The compute internal storage is accessible only to the person who created the compute, whereas the shared storage is accessible to anyone with access to your Azure Machine Learning workspace.

    For more information, see [What is an Azure Machine Learning compute instance?](/en-us/azure/machine-learning/concept-compute-instance).
2. If needed, copy your **msticpyconfig.yaml** file to your selected location.
3. Set the **MSTICPYCONFIG** environment variable to point to that location.

Select one of the following tabs to define the **MSTICPYCONFIG** environment variable on [Windows](?tabs=windows), [Linux](?tabs=linux), or [Azure Machine Learning](?tabs=azure-ml).

# [Windows](#tab/windows)
For example, to set the **MSTICPYCONFIG** environment variable on Windows systems:

1. Move the **msticpyconfig.yaml** file to the Compute instance as needed.
2. Open the **System Properties** dialog box to the **Advanced** tab.
3. Select **Environment Variables...** to open the **Environment Variables** dialog.
4. In the **System variables** area, select **New...**, and define the values as follows:

    - **Variable name**: Define as `MSTICPYCONFIG`
    - **Variable value**: Enter the path to your **msticpyconfig.yaml** file

# [Linux](#tab/linux)
Update the **.bashrc** file to set the **MSTICPYCONFIG** environment variable on Linux systems by using the following steps.

1. Move the **msticpyconfig.yaml** file to the Compute instance as needed.
2. Open an Azure Machine Learning terminal, such as from the Microsoft Sentinel **Notebooks** page.
3. Verify that you can access your **msticpyconfig.yaml** file.

    In your Azure Machine Learning terminal, your current directory should be your Azure Machine Learning file store home directory, mounted in the Compute Linux system. The prompt looks similar to the following example:

    ```bash
    azureuser@alicecontoso-azml7:~/cloudfiles/code/Users/alicecontoso$
    ```

    List all files in the home directory, including the **msticpyconfig.yaml** file, by entering `ls`.
4. To move the **msticpyconfig.yaml** file to the Compute file store, enter:

    ```bash
    mv msticpyconfig.yaml ~
    ```
5. Use one of the following processes to edit the **.bashrc** file for the **MSTICPYCONFIG** environment variable:

    | Command | Steps |
    | --- | --- |
    | **vim** | 1. Run: `vim ~/.bashrc`2. Go to end of file by pressing **SHIFT+G** &gt; **End**. 3. Create a new line by entering **a** and then pressing **ENTER**. 4. Add your environment variable and then press **ESC** to get back to command mode. 5. Save the file by entering **:wq**. |
    | **nano** | 1. Run: `nano ~/.bashrc` 1. Go to end of file by pressing **ALT+/** or **OPTION+/**. 1. Add your environment variable, and then save your file. Press **CTRL+X** and then **Y**. |

    Add one of the following environment variables:

    - If you moved the **msticpyconfig.yaml** file, run `export MSTICPYCONFIG=~/msticpyconfig.yaml`.
    - If you didn't move the **msticpyconfig.yaml** file, run `export MSTICPYCONFIG=~/cloudfiles/code/Users/<YOURNAME>/msticpyconfig.yaml`.

# [Azure Machine Learning options](#tab/azure-ml)
If you need to store your **msticpyconfig.yaml** file somewhere other than your Azure Machine Learning user folder, use either an **nbuser\_settings.py** file or the **kernel.json** file:

- **An *nbuser\_settings.py* file at the root of your user folder**. While using an **nbuser\_settings.py** file is simpler and less intrusive than editing the **kernel.json** file, it's only supported when you run the `init_notebook` function at the start of your notebook code. While this is the default behavior, if you run the notebook code without first running `init_notebook`, MSTICPy mmight not be able to find the configuration file.

    1. In the Azure Machine Learning terminal, create the **nbuser\_settings.py** file in the root of your user folder, which is the folder with your username.
    2. In the **nbuser\_settings.py** file, add the following lines:

        ```python
          import os
          os.environ["MSTICPYCONFIG"] = "~/msticpyconfig.yaml"
        ```

    The **nbuser\_settings.py** file is automatically imported by the `init_notebook` function, and sets the `MSTICPYCONFIG` environment variable for the current notebook.
- **The *kernel.json* file for your Python kernel**. Use the **kernel.json** option if you plan on running the notebook manually, and possibly without calling the `init_notebook` function at the start.

    There are kernels for Python 3.6 and Python 3.8. If you use both kernels, edit both files.

    - **Python 3.8 location**: */usr/local/share/jupyter/kernels/python38-azureml/kernel.json*
    - **Python 3.6 location**: */usr/local/share/jupyter/kernels/python3-azureml/kernel.json*

    To set the environment variable in the **kernel.json** file:

    1. Make a copy of the **kernel.json** file, and open the original in an editor. You might need to use `sudo` to overwrite the **kernel.json** file, and the file contents look similar to the following example:

        ```python
        {
           "argv": [
           "/anaconda/envs/azureml_py38/bin/python",
           "-m",
           "ipykernel_launcher",
           "-f",
           "{connection_file}"
           ],
           "display_name": "Python 3.8 - AzureML",
           "language": "python"
        }
        ```
    2. After the `"language"` item, add the following line: `"env": { "MSTICPYCONFIG": "~/msticpyconfig.yaml" }`

        Make sure to add the comma at the end of the `"language": "python"` line. For example:

        ```python
        {
            "argv": [
            "/anaconda/envs/azureml_py38/bin/python",
            "-m",
            "ipykernel_launcher",
            "-f",
            "{connection_file}"
            ],
            "display_name": "Python 3.8 - AzureML",
            "language": "python",
            "env": { "MSTICPYCONFIG": "~/msticpyconfig.yaml" }
        }
        ```

---

Note

For the Linux and Windows options, you need to restart your Jupyter server so that the server picks up the environment variable that you defined.