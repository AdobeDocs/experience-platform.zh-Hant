---
title: 雲端儲存目標工作流程
seo-title: 雲端儲存目標工作流程
description: 連線至雲端儲存空間的指示
seo-description: 連線至雲端儲存空間的指示
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# 建立雲端儲存空間目標的工作流程

## 概述

本頁說明如何連線至Adobe即時客戶資料平台中的雲端儲存空間。

1. 在「連 **[!UICONTROL 線>目的地]**」中，選取您偏好的雲端儲存空間目的地，然後選取「 **[!UICONTROL 連線目的地」]**。

   ![連線至雲端儲存空間目標](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 在「驗 **證** 」步驟中，如果您先前已設定雲端儲存空間目的地的連線，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您也可以選 **[!UICONTROL 取「新帳戶]** 」來設定雲端儲存目的地的新連線。 填寫您的帳戶驗證憑證，並選取「 **[!UICONTROL 連線至目的地」]**。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在雲端儲存位置輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 在「設 **[!UICONTROL 定]** 」步驟中，輸入啟動流程的「名稱」和「目的地 **[!UICONTROL 」，並將]********** Folder路徑插入要傳送檔案的雲端儲存目的地。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連線至雲端儲存空間目標——驗證步驟](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 不論是哪一種情況，請參閱下一 [節「啟動區段](#activate-segments)」，以瞭解其餘的工作流程，

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。