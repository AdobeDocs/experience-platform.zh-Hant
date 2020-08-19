---
keywords: email;Email;e-mail;email destinations;salesforce;salesforce destination
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
seo-description: Salesforce Marketing Cloud是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建構並自訂歷程，以個人化其體驗。
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## 概述

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是數位行銷套裝，先前稱為ExactTarget，可讓您為訪客和客戶建立和自訂歷程，以個人化其體驗。

若要傳送區段資 [!DNL Salesforce Marketing Cloud]料至，您必須先 [在Adobe Real](#connect-destination) -time CDP中連線目的地，然後 [從儲存位置設定資料匯入](#import-data-into-salesforce)[!DNL Salesforce Marketing Cloud]。

## 連接目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 的地]**」中，選 [!DNL Salesforce Marketing Cloud]擇，然後選 **[!UICONTROL 擇「連接目標]**」。

   ![連線至Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. 在「驗 **[!UICONTROL 證]** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線。 填寫您的帳戶驗證憑證，並選取「 **[!UICONTROL 連線至目的地」]**。 對於 [!DNL Salesforce Marketing Cloud]，您可以在 **[!UICONTROL SFTP與Password之間選擇]** , **[!UICONTROL SFTP與SSH密鑰之間選擇]**。 根據您的連線類型，填寫下列資訊，然後選取「連 **[!UICONTROL 線至目的地」]**。

   對於 **[!UICONTROL 具有密碼連接的SFTP]** ，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL 具有SSH密鑰連接的SFTP]** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Salesforce資訊](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. 在「設 **[!UICONTROL 定]** 」步驟中，填入您目的地的相關資訊，如下所示：
   * **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
   * **[!UICONTROL 說明]**:輸入目標的說明。
   * **[!UICONTROL 資料夾路徑]**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL 檔案格式]**: **[!UICONTROL CSV]** 或 **[!UICONTROL TAB_DELIMITED]**。 選擇要導出到儲存位置的檔案格式。

   ![Salesforce基本資訊](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. 填寫 **[!UICONTROL 上述欄位後]** ，按一下「建立目標」。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 目標屬性 {#destination-attributes}

在啟 [用區段](/help/rtcdp/destinations/activate-destinations.md) ，到目 [!DNL Salesforce Marketing Cloud] 的地時，建議您從聯合架構中選取唯一 [識別碼](../../profile/home.md#profile-fragments-and-union-schemas)。 選擇唯一標識符和要導出到目標的任何其他XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 匯出的資料 {#exported-data}

對於 [!DNL Salesforce Marketing Cloud] 目標，Adobe Real-time CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Salesforce_Marketing_Cloud_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 設定資料匯入至 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

將即時CDP連接到您的或 [!DNL Amazon S3] SFTP儲存後，必須將資料從儲存位置導入到中 [!DNL Salesforce Marketing Cloud]。 如要瞭解如何完成此作業，請參 [閱中的「從檔案將訂閱者匯入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 」 [!DNL Salesforce Help Center]。