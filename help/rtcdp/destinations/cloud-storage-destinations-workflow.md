---
title: 雲端儲存目標工作流程
seo-title: 雲端儲存目標工作流程
description: 連線至雲端儲存空間的指示
seo-description: 連線至雲端儲存空間的指示
translation-type: tm+mt
source-git-commit: 7f6151535f30043413a2c111345b7e2c6367fd50

---


# 建立雲端儲存空間目標的工作流程

## 概述

本頁說明如何連線至Adobe即時客戶資料平台中的雲端儲存空間。

1. 在中 **[!UICONTROL Connections > Destinations]**，選擇您偏好的雲端儲存空間目標，然後選擇 **[!UICONTROL Connect destination]**。

   ![連線至雲端儲存空間目標](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. 在「驗 **證** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取並 **[!UICONTROL Existing Account]** 選取您現有的連線。 或者，您可以選 **[!UICONTROL New Account]** 擇設定到雲儲存目標的新連接。 填寫您的帳戶驗證憑證並選取 **[!UICONTROL Connect to destination]**。 如需 [驗證步驟中憑證輸入的詳細資訊](/help/rtcdp/destinations/amazon-s3-destination.md) ，請參閱Amazon S3目的地和 [SFTP](/help/rtcdp/destinations/sftp-destination.md) 目的地 **** 。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在雲端儲存位置輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. 在步 **[!UICONTROL Setup]** 驟中，輸入啟 **[!UICONTROL Name]** 動流程 **[!UICONTROL Description]** 的和。 <br>
對於Amazon S3目標，請將 **[!UICONTROL Bucket name]** 和 **[!UICONTROL Folder path]** 檔案插入雲儲存目標中。 在您 **[!UICONTROL Create Destination]** 填入上述欄位後選取。

   ![連線至Amazon S3雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   對於SFTP目標，請插入 **[!UICONTROL Folder path]** 要傳送檔案的位置。

   ![連線至SFTP雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. 您的目標現在已建立。 您可以選 **[!UICONTROL Save & Exit]** 取以後要啟用區段，或選取 **[!UICONTROL Next]** 以繼續工作流程並選取要啟用的區段。 在這兩種情況下，請參閱下一 [節「啟用區段](#activate-segments)」，以匯出資料的其餘工作流程。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。