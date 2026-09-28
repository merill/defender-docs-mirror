---
layout: Conceptual
title: Test the Defender for Storage data security features - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-storage-test
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
description: Learn how to test the malware scanning, sensitive data threat detection, and activity monitoring features provided by Defender for Storage.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: ef5f5c3e-2941-c186-ca2f-27f6f1b887fe
document_version_independent_id: cc3843aa-c6d8-43bb-7b79-83ffb7527aa9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-storage-test.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-storage-test
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-storage-test.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 17ba0bd1-9698-44cd-fb94-705b38ce1b53
---

# Test the Defender for Storage data security features - Microsoft Defender for Cloud | Microsoft Learn

After you [enable Microsoft Defender for Storage](tutorial-enable-storage-plan), you can test the service and run a proof of concept. Testing the service helps you familiarize yourself with Defender for Storage features and validate that its advanced security capabilities effectively protect your storage accounts by generating real security alerts. This guide walks you through testing various aspects of the security coverage offered by Defender for Storage.

There are three main components to test:

- Malware scanning (if enabled)
- Sensitive data threat detection (if enabled)
- Activity monitoring

Tip

**A hands-on lab to try out malware scanning in Defender for Storage**

We recommend you try the [Ninja training instructions](https://aka.ms/DfStorage/NinjaTrainingLab) for detailed step-by-step instructions on how to test malware scanning end-to-end with setting up responses to scanning results. This is part of the 'labs' project that helps customers get ramped up with Microsoft Defender for Cloud and provide hands-on practical experience with its capabilities.

## Test malware scanning

Follow these steps to test malware scanning after enabling the feature:

1. To verify that the setup is successful, upload a file to the storage account. You can use the Azure portal to [upload a file](/en-us/azure/storage/blobs/storage-quickstart-blobs-portal#upload-a-block-blob)
2. Inspect new blob index tags:

    1. After uploading the file, view the blob and examine its blob index tags.
    2. You should see two new tags: **Malware scanning scan result** and **Malware scanning scan time**.
    3. The blob index tags serve as a helpful way to view the scan results.
3. If you don't see the new blob index tags, select the **Refresh** button.

[![Screenshot showing how to upload a file to test the Malware Scan.](media/defender-for-storage-test/testing-malware.png)](media/defender-for-storage-test/testing-malware.png#lightbox)

Note

Index tags aren't supported for ADLS Gen. To test and validate your protection for premium block blobs, look at the generated security alert.

### Upload an EICAR test file to simulate malware upload

An EICAR test file is a harmless standardized file that anti-malware software recognizes as malware for testing purposes. To simulate a malware upload using an EICAR test file, follow these steps:

1. Prepare for the EICAR test file:

    1. To avoid causing damage, use an EICAR test file instead of real malware. Standardized anti-malware software treats EICAR test files as malware.
    2. Exclude an empty folder to prevent your endpoint antivirus protection from deleting the file. For Microsoft Defender for Endpoint (MDE) users, refer to [add an exclusion to Windows Security](https://support.microsoft.com/windows/add-an-exclusion-to-windows-security-811816c0-4dfd-af4a-47e4-c301afe13b26#ID0EBF=Windows_11).
2. Create the EICAR test file:

    1. Copy the following string: `X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*`
    2. Paste the string into a .TXT file and save it in the excluded folder.
3. Upload the EICAR test file to your storage account.
4. Verify the **Malware scanning scan result** index tag:

    1. Check for the **Malware scanning scan result** index tag with the value **Malicious**.
    2. If the tags aren't visible, select the **Refresh** button.
5. Receive a Microsoft Defender for Cloud security alert:

    1. Navigate to **Microsoft Defender for Cloud** using the search bar in Azure.
    2. Select on **Security Alerts**.
6. Review the security alert:

    a. Locate the alert titled **Malicious file uploaded to storage account**.

    b. Select on the alert’s **View full details** button to see all the related details.
7. Learn more about Defender for Storage security alerts in the [reference table for all security alerts in Microsoft Defender for Cloud](alerts-azure-storage).

## Test sensitive data threat detection

To test the sensitive data threat detection feature by uploading test data that represents sensitive information to your storage account, follow these steps:

1. Create a new storage account:

    1. Choose a subscription without Defender for Storage enabled.
    2. Create a new storage account with a random name under the selected subscription.
2. Set up a test container:

    1. Go to the **Containers** pane in the newly created storage account.
    2. Select the **+ Container** button to create a new blob container.
    3. Name the new container **test-container**.
3. Upload test data:

    1. Open a text editing application on your computer, such as Notepad or Microsoft Word.
    2. Create a new file and save it in a format like TXT, CSV, or DOCX.
    3. Add the following string to the file: `ASD 100-22-3333 SSN Text` - this string is a test US (United States) SSN (Social Security Number).

        [![Screenshot showing how to test a file in malware scanning for Social Security Number information.](media/defender-for-storage-test/testing-sensitivity-2.png)](media/defender-for-storage-test/testing-sensitivity-2.png#lightbox)
    4. Save and upload the file to the **test-container** in the storage account.

        [![Screenshot showing how to upload a file in malware scanning to test for Social Security Number information.](media/defender-for-storage-test/testing-sensitivity-3.png)](media/defender-for-storage-test/testing-sensitivity-3.png#lightbox)
4. Enable Defender for Storage:

    1. In the Azure portal, go to **Microsoft Defender for Cloud**.
    2. Enable Defender for Storage on the storage account with the Sensitivity Data Discovery feature enabled.

    Sensitive data discovery scans for sensitive information within the first 24 hours. The initial scan occurs when you enable Sensitive Data Discovery at the storage account level or create a new storage account under a subscription protected by Sensitive Data Discovery at the subscription level. Following this initial scan, the service scans for sensitive information every seven days from the time of enablement.

    Note

    If you enable the feature and then add sensitive data on the days after enablement, the next scan for that newly added data will occur within the next 7-day scanning cycle, depending on the day of the week the data was added.
5. Change access level:

    1. Return to the **Containers** pane.
    2. Right-click on the **test-container** and select **Change the access level**.

        [![Screenshot showing how to change the access level for a test of malware scanning.](media/defender-for-storage-test/testing-sensitivity-1.png)](media/defender-for-storage-test/testing-sensitivity-1.png#lightbox)
    3. Choose the **Container (anonymous read access for containers and blobs)** option and select **OK**.

    The previous step exposes the blob container's content to the internet, which triggers a security alert within 30-60 minutes.
6. Review the security alert:

    1. Go to the **Security Alerts** pane.
    2. Look for the alert titled **The access level of a sensitive storage blob container was changed to allow unauthenticated public access**.
    3. Select on the alert’s **View full details** button to see all the related details.

        [![Screenshot showing how to see an alert for a test file in malware scanning.](media/defender-for-storage-test/sensitive-data-alert.png)](media/defender-for-storage-test/sensitive-data-alert.png#lightbox)

Learn more about Defender for Storage security alerts in the [reference table for all security alerts in Microsoft Defender for Cloud](alerts-azure-storage).

## Test activity monitoring

To test the activity monitoring feature by simulating access from a Tor exit node to a storage account, follow these steps:

1. Create a new storage account with a random name.
2. Set up a test container:

    1. Go to the **Containers** pane in the storage account.
    2. Select the **+ Container** button to create a new blob container.
    3. Name the new container **test-container-tor**.
3. Upload any file to the **test-container-tor**.
4. Generate a SAS (shared access signatures) token:

    1. Right-click on the uploaded file and select **Generate SAS**.
    2. Select the **Generate SAS token and URL** button.
    3. Copy the Blob SAS URL.
5. Download the file using a Tor browser:

    1. Open a Tor browser.
    2. Paste the SAS URL into the address bar and press Enter.
    3. Download the file when prompted.

    The previous step triggers a Tor anomaly security alert within 1-3 hours.
6. Review the security alert:

    1. Go to the **Security Alerts** pane.
    2. Look for the alert titled **Access from a Tor exit node to a storage blob container**.
    3. Select on the alert’s **View full details** button to see all the related details.

Learn more about Defender for Storage security alerts in the [reference table for all security alerts in Microsoft Defender for Cloud](alerts-azure-storage).