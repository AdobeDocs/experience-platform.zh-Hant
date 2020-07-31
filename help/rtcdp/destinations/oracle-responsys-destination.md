---
title: Oracle Responsys目標
seo-title: Oracle Responsys目標
description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
seo-description: Responsys是Oracle針對跨通道行銷宣傳提供的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、展示廣告和社交媒體之間的互動。
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## 概述

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 是企業電子郵件行銷工具，適用於跨通道行銷宣傳，可 [!DNL Oracle] 以個人化電子郵件、行動裝置、展示廣告和社交媒體的互動。

若要傳送區段資 [!DNL Oracle Responsys]料至，您必須先 [連線至Adobe即時客戶資料平台中的目的地](#connect-destination) ，然後設 [定從您的儲存位置匯入資料](#import-data-into-responsys)[!DNL Oracle Responsys]。

## 連接目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接」>「目標]**」中，選 [!DNL Oracle Responsys]擇，然後選擇「 **[!UICONTROL 連接目標」]**。

   ![連線至Responsys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. 在「驗 **[!UICONTROL 證]** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線。 填寫您的帳戶驗證憑證，並選取「 **[!UICONTROL 連線至目的地」]**。 對於 [!DNL Oracle Responsys]，您可以在 **[!UICONTROL SFTP與Password之間選擇]** , **[!UICONTROL SFTP與SSH密鑰之間選擇]**。 根據您的連線類型，填寫下列資訊，然後選取「連 **[!UICONTROL 線至目的地」]**。

   對於 **[!UICONTROL 具有密碼連接的SFTP]** ，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL 具有SSH密鑰連接的SFTP]** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫Responsys資訊](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. 在「設 **[!UICONTROL 定]** 」步驟中，填入您目的地的相關資訊，如下所示：
   * **[!UICONTROL 名稱]**: 為目的地選擇相關名稱。
   * **[!UICONTROL 說明]**: 輸入目標的說明。
   * **[!UICONTROL 資料夾路徑]**: 在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。

   ![Responsys基本資訊](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. 填寫 **[!UICONTROL 上述欄位後]** ，按一下「建立目標」。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 目標屬性 {#destination-attributes}

在啟 [用區段](/help/rtcdp/destinations/activate-destinations.md) ，到目 [!DNL Oracle Responsys] 的地時，建議您從聯合架構中選取唯一 [識別碼](../../profile/home.md#profile-fragments-and-union-schemas)。 選擇唯一標識符以及要導出到目標的任何其它XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 匯出的資料 {#exported-data}

對於 [!DNL Oracle Responsys] 目標，Adobe Real-time CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Responsys_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 設定資料匯入至 [!DNL Oracle Responsys] {#import-data-into-responsys}

將即時CDP連接到您的或 [!DNL Amazon S3] SFTP儲存後，必須將資料從儲存位置導入到中 [!DNL Oracle Responsys]。 要瞭解如何完成此操作，請參 [閱中的導入聯繫人](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 或帳戶 [!DNL Oracle Responsys Help Center]。