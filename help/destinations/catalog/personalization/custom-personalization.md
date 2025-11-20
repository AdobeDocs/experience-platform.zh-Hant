---
keywords: 客製化個人化;目的地;體驗平台自訂目的地;
title: 自訂個人化連接
description: 此平台提供外部個人化、內容管理系統、廣告伺服器及其他運行於您網站上的應用程式，從 Adobe 體驗平台擷取受眾資訊。 此平台提供基於用戶資料、受眾會員的即時個人化服務。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 9%

---


# 自訂個人化連接 {#custom-personalization-connection}

## 目的地變更記錄檔 {#changelog}

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 5 月 | 功能和檔案更新 | 自2023年5月起，**[!UICONTROL Custom personalization]**&#x200B;連線支援[屬性式個人化](../../ui/activate-edge-personalization-destinations.md#map-attributes)，通常可供所有客戶使用。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 若要保護此資料，您必須在為屬性式個人化設定[目的地時，使用](https://developer.adobe.com/data-collection-apis/docs/)Edge Network API **[!UICONTROL Custom Personalization]**。 所有Edge Network API呼叫都必須在[已驗證的內容](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication)中進行。
>
><br>您可以新增伺服器端整合，利用您已在網頁或行動SDK實作中使用的相同資料流，透過[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)擷取設定檔屬性。
>
><br>如果您未遵循上述要求，個人化將僅以對象成員資格為基礎。

## 概觀 {#overview}

設置此目的地，讓外部個人化平台、內容管理系統、廣告伺服器及其他在客戶網站上運行的應用程式，能從 Adobe 體驗平台擷取受眾資訊。

## 先決條件 {#prerequisites}

根據您的實作，此目的地需要使用下列其中一個資料收集方法：

* 如果您想要從網站收集資料，請使用[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)。
* 如果你想從行動應用程式收集資料，請使用 [Adobe Experience Platform 行動 SDK](https://developer.adobe.com/client-sdks/documentation/) 。
* 如果你沒有使用 [Web SDK](https://developer.adobe.com/data-collection-apis/docs/) 或[行動 SDK](/help/web-sdk/home.md)，或想根據個人檔案屬性個人化使用者體驗，請使用 [Edge Network API](https://developer.adobe.com/client-sdks/documentation/)。

>[!IMPORTANT]
>
>在建立自訂個人化連結前，請閱讀如何 [啟動受眾資料以優化](../../ui/activate-edge-personalization-destinations.md)個人化目的地的指南。 本指南將帶你了解多個體驗平台元件中，同頁與下一頁個人化使用情境所需的設定步驟。

## 支持觀眾 {#supported-audiences}

本節說明您可以匯出到該目的地的受眾類型。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!DNL Profile request]** | 你是在請求一個個人檔案中所有在自訂個人化目的地中映射的受眾。 不同的 Adobe 資料集資料流[可設定](../../../datastreams/overview.md)不同的客製化個人化目的地。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

## 連線到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="關於資料流"
>abstract="此選項會確定哪個資料集合資料流中會在頁面回應中包含對象。下拉選單僅顯示已啟用目的地設定的資料流。您必須先設定資料流，然後才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=zh-Hant" text="了解如何設定資料流"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL Name]**：填寫此目的地的偏好名稱。
* **[!UICONTROL Description]**：輸入目的地的說明。 例如，你可以說明你使用這個目的地的活動。 此欄位為選填。
* **[!UICONTROL Integration alias]**： 此值會以 JSON 物件名稱傳送至 Experience Platform Web SDK。
* **[!UICONTROL Datastream]**：這會決定頁面回應中將包含哪些資料收集資料串流中的對象。 下拉選單僅顯示已啟用目的地設定的資料流。如需詳細資訊，請參閱[設定資料串流](../../../datastreams/overview.md)。

### 啟用警示 {#enable-alerts}

你可以啟用警示，接收資料流狀態通知到目的地。 從列表中選擇一個警示訂閱，即可接收資料流狀態的通知。 欲了解更多提醒資訊，請參閱使用介面[訂閱目的地提醒的指南](../../ui/alerts.md)。

當您完成目的地轉機的詳細資訊後，請選擇 **[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>要啟用資料，你需要 **[!UICONTROL View Destinations]**、 **[!UICONTROL Activate Destinations]**、 **[!UICONTROL View Profiles]**&#x200B;和 **[!UICONTROL View Segments]** [存取控制權限](/help/access-control/home.md#permissions)。 請閱讀 [存取控制概述](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需權限。

閱讀[啟用設定檔與對象邊緣個人化目的地](../../ui/activate-edge-personalization-destinations.md)，以取得啟用此目的地的對象的指示。

## 匯出的資料 {#exported-data}

如果您使用Adobe Experience Platform[中的](../../../tags/home.md)標籤來部署Experience Platform Web SDK，請使用[傳送事件完成](../../../tags/extensions/client/web-sdk/event-types.md)功能，而您的自訂程式碼動作將有`event.destinations`變數，可用來檢視匯出的資料。

以下是`event.destinations`變數的範例值：

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

如果您不是使用[標籤](/help/tags/home.md)來部署Experience Platform Web SDK，請使用[命令回應](/help/web-sdk/commands/command-responses.md)來檢視匯出的資料。

來自Adobe Experience Platform的JSON回應可加以剖析，以找出您要與Adobe Experience Platform整合之應用程式的對應整合別名。 對象ID可傳入應用程式的程式碼中作為定位引數。 以下是目標回應特有的內容範例。

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### [!UICONTROL Custom Personalization With Attributes]的範例回應

使用&#x200B;**[!UICONTROL Custom Personalization With Attributes]**&#x200B;時，API回應將與以下範例類似。

**[!UICONTROL Custom Personalization With Attributes]**&#x200B;與&#x200B;**[!UICONTROL Custom Personalization]**&#x200B;之間的差異在於API回應中包含`attributes`區段。

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## 資料使用與控管 {#data-usage-governance}

所有 [!DNL Adobe Experience Platform] 目的地在處理資料時都符合資料使用政策。 欲了解如何 [!DNL Adobe Experience Platform] 執行資料治理的詳細資訊，請參閱 [資料治理概述](../../../data-governance/home.md)。
