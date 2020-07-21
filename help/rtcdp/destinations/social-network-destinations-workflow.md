---
title: 社交網路目標工作流程
seo-title: 社交網路目標工作流程
description: 連線至您的社交網路和帳戶的指示
seo-description: 連線至您的社交網路和帳戶的指示
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# 社交網路目標驗證工作流程 {#social-network-destinations-workflow}

## 建立社交網路目的地的工作流程

本教學課 [!DNL Facebook] 程以Adobe即時客戶資料平台為例，但Adobe即時客戶資料平台中的工作流程對於所有社交網路目的地而言都相同，只要再新增至產品即可。

1. 在「 **[!UICONTROL 目標>目錄]**」中，捲動至 **[!UICONTROL Social類別]** 。 選擇您偏好的社交網路目的地，然後選 **[!UICONTROL 擇連線目的地]**。

   ![連線至社交網路目的地](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 在「驗 **證** 」步驟中，如果您先前已設定連線至您的社交網路目的地，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選取「 **[!UICONTROL 新帳戶]** 」來設定與社交網路目的地的新連線。 選 **[!UICONTROL 取「連線至目的地]** 」，這會將您帶往選取的社交網路目的地，以登入Adobe Experience Cloud並將其連接至您的社交網路廣告帳戶。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在社交網路帳戶ID中輸入錯誤的認證，就會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至社交網路目的地——驗證步驟](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 一旦您的認證獲得確認，而Adobe Experience Cloud已連線至您的社交網路後，您可以選取「下 **[!UICONTROL 一]** 步」繼續 **[!UICONTROL 設定步驟]** 。

   ![認證已確認](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在「設 **[!UICONTROL 定]** 」步驟中，輸入啟動流程的「名稱 **[!UICONTROL 」和「說明]** 」，並填寫您社交網路廣告 ******** 帳戶的「ID」帳戶。 <br> 此外，您也可以在此步驟中選取 **[!UICONTROL 任何應套用至此目的地的Marketing]** 使用案例。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。 <br> 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   >[!IMPORTANT]
   >
   > * 「單 *一身分個人化* 」行銷使用案例預設會針對社交網路目的地選取，且無法移除。
   > * 適用於 [!DNL Facebook] 目的地。 **[!UICONTROL 帳戶ID]** 是您的 [!DNL Facebook Ad Account ID]。 您可以在中找到此ID [!DNL Facebook Ads Manager]。 將ID前置詞 `act_` 如下：


   ![連線至社交網路目的地——設定步驟](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟動社交網路的區段](#activate-segments)」，以瞭解其餘的工作流程。

## 將區段啟用至社交網路 {#activate-segments}

如需如何將區段啟用至社交網路的指示，請參 [閱啟用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。