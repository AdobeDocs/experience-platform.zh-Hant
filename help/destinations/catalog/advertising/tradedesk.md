---
keywords: 廣告；貿易部門；
title: The Trade Desk connection
description: '交易台是廣告購買者的自助服務平台，可跨展示廣告、視訊和行動庫存來源執行重新鎖定目標及受眾目標數位宣傳。 '
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# [!DNL The Trade Desk] 連接

## 概述 {#overview}

[!DNL The Trade Desk] 目的地可協助您傳送描述檔資 [!DNL The Trade Desk]料。

[!DNL The Trade Desk] 是自助服務平台，讓廣告購買者跨展示、視訊和行動庫存來源執行重新鎖定目標及受眾鎖定的數位促銷活動。

要向[!DNL Trade Desk]發送配置檔案資料，必須首先連接到目標。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Trade Desk IDs]或裝置ID為基礎的細分來建立重新鎖定目標或受眾鎖定的數位促銷活動。

## 支援的身份{#supported-identities}

[!DNL The Trade Desk] 支援啟用下表所述的身分。進一步瞭解[identities](/help/identity-service/namespaces.md)。

| 目標識別 | 說明 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | Trade Desk平台中的廣告商ID |

## 導出類型{#export-type}

**[!DNL Segment export]** -您正將區段（觀眾）的所有成員匯出至目的地。

## 先決條件 {#prerequisites}

如果您想要使用[!DNL The Trade Desk]建立您的第一個目標，而過去(使用Adobe Audience Manager或其他應用程式)未啟用Experience CloudID服務中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定[!DNL The Trade Desk]整合，您設定的ID同步化會延續至平台。

## 連接到目標{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇[!DNL The Trade Desk] ，然後選擇&#x200B;**[!UICONTROL Configure]**。

![配置交易台目標](../../assets/catalog/advertising/tradedesk/configure.png)

如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

![激活交易台目標](../../assets/catalog/advertising/tradedesk/activate.png)

## 驗證步驟{#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，您需要輸入[!DNL The Trade Desk]連接詳細資訊：

* **[!UICONTROL Name]**:您將來識別此目的地的名稱。
* **[!UICONTROL Description]**:將來幫助您識別此目標的說明。
* **[!UICONTROL Account ID]**:您的 [!DNL Trade Desk] [!UICONTROL Account ID]。
* **[!UICONTROL Server Location]**:詢問您 [!DNL Trade Desk] 的代表您應使用哪個地區伺服器。這些是您可從以下位置選擇的可用區域伺服器：

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱「Adobe Experience Platform的資料治理」頁面。 [](../../../data-governance/policies/overview.md)如需個別Adobe定義之行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

![交易台驗證步驟](../../assets/catalog/advertising/tradedesk/authenticate.png)

按一下「**[!UICONTROL Create destination]**」。您的目標現在已建立。 如果您想稍後啟動區段，可按一下[!UICONTROL Save & Exit]，或選取[!UICONTROL Next]以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節[啟動區段](#activate-segments)。

## 啟用區段{#activate-segments}

如需區段啟動工作流程的相關資訊，請參閱[啟用設定檔和區段至目標](../../ui/activate-destinations.md#select-attributes)。

在[區段排程](../../ui/activate-destinations.md#segment-schedule)步驟中，您必須手動將區段對應至目標中的對應ID或好記名稱。

在對應區段時，建議您使用[!DNL Platform]區段名稱或更短的區段名稱，以方便使用。 不過，您目的地中的區段ID或名稱不需要與[!DNL Platform]帳戶中的區段ID或名稱相符。 您在映射欄位中插入的任何值，都會由目標反映。

如果您使用多個裝置映射(Cookie ID、[!DNL IDFA]、[!DNL GAID])，請務必對所有三個映射使用相同的映射值。 [!DNL The Trade Desk] 會將所有資料匯整為單一區段，並進行裝置層級劃分。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 導出資料{#exported-data}

要驗證資料是否已成功導出到[!DNL The Trade Desk]目標，請檢查[!DNL Trade Desk]帳戶。 如果啟動成功，您的帳戶會填入觀眾。
