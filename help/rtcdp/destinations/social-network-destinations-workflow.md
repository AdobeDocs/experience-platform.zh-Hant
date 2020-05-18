---
title: 社交網路目標工作流程
seo-title: 社交網路目標工作流程
description: 連線至您的社交網路和帳戶的指示
seo-description: 連線至您的社交網路和帳戶的指示
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# 社交網路目標驗證工作流程 {#social-network-destinations-workflow}

## 建立社交網路目的地的工作流程

本教學課程以Facebook為例，但Adobe即時客戶資料平台中的工作流程對於所有社交網路目的地都會相同，只要再將工作流程新增至產品即可。

1. 在「 **[!UICONTROL 目標>目錄]**」中，捲動至 **[!UICONTROL Social類別]** 。 選擇您偏好的社交網路目的地，然後選 **[!UICONTROL 擇連線目的地]**。

   ![連線至社交網路目的地](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 在「驗 **證** 」步驟中，如果您先前已設定連線至您的社交網路目的地，請選取「現有帳戶 **** 」並選取您現有的連線。 或者，您可以選取「 **[!UICONTROL 新帳戶]** 」來設定與社交網路目的地的新連線。 選 **[!UICONTROL 取「連線至目的地]** 」，這會將您帶往選取的社交網路目的地，以登入Adobe Experience Cloud並將其連接至您的社交網路廣告帳戶。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在社交網路帳戶ID中輸入錯誤的認證，就會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至社交網路目的地——驗證步驟](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 一旦您的認證獲得確認，而Adobe Experience Cloud已連線至您的社交網路後，您可以選取「下 **[!UICONTROL 一]** 步」繼續 **[!UICONTROL 設定步驟]** 。

   ![認證已確認](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在「設 **[!UICONTROL 定]** 」步驟中，輸入啟動流程的「名稱 **[!UICONTROL 」和「說明]** 」，並填寫您社交網路廣告 ******** 帳戶的「ID」帳戶。 選取任何應套用至此目的地的行銷使用案例。 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   >[!IMPORTANT]
   >
   > 適用於Facebook目的地。 **[!UICONTROL 帳戶ID是]** 您的Facebook廣告帳戶ID。 您可以在Facebook廣告管理員中找到此ID。 將ID前置詞 `act_` 如下：

   ![連線至社交網路目的地——設定步驟](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟動社交網路的區段](#activate-segments)」，以瞭解其餘的工作流程。

## 將區段啟用至社交網路 {#activate-segments}

如需如何將區段啟用至社交網路的指示，請參 [閱啟用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)