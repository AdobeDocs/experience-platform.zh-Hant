---
keywords: Facebook;facebook；社交網路；社交網路；社交網路；社交網路驗證；社交網路驗證
title: 建立社交網路目的地
type: 教學課程
description: 瞭解如何在Adobe Experience Platform中連線至您的社交網路廣告帳戶。
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# 建立社交網路目標{#social-network-destinations-workflow}

本教學課程以[!DNL Facebook]為例，但Adobe Experience Platform工作流程對於所有社交網路目的地都是相同的。

在&#x200B;**[!UICONTROL 目標]** > **[!UICONTROL 目錄]**&#x200B;中，捲動至&#x200B;**[!UICONTROL Social]**&#x200B;類別。 選擇您偏好的社交網路目的地，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連線至社交網路目的地](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>如果已存在與此目標的連接，您可以在目標卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**Authentication**&#x200B;步驟中，如果您先前已設定到社交網路目的地的連線，請選取&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選取您現有的連線。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定與社交網路目的地的新連線。 選擇&#x200B;**[!UICONTROL 連線至目標]**，這會將您帶往選取的社交網路目的地，以登入Adobe Experience Cloud並將其連接至您的社交網路廣告帳戶。

>[!NOTE]
>
>平台支援驗證程式中的認證驗證，如果您在社交網路帳戶ID中輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連線至社交網路目的地——驗證步驟](../../assets/catalog/social/workflow/pre-connect.png)

一旦您的認證獲得確認，且Adobe Experience Cloud已連線至您的社交網路後，您可以選取「下一個」(**[!UICONTROL Next)，以繼續「設定」(Setup)步驟。]******

![認證已確認](../../assets/catalog/social/workflow/post-connect.png)

在&#x200B;**[!UICONTROL Setup]**&#x200B;步驟中，輸入啟動流程的[!UICONTROL Name]和[!UICONTROL Description]，並填寫社交網路廣告帳戶的[!UICONTROL Account ID]。

>[!IMPORTANT]
>
> 對於[!DNL Facebook]目標，**[!UICONTROL 帳戶ID]**&#x200B;是您的[!DNL Facebook Ad Account ID]。 您可以在[!DNL Facebook Ads Manager]中找到此ID。 將ID前置詞為`act_`，如下所示：

![連線至社交網路目的地——設定步驟](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> 對於[!DNL LinkedIn]目標，**[!UICONTROL 帳戶ID]**&#x200B;是您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在[!DNL LinkedIn Campaign Manager]中找到此ID。

此外，在此步驟中，您也可以選取任何應套用至此目的地的&#x200B;**[!UICONTROL 行銷動作]**。 行銷動作會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

在填寫上述欄位後，選擇「建立目標」。****

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL 儲存並退出]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節[啟用社交網路的區段](#activate-segments)。

## 將區段啟用至社交網路{#activate-segments}

如需如何將區段啟用至社交網路的指示，請參閱[將資料啟用至目標](../../ui/activate-destinations.md)。