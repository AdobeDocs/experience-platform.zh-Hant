---
keywords: cloud storage destination;cloud storage
title: 雲端儲存目標工作流程
seo-title: 雲端儲存目標工作流程
description: 連線至雲端儲存空間的指示
seo-description: 連線至雲端儲存空間的指示
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# 建立雲端儲存空間目標的工作流程

## 概述

本頁說明如何連線至Adobe即時客戶資料平台中的雲端儲存空間。

1. 在「連 **[!UICONTROL 線]** >目 **[!UICONTROL 的地]**」中，選取您偏好的雲端儲存空間目的地，然後選取「 **[!UICONTROL 設定」]**。

   ![連線至雲端儲存空間目標](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](/help/rtcdp/destinations/destinations-workspace.md#catalog) 」(Catalog)部分。

2. 在「驗 **[!UICONTROL 證]** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您也可以選 **[!UICONTROL 取「新帳戶]** 」來設定雲端儲存目的地的新連線。 填寫您的帳戶驗證憑證，並選取「 **[!UICONTROL 連線至目的地」]**。 <br> 如需 [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) 、 [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) Amazon S3目標、 [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) 目標和 [SFTP](/help/rtcdp/destinations/sftp-destination.md) Destination的詳細資訊，請參閱 **** Amazon S3 Destination、Destination和SFTP Destination。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在雲端儲存位置輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 在「設 **[!UICONTROL 定]** 」步驟中，輸入啟 **[!UICONTROL 動流程的「名稱]** 」 **[!UICONTROL 和「說明]** 」。 <br>
此外，您也可以在此步驟中，選取 **[!UICONTROL 任何應套用至此目的地的Marketing]** 使用案例。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。 <br>
對於Amazon S3目標，請將儲 **[!UICONTROL 存貯體名稱]****** 、資料夾路徑插入雲端儲存目的地，以便傳送檔案。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連線至Amazon S3雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   對於SFTP目標，插入 **[!UICONTROL 要傳送檔案的資料夾路徑]** 。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連線至SFTP雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   對於 [!DNL Amazon Kinesis] 目標，請提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。 Adobe即時CDP會將資料匯出至此串流。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連接到Kinesis雲儲存目標——驗證步驟](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   對於 [!DNL Azure Event Hubs] 目標，請提供帳戶中現有資料流的名 [!DNL Amazon Kinesis] 稱。 Adobe即時CDP會將資料匯出至此串流。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連接到Kinesis雲儲存目標——驗證步驟](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟用區段](#activate-segments)」，以匯出資料的其餘工作流程。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。