---
title: 社交網路目標工作流程
seo-title: 社交網路目標工作流程
description: 連線至您的社交網路和帳戶的指示
seo-description: 連線至您的社交網路和帳戶的指示
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# （測試版）社交網路目的地驗證工作流程 {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>在Adobe即時CDP中建立社交網路目的地的工作流程目前正在測試中，並非所有使用者都能使用。 文件和功能可能會有所變更。

## 建立雲端儲存空間目標的工作流程

本教學課程以Facebook為例，但Adobe即時客戶資料平台中的工作流程對於所有社交網路目的地都會相同，只要再將工作流程新增至產品即可。

1. 在 **[!UICONTROL Connections > Destinations]**&#x200B;中，滾動到類 **[!UICONTROL Social]** 別。 選擇您偏好的社交網路目的地，然後選擇 **[!UICONTROL Connect destination]**。

   ![連線至社交網路目的地](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 在「驗 **證** 」步驟中，如果您先前已設定社交網路目的地的連線，請選取並 **[!UICONTROL Existing Account]** 選取您現有的連線。 或者，您可以選 **[!UICONTROL New Account]** 擇設定新的社交網路目的地連線。 選 **[!UICONTROL Connect to destination]** 取後，您將會前往選取的社交網路目的地，以登入Adobe Experience Cloud並將其連接至您的社交網路廣告帳戶。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在社交網路帳戶ID中輸入錯誤的認證，就會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至社交網路目的地——驗證步驟](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 一旦您的認證獲得確認，而Adobe Experience Cloud已連線至您的社交網路，您就可以選 **[!UICONTROL Next]** 擇繼續執行 **[!UICONTROL Setup]** 步驟。

   ![認證已確認](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在步 **[!UICONTROL Setup]** 驟中，輸入啟 **[!UICONTROL Name]** 動流程 **[!UICONTROL Description]** 的和，並填入您的社交網 **[!UICONTROL Account ID]** 路廣告帳戶。 在您 **[!UICONTROL Create Destination]** 填入上述欄位後選取。

   >[!IMPORTANT]
   >
   >適用於Facebook目的地。 **[!UICONTROL Account ID]** 是您的Facebook廣告帳戶ID。 您可以在Facebook廣告管理員中找到此ID。 將ID前置詞 `act_` 如下：

   ![連線至社交網路目的地——設定步驟](/help/rtcdp/destinations/assets/social-network-step.png)

5. 您的目標現在已建立。 您可以選 **[!UICONTROL Save & Exit]** 取以後要啟用區段，或選取 **[!UICONTROL Next]** 以繼續工作流程並選取要啟用的區段。 在這兩種情況下，請參閱下一 [節「啟動社交網路的區段](#activate-segments)」，以瞭解其餘的工作流程。

## 將區段啟用至社交網路 {#activate-segments}

如需如何將區段啟用至社交網路的指示，請參 [閱啟用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。