---
keywords: Facebook;facebook；社交網路；社交網路；社交認證；社交網路認證
title: 建立社交目標
type: Tutorial
description: 瞭解如何連線至您在Adobe Experience Platform的社交廣告帳戶。
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: 805cb72e91e6446f74cc3461d39841740eb576c7
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 建立社交目標{#social-network-destinations-workflow}

## 概述 {#overview}

本教學課程以[!DNL Facebook]為例，但Adobe Experience Platform工作流程對於所有社交目標都是相同的。

## 設定社交目標——影片逐步瀏覽{#video}

以下影片示範如何在Adobe Experience Platform設定社交目的地和啟用區段。 步驟也依序排列在下幾節。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 選擇社交目標{#select-destination}

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;中，滾動到&#x200B;**[!UICONTROL Social]**&#x200B;類別。 選擇您偏好的社交目的地，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連線至社交目的地](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

## 帳戶步驟{#account}

在&#x200B;**Account**&#x200B;步驟中，如果您先前已設定連線至您的社交目的地，請選取&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選取您現有的連線。 或者，您可以選取&#x200B;**[!UICONTROL New Account]**&#x200B;來設定與社交目的地的新連線。 選擇&#x200B;**[!UICONTROL Connect to destination]**，這會帶您前往選取的社交目的地，以登入並連線Adobe Experience Cloud至您的社交廣告帳戶。

>[!NOTE]
>
>平台支援驗證程式中的認證驗證，如果您在您的社交帳戶ID中輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連線至社交目的地——驗證步驟](../../assets/catalog/social/workflow/pre-connect.png)

在確認您的認證並將Adobe Experience Cloud連線至您的社交網路後，您可以選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟。

![認證已確認](../../assets/catalog/social/workflow/post-connect.png)

## 驗證步驟{#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，輸入啟動流程的[!UICONTROL Name]和[!UICONTROL Description]，並填入社交網路廣告帳戶的[!UICONTROL Account ID]。

>[!IMPORTANT]
>
> * 對於[!DNL Facebook]目標，**[!UICONTROL Account ID]**&#x200B;是您的[!DNL Facebook Ad Account ID]。 您可以在[!DNL Facebook Ads Manager]中找到此ID。 將ID前置詞`act_`，如下圖所示。
> * 對於[!DNL LinkedIn]目標，**[!UICONTROL Account ID]**&#x200B;是您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在[!DNL LinkedIn Campaign Manager]中找到此ID。


![連線至社交目的地——驗證步驟](../../assets/catalog/social/workflow/authentication.png)

在此步驟中，您也可以選取任何應套用至此目的地的&#x200B;**[!UICONTROL Marketing action]**。 行銷動作會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL Save & Exit]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節[啟用社交網路的區段](#activate-segments)。

## 將區段啟用至社交網路{#activate-segments}

如需如何將區段啟用至社交網路的指示，請參閱[將資料啟用至目標](../../ui/activate-destinations.md)。
