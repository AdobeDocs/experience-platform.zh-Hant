---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。
seo-description: Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。 如需 [詳細資訊，請參閱關於Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 。

若要傳送區段資料至Adobe Campaign，您必須先 [在Adobe即時客戶資料平台中連接目標](#connect-destination) ，然後設定從儲 [](#import-data-into-campaign) 存位置匯入資料至Adobe Campaign的資料。

## 連接目標 {#connect-destination}

1. 在「 **[!UICONTROL 連線]** >目 **[!UICONTROL 的地]**」中，選取「Adobe Campaign」，然後選取「 **[!UICONTROL 連線目的地」]**。

   ![連線至Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在連接目標工作流中，選擇 **[!UICONTROL 儲存位置的連接類型]** 。 對於Adobe Campaign，您可以在 **[!UICONTROL Amazon S3]**、 **[!UICONTROL SFTP with Password]** 和 **[!UICONTROL SSH Key之間選擇]**。 根據您的連線類型，填入下列資訊，然後選取「連 **[!UICONTROL 線」]**。

   ![設定促銷活動精靈](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   對於 **[!UICONTROL Amazon S3連接]** ，您必須提供您的存取金鑰ID和機密存取金鑰。
對於 **[!UICONTROL 具有密碼連接的SFTP]** ，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL 具有SSH密鑰連接的SFTP]** ，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫促銷活動資訊](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在基 **[!UICONTROL 本資訊]**，填寫您目的地的相關資訊，如下所示：
   * **[!UICONTROL 名稱]**: 為目的地選擇相關名稱。
   * **[!UICONTROL 說明]**: 輸入目標的說明。
   * **[!UICONTROL 貯體名稱]**: *適用於S3連線*。 輸入S3儲存段的位置，即時CDP將將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL 資料夾路徑]**: 在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL 檔案格式]**: **CSV** 或 **TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。

   ![促銷活動基本資訊](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 填入 **[!UICONTROL 上述欄位後]** ，按一下「建立」。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。

## 目標屬性 {#destination-attributes}

在啟 [用區段](/help/rtcdp/destinations/activate-destinations.md) 至Adobe Campaign目的地時，我們建議您從聯合架構中選取唯一 [識別碼](../../profile/home.md#profile-fragments-and-union-schemas)。 選擇唯一標識符以及要導出到目標的任何其它XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。

## 匯出的資料 {#exported-data}

對於 [!DNL Adobe Campaign] 目標，Adobe Real-time CDP會在您提供的儲存位置中建立以Tab `.txt` 分隔 `.csv` 的或檔案。 如需檔案的詳細資訊，請參閱區 [段啟動教學課程中的「電子郵件行銷目標](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 」和「雲端儲存目標」。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 設定資料匯入至Adobe Campaign {#import-data-into-campaign}

在將即時CDP連線至您或SFTP [!DNL Amazon S3] 儲存後，您必須設定從儲存位置匯入資料至Adobe Campaign的資料。 如要瞭解如何完成此作業，請參 [閱Adobe Campaign說明檔案](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 中的匯入資料。