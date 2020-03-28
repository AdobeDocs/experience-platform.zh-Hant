---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。
seo-description: Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe Campaign

## 概述

Adobe Campaign是一套解決方案，可協助您跨所有線上及線下通道個人化並傳遞宣傳活動。 如需 [詳細資訊，請參閱關於Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 。

若要傳送區段資料至Adobe Campaign，您必須先 [在Adobe即時客戶資料平台中連接目標](#connect-destination) ，然後設定從儲 [](#import-data-into-campaign) 存位置匯入資料至Adobe Campaign的資料。

## 連接目標 {#connect-destination}

1. 在中 **[!UICONTROL Connections > Destinations]**，選取「Adobe Campaign」，然後選取 **[!UICONTROL Connect destination]**。

   ![連線至Adobe Campaign](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. 在連接目標工作流中，選擇 **[!UICONTROL Connection type]** 儲存位置。 對於Adobe Campaign，您可以選擇 **[!UICONTROL Amazon S3]**&#x200B;和 **[!UICONTROL SFTP with Password]** 和 **[!UICONTROL SFTP with SSH Key]**。 根據您的連線類型，填入下列資訊，然後選取 **[!UICONTROL Connect]**。

   ![設定促銷活動精靈](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   對於 **[!UICONTROL Amazon S3]** 連接，您必須提供訪問密鑰ID和密鑰。
對於 **[!UICONTROL SFTP with Password]** 連接，必須提供域、埠、用戶名和密碼。
對於 **[!UICONTROL SFTP with SSH Key]** 連接，必須提供域、埠、用戶名和SSH密鑰。

   ![填寫促銷活動資訊](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 在中 **[!UICONTROL Basic Information]**，填寫您目的地的相關資訊，如下所示：
   * **[!UICONTROL Name]**:為目的地選擇相關名稱。
   * **[!UICONTROL Description]**:輸入目標的說明。
   * **[!UICONTROL Bucket Name]**:適 *用於S3連線*。 輸入S3儲存段的位置，即時CDP將將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL Folder Path]**:在儲存位置中提供路徑，即時CDP會將導出資料儲存為CSV或Tab分隔檔案。
   * **[!UICONTROL File Format]**: **CSV****或TAB_DELIMITED**。 選擇要導出到儲存位置的檔案格式。
   ![促銷活動基本資訊](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 填寫 **[!UICONTROL Create]** 上述欄位後按一下。 您的目標現在已連線，您可 [以啟動區段](/help/rtcdp/destinations/activate-destinations.md) 至目標。

## 目標屬性 {#destination-attributes}

在啟 [用區段](/help/rtcdp/destinations/activate-destinations.md) 至Adobe Campaign目的地時，我們建議您從聯合架構中選取唯一 [識別碼](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)。 選擇唯一標識符和要導出到目標的任何其他XDM欄位。 如需詳細資訊，請參 [閱「電子郵件行銷目標」中，選取要在匯出檔案中當做目標屬性使用的架構欄位](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 。


## 設定資料匯入至Adobe Campaign {#import-data-into-campaign}

在將即時CDP連接到Amazon S3或SFTP儲存空間後，您必須設定從儲存位置匯入資料至Adobe Campaign的動作。 如要瞭解如何完成此作業，請參 [閱Adobe Campaign說明檔案](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 中的匯入資料。