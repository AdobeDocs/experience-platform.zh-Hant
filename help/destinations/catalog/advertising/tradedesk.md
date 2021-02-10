---
keywords: 廣告；貿易部門；
title: The Trade Desk connection
description: '交易台是廣告購買者的自助服務平台，可跨展示廣告、視訊和行動庫存來源執行重新鎖定目標及受眾目標數位宣傳。 '
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# [!DNL The Trade Desk] 連接

[!DNL The Trade Desk] 目的地可協助您傳送描述檔資 [!DNL The Trade Desk]料。

[!DNL The Trade Desk] 是自助服務平台，讓廣告購買者跨展示、視訊和行動庫存來源執行重新鎖定目標及受眾鎖定的數位促銷活動。

要向[!DNL The Trade Desk]發送配置檔案資料，必須首先連接到目標。

## 目標規格{#destination-specs}

請注意以下特定於[!DNL The Trade Desk]目標的詳細資訊：

* 您可以將下列[identitys](../../../identity-service/namespaces.md)傳送至[!DNL The Trade Desk]目標：[!DNL The Trade Desk ID]、[!DNL IDFA]、[!DNL GAID]。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Trade Desk IDs]或裝置ID為基礎的細分來建立重新鎖定目標或受眾鎖定的數位促銷活動。

## 導出類型{#export-type}

**[!DNL Segment export]** -您正將區段（觀眾）的所有成員匯出至目的地。

## 連接到目標{#connect-destination}

在&#x200B;**[!UICONTROL 連接]** > **[!UICONTROL 目標]**&#x200B;中，選擇[!DNL The Trade Desk] ，然後選擇&#x200B;**[!UICONTROL 配置]**。

![配置交易台目標](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>如果已存在與此目標的連接，您可以在目標卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[Catalog](../../ui/destinations-workspace.md#catalog)部分。
>
>![激活交易台目標](../../assets/catalog/advertising/tradedesk/activate.png)

在[!UICONTROL Authentication]步驟中，您需要輸入[!DNL The Trade Desk]連接詳細資訊：

* **[!UICONTROL 名稱]**:您將來識別此目的地的名稱。
* **[!UICONTROL 說明]**:將來幫助您識別此目標的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Trade Desk] [!UICONTROL 帳戶ID]。
* **[!UICONTROL 用戶端密碼]**:用 `clientSecret` 戶端認證中使 [!DNL OAuth2] 用的參數。
* **[!UICONTROL 伺服器位置]**:詢問您 [!DNL The Trade Desk] 的代表您應使用哪個地區伺服器。這些是您可從以下位置選擇的可用區域伺服器：

   * **[!UICONTROL 歐洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 北美洲東部]**
   * **[!UICONTROL 北美洲西部]**
   * **[!UICONTROL 拉丁美洲]**

* **[!UICONTROL 行銷使用案例]**:行銷使用案例會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱「Adobe Experience Platform中的[資料治理」頁面。 ](../../../data-governance/policies/overview.md)如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱[資料使用政策概觀](../../../data-governance/policies/overview.md)。

![交易台驗證步驟](../../assets/catalog/advertising/tradedesk/authenticate.png)

按一下&#x200B;**[!UICONTROL 建立目標]**。 您的目標現在已建立。 如果您想稍後啟動區段，可以按一下「儲存並退出」，或選擇「下一步」以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節[啟動區段](#activate-segments)。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md#select-attributes)。

在[區段排程](../../ui/activate-destinations.md#segment-schedule)步驟中，您必須手動將區段對應至目標中的對應ID或好記名稱。

在對應區段時，建議您使用[!DNL Platform]區段名稱或更短的區段名稱，以方便使用。 不過，您目的地中的區段ID或名稱不需要與[!DNL Platform]帳戶中的區段ID或名稱相符。 您在映射欄位中插入的任何值，都會由目標反映。

如果您使用多個裝置映射(Cookie ID、[!DNL IDFA]、[!DNL GAID])，請務必對所有三個映射使用相同的映射值。 [!DNL The Trade Desk] 會將所有資料匯整為單一區段，並進行裝置層級劃分。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 導出資料{#exported-data}

要驗證資料是否已成功導出到[!DNL The Trade Desk]目標，請檢查[!DNL The Trade Desk]帳戶。 如果啟動成功，您的帳戶會填入觀眾。
