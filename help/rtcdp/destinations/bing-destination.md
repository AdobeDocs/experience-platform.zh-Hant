---
keywords: advertising; bing;
title: Microsoft Bing目標
seo-title: Microsoft Bing目標可協助您將描述檔資料傳送至Microsoft Display Advertising。
description: 透過Microsoft Bing目標，您可以跨Microsoft Display Advertising執行重新定位和受眾鎖定的數位宣傳。
seo-description: 透過Microsoft Bing目標，您可以跨Microsoft Display Advertising執行重新定位和受眾鎖定的數位宣傳。
translation-type: tm+mt
source-git-commit: a64f9f1f078d8380cc25c9760eac1699512a5870
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# [!DNL Microsoft Bing] 目的地

## 概述 {#overview}

目標 [!DNL Microsoft Bing] 可協助您傳送描述檔資料 [!DNL Microsoft Display Advertising]。

若要傳送描述檔資 [!DNL Microsoft Bing]料至，您必須先連線至目的地。

## 目標規格 {#destination-specs}

請注意下列目標專屬的詳細 [!DNL Microsoft Bing] 資訊：

* 您可以傳送下列身 [分](../../identity-service/namespaces.md) ，到 [!DNL Microsoft Bing] 目的地： [!DNL Microsoft ID].

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以下細分，透過跨通道 [!DNL Microsoft Advertising IDs] 的展示廣告鎖定 [!DNL Microsoft Advertising] 使用者。

## 匯出類型 {#export-type}

**[!DNL Segment Export]** -您正將區段（觀眾）的所有成員匯出至目 [!DNL Microsoft Bing] 標。

## 先決條件 {#prerequisites}

設定目標時，您會要求提供下列資訊：

* [!UICONTROL 帳戶ID]:這是整數 [!DNL Bing Ads CID]格式的您。

## 連接到目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 標]**」中，選 [!DNL Microsoft Bing]擇並選 **[!UICONTROL 擇配置]**。

   ![配置Microsoft Bing目標](assets/bing-destination-configure.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](../destinations/destinations-workspace.md#catalog) 」(Catalog)部分。
   >
   >![啟動Microsoft Bing目標](assets/bing-destination-activate.png)

1. 在「驗 [!UICONTROL 證] 」步驟中，必須輸入目標連接詳細資訊：

   * **[!UICONTROL 名稱]**:您將來識別此目的地的名稱。
   * **[!UICONTROL 說明]**:將來幫助您識別此目標的說明。
   * **[!UICONTROL 帳戶ID]**:您的 [!DNL Bing Ads CID]。
   * **[!UICONTROL 行銷使用案例]**:行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱Adobe [Experience Platform中的資料治理](../privacy/data-governance-overview.md#destinations) 頁面。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](../../data-governance/policies/overview.md#core-actions)。

   ![Microsoft Bing目標驗證](assets/bing-destination-authentication.png)

1. 按一 **[!UICONTROL 下建立目標]**。 您的目標現在已建立。 如果您想稍 [!UICONTROL 後啟動區段，可以按一下「儲存並退出] 」，或按一下「下一步  」以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟用區段](#activate-segments)」，以瞭解其餘的工作流程。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](activate-destinations.md#select-attributes) ，請參閱啟用設定檔和區段至目的地。

在「區 [段排程](activate-destinations.md#segment-schedule) 」步驟中，您必須手動將區段對應至目標中的對應ID或好記名稱。

在對應區段時，建議您使用 [!DNL Platform] 區段名稱或較短的區段名稱，以方便使用。 不過，您目的地中的區段ID或名稱不需要與帳戶中的區段ID或名稱相 [!DNL Platform] 符。 您在映射欄位中插入的任何值，都會由目標反映。

![區段對應ID](assets/segment-mapping-id.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至目 [!DNL Microsoft Bing] 標，請檢查您的 [!DNL Microsoft Bing Ads] 帳戶。 如果啟動成功，您的帳戶會填入觀眾。