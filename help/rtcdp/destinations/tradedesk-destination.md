---
keywords: advertising; the trade desk;
title: 貿易桌目的地
seo-title: 貿易桌目的地
description: '交易台是廣告購買者的自助服務平台，可跨展示廣告、視訊和行動庫存來源執行重新鎖定目標及受眾目標數位宣傳。 '
seo-description: 交易台是廣告購買者的自助服務平台，可跨展示廣告、視訊和行動庫存來源執行重新鎖定目標及受眾目標數位宣傳。
translation-type: tm+mt
source-git-commit: c9fb63b390d4c7dddcdb35a85710ff664614ad63
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# [!DNL The Trade Desk] 目的地

## 概述 {#overview}

[!DNL The Trade Desk] 目的地可協助您傳送描述檔資 [!DNL The Trade Desk]料。

[!DNL The Trade Desk] 是自助服務平台，讓廣告購買者跨展示、視訊和行動庫存來源執行重新鎖定目標及受眾鎖定的數位促銷活動。

若要傳送描述檔資 [!DNL The Trade Desk]料至，您必須先連線至目的地。

## 目標規格 {#destination-specs}

請注意下列目標專屬的詳細 [!DNL The Trade Desk] 資訊：

* 您可以傳送下列身 [分](../../identity-service/namespaces.md) ，到 [!DNL The Trade Desk] 目的地： [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID]

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以裝置ID為基礎的細分，來建 [!DNL Trade Desk IDs] 立重新鎖定目標或受眾鎖定的數位促銷活動。

## 匯出類型 {#export-type}

**[!DNL Segment export]** -您正將區段（觀眾）的所有成員匯出至目的地。

## 連接到目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 標]**」中，選 [!DNL The Trade Desk]擇並選 **[!UICONTROL 擇配置]**。

   ![配置交易台目標](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](../destinations/destinations-workspace.md#catalog) 」(Catalog)部分。
   >
   >![激活交易台目標](assets/tradedesk-destination-activate.png)

1. 在「驗 [!UICONTROL 證] 」步驟中，您需要輸入連 [!DNL The Trade Desk] 接詳細資訊：

   * **[!UICONTROL 名稱]**:您將來識別此目的地的名稱。
   * **[!UICONTROL 說明]**:將來幫助您識別此目標的說明。
   * **[!UICONTROL 帳戶ID]**:您的 [!DNL Trade Desk] 帳 [!UICONTROL 戶ID]。
   * **[!UICONTROL 用戶端密碼]**:用戶 `clientSecret` 端認證中使用 [!DNL OAuth2] 的參數。
   * **[!UICONTROL 伺服器位置]**:詢問您的 [!DNL The Trade Desk] 代表您應使用哪個地區伺服器。 這些是您可從以下位置選擇的可用區域伺服器：

      * **[!UICONTROL 歐洲]**
      * **[!UICONTROL 新加坡]**
      * **[!UICONTROL 東京]**
      * **[!UICONTROL 北美洲東部]**
      * **[!UICONTROL 北美洲西部]**
      * **[!UICONTROL 拉丁美洲]**
   * **[!UICONTROL 行銷使用案例]**:行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱Adobe [Experience Platform中的資料治理](../privacy/data-governance-overview.md#destinations) 頁面。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](../../data-governance/policies/overview.md#core-actions)。

   ![交易台驗證步驟](assets/tradedesk-destination-authentication.png)

1. 按一 **[!UICONTROL 下建立目標]**。 您的目標現在已建立。 如果您想稍 [!UICONTROL 後啟動區段，可以按一下「儲存並退出] 」，或選取「下一步  」以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟用區段](#activate-segments)」，以瞭解其餘的工作流程。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](activate-destinations.md#select-attributes) ，請參閱啟用設定檔和區段至目的地。

在「區 [段排程](activate-destinations.md#segment-schedule) 」步驟中，您必須手動將區段對應至目標中的對應ID或好記名稱。

在對應區段時，建議您使用 [!DNL Platform] 區段名稱或較短的區段名稱，以方便使用。 不過，您目的地中的區段ID或名稱不需要與帳戶中的區段ID或名稱相 [!DNL Platform] 符。 您在映射欄位中插入的任何值，都會由目標反映。

如果您使用多個裝置對應(Cookie ID [!DNL IDFA]、 [!DNL GAID]、)，請務必對所有三個對應使用相同的對應值。 [!DNL The Trade Desk] 會將所有資料匯整為單一區段，並進行裝置層級劃分。

![區段對應ID](assets/segment-mapping-id.png)


## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至目 [!DNL The Trade Desk] 標，請檢查您的 [!DNL The Trade Desk] 帳戶。 如果啟動成功，您的帳戶會填入觀眾。
